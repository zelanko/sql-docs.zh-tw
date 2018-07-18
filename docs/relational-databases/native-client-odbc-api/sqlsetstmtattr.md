---
title: SQLSetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d4fe70fb3744aa8ae7bddebac7b640fad9bad989
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422277"
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援混合式 (索引鍵集/動態) 資料指標模型。 如果設定的值不等於 0，使用 SQL_ATTR_KEYSET_SIZE 設定索引鍵值大小的嘗試將會失敗。  
  
 應用程式宣告傳回的資料列數目的所有陳述式上設定 SQL_ATTR_ROW_ARRAY_SIZE **SQLFetch**或是[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)函式呼叫。 在表示伺服器資料指標的陳述式上，驅動程式會使用 SQL_ATTR_ROW_ARRAY_SIZE 決定伺服器所產生之資料列區塊的大小以滿足來自資料指標的提取要求。 在動態資料指標的區塊大小內，如果交易隔離等級足以確保可重複讀取已認可的交易，資料列成員資格與排序是固定的。 在此值指出的區塊之外，資料指標是完全動態的。 伺服器資料指標區塊大小是完全動態的，而且可以在提取處理的任何點變更。  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>SQLSetStmtAttr 和資料表值參數  
 SQLSetStmtAttr 可以用來設定應用程式參數描述項 (APD) 中的 SQL_SOPT_SS_PARAM_FOCUS，才能存取資料表值參數資料行的描述項欄位。  
  
 如果嘗試將 SQL_SOPT_SS_PARAM_FOCUS 設定為參數，也就是不是資料表值參數、 SQLSetStmtAttr 傳回 SQL_ERROR 和診斷記錄建立包含 SQLSTATE 的序數 = 其中包含 sqlstate=hy024 及 「 屬性值無效 」 訊息。 當傳回 SQL_ERROR 時，SQL_SOPT_SS_PARAM_FOCUS 不會變更。  
  
 將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0 會還原參數之描述項記錄的存取權。  
  
 SQLSetStmtAttr 也可以用於設定 SQL_SOPT_SS_NAME_SCOPE。 如需詳細資訊，請參閱本主題稍後的「SQL_SOPT_SS_NAME_SCOPE」一節。  
  
 如需詳細資訊，請參閱 <<c0> [ 備妥的陳述式資料表值參數中繼資料](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 如需有關資料表值參數的詳細資訊，請參閱 < [Parameters &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>疏鬆資料行的 SQLSetStmtAttr 支援  
 SQLSetStmtAttr 可以用於設定 SQL_SOPT_SS_NAME_SCOPE。 如需詳細資訊，請參閱 sql_sopt_ss_name_scope 」 一節中，本主題稍後的。如需有關疏鬆資料行的詳細資訊，請參閱 <<c0> [ 疏鬆資料行支援&#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。</c0>  
  
## <a name="statement-attributes"></a>陳述式屬性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式也支援下列驅動程式專屬的陳述式屬性。  
  
### <a name="sqlsoptsscursoroptions"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 SQL_SOPT_SS_CURSOR 屬性會指定驅動程式是否會在資料指標上使用驅動程式專屬的效能選項。 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)設定這些選項時，不允許。 預設值為 SQL_CO_OFF。 *ValuePtr*的值屬於類型是 SQLLEN。  
  
|*ValuePtr*值|描述|  
|----------------------|-----------------|  
|SQL_CO_OFF|預設值。 停用快速順向、 唯讀資料指標與自動擷取，可讓**SQLGetData**順向、 唯讀資料指標。 當 SQL_SOPT_SS_CURSOR_OPTIONS 設定為 SQL_CO_OFF 時，資料指標類型將不會變更。 也就是說，快速順向資料指標仍是快速順向資料指標。 若要變更的資料指標類型，應用程式必須立即設定使用不同的資料指標類型**SQLSetStmtAttr**/SQL_ATTR_CURSOR_TYPE。|  
|SQL_CO_FFO|啟用快速順向、 唯讀資料指標，會停用**SQLGetData**順向、 唯讀資料指標。|  
|SQL_CO_AF|在任何資料指標類型上啟用自動擷取選項。 當此選項設定陳述式控制代碼**SQLExecute**或是**SQLExecDirect**將會產生隱含**SQLFetchScroll** (SQL_FIRST)。 資料指標會開啟，而且第一個批次的資料列會在伺服器的單一往返中傳回。|  
|SQL_CO_FFO_AF|使用自動擷取選項啟用快速順向資料指標。 這在同時指定 SQL_CO_AF 和 SQL_CO_FFO 時相同。|  
  
 設定這些選項時，如果伺服器偵測到已經提取最後一個資料列，則會自動關閉資料指標。 應用程式仍然必須呼叫[SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) (SQL_CLOSE) 或[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)，但驅動程式不需要關閉通知傳送至伺服器。  
  
 如果選取清單包含**文字**， **ntext**，或**映像**資料行，僅向前快轉資料指標會轉換成動態資料指標和**SQLGetData**允許。  
  
### <a name="sqlsoptssdeferprepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 SQL_SOPT_SS_DEFER_PREPARE 屬性會決定是否準備好立即或延後到陳述式**SQLExecute**， [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md)或[SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)會執行。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 和先前版本中，會忽略此屬性 (沒有延遲準備)。 *ValuePtr*的值屬於類型是 SQLLEN。  
  
|*ValuePtr*值|描述|  
|----------------------|-----------------|  
|SQL_DP_ON|預設值。 之後呼叫[SQLPrepare 函數](http://go.microsoft.com/fwlink/?LinkId=59360)，陳述式準備會延遲，直到**SQLExecute**稱為或中繼屬性作業 (**SQLDescribeCol**或**SQLDescribeParam**) 執行。|  
|SQL_DP_OFF|在準備陳述式立即**SQLPrepare**執行。|  
  
### <a name="sqlsoptssregionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 SQL_SOPT_SS_REGIONALIZE 屬性用於決定陳述式層級的資料轉換。 將日期、時間和貨幣值轉換為字元字串時，此屬性會使驅動程式遵從用戶端的地區設定。 此轉換僅能從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生資料類型轉換成字元字串。  
  
 *ValuePtr*的值屬於類型是 SQLLEN。  
  
|*ValuePtr*值|描述|  
|----------------------|-----------------|  
|SQL_RE_OFF|預設值。 此驅動程式不會使用用戶端地區設定，將日期、時間和貨幣資料轉換成字元字串資料。|  
|SQL_RE_ON|將日期、時間和貨幣資料轉換成字元字串資料時，此驅動程式會使用用戶端地區設定。|  
  
 地區轉換設定適用於貨幣、數值、日期和時間資料類型。 此轉換設定只有在貨幣、數值、日期或時間值轉換為字元字串時，才會套用到輸出轉換。  
  
> [!NOTE]  
>  當 SQL_SOPT_SS_REGIONALIZE 陳述式選項開啟時，驅動程式會針對目前的使用者使用地區設定的登錄設定。 驅動程式不會接受目前的執行緒地區設定，如果應用程式設定它，例如，呼叫**SetThreadLocale**。  
  
 變更資料來源的地區行為可能會導致應用程式失敗。 剖析日期字串並預期日期字串如 ODBC 定義之方式顯示的應用程式，可能會受到變更此值的負面影響。  
  
### <a name="sqlsoptsstextptrlogging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 SQL_SOPT_SS_TEXTPTR_LOGGING 屬性切換上包含的資料行的作業記錄**文字**或是**映像**資料。 *ValuePtr*的值屬於類型是 SQLLEN。  
  
|*ValuePtr*值|描述|  
|----------------------|-----------------|  
|SQL_TL_OFF|停用記錄上執行的作業**文字**並**映像**資料。|  
|SQL_TL_ON|預設值。 啟用記錄上執行的作業**文字**並**映像**資料。|  
  
### <a name="sqlsoptsshiddencolumns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 SQL_SOPT_SS_HIDDEN_COLUMNS 屬性會在結果集中公開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT FOR BROWSE 陳述式內隱藏的資料行。 此驅動程式預設不會公開這些資料行。 *ValuePtr*的值屬於類型是 SQLLEN。  
  
|*ValuePtr*值|描述|  
|----------------------|-----------------|  
|SQL_HC_OFF|預設值。 FOR BROWSE 資料行會從結果集隱藏起來。|  
|SQL_HC_ON|公開 FOR BROWSE 資料行。|  
  
### <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 屬性會傳回查詢通知要求的訊息文字。  
  
### <a name="sqlsoptssquerynotificationoptions"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS 屬性會指定用於查詢通知要求的選項。 這些是使用 `name=value` 語法在字串中指定，如下所示。 應用程式會負責建立此服務以及在佇列外部讀取通知。  
  
 查詢通知選項字串的語法為：  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 例如：  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sqlsoptssquerynotificationtimeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT 屬性會指定查詢通知維持作用中的秒數。 預設值是 432000 秒 (5 天)。 *ValuePtr*的值屬於類型是 SQLLEN。  
  
### <a name="sqlsoptssparamfocus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 SQL_SOPT_SS_PARAM_FOCUS 屬性會指定後續 SQLBindParameter、 SQLGetDescField、 SQLSetDescField SQLGetDescRec，焦點和 SQLSetDescRec 呼叫。  
  
 SQL_SOPT_SS_PARAM_FOCUS 的類型是 SQLULEN。  
  
 預設值為 0，表示這些呼叫處理的參數會對應到 SQL 陳述式中的參數標記。 設定為資料表值參數的參數號碼時，這些呼叫會處理該資料表值參數的資料行。 設定為非資料表值參數之參數號碼的值時，這些呼叫會傳回錯誤 IM020：「參數焦點沒有參考資料表值參數」。  
  
### <a name="sqlsoptssnamescope"></a>SQL_SOPT_SS_NAME_SCOPE  
 SQL_SOPT_SS_NAME_SCOPE 屬性會指定後續目錄函數呼叫的名稱範圍。 SQLColumns 所傳回的結果集取決於 SQL_SOPT_SS_NAME_SCOPE 的設定。  
  
 SQL_SOPT_SS_NAME_SCOPE 的類型是 SQLULEN。  
  
|*ValuePtr*值|描述|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|預設值。<br /><br /> 使用資料表值參數時，指出應該傳回實際資料表的中繼資料。<br /><br /> SQLColumns 使用疏鬆資料行功能時，會傳回不是成員的疏鬆資料行**column_set**。|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|表示應用程式需要資料表類型 (而非實際資料表) 的中繼資料 (目錄函數應該傳回資料表類型的中繼資料)。 應用程式接著會傳遞做為資料表值參數的 TYPE_NAME *TableName*參數。|  
|SQL_SS_NAME_SCOPE_EXTENDED|SQLColumns 使用疏鬆資料行功能時，會傳回所有資料行，不論**column_set**成員資格。|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|SQLColumns 使用疏鬆資料行功能時，會傳回成員的疏鬆資料行**column_set**。|  
|SQL_SS_NAME_SCOPE_DEFAULT|等於 SQL_SS_NAME_SCOPE_TABLE。|  
  
 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 會搭配*CatalogName*並*SchemaName*參數，分別以指定的目錄和資料表值參數的結構描述。 當應用程式完成擷取資料表值參數的中繼資料時，必須將 SQL_SOPT_SS_NAME_SCOPE 社回 SQL_SS_NAME_SCOPE_TABLE 的預設值。  
  
 當 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE 時，連結伺服器的查詢會失敗。 SQLColumns 或 SQLPrimaryKeys 使用的類別目錄中包含的伺服器元件的呼叫將會失敗。  
  
 如果嘗試將 SQL_SOPT_SS_NAME_SCOPE 設定為無效值，會傳回 SQL_ERROR，並產生包含 SQLSTATE HY024 與「屬性值無效」訊息的診斷記錄。  
  
 如果目錄函數則 SQLTables、 SQLColumns、 或 SQLPrimaryKeys SQL_SOPT_SS_NAME_SCOPE 以外的值時呼叫會傳回 SQL_SS_NAME_SCOPE_TABLE、 SQL_ERROR。 此時會產生包含 SQLSTATE HY010 與「函數順序錯誤 (SQL_SOPT_SS_NAME_SCOPE 未設定為 SQL_SS_NAME_SCOPE_TABLE)」訊息的診斷記錄。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetStmtAttr 函數](http://go.microsoft.com/fwlink/?LinkId=59355)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
