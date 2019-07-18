---
title: SQLExecute 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecute
helpviewer_keywords:
- SQLExecute function [ODBC]
ms.assetid: 9286a01d-cde2-4b90-af94-9fd7f8da48bf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12dffe315485aadc839654996f6af3a561161246
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003132"
---
# <a name="sqlexecute-function"></a>SQLExecute 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLExecute**執行備妥的陳述式，使用參數標記變數的目前值，如果陳述式中存在的任何參數標記。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLExecute(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR、 SQL_NO_DATA、 SQL_INVALID_HANDLE，還是 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLExecute**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLExecute** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01001|資料指標作業衝突|備妥的陳述式相關聯*StatementHandle*自主定位的 update 或 delete 陳述式，並沒有任何資料列或多個資料列已更新或刪除。 (如需有關更新多個資料列的詳細資訊，請參閱 SQL_ATTR_SIMULATE_CURSOR 描述*屬性*中**SQLSetStmtAttr**。)<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01003|Set 函式刪除了 NULL 值|備妥的陳述式相關聯*StatementHandle*包含 set 函式 (例如**AVG**，**最大**， **MIN**等等)，但不是**計數**設定函式，並且在套用函數之前，也消除了值的 NULL 引數。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|字串或二進位資料傳回輸出參數會導致非空白的字元或二進位資料的非 NULL 的截斷。 如果是字串值，則向右截斷。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01006|未撤銷權限|備妥的陳述式相關聯*StatementHandle*已**撤銷**陳述式，而且使用者沒有指定的權限。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01007|未授與的權限|備妥的陳述式相關聯*StatementHandle*已**授與**陳述式，而且使用者無法獲得指定權限。|  
|01S02|選項值已變更|指定的陳述式屬性是實作運作的情況，因為不正確的因此已暫時替代成類似的值。 (**SQLGetStmtAttr**可以呼叫以判斷其暫時已取代的值為何。)取代值是適用於*StatementHandle*直到資料指標已關閉，此時陳述式屬性會還原為先前的值。 您可以變更的陳述式屬性是：SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_KEYSET_SIZE、 SQL_ATTR_MAX_LENGTH、 SQL_ATTR_MAX_ROWS、 sql_attr_query_timeout 時和 SQL_ATTR_SIMULATE_CURSOR。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S07|小數位數截斷|傳回輸入/輸出的資料，或輸出參數已被截斷，使得已截斷數值資料類型的小數部分，或已遭截斷的小數部分的時間、 時間戳記或時間間隔的資料型別之時間元件。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07002|COUNT 欄位不正確|參數中指定的數目**SQLBindParameter**中所包含的 SQL 陳述式中的參數數目低於\* *StatementText*。<br /><br /> **SQLBindParameter**以叫用*ParameterValuePtr*設定為 null 指標， *StrLen_or_IndPtr*未設定為 SQL_NULL_DATA 或 SQL_DATA_AT_EXEC，和*了*未設定為 SQL_PARAM_OUTPUT，以便在指定的參數數目**SQLBindParameter**大於包含在 SQL 陳述式中的參數數目 **StatementText*.|  
|07006|受限制的資料類型屬性違規|所識別的資料值*ValueType*中的引數**SQLBindParameter**繫結的參數無法轉換成資料類型所識別的*ParameterType*中的引數**SQLBindParameter**。<br /><br /> 資料傳回的值繫結為 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 無法轉換成所識別的資料型別參數*ValueType*中的引數**SQLBindParameter**。<br /><br /> （如果無法轉換一或多個資料列的資料值，但一或多個資料列成功地傳回，此函式會傳回 SQL_SUCCESS_WITH_INFO。）|  
|07007|違反限制的參數值|參數型別 SQL_PARAM_INPUT_OUTPUT_STREAM 只用於傳送和接收資料組件中的參數。 此參數類型不允許的輸入繫結的緩衝區。<br /><br /> 當參數類型 SQL_PARAM_INPUT_OUTPUT，而且會發生此錯誤\* *StrLen_or_IndPtr*中指定**SQLBindParameter**不等於 SQL_NULL_DATA，SQL_DEFAULT_PARAM、 SQL_LEN_DATA_AT_EXEC(len) 或 SQL_DATA_AT_EXEC。|  
|07S01|預設參數用法無效|參數值時，設定**SQLBindParameter**、 已 SQL_DEFAULT_PARAM，和對應的參數不是 ODBC 標準程序引動過程的參數。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|21S02|衍生資料表的程度與資料行清單不符|備妥的陳述式相關聯*StatementHandle*包含**CREATE VIEW**陳述式與不合格的資料行清單 (指定的檢視中的資料行數目*資料行識別碼*SQL 陳述式的引數) 包含更多的名稱中所定義的衍生資料表的資料行數目比*查詢規格*的 SQL 陳述式的引數。|  
|22001|字串資料，右側截斷|字元或二進位值的資料行指派導致截斷的非空白 （字元） 或非 null （二進位） 字元或位元組。|  
|22002|指標變數但未提供|NULL 資料繫結至輸出參數的*StrLen_or_IndPtr*情況下設**SQLBindParameter**是 null 指標。|  
|22003|數值超出範圍|備妥的陳述式相關聯*StatementHandle*包含繫結的數字參數，且參數值會導致要指派至相關聯時，會被截斷的數字 （相對於小數） 的整數部分資料表資料行。<br /><br /> 傳回一或多個輸入/輸出或輸出參數的數值 （以數字或字串） 會造成要截斷的數字 （相對於小數） 的整數部分。|  
|22007|無效的日期時間格式|備妥的陳述式相關聯*StatementHandle*包含 SQL 陳述式包含日期、 時間戳記結構做為繫結的參數和參數，則為，分別、 無效的日期、 時間或時間戳記。<br /><br /> 輸入/輸出或輸出參數繫結至日期、 時間或時間戳記 C 結構，但傳回的參數中的值，分別無效的日期、 時間戳記。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22008|日期時間欄位溢位|備妥的陳述式相關聯*StatementHandle*包含 SQL 陳述式，根據包含日期時間運算式，當計算，導致日期時間戳記結構無效。<br /><br /> 日期時間運算式計算的輸入/輸出或輸出參數會導致日期、 時間或無效的時間戳記 C 結構。|  
|22012|除數為零|備妥的陳述式相關聯*StatementHandle*包含造成除數為零的算術運算式。<br /><br /> 算術運算式計算的輸入/輸出或輸出參數為零會導致除數。|  
|22015|間隔欄位溢位|*\*StatementText*包含確切的數值或時間間隔參數，轉換成 SQL 資料類型的間隔時，造成有效位數遺失。<br /><br /> *\*StatementText*包含多個欄位間隔參數，轉換成資料行中數值資料類型時，有沒有表示法中的數值資料類型。<br /><br /> *\*StatementText*包含已指派給間隔 SQL 類型的參數資料，而且沒有間隔 SQL 型別中的 C 類型的值不表示法。<br /><br /> 指派為精確數值或間隔造成有效位數遺失 C 間隔類型的 SQL 類型的輸入/輸出或輸出參數。<br /><br /> 當輸入/輸出或輸出參數已指派給 C 間隔結構時，時發生間隔的資料結構中的資料沒有表示法。|  
|22018|轉換規格的字元值無效|*\*StatementText*包含 C 類型是精確或近似數值、 日期時間或間隔資料類型; 資料行的 SQL 類型是字元資料類型; 和資料行中的值不是有效的常值的繫結的 C 類型。<br /><br /> SQL 型別時傳回的輸入/輸出或輸出參數，是精確或近似數值、 日期時間或間隔資料類型;C 類型是 SQL_C_CHAR;和資料行中的值不是有效的常值的繫結的 SQL 類型。|  
|22019|無效的逸出字元|備妥的陳述式相關聯*StatementHandle*包含**像是**述詞，以及**逸出**中**其中**子句，並之後的逸出字元的長度**逸出**不是等於 1。|  
|22025|無效的逸出序列|備妥的陳述式相關聯*StatementHandle*包含 「**像是**_模式值_**逸出**_逸出字元_"中**其中**子句，並遵循模式值的逸出字元的字元不是其中一個"%"或"_"。|  
|23000|完整性條件約束違規|備妥的陳述式相關聯*StatementHandle*包含參數。 參數值是 NULL，定義為 NOT NULL 相關聯的資料表資料行中的資料行、 資料行限制為只包含唯一值，卻提供了重複的值或違反某些其他的完整性條件約束。|  
|24000|指標狀態無效|資料指標已定位*StatementHandle*依**SQLFetch**或是**SQLFetchScroll**。 如果此錯誤會傳回由驅動程式管理員**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 資料指標是開啟*StatementHandle*。<br /><br /> 備妥的陳述式相關聯*StatementHandle*包含定位的 update 或 delete statemen、 t 和資料指標置於結果集或結果集的結尾之後開始之前。|  
|40001|序列化失敗|交易已回復因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|42000|語法錯誤或存取違規|使用者沒有執行備妥的陳述式相關聯的權限*StatementHandle*。|  
|44000|WITH CHECK OPTION 違規|備妥的陳述式相關聯*StatementHandle*包含**插入**檢視的資料表上執行的陳述式或衍生自檢視的資料表所建立的指定資料表**WITH CHECK OPTION**，讓一或多個資料列受到**插入**陳述式將不再會出現在檢視的資料表。<br /><br /> 備妥的陳述式相關聯*StatementHandle*包含**更新**檢視的資料表上執行的陳述式或衍生自檢視的資料表所建立的指定資料表**WITH CHECK OPTION**，讓一或多個資料列受到**更新**陳述式將不再會出現在檢視的資料表。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLExecute**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) *StatementHandle*尚未準備。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|參數值時，設定**SQLBindParameter**、 為 null 指標，以及參數長度值不是 0，SQL_NULL_DATA，SQL_DATA_AT_EXEC，SQL_DEFAULT_PARAM，或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 參數值時，設定**SQLBindParameter**、 不是 null 指標; C 資料類型 SQL_C_BINARY 或 SQL_C_CHAR;，參數長度值小於 0，但不是 SQL_NTS、 SQL_NULL_DATA、 SQL_DEFAULT_PARAM 或 SQL_DATA_AT_EXEC，或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 參數長度值受限於**SQLBindParameter**是設定為 SQL_DATA_AT_EXEC; 的 SQL 型別是 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特有的資料類型; 以及 SQL_NEED_LONG_DATA_LEN 資訊在中輸入**SQLGetInfo**是"Y"。|  
|HY105|無效的參數類型|指定的引數的值*了*中**SQLBindParameter**是 SQL_PARAM_OUTPUT，而參數是輸入的參數。|  
|HY109|無效的資料指標位置|備妥的陳述式所定位的 update 或 delete 陳述式，以及指標置於 (由**SQLSetPos**或**SQLFetchScroll**) 上的已刪除或無法擷取資料列。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 陳述式屬性已設定為驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
 **SQLExecute**可以傳回任何可傳回的 SQLSTATE **SQLPrepare**，這取決於資料來源時評估陳述式相關聯的 SQL 陳述式。  
  
## <a name="comments"></a>註解  
 **SQLExecute**執行陳述式的備妥**SQLPrepare**。 應用程式處理或捨棄在呼叫的結果之後**SQLExecute**，應用程式可以呼叫**SQLExecute**再次使用新的參數值。 如需備妥的執行的詳細資訊，請參閱[已備妥執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
 若要執行**選取** 不止一次的陳述式，呼叫應用程式必須**SQLCloseCursor**之前重新**選取**陳述式。  
  
 如果資料來源是在手動認可模式 （需要明確的交易初始），而且已經尚未起始交易，此驅動程式傳送的 SQL 陳述式之前，就會起始交易。 如需詳細資訊，請參閱 <<c0> [ 交易](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 如果應用程式使用**SQLPrepare**準備並**SQLExecute**提交**認可**或**回復**陳述式，它不會DBMS 的產品之間的互通性。 若要認可或回復交易，呼叫**SQLEndTran**。  
  
 如果**SQLExecute**遇到資料在執行中參數，它會傳回 SQL_NEED_DATA。 應用程式傳送資料使用**SQLParamData**並**SQLPutData**。 請參閱[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)， [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)，以及[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 如果**SQLExecute**執行搜尋的 update、 insert 或 delete 陳述式而不會影響任何資料來源，呼叫端的資料列**SQLExecute**傳回 sql_no_data 為止。  
  
 SQL_ATTR_PARAMSET_SIZE 陳述式屬性的值大於 1，且 SQL 陳述式中包含至少一個參數標記，如果**SQLExecute**陣列中執行 SQL 陳述式，針對每一組參數值執行一次指向 *\*ParameterValuePtr*的呼叫中引數**SQLBindParameter**。 如需詳細資訊，請參閱 <<c0> [ 參數值的陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 如果您啟用書籤，並執行的查詢可能不支援書籤、 驅動程式應該嘗試強制轉型環境，以變更屬性值，並傳回 SQLSTATE 01S02 支援書籤 （選項值已變更）。 如果無法變更屬性，驅動程式應該會傳回 SQLSTATE HY024 （無效的屬性值）。  
  
> [!NOTE]  
>  使用連接共用時，應用程式必須執行 SQL 陳述式，例如變更資料庫或資料庫的內容**使用**_資料庫_變更的 SQL Server 中的陳述式資料來源所使用的目錄。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)，以及[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|關閉資料指標|[SQLCloseCursor 函式](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|執行認可或復原作業|[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|正在擷取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|釋放陳述式控制代碼|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|傳回資料指標名稱|[SQLGetCursorName 函式](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|正在擷取部分或全部的資料行|[SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回的資料傳送至下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|準備執行陳述式|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|在執行階段傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
