---
title: SQLColumns 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94afb817462022ff21c312291b31c738be15c72f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537689"
---
# <a name="sqlcolumns-function"></a>SQLColumns 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：開啟群組  
  
 **摘要**  
 **SQLColumns**傳回指定之資料表中資料行名稱的清單。 驅動程式會傳回這項資訊當作結果集上指定*StatementHandle*。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *CatalogName*  
 [輸入]目錄名稱。 如果驅動程式支援的目錄，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有目錄的資料表。 *CatalogName*不能包含字串的搜尋模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*CatalogName*是一般的引數; 也就是，則會視為和其案例很重要。 如需詳細資訊，請參閱 <<c0> [ 目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]中的字元長度 **CatalogName*。  
  
 *SchemaName*  
 [輸入]結構描述名稱的字串搜尋模式。 如果驅動程式支援的結構描述，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有結構描述的資料表。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *SchemaName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*SchemaName*模式值引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength2*  
 [輸入]中的字元長度 **SchemaName*。  
  
 *TableName*  
 [輸入]資料表名稱的字串搜尋模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *TableName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*TableName*模式值引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength3*  
 [輸入]中的字元長度 **TableName*。  
  
 *ColumnName*  
 [輸入]資料行名稱的字串搜尋模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *ColumnName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*ColumnName*模式值引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength4*  
 [輸入]中的字元長度 **ColumnName*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLColumns**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLColumns** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|資料指標是開啟*StatementHandle*，並**SQLFetch**或是**SQLFetchScroll**呼叫。 如果此錯誤會傳回由驅動程式管理員**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 資料指標是開啟*StatementHandle*但**SQLFetch**或是**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復，因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|使用無效的 null 指標|SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*引數為 null 指標，以及 SQL_CATALOG_NAME*資訊類型*支援的目錄名稱，傳回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，而*SchemaName*， *TableName*，或*ColumnName*引數是 null 指標。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLColumns**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 其中一個名稱的長度引數的值小於 0，但不是等於 SQL_NTS。|  
|||其中一個名稱的長度引數的值超過最大長度值，對應的目錄或名稱。 每個類別目錄或名稱的最大長度，可由呼叫**SQLGetInfo**具有*資訊類型*值。 （請參閱 「 註解。"）|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的目錄名稱，並在驅動程式或資料來源不支援目錄。<br /><br /> 指定的結構描述名稱，且驅動程式或資料來源不支援結構描述。<br /><br /> 結構描述名稱、 資料表名稱或資料行名稱，為指定的字串搜尋模式和資料來源不支援搜尋模式的一個或多個這些引數。<br /><br /> 驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 陳述式屬性已設定為驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 此函式通常用於陳述式執行之前從資料來源的目錄中擷取的資料表或資料表的資料行的相關資訊。 **SQLColumns**可以用來擷取所有類型的項目所傳回的資料**SQLTables**。 除了基底資料表，這可能包括 （但不限於） 檢視、 同義字、 系統資料表等等。 相較之下，函式**SQLColAttribute**並**SQLDescribeCol**描述結果集和函式的資料行**SQLNumResultCols**傳回的數目在結果集中的資料行。 如需詳細資訊，請參閱 <<c0> [ 使用的目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLColumns**標準的結果集，依 TABLE_CAT、 再依據 table_schem 排列、 TABLE_NAME 和 ORDINAL_POSITION 排序的方式傳回結果。  
  
> [!NOTE]  
>  當應用程式適用於 ODBC 2。*x*驅動程式，任何的 ORDINAL_POSITION 資料行傳回結果集內。 如此一來，當使用 ODBC 2。*x*驅動程式和所傳回的資料行清單中的資料行的順序**SQLColumns**一定的資料行順序相同時不會傳回所有應用程式會執行的 SELECT 陳述式該資料表中的資料行。  
  
> [!NOTE]  
>  **SQLColumns**可能不會傳回所有資料行。 例如，驅動程式可能不會傳回虛擬資料行，例如 Oracle ROWID 的相關資訊。 應用程式可以使用任何有效的資料行，它會傳回**SQLColumns**。  
>   
>  可傳回的某些資料行**SQLStatistics**不會傳回**SQLColumns**。 例如， **SQLColumns**不會傳回資料行在索引建立運算式或篩選，例如薪資 + 權益或 DEPT = 0012。  
  
 VARCHAR 資料行的長度不會顯示在表格中，實際長度取決於資料來源。 若要判斷 TABLE_CAT，再依據 table_schem 排列、 TABLE_NAME、 COLUMN_NAME 資料行的實際長度，應用程式可以呼叫**SQLGetInfo**搭配 SQL_MAX_CATALOG_NAME_LEN SQL_MAX_SCHEMA_NAME_LEN、 SQL_MAX_TABLE_NAME_LEN，和 SQL_MAX_COLUMN_NAME_LEN 選項。  
  
 下列資料行已重新命名，針對 ODBC 3。*x*。 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3。*x*資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 已新增下列資料行所傳回的結果集**SQLColumns** ODBC 3。*x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 下表列出結果集內的資料行。 驅動程式，可以定義資料行 18 (IS_NULLABLE) 以外的其他資料行。 應用程式應該透過從結果集而不是指定明確的序數位置的結尾算起往下取得驅動程式特有的資料行權限。 如需詳細資訊，請參閱 <<c0> [ 目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|「資料行」<br /><br /> number|資料類型|註解|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|目錄名稱;如果不適用於資料來源，則為 NULL。 如果驅動程式支援目錄對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 沒有目錄這些資料表。|  
|再依據 TABLE_SCHEM 排列 (ODBC 1.0)|2|Varchar|結構描述名稱;如果不適用於資料來源，則為 NULL。 如果驅動程式支援結構描述對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 並沒有結構描述這些資料表。|  
|TABLE_NAME (ODBC 1.0)|3|非 NULL Varchar|資料表名稱。|  
|COLUMN_NAME (ODBC 1.0)|4|非 NULL Varchar|資料行名稱。 驅動程式會傳回沒有名稱的資料行的空字串。|  
|DATA_TYPE (ODBC 1.0)|5|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或驅動程式專屬的 SQL 資料型別。 日期時間和間隔資料類型，此資料行都會傳回精確的資料類型 （例如 SQL_TYPE_DATE 或 SQL_INTERVAL_YEAR_TO_MONTH，而不是 nonconcise 資料類型，例如，如果是 SQL_DATETIME 或 SQL_INTERVAL）。 如需有效的 ODBC SQL 資料類型的清單，請參閱 < [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d:資料類型。 如需驅動程式專用的 SQL 資料類型資訊，請參閱驅動程式的文件。<br /><br /> 適用於 ODBC 3 傳回的資料型別。*x*和 ODBC 2。*x*應用程式可能會不同。 如需詳細資訊，請參閱 <<c0> [ 回溯相容性與標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|TYPE_NAME (ODBC 1.0)|6|非 NULL Varchar|資料來源相關的資料型別名稱;比方說，"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINAR"或者"CHAR （） FOR BIT DATA 中的 」。|  
|COLUMN_SIZE (ODBC 1.0)|7|Integer|如果 DATA_TYPE 是 SQL_CHAR 或 SQL_VARCHAR，此資料行包含以字元為單位的資料行的最大長度。 對於 datetime 資料類型，這是要顯示的值，則會轉換成字元時所需的字元總數。 對於數值資料類型，這是的位數總數，或是資料行，允許的位元的總數根據 NUM_PREC_RADIX 資料行。 間隔資料類型，這是常值的時間間隔之字元表示法中的字元數 (如間隔開頭有效位數所定義，請參閱[間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)附錄 d:資料型別）。 如需詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。|  
|BUFFER_LENGTH (ODBC 1.0)|8|Integer|在 SQLGetData、 SQLFetch 或 SQLFetchScroll 作業上的事件，是如果指定 SQL_C_DEFAULT，則傳輸的位元組長度的資料。 針對數值資料，這個大小可能與不同的資料來源上儲存的資料大小。 這個值是以字元資料的 COLUMN_SIZE 資料行可能會有所不同。 如需長度的詳細資訊，請參閱[資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|要在小數點右邊的位數總數。 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP 時，此資料行包含的小數秒數元件中的位數。 針對其他資料類型，這是資料來源上的資料行的小數位數。 包含時間元件的 interval 資料類型，此資料行包含的位數 （小數秒數） 之小數點右邊。 此資料行不包含時間元件的 interval 資料類型，為 0。 多個十進位數字的詳細資訊，請參閱[資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。 會傳回 NULL 的資料型別 DECIMAL_DIGITS 不適用。|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|針對數值資料類型，10 或 2。 如果是 10，COLUMN_SIZE 與 DECIMAL_DIGITS 中的值會提供允許的資料行的小數位數。 比方說，DECIMAL(12,5) 資料行就會傳回為 10，COLUMN_SIZE 為 12，並為 5; DECIMAL_DIGITS NUM_PREC_RADIX浮點數資料行可能會傳回 NUM_PREC_RADIX 是 10，15，個 COLUMN_SIZE DECIMAL_DIGITS 的 null 值。<br /><br /> 如果是 2，COLUMN_SIZE 與 DECIMAL_DIGITS 中的值會提供資料行中允許的位元數。 比方說，浮點數資料行可能會傳回 2 的 53，COLUMN_SIZE 和 DECIMAL_DIGITS 的 null 值的基數。<br /><br /> 會傳回 NULL 的資料型別 NUM_PREC_RADIX 不適用。|  
|可為 NULL (ODBC 1.0)|11|Smallint 非 NULL|SQL_NO_NULLS 如果資料行不能包含 NULL 值。<br /><br /> 如果資料行接受 NULL 值的 SQL_NULLABLE。<br /><br /> SQL_NULLABLE_UNKNOWN 如果不知道資料行是否接受 NULL 值。<br /><br /> 傳回這個資料行的值不同於針對 IS_NULLABLE 資料行傳回的值。 確實可以接受 Null 資料行，但無法指出確實的資料行不接受 null 值，表示可為 NULL 的資料行。 IS_NULLABLE 資料行指出資料行無法接受 null 值，但無法表示資料行接受 null 值的確實的確定性。|  
|註解 (ODBC 1.0)|12|Varchar|資料行的描述。|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|資料行的預設值。 此資料行中的值應解譯為字串，如果它以引號括住。<br /><br /> NULL 指定為預設值，這個資料行為 NULL 一字，不包含在引號中。 無法表示的預設值，而不會截斷，則此資料行就會包含已截斷，未納入單一引號。 如果已指定沒有預設值，這個資料行就會是 NULL。<br /><br /> 包含已截斷的值時，產生新的資料行定義中，除了可用 COLUMN_DEF 的值。|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint 非 NULL|SQL 資料類型，因為它會出現在 IRD 中的 SQL_DESC_TYPE 記錄欄位。 這可以是 ODBC SQL 資料類型或驅動程式專屬的 SQL 資料型別。 這個資料行是與 DATA_TYPE 資料行，除了 datetime 和間隔資料類型相同。 此資料行傳回 nonconcise 資料類型 （例如，如果是 SQL_DATETIME 或 SQL_INTERVAL），而不是精確的資料類型 （例如 SQL_TYPE_DATE 或 SQL_INTERVAL_YEAR_TO_MONTH） 的日期時間和間隔資料類型。 如果這個資料行會傳回，如果是 SQL_DATETIME 或 SQL_INTERVAL，就可以判斷特定資料類型從 SQL_DATETIME_SUB 資料行。 如需有效的 ODBC SQL 資料類型的清單，請參閱 < [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d:資料類型。 如需驅動程式專用的 SQL 資料類型資訊，請參閱驅動程式的文件。<br /><br /> 適用於 ODBC 3 傳回的資料型別。*x*和 ODBC 2。*x*應用程式可能會不同。 如需詳細資訊，請參閱 <<c0> [ 回溯相容性與標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|日期時間和間隔資料類型的子型別程式碼。 其他資料類型的這個資料行都會傳回 NULL。 多個日期時間和間隔子代碼的詳細資訊，請參閱 「 SQL_DESC_DATETIME_INTERVAL_CODE 」，在[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|Integer|以位元組為單位的最大長度的字元或二進位資料類型資料行。 所有其他資料類型的這個資料行都會傳回 NULL。|  
|ORDINAL_POSITION (ODBC 3.0)|17|整數不是 NULL|資料行在資料表中的序數位置。 在資料表中的第一個資料行是一個數字 1。|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|[否] 如果資料行不包含 Null。<br /><br /> 「 是 」 如果資料行可以包括 NULLs。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 遵照 ISO 規則來決定 Null 屬性。 ISO SQL 標準 DBMS 無法傳回空字串。<br /><br /> 傳回這個資料行的值不同於可為 NULL 的資料行所傳回的值。 （請參閱可為 NULL 的資料行的描述。）|  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會宣告所傳回的結果集的緩衝區**SQLColumns**。 它會呼叫**SQLColumns**傳回描述 EMPLOYEE 資料表中的每個資料行的結果集。 然後它會呼叫**SQLBindCol**繫結結果集之緩衝區中的資料行。 最後，應用程式會擷取資料的每個資料列**SQLFetch**並予以處理。  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回的資料行或資料行的權限|[SQLColumnPrivileges 函式](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|正在擷取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回唯一識別資料列的資料行或資料行自動更新的交易|[SQLSpecialColumns 函式](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|傳回資料表的統計資料和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|傳回一份資料表中的資料來源|[SQLTables 函式](../../../odbc/reference/syntax/sqltables-function.md)|  
|傳回針對資料表或資料表的權限|[SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
