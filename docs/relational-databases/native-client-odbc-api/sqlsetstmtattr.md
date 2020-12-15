---
description: SQLSetStmtAttr
title: SQLSetStmtAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetStmtAttr function
ms.assetid: 799c80fd-c561-4912-8562-9229076dfd19
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e338ba67bdd2535f54e4678b4ff013c768571da8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465099"
---
# <a name="sqlsetstmtattr"></a>SQLSetStmtAttr
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不支援混合式 (索引鍵集/動態) 資料指標模型。 如果設定的值不等於 0，使用 SQL_ATTR_KEYSET_SIZE 設定索引鍵值大小的嘗試將會失敗。  
  
 應用程式會將所有語句上的 SQL_ATTR_ROW_ARRAY_SIZE 設定為宣告 **SQLFetch** 或 [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) 函式呼叫所傳回的資料列數目。 在表示伺服器資料指標的陳述式上，驅動程式會使用 SQL_ATTR_ROW_ARRAY_SIZE 決定伺服器所產生之資料列區塊的大小以滿足來自資料指標的提取要求。 在動態資料指標的區塊大小內，如果交易隔離等級足以確保可重複讀取已認可的交易，資料列成員資格與排序是固定的。 在此值指出的區塊之外，資料指標是完全動態的。 伺服器資料指標區塊大小是完全動態的，而且可以在提取處理的任何點變更。  
  
## <a name="sqlsetstmtattr-and-table-valued-parameters"></a>SQLSetStmtAttr 和資料表值參數  
 在存取資料表值參數資料行的描述項欄位之前，SQLSetStmtAttr 可以用來將應用程式參數描述項中的 SQL_SOPT_SS_PARAM_FOCUS 設定 (APD) 。  
  
 如果嘗試將 SQL_SOPT_SS_PARAM_FOCUS 設定為不是資料表值參數之參數的序數，SQLSetStmtAttr 會傳回 SQL_ERROR，而且會以 SQLSTATE = HY024 和訊息「不正確屬性值」來建立診斷記錄。 當傳回 SQL_ERROR 時，SQL_SOPT_SS_PARAM_FOCUS 不會變更。  
  
 將 SQL_SOPT_SS_PARAM_FOCUS 設定為 0 會還原參數之描述項記錄的存取權。  
  
 SQLSetStmtAttr 也可用來設定 SQL_SOPT_SS_NAME_SCOPE。 如需詳細資訊，請參閱本主題稍後的「SQL_SOPT_SS_NAME_SCOPE」一節。  
  
 如需詳細資訊，請參閱備妥之 [語句的資料表值參數中繼資料](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)。  
  
 如需資料表值參數的詳細資訊，請參閱 [&#40;ODBC&#41;的資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetstmtattr-support-for-sparse-columns"></a>疏鬆資料行的 SQLSetStmtAttr 支援  
 SQLSetStmtAttr 可以用來設定 SQL_SOPT_SS_NAME_SCOPE。 如需詳細資訊，請參閱本主題稍後的 SQL_SOPT_SS_NAME_SCOPE 一節。如需有關稀疏資料行的詳細資訊，請參閱 [&#40;ODBC&#41;的稀疏資料行支援 ](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)。  
  
## <a name="statement-attributes"></a>陳述式屬性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式也支援下列驅動程式專屬的陳述式屬性。  
  
### <a name="sql_sopt_ss_cursor_options"></a>SQL_SOPT_SS_CURSOR_OPTIONS  
 SQL_SOPT_SS_CURSOR 屬性會指定驅動程式是否會在資料指標上使用驅動程式專屬的效能選項。 設定這些選項時，不允許[SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 。 預設值為 SQL_CO_OFF。 *ValuePtr* 值的類型為 SQLLEN。  
  
|*ValuePtr* 值|描述|  
|----------------------|-----------------|  
|SQL_CO_OFF|預設值。 停用快速順向、唯讀資料指標和自動擷取，可讓您在順向、唯讀資料指標上 **SQLGetData** 。 當 SQL_SOPT_SS_CURSOR_OPTIONS 設定為 SQL_CO_OFF 時，資料指標類型將不會變更。 也就是說，快速順向資料指標仍是快速順向資料指標。 若要變更資料指標類型，應用程式現在必須使用 **SQLSetStmtAttr**/SQL_ATTR_CURSOR_TYPE 設定不同的資料指標類型。|  
|SQL_CO_FFO|啟用快速順向、唯讀資料指標，在順向、唯讀資料指標上停用 **SQLGetData** 。|  
|SQL_CO_AF|在任何資料指標類型上啟用自動擷取選項。 針對語句控制碼設定此選項時， **SQLExecute** 或 **SQLExecDirect** 將會產生隱含 **SQLFetchScroll** (SQL_FIRST) 。 資料指標會開啟，而且第一個批次的資料列會在伺服器的單一往返中傳回。|  
|SQL_CO_FFO_AF|使用自動擷取選項啟用快速順向資料指標。 這在同時指定 SQL_CO_AF 和 SQL_CO_FFO 時相同。|  
  
 設定這些選項時，如果伺服器偵測到已經提取最後一個資料列，則會自動關閉資料指標。 應用程式仍然必須呼叫 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) (SQL_CLOSE) 或 [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)，但驅動程式不需要將關閉通知傳送至伺服器。  
  
 如果選取清單包含 **text**、 **Ntext** 或 **image** 資料行，則快速順向資料指標會轉換成動態資料指標，並允許 **SQLGetData** 。  
  
### <a name="sql_sopt_ss_defer_prepare"></a>SQL_SOPT_SS_DEFER_PREPARE  
 SQL_SOPT_SS_DEFER_PREPARE 屬性會決定在執行 **SQLExecute**、 [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) 或 [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md) 之前，語句是否立即準備或延後。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 和先前版本中，會忽略此屬性 (沒有延遲準備)。 *ValuePtr* 值的類型為 SQLLEN。  
  
|*ValuePtr* 值|描述|  
|----------------------|-----------------|  
|SQL_DP_ON|預設值。 在呼叫 [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)函式之後，語句準備會延遲，直到呼叫 **SQLExecute** ，或執行中繼屬性作業 (**SQLDescribeCol** 或 **SQLDescribeParam**) 執行為止。|  
|SQL_DP_OFF|語句會在 **SQLPrepare** 執行時立即備妥。|  
  
### <a name="sql_sopt_ss_regionalize"></a>SQL_SOPT_SS_REGIONALIZE  
 SQL_SOPT_SS_REGIONALIZE 屬性用於決定陳述式層級的資料轉換。 將日期、時間和貨幣值轉換為字元字串時，此屬性會使驅動程式遵從用戶端的地區設定。 此轉換僅能從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生資料類型轉換成字元字串。  
  
 *ValuePtr* 值的類型為 SQLLEN。  
  
|*ValuePtr* 值|描述|  
|----------------------|-----------------|  
|SQL_RE_OFF|預設值。 此驅動程式不會使用用戶端地區設定，將日期、時間和貨幣資料轉換成字元字串資料。|  
|SQL_RE_ON|將日期、時間和貨幣資料轉換成字元字串資料時，此驅動程式會使用用戶端地區設定。|  
  
 地區轉換設定適用於貨幣、數值、日期和時間資料類型。 此轉換設定只有在貨幣、數值、日期或時間值轉換為字元字串時，才會套用到輸出轉換。  
  
> [!NOTE]  
>  當 SQL_SOPT_SS_REGIONALIZE 陳述式選項開啟時，驅動程式會針對目前的使用者使用地區設定的登錄設定。 如果應用程式設定，驅動程式不會接受目前線程的地區設定，例如，呼叫 **SetThreadLocale**。  
  
 變更資料來源的地區行為可能會導致應用程式失敗。 剖析日期字串並預期日期字串如 ODBC 定義之方式顯示的應用程式，可能會受到變更此值的負面影響。  
  
### <a name="sql_sopt_ss_textptr_logging"></a>SQL_SOPT_SS_TEXTPTR_LOGGING  
 SQL_SOPT_SS_TEXTPTR_LOGGING 屬性會在包含 **文字** 或 **影像** 資料的資料行上，切換作業的記錄。 *ValuePtr* 值的類型為 SQLLEN。  
  
|*ValuePtr* 值|描述|  
|----------------------|-----------------|  
|SQL_TL_OFF|停用對 **文字** 和 **影像** 資料所執行之作業的記錄。|  
|SQL_TL_ON|預設值。 可記錄在 **文字** 和 **影像** 資料上執行的作業。|  
  
### <a name="sql_sopt_ss_hidden_columns"></a>SQL_SOPT_SS_HIDDEN_COLUMNS  
 SQL_SOPT_SS_HIDDEN_COLUMNS 屬性會在結果集中公開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT FOR BROWSE 陳述式內隱藏的資料行。 此驅動程式預設不會公開這些資料行。 *ValuePtr* 值的類型為 SQLLEN。  
  
|*ValuePtr* 值|描述|  
|----------------------|-----------------|  
|SQL_HC_OFF|預設值。 FOR BROWSE 資料行會從結果集隱藏起來。|  
|SQL_HC_ON|公開 FOR BROWSE 資料行。|  
  
### <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 屬性會傳回查詢通知要求的訊息文字。  
  
### <a name="sql_sopt_ss_querynotification_options"></a>SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS 屬性會指定用於查詢通知要求的選項。 這些是使用 `name=value` 語法在字串中指定，如下所示。 應用程式會負責建立此服務以及在佇列外部讀取通知。  
  
 查詢通知選項字串的語法為：  
  
 `service=<service-name>[;(local database=<database>|broker instance=<broker instance>)]`  
  
 例如：  
  
 `service=mySSBService;local database=mydb`  
  
### <a name="sql_sopt_ss_querynotification_timeout"></a>SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
 SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT 屬性會指定查詢通知維持作用中的秒數。 預設值是 432000 秒 (5 天)。 *ValuePtr* 值的類型為 SQLLEN。  
  
### <a name="sql_sopt_ss_param_focus"></a>SQL_SOPT_SS_PARAM_FOCUS  
 SQL_SOPT_SS_PARAM_FOCUS 屬性會指定後續 SQLBindParameter、SQLGetDescField、SQLSetDescField、SQLGetDescRec 和 SQLSetDescRec 呼叫的焦點。  
  
 SQL_SOPT_SS_PARAM_FOCUS 的類型是 SQLULEN。  
  
 預設值為 0，表示這些呼叫處理的參數會對應到 SQL 陳述式中的參數標記。 設定為資料表值參數的參數號碼時，這些呼叫會處理該資料表值參數的資料行。 設定為非資料表值參數之參數號碼的值時，這些呼叫會傳回錯誤 IM020：「參數焦點沒有參考資料表值參數」。  
  
### <a name="sql_sopt_ss_name_scope"></a>SQL_SOPT_SS_NAME_SCOPE  
 SQL_SOPT_SS_NAME_SCOPE 屬性會指定後續目錄函數呼叫的名稱範圍。 SQLColumns 所傳回的結果集會視 SQL_SOPT_SS_NAME_SCOPE 的設定而定。  
  
 SQL_SOPT_SS_NAME_SCOPE 的類型是 SQLULEN。  
  
|*ValuePtr* 值|描述|  
|----------------------|-----------------|  
|SQL_SS_NAME_SCOPE_TABLE|預設值。<br /><br /> 使用資料表值參數時，指出應該傳回實際資料表的中繼資料。<br /><br /> 使用「稀疏資料行」功能時，SQLColumns 只會傳回非「稀疏 **column_set**」成員的資料行。|  
|SQL_SS_NAME_SCOPE_TABLE_TYPE|表示應用程式需要資料表類型 (而非實際資料表) 的中繼資料 (目錄函數應該傳回資料表類型的中繼資料)。 然後，應用程式會以 *TableName* 參數的形式傳遞資料表值參數的 TYPE_NAME。|  
|SQL_SS_NAME_SCOPE_EXTENDED|使用「稀疏資料行」功能時，SQLColumns 會傳回所有資料行，不論 **column_set** 成員資格。|  
|SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET|使用「稀疏資料行」功能時，SQLColumns 只會傳回屬於稀疏 **column_set** 成員的資料行。|  
|SQL_SS_NAME_SCOPE_DEFAULT|等於 SQL_SS_NAME_SCOPE_TABLE。|  
  
 SS_TYPE_CATALOG_NAME 和 SS_TYPE_SCHEMA_NAME 分別用於 *CatalogName* 和 *SchemaName* 參數，以識別資料表值參數的目錄和架構。 當應用程式完成擷取資料表值參數的中繼資料時，必須將 SQL_SOPT_SS_NAME_SCOPE 社回 SQL_SS_NAME_SCOPE_TABLE 的預設值。  
  
 當 SQL_SOPT_SS_NAME_SCOPE 設定為 SQL_SS_NAME_SCOPE_TABLE 時，連結伺服器的查詢會失敗。 使用包含伺服器元件的目錄呼叫 SQLColumns 或 SQLPrimaryKeys 將會失敗。  
  
 如果嘗試將 SQL_SOPT_SS_NAME_SCOPE 設定為無效值，會傳回 SQL_ERROR，並產生包含 SQLSTATE HY024 與「屬性值無效」訊息的診斷記錄。  
  
 如果 SQL_SOPT_SS_NAME_SCOPE 具有 SQL_SS_NAME_SCOPE_TABLE 以外的值，則會呼叫目錄函式，然後再呼叫 SQLTables、SQLColumns 或 SQLPrimaryKeys，SQL_ERROR 會傳回。 此時會產生包含 SQLSTATE HY010 與「函數順序錯誤 (SQL_SOPT_SS_NAME_SCOPE 未設定為 SQL_SS_NAME_SCOPE_TABLE)」訊息的診斷記錄。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetStmtAttr 函式](../../odbc/reference/syntax/sqlgetstmtattr-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
