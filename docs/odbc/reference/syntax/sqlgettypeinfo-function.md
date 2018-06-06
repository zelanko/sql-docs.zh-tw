---
title: SQLGetTypeInfo 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac27290ce265a673e113d0cb59195708a34bebd7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetTypeInfo**傳回資料來源所支援的資料類型的相關資訊。 驅動程式將 SQL 結果集的形式傳回的資訊。 資料型別是用於資料定義語言 (DDL) 陳述式。  
  
> [!IMPORTANT]  
>  應用程式必須使用 TYPE_NAME 資料行中傳回的型別名稱**SQLGetTypeInfo**結果集， **ALTER TABLE**和**CREATE TABLE**陳述式。 **SQLGetTypeInfo** DATA_TYPE 資料行中可能會傳回相同值的多個資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]結果集的陳述式控制代碼。  
  
 *DataType*  
 [輸入]SQL 資料型別。 這必須是其中一個值在[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d： 資料類型或驅動程式專屬 SQL 資料類型的區段。 SQL_ALL_TYPES 指定應傳回的所有資料類型的相關資訊。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetTypeInfo**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*的 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetTypeInfo** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|指定的陳述式屬性不實作工作狀況，造成無效的因此暫時取代相似的值。 (呼叫**SQLGetStmtAttr**判斷暫時替代的值。)取代值無效， *StatementHandle*直到關閉資料指標。 您可以變更陳述式屬性是： SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_KEYSET_SIZE、 SQL_ATTR_MAX_LENGTH、 SQL_ATTR_MAX_ROWS sql_attr_query_timeout 時和 SQL_ATTR_SIMULATE_CURSOR。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在開啟游標的*StatementHandle，*和**SQLFetch**或**SQLFetchScroll**如同呼叫。 傳回這個錯誤是由驅動程式管理員如果**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 結果集是在開啟*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復由於與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法決定交易的狀態。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY004|無效的 SQL 資料類型|指定的引數的值*DataType*是驅動程式支援驅動程式特定資料類型識別項都是有效的 ODBC SQL 資料類型識別碼。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*，然後呼叫函式並，之前已完成執行， **SQLCancel**或**SQLCancelHandle**已在呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫函式和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLGetTypeInfo**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，，並且 SQL_ATTR_CURSOR_TYPE 陳述式屬性設定為 驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 逾時期限透過設定**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 對應的驅動程式*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLGetTypeInfo**做為標準的結果集，DATA_TYPE 由再依資料類型對應的 ODBC SQL 資料類型的對應緊密程度排序傳回的結果。 資料來源所定義的資料類型會優先於使用者自訂資料類型。 因此，在排序次序不一定一致，但可以是 DATA_TYPE 為一般化的第一次，後面接著 TYPE_NAME，這兩個遞增。 比方說，假設資料來源定義的整數和計數器資料類型，其中計數器是自動遞增，而使用者定義資料型別 WHOLENUM 也已定義。 這些將會傳回順序的整數，WHOLENUM，和計數器，因為 WHOLENUM 之間有密切的 ODBC SQL 資料類型 SQL_INTEGER，而自動遞增的資料類型，即使支援的資料來源，不會不緊密地對應至 ODBC SQL 資料類型。 如需這項資訊可能會如何使用資訊，請參閱[DDL 陳述式](../../../odbc/reference/develop-app/ddl-statements.md)。  
  
 如果*DataType*引數指定的資料類型適用於 ODBC 驅動程式，支援的版本，但不是支援驅動程式，則它會傳回空的結果集。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 下列資料行已重新命名，針對 ODBC 3。*x*。 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3。*x*資料行|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 已加入下列資料行所傳回的結果集**SQLGetTypeInfo** ODBC 3。*x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 下表列出結果集內的資料行。 驅動程式，可以定義資料行 19 (INTERVAL_PRECISION) 以外的其他資料行。 應用程式應該要存取驅動程式特有的資料行向下計數從結果集的結尾，而非指定明確的序數位置。 如需詳細資訊，請參閱[目錄函數所傳回資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**可能不會傳回所有資料型別。 例如，驅動程式可能不會傳回使用者定義資料類型。 應用程式可以使用任何有效的資料類型，不論是否由傳回**SQLGetTypeInfo**。 所傳回的資料型別**SQLGetTypeInfo**所支援的資料來源。 它們被供資料定義語言 (DDL) 陳述式中。 驅動程式可以使用資料類型以外的傳回類型的結果集資料傳回**SQLGetTypeInfo**。 在建立時的結果集目錄函數，驅動程式可能使用不支援的資料類型資料來源。  
  
|資料行名稱|資料行<br /><br /> number|資料類型|註解|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|Varchar 不是 NULL|資料來源而定的資料類型名稱。比方說，「 char （)"、"Varchar （)"、"MONEY"、"LONG VARBINARY"或者 「 CHAR （） FOR BIT DATA 中的 」。 應用程式必須使用此名稱在**CREATE TABLE**和**ALTER TABLE**陳述式。|  
|DATA_TYPE (ODBC 2.0)|2|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或驅動程式專屬 SQL 資料類型。 日期時間或間隔資料型別，這個資料行會傳回精確的資料類型 （例如 SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR_TO_MONTH）。 如需有效的 ODBC SQL 資料類型的清單，請參閱[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d： 資料型別中。 如需驅動程式特有的 SQL 資料類型資訊，請參閱驅動程式的文件。|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|伺服器支援此資料類型最大資料行大小。 針對數值資料，這是最大有效位數。 字串資料，這是以字元為單位的長度。 Datetime 資料類型，這是以字元為單位 （假設最大值可以容納分數秒元件的有效位數） 的字串表示的長度。 會傳回 NULL 的資料類型資料行大小不適用。 間隔資料類型，這是字元的常值的時間間隔的表示法中的字元數目 (所定義的間隔開頭有效位數; 請參閱[間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)附錄 d： 資料型別中)。<br /><br /> 如需有關資料行大小的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|使用常值; 前置詞字元例如，單引號 （'） 的字元資料類型或 0x 用於二進位資料類型。會傳回 NULL 的資料類型的常值前置詞不適用。|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|字元或字元用來終止常值。例如，單引號 （'） 的字元資料類型。會傳回 NULL 的資料類型的常值後置詞不適用。|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|關鍵字，並以逗號分隔，對應至應用程式時使用的名稱，傳回 TYPE_NAME 欄位中可能指定括號括住每個參數的清單。 在清單中的關鍵字可以是下列任一項： 長度、 有效位數或小數位數。 這個語法需要其能使用的順序顯示。 比方說，是十進位的 CREATE_PARAMS 「 有效位數、 小數位數;"針對 VARCHAR CREATE_PARAMS 會等於 「 長度 」。 如果資料型別定義; 沒有參數，則傳回 NULL例如，整數。<br /><br /> 驅動程式提供的國家/地區使用該語言的 CREATE_PARAMS 文字。|  
|可為 NULL (ODBC 2.0)|7|Smallint 非 NULL|資料類型是否接受 NULL 值：<br /><br /> SQL_NO_NULLS 如果資料類型不接受 NULL 值。<br /><br /> SQL_NULLABLE 如果資料類型接受 NULL 值。<br /><br /> SQL_NULLABLE_UNKNOWN 如果不知道資料行是否接受 NULL 值。|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint 非 NULL|是否區分大小寫定序和比較字元資料類型：<br /><br /> SQL_TRUE 如果資料類型是字元資料類型且區分大小寫。<br /><br /> 如果資料類型不是字元資料類型，或不區分大小寫，SQL_FALSE。|  
|可搜尋 (ODBC 2.0)|9|Smallint 非 NULL|資料型別用於**其中**子句：<br /><br /> 如果資料行不能在 SQL_PRED_NONE**其中**子句。 （這是 ODBC 2 SQL_UNSEARCHABLE 值相同。*x*。)<br /><br /> 如果資料行可以用於 SQL_PRED_CHAR**其中**子句，但是只能搭配**像**述詞。 （這是 ODBC 2 SQL_LIKE_ONLY 值相同。*x*。)<br /><br /> SQL_PRED_BASIC 如果資料行可以用於**其中**子句以外的所有比較運算子搭配**像**(比較、 定量的比較， **BETWEEN**， **相異**， **IN**，**相符**，和**UNIQUE**)。 （這是 ODBC 2 SQL_ALL_EXCEPT_LIKE 值相同。*x*。)<br /><br /> 如果資料行可以用於 SQL_SEARCHABLE**其中**子句搭配任何比較運算子。|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|資料類型是否不帶正負號：<br /><br /> 如果資料類型是不帶正負號，SQL_TRUE。<br /><br /> 如果資料型別為 signed，SQL_FALSE。<br /><br /> 如果屬性不是適用於資料類型或資料類型不是數值，則傳回 NULL。|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint 非 NULL|資料類型是否有預先定義固定有效位數和小數位數 （也就是資料來源專用），例如 money 資料類型：<br /><br /> SQL_TRUE 如果它具有預先定義的固定有效位數和小數位數。<br /><br /> 如果沒有預先定義的固定有效位數和小數位數，SQL_FALSE。|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|資料型別是否自動遞增：<br /><br /> 如果資料類型為自動遞增，SQL_TRUE。<br /><br /> 如果資料類型不會自動遞增，SQL_FALSE。<br /><br /> 如果屬性不是適用於資料類型或資料類型不是數值，則傳回 NULL。<br /><br /> 應用程式可以將值插入資料行具有此屬性，但通常無法更新資料行中的值。<br /><br /> 進行插入時自動遞增資料行，唯一的值被插入資料行在插入時。 未定義時，遞增，但資料來源專用。 應用程式不應該假設任何特定值的自動遞增資料行開始在任何特定點或增量。|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|資料來源相依名稱的資料類型的當地語系化的版本。 如果資料來源不支援當地語系化名稱，便傳回 NULL。 此名稱僅供，例如在對話方塊中顯示。|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|資料來源的資料類型的最小小數位數。 如果資料類型有固定的小數位數，MINIMUM_SCALE 和 MAXIMUM_SCALE 資料行都包含這個值。 例如，SQL_TYPE_TIMESTAMP 資料行可能會有固定的小數位數的小數秒數。 當小數位數不適用時，會傳回 NULL。 如需詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|資料來源的資料類型最大刻度。 當小數位數不適用時，會傳回 NULL。 如果未在資料來源上個別定義最大小數位數，但定義成與最大有效位數相同，這個資料行包含 COLUMN_SIZE 資料行相同的值。 如需詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。|  
|SQL_DATA_TYPE (ODBC 3.0)|16|Smallint 非 NULL|SQL 資料類型，因為它的值會出現在描述元的 SQL_DESC_TYPE 欄位。 此資料行是與 DATA_TYPE 資料行，除了間隔和 datetime 資料類型相同。<br /><br /> 間隔和日期時間資料類型，結果集中的 SQL_DATA_TYPE 欄位將會傳回 SQL_INTERVAL 或 SQL_DATETIME，而且 SQL_DATETIME_SUB 欄位將會傳回特定的間隔或 datetime 資料類型的子代碼。 (請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|當 SQL_DATA_TYPE 的值是 SQL_DATETIME 或 SQL_INTERVAL 時，此資料行包含 datetime/間隔子代碼。 日期時間和間隔以外的資料類型，此欄位為 NULL。<br /><br /> 間隔或 datetime 資料類型，結果集中的 SQL_DATA_TYPE 欄位將會傳回 SQL_INTERVAL 或 SQL_DATETIME，而且 SQL_DATETIME_SUB 欄位將會傳回特定的間隔或 datetime 資料類型的子代碼。 (請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|如果資料類型是近似數值類型，此資料行包含值 2 表示 COLUMN_SIZE 指定的位元數。 精確數值類型，此資料行包含 10 這個值來表示 COLUMN_SIZE 指定的小數位數。 否則，這個資料行就是 NULL。|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|如果間隔資料類型的資料類型，此資料行包含間隔開頭有效位數的值。 (請參閱[間隔資料類型有效位數](../../../odbc/reference/appendixes/interval-data-type-precision.md)附錄 d： 資料型別中。)否則，這個資料行就是 NULL。|  
  
 屬性的資訊可套用至資料類型或結果集內的特定資料行。 **SQLGetTypeInfo**傳回資料類型，與相關聯屬性的相關資訊**SQLColAttribute**傳回結果集中的資料行相關聯屬性的相關資訊。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集內的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集內的資料行的相關資訊|[SQLColAttribute 函式](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|提取資料的區塊或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|擷取單一資料列或資料區塊的順向的方向|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回的驅動程式或資料來源的相關資訊|[SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
