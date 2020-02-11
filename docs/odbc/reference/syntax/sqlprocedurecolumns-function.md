---
title: SQLProcedureColumns 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5a869d38782478b69ce47656455c38c2b4645b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005748"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLProcedureColumns**會傳回輸入和輸出參數的清單，以及組成指定程式之結果集的資料行。 驅動程式會在指定的語句上，以結果集的形式傳回信息。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *CatalogName*  
 源程式目錄名稱。 如果驅動程式支援某些程式的類別目錄，但不適用於其他程式，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有目錄的程式。 *CatalogName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*CatalogName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*CatalogName*是一般引數;它會以字面方式處理，而且其大小寫很重要。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 源**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 源程式架構名稱的字串搜尋模式。 如果驅動程式支援某些程式的架構，但不適用於其他程式，例如，當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表不具有架構的程式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*SchemaName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*SchemaName*是模式值引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength2*  
 源**SchemaName*的長度（以字元為單位）。  
  
 *ProcName*  
 源程式名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*ProcName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*ProcName*是模式值引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength3*  
 源**ProcName*的長度（以字元為單位）。  
  
 *ColumnName*  
 源資料行名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則*ColumnName*會被視為識別碼，而且其大小寫並不重要。 如果 SQL_FALSE， *ColumnName*就是模式值引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength4*  
 源**ColumnName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLProcedureColumns**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLProcedureColumns**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|已在*StatementHandle*上開啟資料指標，且已呼叫**SQLFetch**或**SQLFetchScroll** 。 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 已在*StatementHandle*上開啟資料指標，但尚未呼叫**SQLFetch**或**SQLFetchScroll** 。|  
|40001|序列化失敗|因為另一筆交易發生資源鎖死，所以交易已回復。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLError**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已呼叫函式，在完成執行之前，會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的使用不正確|SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE， *CatalogName*引數為 null 指標，而 SQL_CATALOG_NAME *InfoType*會傳回支援的目錄名稱。<br /><br /> （DM） SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，而*SchemaName*、 *ProcName*或*ColumnName*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫 SQLProcedureColumns 函式時，此 aynschronous 函數仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY090|不正確字串或緩衝區長度|（DM）其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。<br /><br /> 其中一個 name length 引數的值超過對應的目錄、架構、程式或資料行名稱的最大長度值。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|已指定程式目錄，而驅動程式或資料來源不支援目錄。<br /><br /> 已指定程式架構，而驅動程式或資料來源不支援架構。<br /><br /> 已為程式架構、程式名稱或資料行名稱指定了字串搜尋模式，而且資料來源不支援其中一個或多個引數的搜尋模式。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|在資料來源傳回結果集之前，超時期間已過期。 超時期間是透過**SQLSetStmtAttr**設定，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
 在語句執行之前，通常會使用此函式來抓取程式參數的相關資訊，以及組成程式所傳回之結果集或集合的資料行（如果有的話）。 如需詳細資訊，請參閱[程式](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
> [!NOTE]  
>  **SQLProcedureColumns**可能不會傳回程序所使用的所有資料行。 例如，驅動程式可能只會傳回有關進程所使用之參數的資訊，而不會傳回它所產生的結果集內的資料行。  
  
 *SchemaName*、 *ProcName*和*ColumnName*引數接受搜尋模式。 如需有效搜尋模式的詳細資訊，請參閱[模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLProcedureColumns**會以標準結果集的形式傳回結果，並依 PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME 和 COLUMN_TYPE 排序。 每個程式的資料行名稱會依照下列順序傳回：傳回值的名稱、程式調用中每個參數的名稱（以呼叫順序），然後是程式所傳回之結果集中每個資料行的名稱（依資料行順序）。  
  
 應用程式應該系結相對於結果集結尾的驅動程式特定資料行。 如需詳細資訊，請參閱[目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
 若要判斷 PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME 和 COLUMN_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_PROCEDURE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 選項來呼叫**SQLGetInfo** 。  
  
 ODBC 3 的下列資料行已經重新命名。*x*。 資料行名稱變更不會影響回溯相容性，因為應用程式會依資料行編號來系結。  
  
|ODBC 2.0 資料行|ODBC 3。*x*資料行|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|程式 _OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 下列資料行已新增至**SQLProcedureColumns** for ODBC 3 所傳回的結果集。*x*：  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 下表列出結果集中的資料行。 驅動程式可定義超出資料行19（IS_NullABLE）的其他資料行。 應用程式應該從結果集的結尾向下計算，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱[目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT （ODBC 2.0）|1|Varchar|程式目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些程式的類別目錄，但不適用於其他程式，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有目錄的程式傳回空字串（""）。|  
|PROCEDURE_SCHEM （ODBC 2.0）|2|Varchar|程式架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些程式的架構，但不適用於其他程式，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有架構的程式傳回空字串（""）。|  
|PROCEDURE_NAME （ODBC 2.0）|3|Varchar not Null|程序名稱。 針對沒有名稱的程式，會傳回空字串。|  
|COLUMN_NAME （ODBC 2.0）|4|Varchar not Null|程式資料行名稱。 驅動程式會針對沒有名稱的 procedure 資料行傳回空字串。|  
|COLUMN_TYPE （ODBC 2.0）|5|Smallint 非 NULL|將 procedure 資料行定義為參數或結果集資料行：<br /><br /> SQL_PARAM_TYPE_UNKNOWN：程式資料行是其類型未知的參數。 （ODBC 1.0）<br /><br /> SQL_PARAM_INPUT： procedure 資料行是輸入參數。 （ODBC 1.0）<br /><br /> SQL_PARAM_INPUT_OUTPUT： procedure 資料行是輸入/輸出參數。 （ODBC 1.0）<br /><br /> SQL_PARAM_OUTPUT： procedure 資料行是輸出參數。 （ODBC 2.0）<br /><br /> SQL_RETURN_VALUE： procedure 資料行是程式的傳回值。 （ODBC 2.0）<br /><br /> SQL_RESULT_COL： procedure 資料行是結果集資料行。 （ODBC 1.0）|  
|DATA_TYPE （ODBC 2.0）|6|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或驅動程式特有的 SQL 資料類型。 若為 datetime 和 interval 資料類型，這個資料行會傳回精簡的資料類型（例如，SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR_TO_MONTH）。 如需有效 ODBC SQL 資料類型的清單，請參閱附錄 D：資料類型中的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)。 如需有關驅動程式特定 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。|  
|TYPE_NAME （ODBC 2.0）|7|Varchar not Null|與資料來源相關的資料類型名稱;例如，"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINARY" 或 "CHAR （） FOR BIT DATA"。|  
|COLUMN_SIZE （ODBC 2.0）|8|整數|資料來源上程式資料行的資料行大小。 資料行大小不適用的資料類型會傳回 Null。 如需有效位數的詳細資訊，請參閱附錄 D：資料類型中的資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|BUFFER_LENGTH （ODBC 2.0）|9|整數|指定 SQL_C_DEFAULT 時，在**SQLGetData**或**SQLFetch**作業上傳輸的資料長度（以位元組為單位）。 針對數值資料，此大小可能會與儲存在資料來源上的資料大小不同。 如需詳細資訊，請參閱附錄 D：資料類型中的資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|DECIMAL_DIGITS （ODBC 2.0）|10|Smallint|資料來源上程式資料行的小數位數。 十進位數不適用的資料類型會傳回 Null。 如需有關十進位數的詳細資訊，請參閱附錄 D：資料類型中的資料[行大小、十進位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|NUM_PREC_RADIX （ODBC 2.0）|11|Smallint|若為數值資料類型，則為10或2。<br /><br /> 如果是10，COLUMN_SIZE 和 DECIMAL_DIGITS 中的值會提供資料行允許的十進位數。 例如，十進位（12，5）資料行會傳回10的 NUM_PREC_RADIX、COLUMN_SIZE 12，以及 DECIMAL_DIGITS 為 5;FLOAT 資料行可能會傳回10、COLUMN_SIZE 15 和 Null DECIMAL_DIGITS 的 NUM_PREC_RADIX。<br /><br /> 如果是2，COLUMN_SIZE 和 DECIMAL_DIGITS 中的值會提供資料行中允許的位數。 例如，FLOAT 資料行可能會傳回2的 NUM_PREC_RADIX、53的 COLUMN_SIZE 和 DECIMAL_DIGITS 的 Null。<br /><br /> NUM_PREC_RADIX 不適用的資料類型會傳回 Null。|  
|可為 Null （ODBC 2.0）|12|Smallint 非 NULL|程式資料行是否接受 Null 值：<br /><br /> SQL_NO_NullS：程式資料行不接受 Null 值。<br /><br /> SQL_NullABLE： procedure 資料行接受 Null 值。<br /><br /> SQL_NullABLE_UNKNOWN：如果 [程式] 資料行接受 Null 值，則不知道。|  
|備註（ODBC 2.0）|13|Varchar|程式資料行的描述。|  
|COLUMN_DEF （ODBC 3.0）|14|Varchar|資料行的預設值。<br /><br /> 如果將 Null 指定為預設值，這個資料行就是 Null 文字，不會括在引號中。 如果無法在不截斷的情況下表示預設值，則此資料行會包含截斷的，而且不會有封閉的單引號。 如果未指定預設值，這個資料行就是 Null。<br /><br /> COLUMN_DEF 的值可用來產生新的資料行定義，除非它包含已截斷的值。|  
|SQL_DATA_TYPE （ODBC 3.0）|15|Smallint 非 NULL|SQL 資料類型出現在描述項的 SQL_DESC_TYPE 欄位中的值。 除了 datetime 和 interval 資料類型以外，這個資料行與 DATA_TYPE 資料行相同。<br /><br /> 若為 datetime 和 interval 資料類型，結果集中的 SQL_DATA_TYPE 欄位會傳回 SQL_INTERVAL 或 SQL_DATETIME，而 SQL_DATETIME_SUB 欄位會傳回特定 interval 或 datetime 資料類型的子代碼。 （請參閱[附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)）。|  
|SQL_DATETIME_SUB （ODBC 3.0）|16|Smallint|Datetime 和 interval 資料類型的子類型代碼。 其他資料類型的這個資料行都會傳回 NULL。|  
|CHAR_OCTET_LENGTH （ODBC 3.0）|17|整數|字元或二進位資料類型資料行的最大長度（以位元組為單位）。 所有其他資料類型的這個資料行都會傳回 NULL。|  
|ORDINAL_POSITION （ODBC 3.0）|18|整數不是 NULL|針對輸入和輸出參數，參數在程序定義中的序數位置（以遞增的參數順序，從1開始）。 若為傳回值（如果有的話），則會傳回0。 對於結果集資料行，這是結果集中資料行的序數位置，而結果集中的第一個資料行則是編號1。 如果有多個結果集，則會以驅動程式特定的方式傳回資料行序數位置。|  
|IS_NullABLE （ODBC 3.0）|19|Varchar|如果資料行不包含 Null，則為 "NO"。<br /><br /> 如果資料行可以包含 Null，則為 "YES"。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 遵照 ISO 規則來決定 Null 屬性。 ISO SQL 標準 DBMS 無法傳回空字串。<br /><br /> 這個資料行的傳回值不同於 NULLABLE 資料行的傳回值。 （請參閱可為 Null 的資料行描述）。|  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回資料來源中的程式清單|[SQLProcedures 函數](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
