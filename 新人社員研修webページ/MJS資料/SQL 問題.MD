# SQL問題　解答まとめ

## 【第２回】
### １．学生の情報を、年の大きい順・組の小さい順・学生Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「年」「組」「学生No」「氏名」とする

```sql
SELECT Nen,Kumi,GakuseiNo,Name FROM "DBA"."Gakusei"ORDER BY Nen DESC
```

### ２．2008年5月20日に実施された数学のテストの情報を、学生Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「学生No」「点数」とする日付を条件に指定する際はCAST関数を使用する事とする
※参考※
ＣＡＳＴ関数の使用例　⇒　CAST(‘日付の文字列’ AS DATETIME)

```sql
SELECT GakuseiNo,Tensu FROM "DBA"."Saiten" WHERE JissiDate =CAST('20080520' AS DATETIME)ORDER BY GakuseiNo
```

### ３．2008年5月20日に実施されたテストの点数が60点未満の人の情報を、年の大きい順・学生Noの小さい順・科目Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「年」「学生Ｎｏ」「氏名」「科目No」「点数」とする
※参考※
ＣＡＳＴ関数の使用例　⇒　CAST(‘日付の文字列’ AS DATETIME)

```sql
SELECT G.Nen,S.GakuseiNo,G.name,KamokuNo,Tensu FROM "DBA"."Saiten" AS S
INNER JOIN "Gakusei"AS G ON G.GakuseiNo=S.GakuseiNo 
WHERE JissiDate =CAST('20080520' AS DATETIME) AND tensu <= 60
ORDER BY Nen DESC ,S.GakuseiNo,S.KamokuNo
```

### ４．点数が60点未満の人の情報を、実施年月日の大きい順･年の大きい順・学生Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「実施年月日」「年」「学生Ｎｏ」「氏名」とし、同一の学生は複数取得しないものとする

```sql
SELECT S.JissiDate,G.Nen,S.GakuseiNo,G.name FROM "DBA"."Saiten" AS S 
INNER  JOIN "Gakusei"AS G ON G.GakuseiNo=S.GakuseiNo 
WHERE tensu <= 60
GROUP BY S.JissiDate,G.Name,G.Nen,S.GakuseiNo
ORDER BY Nen DESC, S.GakuseiNo DESC,G.Nen DESC ,S.GakuseiNo ASC
```

## 【第３回】


### １．学生・科目毎の最高点数・最低点数の情報を、学生Noの小さい順・科目Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「学生No」「科目No」「最高点数（Saikou）」「最低点数（Saitei）」とする

```sql
SELECT S.GakuseiNo, K.KamokuNo,MAX(Tensu)AS Saikou, MIN(Tensu)AS Saitei FROM "Saiten"AS S
INNER JOIN "Kamoku"AS K ON S.KamokuNo = K.KamokuNo
GROUP BY S.GakuseiNo ,K.KamokuNo
ORDER BY GakuseiNo,K.KamokuNo;
```
### ２．年・科目毎の最高点数・最低点数の情報を、年の大きい順・科目Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「年」「科目名」「最高点数（Saikou）」「最低点数（Saitei）」とする

```sql
SELECT Nen, S.KamokuNo,MAX(Tensu)AS Saikou, MIN(Tensu)AS Saitei FROM "Gakusei"AS G
INNER JOIN "Saiten"AS S ON S.GakuseiNo = G.GakuseiNo
GROUP BY Nen,S.KamokuNo
ORDER BY Nen DESC, S.KamokuNo;
```

### ３．学生・科目毎の平均点の情報を、年の大きい順・組の小さい順・学生Noの小さい順・科目Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「年」「組」「氏名（GakuseiName）」「科目名（KamokuName）」「平均点（Heikin）」とする

```sql
SELECT Nen, Kumi,G.name,K.name AS KamokuName,AVG(Tensu)AS Heikin FROM "Gakusei"AS G
INNER JOIN "Saiten"AS S ON S.GakuseiNo = G.GakuseiNo
INNER JOIN "Kamoku"AS K ON K.KamokuNo = S.KamokuNo
GROUP BY Nen, Kumi,G.name,K.name
ORDER BY Nen DESC, Kumi;
```

### ４．テストの平均値が60点以上かつ70点未満の学生の情報を、学生Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「学生No」「平均点（Heikin）」とする

```sql
SELECT GakuseiNo,AVG(Tensu)AS Heikin FROM "Saiten"
GROUP BY GakuseiNo
HAVING Heikin >=60 AND Heikin <70
ORDER BY GakuseiNo

```


## 【第４回】
### １．テストで90点以上取った学生の情報を、年の大きい順・組の小さい順・学生Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「年」「組」「学生No」「氏名」とする

```sql
SELECT Nen, Kumi,G.GakuseiNo,name FROM "Gakusei"AS G
INNER JOIN "Saiten" AS S
ON G.GakuseiNo = S.GakuseiNo
WHERE tensu >=90
ORDER BY Nen DESC, Kumi, G.GakuseiNo
```


### ２．現在までに実施されたテスト（3回×3科目）を全て受けていない学生の情報を、年の大きい順・組の小さい順・学生Noの小さい順に取得するSQLを作りなさい。
##### 取得する項目は「年」「組」「学生No」「氏名」とする

```sql
SELECT Nen, Kumi,G.GakuseiNo,name FROM "Gakusei"AS G
LEFT OUTER JOIN "Saiten" AS S
ON G.GakuseiNo = S.GakuseiNo
GROUP BY Nen,Kumi,G.GakuseiNo ,name
HAVING COUNT(G.GakuseiNo) !=9
ORDER BY Nen DESC, Kumi, G.GakuseiNo
```

### ３．実施年月日・学年毎の国語の最高点数と取得した学生の情報を、実施年月日の小さい順・年の大きい順に取得するSQLを作りなさい。
##### 取得する項目は「実施年月日」「年」「学生No」「氏名」「最高点数（Saikou）」とする

```sql
SELECT S.Jissidate,Nen,MAX(S.Tensu)AS Saikou FROM "Gakusei"AS G
INNER JOIN "Saiten" AS S
ON G.GakuseiNo = S.GakuseiNo
GROUP BY S.JissiDate,Nen
ORDER BY S.JissiDate DESC,G.Nen
//学生ナンバーと氏名を入れるとうまくいかない
```


## 【第５回】

### １．2008年5月20日に実施されたテストを受けていない学生の点数を、0点で登録するSQLを作りなさい。

```sql
INSERT INTO Saiten (JissiDate,GakuseiNo,KamokuNo,Tensu)
SELECT 
CAST('2008/05/20' AS DATETIME),GakuseiNo,Kamoku.KamokuNo,0
FROM Gakusei CROSS JOIN Kamoku
EXCEPT
SELECT 
JissiDate,GakuseiNo,KamokuNo, 0
FROM Saiten
WHERE 
JissiDate =CAST('2008/05/20' AS DATETIME)
```

### ２．2008年10月15日に実施された3年の採点データの情報を、全て削除するSQLを作りなさい。

```sql
DELETE FROM Saiten 
WHERE  JissiDate = CAST('2008/05/20' AS DATETIME)AND GakuseiNo 
IN(SELECT GakuseiNo FROM Gakusei WHERE Nen = 3)
```

### ３．2008年7月8日に行われた2年の国語の点数を、5点加算するSQLを作りなさい。

```sql
UPDATE Saiten SET Tensu = Tensu+5
WHERE  JissiDate = CAST('2008/07/08' AS DATETIME)AND GakuseiNo 
IN(SELECT GakuseiNo FROM Gakusei WHERE Nen = 2)
```

## 【第６回】
### １．2008年5月20日に実施されたテストの学生ごとの科目の点数情報を、年の大きい順、組の小さい順、学生Noの小さい順で取得するSQLを作りなさい。

##### 取得する項目は「年」「組」「学生No」「氏名」「国語」「算数」「英語」とする。

テストを受けていない科目は「-」(ハイフン)を表示して下さい。

取得イメージ　（例）
年	組	学生No	氏名	国語	数学	英語
3	1	100100	…	90	80	78
3	1	100110	…	80	－	60
3	2	200101	…	－	－	－
2	1	200105	…	70	80	90
2	2	200106	…	90	60	80
1	1	200115	…	80	90	
1	1	200116	…	60	80	90

こんな感じで取得できれば問題ありません。


