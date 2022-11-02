```delphi
//************************************************************************
//	System		:	XXXXXXXX
//	Program		:	XXXXXXXX処理
//	ProgramID	:	MAS290200
//	Name		:
//	Create		:	2001 / 99 / 99
//	Comment		:	XXXX注意事項等XXXXXXXXXXXXX
//					XXXXXXXXXXXXXXXXXXXXXXXXX
//	History		:	2001 / 99 / 99	X.Xxxxxx
//					XXXXXXXX更新内容XXXXXXX
//*************************************************************************
unit MAS290200u;

interface

uses
  Buttons, Classes, VCL.Controls, ComCtrls, dxGrClms, dxDBGrid, dxTL, dxCntner, dxmdaset,
  daDatMod, VCL.Dialogs, MJSCommonDialogs, Db, FireDAC.Comp.Client, VCL.ExtCtrls, VCL.Forms, VCL.Graphics, Grids, VCL.ImgList, jpeg,
  Menus, Messages, MJSComboBox, MJSLabel, MJSFunctionBar, MJSSPFunctionBar,
  MJSStatusBar, MJSSpeedButton, MJSPanel, MJSEdits, MJSQuery, MasComu, MasWndIFu,
  MJSPreviewIFLu, MjsPrnDlgLu, MjsPrnSupportLu,
  MjsDBModuleu, MJSMsgStdu, MJSPageControl,
  MJSRadioGroup, MjsDispCtrl, MJSCommonu, MasMonth, MjsStrCtrl, MJSTab, Mask, Math,
  MjsDateCtrl, MJSPostCtrl, MJSMemo, MJSStringGrid, MjsExceptU, MJSBitBtn, MasMailEntu,
  ppDB, ppDBPipe, ppBands, ppCtrls, ppVar, ppPrnabl, ppClass, ppCache, ppComm,
  ppRelatv, ppProd, ppReport, VCL.StdCtrls, SysUtils, Windows, ppModule,
  MJSCommon3u,
  MLXAppWrapperU,
  MJSKeyDataState,
  MJSScrollBox, FireDAC.Stan.Intf, FireDAC.Stan.Option, FireDAC.Stan.Param,Label, MJSFunctionBar, MJSSPFunctionBar,
  MJSStatusBar, MJSSpeedButton, MJSPanel, MJSEdits, MJSQuery, MasComu, MasWndIFu,
  MJSPreviewIFLu, MjsPrnDlgLu, MjsPrnSupportLu,
  MjsDBModuleu, MJSMsgStdu, MJSPageControl,
  MJSRadioGroup, MjsDispCtrl, MJSCommonu, MasMonth, MjsStrCtrl, MJSTab, Mask, Math,
  MjsDateCtrl, MJSPostCtrl, MJSMemo, MJSStringGrid, MjsExceptU, MJSBitBtn, MasMailEntu,
  ppDB, ppDBPipe, ppBands, ppCtrls, ppVar, ppPrnabl, ppClass, ppCache, ppComm,
  ppRelatv, ppProd, ppReport, VCL.StdCtrls, SysUtils, Windows, ppModule,
  MJSCommon3u,
  MLXAppWrapperU,
  MJSKeyDataState,
  MJSScrollBox, FireDAC.Stan.Intf, FireDAC.Stan.Option, FireDAC.Stan.Param,
  FireDAC.Stan.Error, FireDAC.DatS, FireDAC.Phys.Intf, FireDAC.DApt.Intf,
  FireDAC.Stan.Async, FireDAC.DApt, ppDesignLayer, ppParameter,
  FireDAC.Stan.Error, FireDAC.DatS, FireDAC.Phys.Intf, FireDAC.DApt.Intf,
  FireDAC.Stan.Async, FireDAC.DApt, ppDesignLayer, ppParameter,
  FireDAC.Comp.DataSet, MJSPopupMenu, MJSRadioButton;

const
	WM_ONPAINT = WM_APP + 1;					// OnPaint時の処理起動メッセージ用
    {INDEX_COL_GCODE = 1;
    INDEX_COL_YODATE = 2;
	INDEX_COL_SWKKBN = 3;  }
	// 和暦西暦区分
    YEARKBN_WAREKI	= 0;			//和暦
    YEARKBN_SEIREKI	= 1;			//西暦
    // 関数返り値
    RET_NG			= -1;
    RET_OK			= 0;
	// 簡略・正式名称区分
    NAMEKBN_SIMPLE	= 0;
    NAMEKBN_LONG	= 1;
 	// ﾊﾟﾀｰﾝ取得順の区分
    ORDERKBN_INIT			= 0;

type
  {$I ActionInterface.inc}
    	TDTMainData = class
  private
	FYearKbn	: Integer;	// 和暦西暦区分
    FComKbn2	: Integer;  // 決算確定区分
    FComKbn3	: Integer;  // メール会計区分
    FDTName7	: String;   // ﾌﾘｰｺｰﾄﾞに使用する記号
  public
  	constructor Create();
	property YearKbn: Integer read FYearKbn write FYearKbn;
	property ComKbn2: Integer read FComKbn2 write FComKbn2;
	property ComKbn3: Integer read FComKbn3 write FComKbn3;
	property DTName7: String read FDTName7 write FDTName7;
  end;

  TMAS290200f = class(TForm)
    Pnl_ApToolBar: TMPanel;
    Sb_End: TMSpeedButton;
    Sb_Change: TMSpeedButton;
    Pnl_Footer: TMPanel;
    Sb_StatusBar: TMStatusBar;
    Fb_FunctionBar: TMSPFunctionBar;
    Sb_Main: TMScrollBox;
    dxMemData1: TdxMemData;
    dxDBGrid1: TdxDBGrid;
    DataSource1: TDataSource;
    AddBtn: TMBitBtn;
    dxMemData1Name: TStringField;
    dxMemData1Code: TStringField;
    NameForm: TEdit;
    ここに入力してください: TLabel;
    ChangeBtn: TMBitBtn;
    DeleteBtn: TMBitBtn;
    DecideBtn: TMBitBtn;
    MPopupMenu1: TMPopupMenu;
    ppReport1: TppReport;
    ppDBPipeline1: TppDBPipeline;
    DataSource_print: TDataSource;
    ppParameterList1: TppParameterList;
    ppHeaderBand1: TppHeaderBand;
    TopLabel: TppLabel;
    ppLine631: TppLine;
    SVppDate: TppSystemVariable;
    ppLine1: TppLine;
    ppLine5: TppLine;
    ppLine6: TppLine;
    ppLine12: TppLine;
    LppCorpCode: TppLabel;
    LppCorpName: TppLabel;
    ppLine11: TppLine;
    ppLabel1: TppLabel;
    ppLine8: TppLine;
    ppLabel2: TppLabel;
    ppDetailBand_Ptn: TppDetailBand;
    ppUnderLine: TppLine;
    ppLine3: TppLine;
    ppLine7: TppLine;
    ppLine2: TppLine;
    ppLine4: TppLine;
    GCode: TppDBText;
    LongName: TppDBText;
    ppFooterBand1: TppFooterBand;
    SVppPage: TppSystemVariable;
    LppAccOffice: TppLabel;
    ppDesignLayers1: TppDesignLayers;
    ppDesignLayer1: TppDesignLayer;
    Sb_Print: TMSpeedButton;
    Code: TdxDBGridColumn;
    Name: TdxDBGridColumn;
    ID: TdxDBGridColumn;
    dxMemData1ID: TStringField;
    MBitBtn2: TMBitBtn;
    MBitBtn3: TMBitBtn;
    MBitBtn5: TMBitBtn;
    dxDBGrid2: TdxDBGrid;
    SYOUHAI: TdxDBGridColumn;
    Hand: TdxDBGridColumn;
    SeriousLevel: TdxDBGridColumn;
    Num: TdxDBGridColumn;
    DrowNo: TdxDBGridColumn;
    HandText: TEdit;
    Label4: TLabel;
    Label6: TLabel;
    Label9: TLabel;
    LoseBtn: TMBitBtn;
    WinBtn: TMBitBtn;
    勝敗: TLabel;
    SinkenBtn2: TMRadioButton;
    SinkenBtn3: TMRadioButton;
    SinkenBtn1: TMRadioButton;
    RadioGroup1: TRadioGroup;
    DrowNoBox: TMComboBox;
    SYOUHAIlabel: TEdit;
    Label7: TLabel;
    dxMem_SENREKI: TdxMemData;
    DataSource_SENREKI: TDataSource;
    dxMem_SENREKIID: TStringField;
    dxMem_SENREKISYOUHAI: TStringField;
    dxMem_SENREKIHand: TStringField;
    dxMem_SENREKISeriouslyLevel: TStringField;
    dxMem_SENREKIDrowNo: TIntegerField;
    dxMem_SENREKINum: TIntegerField;
    Label8: TLabel;
    YoiBox: TMComboBox;
    CodeLabel: TLabel;
    YOi: TdxDBGridColumn;
    BackBtn: TMBitBtn;
    MEkakusi: TGroupBox;
    dxMem_SENREKIYoi: TStringField;
    dxMem_Bunseki: TdxMemData;
    DataSource_Bunseki: TDataSource;
    dxDBGrid3: TdxDBGrid;
    Gu: TdxDBGridColumn;
    Tyoki: TdxDBGridColumn;
    Pa: TdxDBGridColumn;
    Most: TdxDBGridColumn;
    Label10: TLabel;
    Label12: TLabel;
    Label13: TLabel;
    Label14: TLabel;
    dxMem_BunsekiGu: TStringField;
    dxMem_BunsekiTyoki: TStringField;
    dxMem_BunsekiPa: TStringField;
    dxMem_BunsekiMost: TStringField;
    MComboBox1: TMComboBox;
    dxMemData_print: TdxMemData;
    StringField1: TStringField;
    StringField2: TStringField;
    StringField3: TStringField;
    ppLabel3: TppLabel;
    ppDBText1: TppDBText;



	procedure FormCreate(Sender: TObject);
	procedure MemdataSetSuru(var aMem: TdxMemData);
	procedure IDCount();
	procedure SENREKIdataTOUROKU(Sender: TObject);
	procedure FormClose(Sender: TObject; var Action: TCloseAction);
	procedure FormCloseQuery(Sender: TObject; var CanClose: Boolean);
	procedure SetFileOut(var aTitle, aMemFld: TStringList);
	procedure FormActivate(Sender: TObject);
	procedure FormHide(Sender: TObject);
	procedure FormDestroy(Sender: TObject);
	procedure FormShow(Sender: TObject);
	procedure Sb_ChangeClick(Sender: TObject);
	procedure Sb_EndClick(Sender: TObject);
    procedure AddBtnClick(Sender: TObject);
    procedure ChangeBtnClick(Sender: TObject);
    procedure DeleteBtnClick(Sender: TObject);
    procedure Sb_MainClick(Sender: TObject);
    procedure Sb_PrintClick(Sender: TObject);
	procedure GetDTMain(var aDTMainData: TDTMainData);
	procedure dxPlayerSelect(Sender: TObject);
    procedure NameFormClick(Sender: TObject);
    procedure DecideBtnClick(Sender: TObject);
    procedure WinBtnClick(Sender: TObject);
	procedure BackBtnClick(Sender: TObject);
	procedure Bunseki();
	procedure BunsekiSQL(Hand,ZYOUKEN:string; m_iMAX:Integer; Colum: string);

  private
	{ Private 宣言 }
	m_pMyAppRecord	:	^TMjsAppRecord;
	m_CorpConnect	:	TFDConnection;
	m_DataModule	:	TMDataModulef;
	m_Query			:	TMQuery;
	m_MASCom		:	TMASCom;
    m_iZoom         :   Integer;
	m_AcControl		:	TWinControl;
	m_Owner         :  TComponent;
	m_PrnSupport	: TMjsPrnSupportL;          // 印刷情報
    m_MjsPre		: TMJSPreviewIFL;       	// 印刷プレビュー
	m_DTMainData	: TDTMainData;      		// 会社基本情報
	m_bInsertCheck	: Boolean;					// 登録チェック
	m_bFirstInsCheck : Boolean;                // 先頭行登録チェック
	m_MjsMsgRec     : TMjsMsgRec;
	m_sSinkenLv     :String;
	m_sYoiLv        :String;
	m_sDrowNo       :String;
	M_sHand         :String;
	m_iDrowNo       :integer;
	m_iMAX          : Integer;


  public
	{ Public 宣言 }
	constructor CreateForm(pRec: Pointer);
	procedure	CMChildKey(var Msg: TWMKey); message CM_CHILDKEY;

  end;


function AppEntry(pParam:Pointer) : Integer;

exports
	AppEntry;

implementation

{$R *.DFM}

//**************************************************************************
//	Proccess  :	TDTMainDataのｺﾝｽﾄﾗｸﾀ
//	Name	  :	A.Narita
//	Date	  :	2021 / 8 / 20
//**************************************************************************
constructor TDTMainData.Create();
begin
	inherited;
	YearKbn	:= 0;
    ComKbn2	:= 0;
    ComKbn3	:= 0;
    DTName7	:= '';
end;
//**************************************************************************
//	Proccess  :	引数にﾌｧｲﾙ出力情報をセット
//	Name	  :	A.Narita
//	Date	  :	2021 / 8 / 20
//	Parameter :	aTitle	: TStringList	タイトルリスト
//	Parameter : aMemFld	: TStringList   参照フィールドリスト
//**************************************************************************
procedure TMAS290200f.SetFileOut(var aTitle, aMemFld: TStringList);
begin

    aTitle.Add('ID');                                                           // <#5> Add st
    aTitle.Add('コード');                                                  // <#5> ed
    aTitle.Add('名前');
    aMemFld.Add('ID');
    aMemFld.Add('Code');
	aMemFld.Add('Name');
end;



//**************************************************************************
//	Proccess  :	外部ﾌﾟﾛｸﾞﾗﾑからのｴﾝﾄﾘﾎﾟｲﾝﾄ
//	Name	  :
//	Date	  :	2001 / 08 / 29
//	Parameter :	pParam	Pointer
//	Retrun	  :	result
//	History	  :	2001 / 99 / 99	X.Xxxxxx
//				XXXXXXXX修正内容
//**************************************************************************
function AppEntry(pParam: Pointer): Integer;
var
	pMyForm	:   ^TMAS290200f;
	pRec	:   ^TMjsAppRecord;
begin
	result	:= ACTID_RET_OK;
	pRec	:= Pointer(TAppParam(pParam^).pRecord);

	case TAppParam(pParam^).iAction of

		ACTID_FORMCREATESTART:						// ﾌｫｰﾑの作成要求（作成のみ）
		begin
			new (pMyForm);
			try
				pMyForm^ := TMAS290200f.CreateForm(pRec);
				pRec^.m_pChildForm := pMyForm;
			except
				Dispose(pMyForm);
				result := ACTID_RET_NG;
			end;
		end;

		ACTID_FORMCREATESHOWSTART:					// ﾌｫｰﾑの作成要求（作成&表示）
		begin
			new (pMyForm);
			try
				pMyForm^ := TMAS290200f.CreateForm(pRec);
				pMyForm^.Show;
				pRec^.m_pChildForm := pMyForm;
			except
				Dispose(pMyForm);
				result := ACTID_RET_NG;
			end;
		end;

		ACTID_FORMCLOSESTART:						// ﾌｫｰﾑの解放要求
		begin
			pMyForm := Pointer(pRec^.m_pChildForm);
			pMyForm^.Close;
			pMyForm^.Free;
			Dispose(pMyForm);
		end;

		ACTID_FORMCANCLOSESTART:					// ﾌｫｰﾑの解放直前要求
		begin
			pMyForm := Pointer(pRec^.m_pChildForm);
			if pMyForm^.CloseQuery = False then
				result := ACTID_RET_NG;
		end;

		ACTID_SHOWSTART:							// ﾌｫｰﾑの表示要求
		begin
			pMyForm := Pointer(pRec^.m_pChildForm);
			pMyForm^.Show;
		end;

		ACTID_HIDESTART:
		begin
			pMyForm := Pointer( pRec^.m_pChildForm );

			if pMyForm^.Parent <> nil then
			begin
				pMyForm^.Hide;
			end;
		end;
	end;
end;

//**************************************************************************
//	Proccess  :	ﾌｫｰﾑｺﾝｽﾄﾗｸﾄ
//	Name	  :
//	Date	  :	2001 / 08 / 29
//	Parameter :	pRec	Pointer
//	Retrun	  :
//	History	  :	2001 / 99 / 99	X.Xxxxxx
//				XXXXXXXX修正内容
//**************************************************************************
constructor TMAS290200f.CreateForm(pRec: Pointer);
begin
	m_pMyAppRecord := pRec;											// 構造体のSave

	m_DataModule := TMDataModulef(m_pMyAppRecord^.m_pDBModule^);		// DBModuleを取得
	m_MASCom := TMASCom(m_pMyAppRecord^.m_pSystemArea^);				// 会社Noを共通ﾒﾓﾘから取得

	// DBOpne
	m_CorpConnect := m_DataModule.COPDBOpen(1, m_MASCom.m_iCopNo);	// DB Open
	if m_CorpConnect = nil then
	begin
		ShowMessage('CreateFormでｴﾗｰが発生しました｡');
		raise EMathError.Create('エラー');
	end;

    inherited 	Create(MLXApplication);
end;



//**************************************************************************
//	Component	:	Form
//	Event	    :	OnDestroy
//	Name		:
//**************************************************************************
procedure TMAS290200f.FormDestroy(Sender: TObject);
begin
	// 印刷プレビューの破棄
	m_MjsPre.Term ();
	m_MjsPre.Free ();
    m_MjsPre := Nil;

    // 会社基本ﾃﾞｰﾀｸﾗｽの破棄
    if Assigned(m_DTMainData) then
    begin
        m_DTMainData.Free;
        m_DTMainData := Nil;
    end;

	// クエリを破棄
    if Assigned(m_Query) then
    begin
        m_Query.Free;
        m_Query := Nil;
    end;

    // 会社DBをクローズ
    if Assigned(m_CorpConnect) then
    begin
    	m_DataModule.COPDBClose(m_CorpConnect);
        m_CorpConnect := Nil;
    end;

	inherited;
end;

//**************************************************************************
//	Component   :	Form
//	Event	    :	OnCreate
//	Name	    :
//**************************************************************************
procedure TMAS290200f.FormCreate(Sender: TObject);
begin
	Parent := TMPanel(m_pMyAppRecord^.m_pOwnerPanel^);		// 親ﾊﾟﾈﾙをParent
	Align := alClient;										// 全領域を作成

	MjsCompoColorSet(TMAS290200f(Self),
					TMASCom(m_pMyAppRecord^.m_pSystemArea^).SystemArea.SysBaseColorB,
					TMASCom(m_pMyAppRecord^.m_pSystemArea^).SystemArea.SysBaseColorD
	);

	MjsColorChange(TMAS290200f(Self),
					TMASCom(m_pMyAppRecord^.m_pSystemArea^).SystemArea.SysColorB,
					TMASCom(m_pMyAppRecord^.m_pSystemArea^).SystemArea.SysColorD,
					TMASCom(m_pMyAppRecord^.m_pSystemArea^).SystemArea.SysBaseColorB,
					TMASCom(m_pMyAppRecord^.m_pSystemArea^).SystemArea.SysBaseColorD,
					rcCOMMONAREA(m_pMyAppRecord^.m_pCommonArea^).SysFocusColor);

	m_iZoom := MjsFontResize(TMAS290200f(Self), Pointer(m_pMyAppRecord));

	m_Query := TMQuery.Create(Self);
	m_DataModule.SetDBInfoToQuery(m_CorpConnect, m_Query);

    m_MjsPre	:= TMJSPreviewIFL.Create();
	m_MjsPre.Init(m_pMyAppRecord);
		// 会社基本ﾃﾞｰﾀｸﾗｽを生成
    m_DTMainData	:= TDTMainData.Create();
    GetDTMain(m_DTMainData);
end;

//**************************************************************************
//	Component   :	Form
//	Event	    :	OnActivate
//	Memo		:	フォーム アクティブ
//	Name	    :
//**************************************************************************
procedure TMAS290200f.FormActivate(Sender: TObject);
var
	AppPara : TAppParam;
begin
	AppPara.iAction := ACTID_ACTIVEEND;
	AppPara.pRecord := Pointer(m_pMyAppRecord);
	AppPara.pActionParam := nil;

	TMjsAppRecord( m_pMyAppRecord^ ).m_pOwnerEntry( @AppPara );
end;

//**************************************************************************
//	Component	:	Form // 01/04/18追加
//	Event	    :	OnShow
//	Name	    :
//**************************************************************************
procedure TMAS290200f.FormShow(Sender: TObject);
begin
MemdataSetSuru(dxMemData1);
IDCount();
//
end;
//
//**************************************************************************
//目次
//・1部-プレイヤーデータベース関係
//・0 IDを振る処理
//・1Memデータに処理を渡す
//・2作成ボタン
//	・2-2 名前欄　選択時
//	・2-3 プレイヤー選択時
//・3変更ボタン
//・4削除ボタン
//・5決定ボタン

//	ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー

//・2部-戦歴データベース関係
//**************************************************************************
//**************************************************************************
//	Proccess  :	0 IDを振る処理
//	Name	  :	若杉泰周
//	Date	  :	2022 / 9 / 27
//**************************************************************************
procedure TMAS290200f.IDCount();
var
	i : Integer;
begin
	dxMemData1.DisableControls;
	m_DataModule.BeginTran(m_CorpConnect);

	with m_Query do
	begin
		try
			dxMemData1.First;
                for i := 1 to dxMemData1.RecordCount do
                begin
                    Close;
                    SQL.Clear;
                    SQL.Add('UPDATE _PLAYER');
                    SQL.Add('SET');
                    SQL.Add('SortID = :AfterSortID');
                    SQL.Add('WHERE');
                    SQL.Add('id = :ID' );
                    SetFld('AfterSortID').AsInteger := i;
                    SetFld('ID').AsInteger := dxMemData1Code.AsInteger;

					if ExecSQL() then
                	begin
                    	m_DataModule.Commit(m_CorpConnect);   	// コミット
                	end;
					dxMemData1.Next;
                end;
        finally
        	Close;
			if m_CorpConnect.InTransaction then
			begin
            	m_DataModule.Rollback(m_CorpConnect); 			// ロールバック
				m_MASCom.m_MsgStd.GetMsgDB(m_MjsMsgRec, m_Query);
            end;
			dxMemData1.EnableControls;
        end;
    end;
	MemdataSetSuru(dxMemData1); // 表示処理
end;


//**************************************************************************
//	Proccess  :	1 Player Memデータに処理を渡す
//	Name	  :	若杉泰周
//	Date	  :	2022 / 9 / 27
//**************************************************************************

procedure TMAS290200f.MemdataSetSuru(var aMem: TdxMemData);
begin
    with m_Query do
    begin

		if aMem.RecordCount > 0 then
        begin
            aMem.Close();  		//念のため一回閉じる
        end;
        aMem.Open();   			//そして開く
        aMem.DisableControls;		//描画を一旦止める処理（速度向上目的）
    	try
            Close;
            SQL.Clear;

			SQL.Add('SELECT ID,SortID,NAME FROM _PLAYER');
			SQL.Add('ORDER BY');
			SQL.Add('ID');

			Open(True);  		  //クエリに入れたSQLを開く

			while EOF = false do  //データの終端じゃなかったら代入
            begin
				aMem.Append;     //追加の準備（レコードを追加
                aMem.FieldByName('Code').AsInteger := GetFld('ID').AsInteger;
				aMem.FieldByName('Name').AsString := GetFld('NAME').AsString;
				aMem.FieldByName('ID').AsString := GetFld('SortID').AsString;
				aMem.Post;       //追加完了（データ書き込み）
				Next;            //終端まで続ける
            end;

        finally
            Close;               //クエリを閉じる
			aMem.EnableControls; //描画を再開する（速度向上目的）
        end;
    end;
end;





//**************************************************************************
//	Component	:	Form // 22/09/21追加
//	Event	    :	2 作成ボタン
//	Name	    :       若杉泰周
//**************************************************************************

procedure TMAS290200f.AddBtnClick(Sender: TObject);
var I : Integer;
	S : String;
begin
	m_DataModule.BeginTran(m_CorpConnect);//トランザクションの開始
	with m_Query do
	begin
		if dxMemData1.Active = False then
        begin
            dxMemData1.Open();
        end;
        SQL.Clear;
		SQL.Add('INSERT INTO _PLAYER (NAME,SortID) values (:Name,:SortID);');
		SetFld('Name').AsString := NameForm.Text;
		SetFld('SortID').AsInteger := dxMemData1.RecordCount+1;
		if(ExecSQL())then ShowMessage('第１段階プレイヤーデータを作成作成しました。続けます。')
        else begin
            ShowMessage('プレイヤーデータを作成できませんでした。すでに作られている可能性があります。キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;

        SQL.Clear;
		SQL.Add('SELECT FIRST ID FROM _PLAYER ORDER BY ID DESC ;');
		if(Open())then ShowMessage('第２段階コードを取得しました｡続けます。')
        else begin
            ShowMessage('第２段階コードを取得できませんでした｡キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;

		I := GetFld('ID').AsInteger;
		S := IntToStr(I);
		SQL.Clear;
		SQL.Add('INSERT INTO _SENREKI (ID) values (' +S+ ');');


		if(ExecSQL(True))then ShowMessage('最終段階｡戦歴データを用意。確定します。')
        else begin
			ShowMessage('第三段階、戦歴データを作れませんでした。キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;

		m_DataModule.Commit(m_CorpConnect);  // コミット

        MemdataSetSuru(dxMemData1);

    end;

end;
//**************************************************************************
//	Component	:	Form // 22/09/21追加
//	Event	    :	2-2 名前欄クリック（作成スイッチング）
//	Name	    :       若杉泰周
//**************************************************************************

procedure TMAS290200f.NameFormClick(Sender: TObject);
begin
	ここに入力してください.Caption := '新しい名前を登録' ;
	Nameform.Text := '';
	if AddBtn.visible = False then
    	AddBtn.visible := True;
	if DeleteBtn.visible = True then
    	DeleteBtn.visible := False;
	if ChangeBtn.visible = True then
    	ChangeBtn.visible := False;
	if DecideBtn.visible = True then
    	DecideBtn.visible := False;
end;

//**************************************************************************
//	Component	:	Form // 22/10/3追加
//	Event	    :	2-3 プレーヤーグリッドクリック（プレイヤー選択）
//	Name	    :       若杉泰周
//**************************************************************************

procedure TMAS290200f.dxPlayerSelect(Sender: TObject);
begin
	ここに入力してください.Caption := '名前を編集する' ;
	NameForm.Text := dxMemData1Name.AsString;
	CodeLabel.caption := IntToStr(dxMemData1Code.AsInteger);
	if AddBtn.visible = True then
    	AddBtn.visible := False;
	if DeleteBtn.visible = False then
    	DeleteBtn.visible := True;
	if ChangeBtn.visible = False then
		ChangeBtn.visible := True;
	if DecideBtn.visible = False then
    	DecideBtn.visible := True;
    NameForm.SetFocus;
end;
//**************************************************************************
//	Component	:	Form // 22/09/21追加
//	Event	    :	3 変更ボタン
//	Name	    :       若杉泰周
//**************************************************************************

procedure TMAS290200f.ChangeBtnClick(Sender: TObject);
begin

	m_DataModule.BeginTran(m_CorpConnect);
	with m_Query do
	begin
        SQL.Clear;
		SQL.Add('UPDATE _PLAYER SET name =(:Name)WHERE id =(:Code) ');
		SetFld('Name').AsString := NameForm.Text;
		SetFld('Code').AsInteger := dxmemdata1.FieldByName('Code').AsInteger;
		if(ExecSQL())then m_DataModule.Commit(m_CorpConnect)  // コミット
        else begin
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
        end;
		if dxMemData1.Active = False then
        begin
            dxMemData1.Open();
        end;
        MemdataSetSuru(dxMemData1);

    end;

end;


//**************************************************************************
//	Component	:	Form // 22/09/21追加
//	Event	    :	4 削除ボタン
//	Name	    :       若杉泰周
//**************************************************************************

procedure TMAS290200f.DeleteBtnClick(Sender: TObject);
begin

		m_DataModule.BeginTran(m_CorpConnect);
	with m_Query do
	begin
        SQL.Clear;
		SQL.Add('DELETE FROM _PLAYER WHERE id =(:Code) ');
		SetFld('Code').AsInteger := dxmemdata1.FieldByName('Code').AsInteger;
		if(ExecSQL())then m_DataModule.Commit(m_CorpConnect)  // コミット
        else begin
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
        end;
		if dxMemData1.Active = False then
        begin
            dxMemData1.Open();
        end;
        MemdataSetSuru(dxMemData1);

    end;
	IDCount();
end;



//**************************************************************************
//	Component	:	Form // 22/09/21追加
//	Event	    :	5 決定ボタン＆戦績データ読み込み
//	Name	    :       若杉泰周
//**************************************************************************
procedure TMAS290200f.DecideBtnClick(Sender: TObject);
var I: Integer;
	S: String;
begin
	m_DataModule.BeginTran(m_CorpConnect);//トランザクションの開始
    if dxMem_SENREKI.RecordCount > 0 then
    begin
        dxMem_SENREKI.Close();  		//念のため一回閉じる
    end;
    dxMem_SENREKI.Open();   			//そして開く
    dxMem_SENREKI.DisableControls;		//描画を一旦止める処理（速度向上目的）

	S := dxMemData1Code.AsString;
	with m_Query do
	begin
        SQL.Clear;
		SQL.Add('SELECT Num,SeriouslyLevel,DrowNo,Hand,SYOUHAI,YOI FROM _SENREKI');
		SQL.Add('WHERE ID ='+ S +'ORDER BY ID DESC ;');
		if(Open(True))then
		begin
            m_DataModule.Commit(m_CorpConnect);  // コミット
		end
        else begin
            ShowMessage('選択中のプレイヤーの戦績データを取得できませんでした。キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;

        while EOF = false do  //データの終端でなければ実行
        begin
            dxMem_SENREKI.Append;     //追加の準備（レコードを追加
            dxMem_SENREKI.FieldByName('Num').AsInteger := GetFld('Num').AsInteger;
            dxMem_SENREKI.FieldByName('SeriouslyLevel').AsString := GetFld('SeriouslyLevel').AsString;
            dxMem_SENREKI.FieldByName('DrowNo').AsInteger := GetFld('DrowNo').AsInteger;
            dxMem_SENREKI.FieldByName('Hand').AsString := GetFld('Hand').AsString;
			dxMem_SENREKI.FieldByName('SYOUHAI').AsString := GetFld('SYOUHAI').AsString;
			dxMem_SENREKI.FieldByName('YOI').AsString := GetFld('YOI').AsString;
            dxMem_SENREKI.Post;       //追加完了（データ書き込み）
            Next;            //終端まで続ける
        end;
    	Close;               //クエリを閉じる
		dxMem_SENREKI.EnableControls; //描画を再開する（速度向上目的）
		if dxMem_SENREKI.RecordCount = 0 then
        	ShowMessage('データがまだありませんでした');
      end;
		//画面切り替え
		dxDBGrid2.visible := True;
        dxDBGrid1.visible := False;
		BackBtn.visible := True;
		DecideBtn.visible := False;
		ChangeBtn.visible := False;
		DeleteBtn.visible := False;
		DeleteBtn.visible := False;
        MEkakusi.visible := False;
		Bunseki();

end;
//**************************************************************************
//	Component	:	Form // 22/09/21追加
//	Event	    :	6 戻るボタン
//	Name	    :       若杉泰周
//**************************************************************************
procedure TMAS290200f.BackBtnclick(Sender: TObject);
begin
	if dxMem_SENREKI.RecordCount > 0 then
    begin
        dxMem_SENREKI.Close();  		//戦歴データを閉じる。
    end;
	dxDBGrid2.visible := False;
    dxDBGrid1.visible := True;
    DecideBtn.visible := True;
	BackBtn.visible := False;
    DecideBtn.visible := True;
    ChangeBtn.visible := True;
    DeleteBtn.visible := True;
    MEkakusi.visible  := True;
end;
//**************************************************************************
//目次
//・1部-プレイヤーデータベース関係
//	ーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーーー

//・2部-戦歴データベース関係

//・2-1戦歴データ登録
//・2-2 勝ち負け判定
//・2-3 データ分析

//**************************************************************************
//**************************************************************************
//	Component	:	Form // 22/10/3追加
//	Event	    :	2-1戦歴データ登録
//	Name	    :       若杉泰周
//**************************************************************************
procedure TMAS290200f.SENREKIdataTOUROKU(Sender: TObject);
var I : Integer;
	PlayerCode : String;
	MaxNum: string;
begin
    //	真剣度
    if SinkenBtn3.checked =true then        m_sSinkenLv:='''ガチ'''
    else if SinkenBtn2.checked =true then   m_sSinkenLv:='''普通'''
    else if SinkenBtn1.checked =true then   m_sSinkenLv:='''適当''';

    //酔い
    if YoiBox.text ='なし' then             m_sYoiLv :='''なし'''
    else if YoiBox.text ='ほろ酔い' then    m_sYoiLv :='''ほろ酔い'''
    else if YoiBox.text ='べろべろ' then    m_sYoiLv :='''べろべろ''';

    //何手目
    if DrowNoBox.text ='１手目' then         m_sDrowNo  :='1'
    else if DrowNoBox.text ='２手目' then    m_sDrowNo  :='2'
    else if DrowNoBox.text ='３手目' then    m_sDrowNo  :='3';
	//勝敗がつくまで更新する
	m_iDrowNo:= m_iDrowNo +1;
	if m_iDrowNo=1 then DrowNoBox.text :='２手目'
	else if m_iDrowNo=2 then DrowNoBox.text :='３手目';


    //手
    if TButton(Sender).Caption ='グー'        then
    begin
         M_sHand :='''グー''';
		HandText.Text := 'グー';
    end
    else if TButton(Sender).Caption ='チョキ' then
    begin
         M_sHand :='''チョキ''';
		HandText.Text := 'チョキ';
    end
    else if TButton(Sender).Caption ='パー'   then
    begin
        M_sHand :='''パー''';;
		HandText.Text := 'グー';
    end;

    //勝敗
	SYOUHAIlabel.Text := 'あいこ';

    //SQL
    //トランザクションの開始
	m_DataModule.BeginTran(m_CorpConnect);
	with m_Query do
	begin
	//プレイヤーコード（ID）の取得
		PlayerCode := dxMemData1Code.AsString;
	//プレイヤーの戦歴数（Num）の取得
        SQL.Clear;
		SQL.Add('SELECT FIRST Num FROM _SENREKI WHERE ID = '+PlayerCode+' ORDER BY Num DESC ;');
	//SQL実行判定
		if(Open())then
        else begin
            ShowMessage('プレイヤー戦歴データ数を取得できませんでした｡キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;
		I := GetFld('Num').AsInteger+1;
		MaxNum := IntToStr(I);

        SQL.Clear;
		SQL.Add('INSERT INTO _SENREKI (ID,Num,SYOUHAI,Hand,SeriouslyLevel,DrowNo,YOI) values (');//データベース入力部分
		SQL.Add(''+ PlayerCode +',');                                                    //ID
		SQL.Add(MaxNum +',');                                                   //Num（その人のデータ数）
		SQL.Add('''あいこ'''+',');                                              //勝敗
		SQL.Add(m_sHand +',');                                                  //手
		SQL.Add(m_SSinkenLv+',');                                               //真剣度
		SQL.Add(m_sDrowNo+',');                                                 //何手目
		SQL.Add(m_sYoiLv+');');                                                 //酔い

		if(ExecSQL(true))then
        else begin
            ShowMessage('データを作成できませんでした。キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;


		m_DataModule.Commit(m_CorpConnect);  // コミット
        DecideBtnClick(Sender);

    end;

end;
//**************************************************************************
//	Component	:	Form // 22/10/3追加
//	Event	    :	2-2 勝ち負け判定
//	Name	    :       若杉泰周
//**************************************************************************
procedure TMAS290200f.WinBtnClick(Sender: TObject);
var I : Integer;
	PlayerCode : String;
	MaxNum: string;
	m_sSYOUHAI : string;
begin
	//勝ちか負けを変数に入れる
	m_sSYOUHAI:= ''''+TBUtton(Sender).caption+'''';
	 //SQL
    //トランザクションの開始
	m_DataModule.BeginTran(m_CorpConnect);
	with m_Query do
	begin
	//プレイヤーコード（ID）の取得
		PlayerCode := dxMemData1Code.AsString;
	//プレイヤーの戦歴数（Num）の取得
        SQL.Clear;
		SQL.Add('SELECT FIRST Num FROM _SENREKI WHERE ID = '+PlayerCode+' ORDER BY Num DESC ;');
	//SQL実行判定
		if(Open())then
        else begin
            ShowMessage('プレイヤー戦歴データ数を取得できませんでした｡キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;
		I := GetFld('Num').AsInteger;
		MaxNum := IntToStr(I);
        CodeLabel.caption := MaxNum;
        SQL.Clear;
		SQL.Add('UPDATE _SENREKI SET SYOUHAI='+m_sSYOUHAI);
		SQL.Add('WHERE ID ='+ PlayerCode +'AND Num='+ MaxNum);

		if(ExecSQL())then
        else begin
            ShowMessage('勝敗を更新できませんでした。キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;
		SYOUHAIlabel.text:= TBUtton(Sender).caption;
		m_DataModule.Commit(m_CorpConnect);  // コミット
        DecideBtnClick(Sender);

    end;
	//引き分け回数をリセット
	m_iDrowNo:= 0;
	DrowNoBox.text :='１手目';



end;
//**************************************************************************
//	Component	:	Form // 22/10/3追加
//	Event	    :	2-3 データ分析
//	Name	    :       若杉泰周
//**************************************************************************
procedure TMAS290200f.Bunseki();
var I : Integer;
	PlayerCode : String;
	MaxNum: string;

	Colum: string;
begin
	//プレイヤーコード（ID）の取得
	PlayerCode := dxMemData1Code.AsString;
	m_iMAX:=0;
    if dxMem_Bunseki.RecordCount > 0 then
    begin
        dxMem_Bunseki.Close();  		//念のため一回閉じる
    end;
    dxMem_Bunseki.Open();
	dxMem_Bunseki.DisableControls;		//描画を一旦止める処理（速度向上目的）
    //トランザクションの開始
	m_DataModule.BeginTran(m_CorpConnect);
	with m_Query do
	begin
//手の数を取得
        dxMem_Bunseki.Append;
        BunsekiSQL('グー','',m_iMAX,'Gu');
        BunsekiSQL('チョキ','',m_iMAX,'Tyoki');
        BunsekiSQL('パー','',m_iMAX,'Pa');
        SQL.Clear;
        SQL.Add('SELECT Hand,COUNT(Num)AS 数 FROM _SENREKI WHERE ID = '+PlayerCode+'GROUP BY Hand ORDER BY 数 DESC;');
        Open();
        dxMem_Bunseki.FieldByName('Most').AsString:=GetFld('Hand').AsString;
        dxMem_Bunseki.Post;
//-------------------------------------------
        dxMem_Bunseki.Append;
        BunsekiSQL('グー','AND DrowNo = 1',m_iMAX,'Gu');
        BunsekiSQL('チョキ','AND DrowNo = 1',m_iMAX,'Tyoki');
        BunsekiSQL('パー','AND DrowNo = 1',m_iMAX,'Pa');
		SQL.Clear;
        SQL.Add('SELECT Hand,COUNT(Num)AS 数 FROM _SENREKI WHERE ID = '+PlayerCode+'AND DrowNo = 1 GROUP BY Hand ORDER BY 数 DESC;');
        Open();
        dxMem_Bunseki.FieldByName('Most').AsString:=GetFld('Hand').AsString;
        dxMem_Bunseki.Post;
//-------------------------------------------
        dxMem_Bunseki.Append;
        BunsekiSQL('グー','AND DrowNo = 2',m_iMAX,'Gu');
        BunsekiSQL('チョキ','AND DrowNo = 2',m_iMAX,'Tyoki');
        BunsekiSQL('パー','AND DrowNo = 2',m_iMAX,'Pa');
		SQL.Clear;
        SQL.Add('SELECT Hand,COUNT(Num)AS 数 FROM _SENREKI WHERE ID = '+PlayerCode+'AND DrowNo = 2 GROUP BY Hand ORDER BY 数 DESC;');
        Open();
        dxMem_Bunseki.FieldByName('Most').AsString:=GetFld('Hand').AsString;
        dxMem_Bunseki.Post;
//-------------------------------------------
        dxMem_Bunseki.Append;
        BunsekiSQL('グー','AND DrowNo = 3',m_iMAX,'Gu');
        BunsekiSQL('チョキ','AND DrowNo = 3',m_iMAX,'Tyoki');
        BunsekiSQL('パー','AND DrowNo = 3',m_iMAX,'Pa');
		SQL.Clear;
        SQL.Add('SELECT Hand,COUNT(Num)AS 数 FROM _SENREKI WHERE ID = '+PlayerCode+'AND DrowNo = 3 GROUP BY Hand ORDER BY 数 DESC;');
        Open();
        dxMem_Bunseki.FieldByName('Most').AsString:=GetFld('Hand').AsString;
        dxMem_Bunseki.Post;
    end;

	dxMem_Bunseki.EnableControls; //描画を再開する（速度向上目的）
	m_DataModule.Commit(m_CorpConnect);  // コミット
 // dxMem_Bunseki.close();



end;

procedure TMAS290200f.BunsekiSQL(Hand,ZYOUKEN:string; m_iMAX:Integer; Colum: string);
var I : Integer;
	PlayerCode,A: String;
begin
    //SQL
	with m_Query do
	begin
	//プレイヤーコード（ID）の取得
		PlayerCode := dxMemData1Code.AsString;
	//手の数を取得
        SQL.Clear;
		SQL.Add('SELECT Hand,COUNT(Num)AS 数 FROM _SENREKI WHERE ID = '+PlayerCode+' AND Hand='''+Hand+''''+ZYOUKEN+' GROUP BY Hand;');
	//SQL実行判定
		if(Open())then
        else begin
            ShowMessage(Hand+'の数を取得できませんでした｡キャンセルします。');
            m_DataModule.Rollback(m_CorpConnect); // ロールバック
			exit;
        end;
        A := GetFld('Hand').AsString;
        if A =Hand then
		begin
			I:= StrToInt(GetFld('数').AsString);
        	dxMem_Bunseki.FieldByName(Colum).AsString:=GetFld('数').AsString;
            if m_iMAX< I then
				m_iMAX:= I
        end
        else
            dxMem_Bunseki.FieldByName(Colum).AsString:='0';
    end;
end;
//**************************************************************************
//	Component	:	Form // 00/11/01追加
//	Event	    :	OnHide
//	Name	    :
//**************************************************************************
procedure TMAS290200f.FormHide(Sender: TObject);
begin
//
end;

//**************************************************************************
//	Component	:	Form
//	Event	    :	OnCloseQuery
//	Name	    :
//**************************************************************************
procedure TMAS290200f.FormCloseQuery(Sender: TObject;
  var CanClose: Boolean);
begin
	CanClose := True;
end;

//**************************************************************************
//	Component	:	Form
//	Event		:	OnClose
//	Name		:
//**************************************************************************
procedure TMAS290200f.FormClose(Sender: TObject; var Action: TCloseAction);
var
	AppPara	:	TAppParam;
begin
	m_pMyAppRecord^.m_iDelete := 1;
	AppPara.iAction			  := ACTID_FORMCLOSEEND;			// 呼び出し区分 設定
	AppPara.pRecord			  := Pointer(m_pMyAppRecord);		// 管理構造体ﾎﾟｲﾝﾀ設定
	AppPara.pActionParam	  := nil;							// 予備ﾎﾟｲﾝﾀ 設定

	TMjsAppRecord(m_pMyAppRecord^).m_pOwnerEntry(@AppPara);		// 親を呼び出す!!

	Action := caFree;
end;

//**************************************************************************
//	Proccess  :	CM_CHILDKEY
//	Name	  :
//	Date	  :	2001 / 06 / 05
//	Parameter :	Msg		TWMKey
//	Retrun	  :
//	History	  :	2001 / 99 / 99	X.Xxxxxx
//				XXXXXXXX修正内容
//**************************************************************************
procedure TMAS290200f.CMChildKey(var Msg: TWMKey);
var
	sShift		:	TShiftState;
	twAcCtrl	:	TWinControl;
begin
	sShift := MJSKeyDataToShiftState(Msg.KeyData);			// Shiftｷｰの取得<ML30063> MOD KeyDataToShiftState

	if GetKeyState(VK_MENU) < 0 then						// Altキーをひろう
		Exit;

	twAcCtrl := Screen.ActiveControl;
	if twAcCtrl is TSelectStrGrid then						// TMNumEditのItemsが開いている？
		Exit;

	m_AcControl := Screen.ActiveControl;

	inherited;
end;

//**************************************************************************
//	Component	:	Sb_End
//	Event		:	OnClick
//	Name		:
//**************************************************************************
procedure TMAS290200f.Sb_EndClick(Sender: TObject);
begin
	Close;
end;

procedure TMAS290200f.Sb_MainClick(Sender: TObject);
begin

end;


//**************************************************************************
//	Proccess  :	会社基本情報読込処理
//	Name	  :	 Y.Yanagihara
//	Date	  :	2021/ 08 / 20
//**************************************************************************
procedure TMAS290200f.GetDTMain(var aDTMainData: TDTMainData);
begin
    with m_Query do
    begin
    	try
            Close;
            SQL.Clear;
            SQL.Add('SELECT');
            SQL.Add(' YearKbn');
            SQL.Add(',ComKbn2');
            SQL.Add(',ComKbn3');
            SQL.Add(',DTName7');
            SQL.Add('FROM');
            SQL.Add(' DTMain');

            Open(True);

            if (EOF = False) then
            begin
				aDTMainData.YearKbn := GetFld('YearKbn').AsInteger;
                aDTMainData.ComKbn2	:= GetFld('ComKbn2').AsInteger;
                aDTMainData.ComKbn3	:= GetFld('ComKbn3').AsInteger;
                aDTMainData.DTName7	:= GetFld('DTName7').AsString;
            end;
        finally
            Close;
        end;
    end;
end;
//**************************************************************************
//	Proccess  :	印刷処理
//	Name	  : Y.Yanagihara
//	Date	  :	2021/ 08 / 20
//**************************************************************************　
procedure TMAS290200f.Sb_PrintClick(Sender: TObject);
var
    oMjsPrnDlg : TMJSPrnDlgLf;      // 印刷条件設定DLG
    iRet_Prn	: Integer;
    sTitle, sMemFld : TStringList;
begin
    // 印刷用Memdataをセットする
	if (dxMemData_Print.RecordCount > 0) then
        dxMemData_Print.Close;
	MemdataSetSuru(dxMemData_Print);
    dxMemData_Print.First;

    // ﾃﾞｰﾀなしならﾒｯｾｰｼﾞ表示して抜ける
    if (dxMemData_Print.RecordCount = 0) then
    begin
        MjsMessageBoxEx(m_Owner, '対象データが存在しません。', '確認', mjInformation, mjOk, mjDefOk);
        Exit;
    end;

	m_PrnSupport := TMJSPrnSupportL.Create;
    oMJSPrnDlg := TMJSPrnDlgLf.Create(m_Owner);
    try
        m_PrnSupport.ApRB			:=	ppReport1;
        m_PrnSupport.strDocName		:=	('原価率登録');
        m_PrnSupport.pPage			:=	SVppPage;
        m_PrnSupport.pDate			:=	SVppDate;
        m_PrnSupport.pCorpCode		:=	LppCorpCode;
        m_PrnSupport.pCorpName		:=	LppCorpName;
        m_PrnSupport.pAccountOffice	:=	LppAccOffice;
        m_PrnSupport.iReportID		:=  990100;			// ﾁｪｯｸﾘｽﾄ系
        m_PrnSupport.strFileName    :=	rcCOMMONAREA(m_pMyAppRecord^.m_pCommonArea^).SysCliRoot + '\tmp\' + m_PrnSupport.strDocName + '.csv';
        m_PrnSupport.pComArea 		:=  m_pMyAppRecord^.m_pCommonArea;
        m_PrnSupport.pApRec			:=  m_pMyAppRecord;
        m_PrnSupport.MdataModule    :=	m_DataModule;   //m_DataModule
        m_PrnSupport.iDspWriteBtn   :=  0;              // 保存ﾎﾞﾀﾝ制御(0:表示する)
        m_PrnSupport.iDspFileBtn    :=	1;              // ﾌｧｲﾙ出力表示

        if ( m_DTMainData.YearKbn = YEARKBN_WAREKI ) then
            m_PrnSupport.iCalendarKbn	:=  1	//　和暦
        else
            m_PrnSupport.iCalendarKbn	:=  2;	//　西暦

		gfnMasSetPrnInfo (m_PrnSupport,m_Query );

        // 印刷ﾀﾞｲｱﾛｸﾞ表示
        iRet_Prn := oMjsPrnDlg.DoDLG(m_PrnSupport);

        if ( iRet_Prn > 0 ) then
        begin
            // 戻り値が「ﾌﾟﾚﾋﾞｭｰ」かつ、他のAPでﾌﾟﾚﾋﾞｭｰ起動中はｴﾗｰ
            if (m_MjsPre.IsExistPreview) and
               (m_PrnSupport.iCommand = PDLG_PREVIEW) then
            begin
                MessageBeep(MB_OK);
                MjsMessageBox(m_Owner, '他の処理でプレビューが起動しています。'+#13#10+
                                    '他のプレビューを終了してください。',
                            mjInformation, mjDefOk);
                Exit;
            end;

            case m_PrnSupport.iCommand of
            PDLG_PRINT, PDLG_PREVIEW:
                begin
                    m_MjsPre.Exec(m_PrnSupport, oMJSPrnDlg, Nil);
                end;
            PDLG_FILE:
                begin
                    sTitle	:= TStringList.Create;
                    sMemFld := TStringList.Create;

                    try
                        SetFileOut(sTitle,sMemFld);
                        if (MjsFileOutL(dxMemData_Print, sMemFld, sTitle,
                                       m_PrnSupport, m_pMyAppRecord ) = RET_NG) then
                        begin
                           MessageBeep(MB_OK);
                           MessageDlg('ファイル出力に失敗しました。', mtError, [mbOk], 0);
                        end;
                    finally
                        sTitle.Free;
                        sMemFld.Free;
                    end;
                end;
            end;
        end;
    finally
		if Assigned(m_PrnSupport) then
        	m_PrnSupport.Free;
        if Assigned(oMjsPrnDlg) then
        	oMjsPrnDlg.Free;
    end;
end;

//**************************************************************************
//	Component	:	Sb_Change
//	Event		:	OnClick
//	Name		:
//**************************************************************************
procedure TMAS290200f.Sb_ChangeClick(Sender: TObject);
var
	wkParam : TAppParam;
	iAction : Integer;
begin
	// 切り出し
	if CompareStr(Sb_Change.Caption,'切出(&G)') = 0 then
	begin
		Sb_Change.Caption := '埋込(&G)';
		ClientHeight := Trunc(622 * m_iZoom / 100);
		ClientWidth  := Trunc(945 * m_iZoom / 100);
		iAction      := ACTID_DOCKINGOUTEND;
	end
	// 埋め込み
	else
	begin
		Sb_Change.Caption := '切出(&G)';
		ClientHeight := Trunc(622 * m_iZoom / 100);
		ClientWidth  := Trunc(945 * m_iZoom / 100);
		iAction      := ACTID_DOCKINGINEND;
	end;

	wkParam.iAction := iAction;
	wkParam.pRecord := Pointer(m_pMyAppRecord);
	wkParam.pActionParam := nil;
	TMjsAppRecord(m_pMyAppRecord^).m_pOwnerEntry(@wkParam);
end;

end.
```