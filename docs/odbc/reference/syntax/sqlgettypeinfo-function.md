---
title: SQLGetTypeInfo 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f83b8ce83c1433ce7e20f00580100b65be84961
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209247"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLGetTypeInfo**傳回資料來源所支援的資料類型的相關資訊。 驅動程式的 SQL 結果集形式傳回的資訊。 資料類型僅供資料定義語言 (DDL) 陳述式中的使用。  
  
> [!IMPORTANT]  
>  應用程式必須使用 TYPE_NAME 資料行中傳回的類型名稱**SQLGetTypeInfo**結果集中**ALTER TABLE**並**CREATE TABLE**陳述式。 **SQLGetTypeInfo**可能會傳回在 DATA_TYPE 資料行中具有相同值的多個資料列。  
  
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
 [輸入]SQL 資料型別。 這必須是在值的其中一個[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)一節的附錄 d:資料類型或驅動程式專屬的 SQL 資料型別。 SQL_ALL_TYPES 指定應傳回的所有資料類型的相關資訊。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetTypeInfo**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetTypeInfo** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|指定的陳述式屬性是實作運作的情況，因為不正確的因此已暫時替代成類似的值。 (呼叫**SQLGetStmtAttr**判斷暫時替代的值。)取代值是適用於*StatementHandle*直到關閉資料指標。 您可以變更的陳述式屬性是：SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_KEYSET_SIZE、 SQL_ATTR_MAX_LENGTH、 SQL_ATTR_MAX_ROWS、 sql_attr_query_timeout 時和 SQL_ATTR_SIMULATE_CURSOR。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|資料指標是開啟*StatementHandle，* 並**SQLFetch**或**SQLFetchScroll**呼叫。 如果此錯誤會傳回由驅動程式管理員**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 結果集是在上開啟*StatementHandle*，但**SQLFetch**或是**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY004|無效的 SQL 資料類型|指定的引數的值*DataType*不是有效的 ODBC SQL 資料類型識別項或驅動程式支援的驅動程式專屬資料型別識別項。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*，然後呼叫函式並，之前執行，完成**SQLCancel**或是**SQLCancelHandle**已在上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLGetTypeInfo**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 陳述式屬性已設定為驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 對應的驅動程式*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLGetTypeInfo**標準的結果集，DATA_TYPE 由再依資料類型對應的 ODBC SQL 資料類型的程度排序的方式傳回結果。 資料來源所定義的資料類型的優先順序高於使用者定義資料類型。 因此，排序順序不一定一致，但可以是第一次歸類為 DATA_TYPE，後面 TYPE_NAME，這兩個遞增。 例如，假設資料來源定義的整數和計數器資料類型，其中計數器是自動遞增，和使用者定義資料型別 WHOLENUM 也已定義。 這些會傳回整數，WHOLENUM、 順序和計數器，因為 WHOLENUM 對應密切至 ODBC SQL 資料型別 SQL_INTEGER，而自動遞增的資料類型，即使支援的資料來源，不會不緊密地對應至 ODBC SQL 資料類型。 如需如何使用這項資訊，請參閱[DDL 陳述式](../../../odbc/reference/develop-app/ddl-statements.md)。  
  
 如果*DataType*引數指定的資料類型，也就是適用於 ODBC 驅動程式，支援的版本，但不是支援的驅動程式，則它會傳回空的結果集。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 下列資料行已重新命名，針對 ODBC 3。*x*。 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3。*x*資料行|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 已新增下列資料行所傳回的結果集**SQLGetTypeInfo** ODBC 3。*x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 下表列出結果集內的資料行。 驅動程式，可以定義資料行 19 (INTERVAL_PRECISION) 以外的其他資料行。 應用程式應該取得存取權的驅動程式特有的資料行，倒數，從結果集的結尾，而不是指定明確的序數位置。 如需詳細資訊，請參閱 <<c0> [ 目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**可能不會傳回所有資料類型。 例如，驅動程式可能不會傳回使用者定義資料類型。 應用程式可以使用任何有效的資料型別，不論它會傳回所**SQLGetTypeInfo**。 所傳回的資料型別**SQLGetTypeInfo**所支援的資料來源。 它們僅供資料定義語言 (DDL) 陳述式中的使用。 驅動程式可傳回結果集資料使用的資料類型所傳回的型別以外**SQLGetTypeInfo**。 在建立時的結果集的目錄函式，驅動程式可能會使用資料來源不支援的資料類型。  
  
|資料行名稱|「資料行」<br /><br /> number|資料類型|註解|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|非 NULL Varchar|資料來源相關的資料類型名稱;比方說，「 char （）"、"Varchar （）"、"MONEY"、"長 VARBINARY"或者"CHAR （） FOR BIT DATA 中的"。 應用程式必須使用此名稱在**CREATE TABLE**並**ALTER TABLE**陳述式。|  
|DATA_TYPE (ODBC 2.0)|2|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或驅動程式專屬的 SQL 資料型別。 日期時間或間隔資料類型，這個資料行會傳回精確的資料類型 （例如 SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR_TO_MONTH）。 如需有效的 ODBC SQL 資料類型的清單，請參閱 < [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d:資料類型。 如需驅動程式專用的 SQL 資料類型資訊，請參閱驅動程式的文件。|  
|COLUMN_SIZE (ODBC 2.0)|3|Integer|伺服器支援此資料類型的最大資料行大小。 針對數值資料，這是最大有效位數。 針對字串資料，這是以字元為單位的長度。 對於 datetime 資料類型，這會是 （假設最大值可以容納分數秒元件的有效位數） 的字串表示法的字元長度。 會傳回 NULL 的資料類型資料行大小不適用。 間隔資料類型，這是常值的時間間隔之字元表示法中的字元數 (所定義的間隔開頭有效位數; 請參閱[間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)附錄 d:資料型別）。<br /><br /> 如需有關資料行大小的詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|用來做為常值; 前置詞的字元例如，單引號 （'） 的字元資料類型或 0x 用於二進位資料類型;會傳回 NULL 的資料類型的常值的前置詞不適用。|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|字元或字元用來終止常值;例如，單引號 （'） 字元資料類型;會傳回 NULL 的資料類型的常值後置詞不適用。|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|關鍵字，以對應至應用程式時使用的名稱，傳回 TYPE_NAME 欄位中可能指定括號括住每個參數的逗號分隔清單。 在清單中的關鍵字可以是下列任一項： 長度、 有效位數或小數位數。 它們會出現在這個語法需要使用的順序。 比方說，是代表小數點的 CREATE_PARAMS 「 有效位數、 小數位數 」;Varchar CREATE_PARAMS 就會等於 「 長度 」。 如果資料型別定義; 沒有參數，則傳回 NULL例如，整數。<br /><br /> 驅動程式提供 CREATE_PARAMS 文字語言的國家/地區使用的位置。|  
|可為 NULL (ODBC 2.0)|7|Smallint 非 NULL|資料類型是否接受 NULL 值：<br /><br /> SQL_NO_NULLS 如果資料類型不接受 NULL 值。<br /><br /> 如果資料類型接受 NULL 值的 SQL_NULLABLE。<br /><br /> SQL_NULLABLE_UNKNOWN 如果不知道資料行是否接受 NULL 值。|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint 非 NULL|是否區分大小寫定序和比較字元資料類型：<br /><br /> SQL_TRUE 當資料類型是字元資料類型，而且會區分大小寫。<br /><br /> 如果資料類型不是字元資料類型，或不區分大小寫，SQL_FALSE。|  
|可搜尋 (ODBC 2.0)|9|Smallint 非 NULL|如何在中，使用的資料型別**其中**子句：<br /><br /> 如果資料行不能在 SQL_PRED_NONE**其中**子句。 （這是 ODBC 2 SQL_UNSEARCHABLE 值相同。*x*。)<br /><br /> SQL_PRED_CHAR 如果資料行可以用於**何處**子句，但僅限**像**述詞。 （這是 ODBC 2 SQL_LIKE_ONLY 值相同。*x*。)<br /><br /> SQL_PRED_BASIC 如果資料行可以用於**何處**子句以外的所有比較運算子搭配**像**(比較、 定量相較之下， **BETWEEN**， **相異**， **IN**，**相符項目**，和**UNIQUE**)。 （這是 ODBC 2 SQL_ALL_EXCEPT_LIKE 值相同。*x*。)<br /><br /> 如果資料行可以用於 SQL_SEARCHABLE**其中**搭配任何比較運算子的子句。|  
|UNSIGNED_ATTRIBUTE 設 (ODBC 2.0)|10|Smallint|資料類型是否使用不帶正負號：<br /><br /> 如果資料類型是不帶正負號的 SQL_TRUE。<br /><br /> 如果資料型別為 signed，SQL_FALSE。<br /><br /> 如果屬性不是適用於資料類型或資料類型不是數字，則傳回 NULL。|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint 非 NULL|是否有預先定義的資料型別固定有效位數和小數位數 （也就是資料來源特有），例如 money 資料類型：<br /><br /> SQL_TRUE 如果它具有預先定義的固定有效位數和小數位數。<br /><br /> 如果沒有預先定義的固定有效位數和小數位數，SQL_FALSE。|  
|AUTO_UNIQUE_VALUE 會 (ODBC 2.0)|12|Smallint|資料型別是否自動遞增：<br /><br /> SQL_TRUE 的資料型別是否自動遞增。<br /><br /> 如果資料類型不會自動遞增，SQL_FALSE。<br /><br /> 如果屬性不是適用於資料類型或資料類型不是數字，則傳回 NULL。<br /><br /> 應用程式可以將值插入資料行需要此屬性，但通常無法更新資料行的值。<br /><br /> 自動遞增資料行進行插入時，唯一的值會插入資料行在插入時。 增量未定義，但資料來源特有。 應用程式不應該假設任何特定值的自動遞增資料行開始在任何特定點或遞增。|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|資料類型之資料來源相依名稱的當地語系化版本。 如果資料來源不支援當地語系化名稱，便傳回 NULL。 這個名稱被供顯示，例如對話方塊。|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|小數位數的資料來源的資料類型。 如果資料類型有固定的小數位數，MINIMUM_SCALE 和 MAXIMUM_SCALE 資料行都包含這個值。 比方說，SQL_TYPE_TIMESTAMP 資料行可能有固定的小數位數的小數秒數。 當小數位數不適用時，會傳回 NULL。 如需詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|資料來源上的資料類型最大小數位數。 當小數位數不適用時，會傳回 NULL。 如果未在資料來源上個別定義最大小數位數，但定義成與最大有效位數相同，這個資料行包含 COLUMN_SIZE 資料行相同的值。 如需詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。|  
|SQL_DATA_TYPE (ODBC 3.0)|16|smallint 非 NULL|SQL 資料類型，因為它的值會出現在描述子 SQL_DESC_TYPE 欄位。 這個資料行是與 DATA_TYPE 資料行，除了間隔和 datetime 資料類型相同。<br /><br /> 間隔和 datetime 資料類型，結果集中的 SQL_DATA_TYPE 欄位會傳回 SQL_INTERVAL 或如果是 SQL_DATETIME，而且 SQL_DATETIME_SUB 欄位將會傳回特定的間隔或 datetime 資料類型的子代碼。 (請參閱[附錄 d:資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|當 SQL_DATA_TYPE 的值是 SQL_DATETIME 或 SQL_INTERVAL 時，此資料行包含日期時間/間隔子代碼。 日期時間和間隔以外的資料類型，此欄位會是 NULL。<br /><br /> 間隔或 datetime 資料類型，結果集中的 SQL_DATA_TYPE 欄位會傳回 SQL_INTERVAL 或如果是 SQL_DATETIME，而且 SQL_DATETIME_SUB 欄位將會傳回特定的間隔或 datetime 資料類型的子代碼。 (請參閱[附錄 d:資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)|  
|NUM_PREC_RADIX (ODBC 3.0)|18|Integer|如果資料類型是近似的數值類型，此資料行包含值 2 表示 COLUMN_SIZE 指定的位元數。 精確數值類型，此資料行包含 10 這個值來表示 COLUMN_SIZE 指定的小數位數。 否則，這個資料行就是 NULL。|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|如果間隔資料類型的資料型別，這個資料行就會包含間隔開頭有效位數的值。 (請參閱[間隔資料類型有效位數](../../../odbc/reference/appendixes/interval-data-type-precision.md)附錄 d:資料型別。）否則，這個資料行就是 NULL。|  
  
 屬性資訊可以套用至資料型別或結果集內的特定資料行。 **SQLGetTypeInfo**傳回資料類型，與相關聯屬性的相關資訊**SQLColAttribute**傳回結果集中的資料行相關聯的屬性的相關資訊。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在結果集中傳回資料行的相關資訊|[SQLColAttribute 函式](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|擷取單一資料列或順向方向中的資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回的驅動程式或資料來源的相關資訊|[SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
