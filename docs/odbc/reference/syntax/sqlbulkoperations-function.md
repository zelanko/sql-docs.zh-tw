---
title: SQLBulkOperations 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60bcb6851adeba08105dabd6fb0800d2e969a04e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343178"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 函式
**標準**  
 引進的版本:ODBC 3.0 標準合規性:ODBC  
  
 **摘要**  
 **SQLBulkOperations**會執行大量插入和大量書簽作業, 包括依書簽的更新、刪除和提取。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *運算*  
 源要執行的作業:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 如需詳細資訊, 請參閱「批註」。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBulkOperations**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫**SQLGetDiagRec**與 HandleType handletype 來, 以及*StatementHandle*的  *控制碼*, 來取得相關聯的 SQLSTATE 值. 下表列出通常由**SQLBulkOperations**所傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
 對於可傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 的所有 SQLSTATEs (01xxx SQLSTATEs 除外), 如果一或多個 (但非全部) SQL_SUCCESS_WITH_INFO 作業的資料列發生錯誤, 則會傳回多資料列, 如果發生錯誤, 則會傳回 SQL_ERROR單一資料列作業。  
  
|SQLSTATE|Error|說明|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01004|字串資料右側截斷|*Operation*引數為 SQL_FETCH_BY_BOOKMARK, 且資料類型為 SQL_C_CHAR 或 SQL_C_BINARY 的一或多個資料行傳回的字串或二進位資料, 導致截斷非空白字元或非 Null 的二進位資料。|  
|01S01|資料列發生錯誤|作業  引數已 SQL_ADD, 且在執行作業但至少已成功加入一個資料列時, 在一或多個資料列中發生錯誤。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。<br /><br /> (只有在應用程式與 ODBC 2 搭配使用時, 才會引發此錯誤。*x*驅動程式)。|  
|01S07|小數截斷|*Operation*引數為 SQL_FETCH_BY_BOOKMARK, 應用程式緩衝區的資料類型不是 SQL_C_CHAR 或 SQL_C_BINARY, 而且已截斷一或多個資料行的應用程式緩衝區傳回的資料。 (對於數值 C 資料類型, 數位的小數部分已截斷。 若為包含時間元件的 time、timestamp 和 interval C 資料類型, 則會截斷時間的小數部分)。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|07006|限制的資料類型屬性違規|*Operation*引數是 SQL_FETCH_BY_BOOKMARK, 而且結果集中資料行的資料值無法轉換成**SQLBindCol**呼叫中的*TargetType*引數所指定的資料類型。<br /><br /> *Operation*引數為 SQL_UPDATE_BY_BOOKMARK 或 SQL_ADD, 而且應用程式緩衝區中的資料值無法轉換成結果集內資料行的資料類型。|  
|07009|不正確描述項索引|已 SQL_ADD  引數作業, 且資料行系結的資料行編號大於結果集內的資料行數目。|  
|21S02|衍生資料表的程度與資料行清單不符|引數  作業已 SQL_UPDATE_BY_BOOKMARK;而且沒有任何資料行是可更新的, 因為所有資料行都是未系結或唯讀, 或系結長度/指標緩衝區中的值已 SQL_COLUMN_IGNORE。|  
|22001|字串資料右側截斷|將字元或二進位值指派給結果集中的資料行, 會造成截斷非空白 (字元) 或非 null (二進位) 字元或位元組。|  
|22003|數值超出範圍|*Operation*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK, 而將數值指派給結果集中的資料行, 會導致整個 (而不是小數) 部分的數位被截斷。<br /><br /> 引數  作業已 SQL_FETCH_BY_BOOKMARK, 而傳回一個或多個系結資料行的數值可能會造成有效位數遺失。|  
|22007|不正確日期時間格式|*Operation*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK, 而且將日期或時間戳記值指派給結果集中的資料行, 導致 year、month 或 day 欄位超出範圍。<br /><br /> 引數  作業已 SQL_FETCH_BY_BOOKMARK, 而傳回一或多個系結資料行的日期或時間戳記值, 會導致 year、month 或 day 欄位超出範圍。|  
|22008|日期/時間欄位溢位|*Operation*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK, 而傳送至結果集中資料行之資料的 datetime 算術效能, 導致結果的日期時間欄位 (年、月、日、小時、分鐘或第二個欄位)落在欄位的允許值範圍外, 或根據西曆的日期時間自然規則而無效。<br /><br /> 作業  引數已 SQL_FETCH_BY_BOOKMARK, 而從結果集取得之資料的 datetime 算術效能, 導致結果出現在範圍外的日期時間欄位 (年、月、日、小時、分鐘或第二個欄位)欄位的允許值範圍, 或根據西曆的日期時間自然規則而無效。|  
|22015|間隔欄位溢位|*Operation*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK, 而將精確數值或間隔 C 類型指派給 interval SQL 資料類型會造成有效位數遺失。<br /><br /> *Operation*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK;指派至間隔 SQL 類型時, 不會在 interval SQL 類型中表示 C 類型的值。<br /><br /> *Operation*引數已 SQL_FETCH_BY_BOOKMARK, 且從精確的數值或間隔 SQL 類型指派到間隔 C 類型, 導致前置欄位中的有效位數遺失。<br /><br /> *Operation*引數為 SQL_FETCH_BY_BOOKMARK;指派至間隔 C 類型時, 不會在間隔 C 類型中表示 SQL 類型的值。|  
|22018|轉換規格的字元值無效|*Operation*引數為 SQL_FETCH_BY_BOOKMARK;C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;而資料行中的值不是系結 C 類型的有效常值。<br /><br /> 引數  作業為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK;SQL 類型是精確或近似的數值、日期時間或間隔資料類型;C 類型為 SQL_C_CHAR;而資料行中的值不是系結 SQL 類型的有效常值。|  
|23000|完整性條件約束違規|*Operation*引數為 SQL_ADD、SQL_DELETE_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK, 但違反了完整性條件約束。<br /><br /> *Operation*引數為 SQL_ADD, 且未系結的資料行定義為 not Null 且沒有預設值。<br /><br /> 作業  引數為 SQL_ADD, 系結*StrLen_or_IndPtr*緩衝區中指定的長度為 SQL_COLUMN_IGNORE, 且資料行沒有預設值。|  
|24000|指標狀態無效|*StatementHandle*處於已執行狀態, 但沒有與*StatementHandle*相關聯的結果集。|  
|40001|序列化失敗|交易已回復, 因為有另一個交易的資源鎖死。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗, 無法判斷交易的狀態。|  
|42000|語法錯誤或存取違規|驅動程式無法視需要鎖定資料列, 以執行*operation*引數中要求的作業。|  
|44000|WITH CHECK OPTION 違規|*Operation*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK, 且 insert 或 UPDATE 已在已查看的資料表 (或衍生自已查看資料表的資料表) 上執行, 這種方式是藉由指定**WITH CHECK OPTION**來建立, 讓一個或多個資料列受 insert 或 update 影響的會再出現在已查看的資料表中。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|作業已取消|已啟用*StatementHandle*的非同步處理。 已呼叫函式, 在完成執行之前, 會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式, 並在完成執行之前, 從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|(DM) 已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLBulkOperations**函數時, 這個非同步函式仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** , 並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前, 會呼叫這個函式。<br /><br /> (DM) 指定的*StatementHandle*不是處於執行中狀態。 在未先呼叫**SQLExecDirect**、 **SQLExecute**或目錄函式的情況下呼叫函數。<br /><br /> (DM) 已針對*StatementHandle*呼叫非同步執行的函式 (而非這個函式), 而且在呼叫這個函數時仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。<br /><br /> (DM) 驅動程式是 ODBC 2。在呼叫**SQLFetchScroll**或**SQLFetch**之前, 已針對*StatementHandle*呼叫*x*驅動程式和**SQLBulkOperations** 。<br /><br /> 在*StatementHandle*上呼叫**SQLExtendedFetch**之後, 已呼叫 (DM) **SQLBulkOperations** 。|  
|HY011|無法立即設定屬性|(DM) 驅動程式是 ODBC 2。*x*驅動程式, 而且 SQL_ATTR_ROW_STATUS_PTR 語句屬性是在呼叫**SQLFetch**或**SQLFetchScroll**和**SQLBulkOperations**之間設定。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|*Operation*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK;資料值不是 null 指標;C 資料類型為 SQL_C_BINARY 或 SQL_C_CHAR;而資料行長度值小於 0, 但不等於 SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS 或 SQL_Null_DATA, 或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 長度/指標緩衝區中的值是 SQL_DATA_AT_EXEC;SQL 類型可能是 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定資料類型;而**SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型是 "Y"。<br /><br /> *Operation*引數為 SQL_ADD, SQL_ATTR_USE_BOOKMARK 語句屬性設為 SQL_UB_VARIABLE, 而資料行0系結至緩衝區, 其長度不等於此結果集之書簽的最大長度。 (此長度適用于 IRD 的 [SQL_DESC_OCTET_LENGTH] 欄位, 可透過呼叫**SQLDescribeCol**、 **SQLColAttribute**或**SQLGetDescField**取得)。|  
|HY092|不正確屬性識別碼|(DM) 為*Operation*引數指定的值無效。<br /><br /> *Operation*引數為 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK, 而 SQL_ATTR_CONCURRENCY 語句屬性已設定為 SQL_CONCUR_READ_ONLY。<br /><br /> *Operation*引數為 SQL_DELETE_BY_BOOKMARK、SQL_FETCH_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK, 但書簽資料行未系結, 或 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_OFF。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援*operation*引數中要求的作業。|  
|HYT00|已超過逾時的設定|在資料來源傳回結果集之前, 查詢超時時間已過期。 您可透過**SQLSetStmtAttr** , 使用 SQL_ATTR_QUERY_TIMEOUT 的*屬性*引數來設定超時時間。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時, 就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING, 而且如果啟用通知模式, 則必須在控制碼上呼叫**SQLCompleteAsync** , 才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
  
> [!CAUTION]  
>  如需有關如何在中呼叫哪些語句狀態**SQLBulkOperations** , 以及它必須如何做以與 ODBC 2 相容的詳細資訊。*x*應用程式, 請參閱附錄 G: 中的[區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)一節。回溯相容性的驅動程式方針。  
  
 應用程式會使用**SQLBulkOperations** , 在對應至目前查詢的基表或視圖上執行下列作業:  
  
-   加入新的資料列。  
  
-   更新一組資料列, 其中的每個資料列都是由書簽所識別。  
  
-   刪除一組資料列, 其中的每個資料列都是由書簽所識別。  
  
-   提取一組資料列, 其中的每個資料列都是由書簽所識別。  
  
 呼叫**SQLBulkOperations**之後, 區塊資料指標位置會是未定義的。 應用程式必須呼叫**SQLFetchScroll**來設定游標位置。 應用程式應該只使用 SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE 或 SQL_FETCH_BOOKMARK 的*FetchOrientation*引數呼叫**SQLFetchScroll** 。 如果應用程式使用 SQL_FETCH_PRIOR、SQL_FETCH_NEXT 或 SQL_FETCH_RELATIVE 的*FetchOrientation*引數呼叫**SQLFetch**或**SQLFetchScroll** , 則資料指標位置會是未定義的。  
  
 在呼叫**SQLBulkOperations**時, 您可以將呼叫**SQLBindCol**所指定的資料行長度/指標緩衝區設定為 SQL_COLUMN_IGNORE, 以忽略資料行的呼叫所執行的大量作業。  
  
 應用程式在呼叫**SQLBulkOperations**時, 不需要設定 SQL_ATTR_ROW_OPERATION_PTR 語句屬性, 因為使用此函數執行大量作業時無法忽略資料列。  
  
 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性所指向的緩衝區包含受**SQLBulkOperations**呼叫影響的資料列數目。  
  
 當*Operation*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK, 且與資料指標相關聯的查詢規格的選取清單包含相同資料行的多個參考時, 不論是否產生錯誤, 都會定義驅動程式, 或驅動程式會忽略重複的參考, 並執行要求的作業。  
  
 如需有關如何使用**SQLBulkOperations**的詳細資訊, 請參閱[使用 SQLBulkOperations 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。  
  
## <a name="performing-bulk-inserts"></a>執行大量插入  
 若要使用**SQLBulkOperations**插入資料, 應用程式會執行下列一連串的步驟:  
  
1.  執行傳回結果集的查詢。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為它想要插入的資料列數目。  
  
3.  呼叫**SQLBindCol**來系結它想要插入的資料。 資料會系結至大小等於 SQL_ATTR_ROW_ARRAY_SIZE 值的陣列。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的陣列大小應該等於 SQL_ATTR_ROW_ARRAY_SIZE, 或 SQL_ATTR_ROW_STATUS_PTR 應該是 null 指標。  
  
4.  呼叫**SQLBulkOperations**(*StatementHandle,* SQL_ADD) 以執行插入。  
  
5.  如果應用程式已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性, 它就可以檢查此陣列, 以查看作業的結果。  
  
 如果應用程式在呼叫具有 SQL_ADD 的作業引數的  **SQLBulkOperations**之前系結資料行 0, 驅動程式將會使用新插入之資料列的書簽值來更新系結的資料行0緩衝區。 若要進行這種情況, 應用程式必須先將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE, 才能執行語句。 (這無法與 ODBC 2 搭配使用。*x*驅動程式)。  
  
 您可以使用 SQLParamData 和 SQLPutData 的呼叫, 以 SQLBulkOperations 的方式將長資料新增至元件。 如需詳細資訊, 請參閱本函數參考後面的「提供大量插入和更新的長資料」。  
  
 應用程式在呼叫**SQLBulkOperations**之前, 不需要呼叫**SQLFetch**或**SQLFetchScroll** (除了針對 ODBC 2 進行時除外)。*x*驅動程式;請參閱回溯[相容性和標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md))。  
  
 如果**SQLBulkOperations**(具有 SQL_ADD 的*Operation*引數) 在包含重復資料行的資料指標上呼叫, 則此行為是驅動程式定義的。 驅動程式可以傳回驅動程式定義的 SQLSTATE、將資料新增至結果集內出現的第一個資料行, 或執行其他驅動程式定義的行為。  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>使用書簽執行大量更新  
 若要使用書簽搭配**SQLBulkOperations**來執行大量更新, 應用程式會依序執行下列步驟:  
  
1.  將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。  
  
2.  執行傳回結果集的查詢。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為它想要更新的資料列數目。  
  
4.  呼叫**SQLBindCol**來系結它想要更新的資料。 資料會系結至大小等於 SQL_ATTR_ROW_ARRAY_SIZE 值的陣列。 它也會呼叫**SQLBindCol**來系結資料行 0 (書簽資料行)。  
  
5.  將想要更新之資料列的書簽複製到系結至資料行0的陣列。  
  
6.  更新系結緩衝區中的資料。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的陣列大小應該等於 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 應該是 null 指標。  
  
7.  呼叫**SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK)。  
  
    > [!NOTE]  
    >  如果應用程式已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性, 它就可以檢查此陣列, 以查看作業的結果。  
  
8.  選擇性地呼叫**SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) 以將資料提取到系結的應用程式緩衝區, 以確認已發生更新。  
  
9. 如果資料已更新, 驅動程式會將資料列狀態陣列中的值變更為要 SQL_ROW_UPDATED 的適當資料列。  
  
 **SQLBulkOperations**所執行的大量更新可以使用**SQLParamData**和**SQLPutData**的呼叫來包含長資料。 如需詳細資訊, 請參閱本函數參考後面的「提供大量插入和更新的長資料」。  
  
 如果書簽保存在資料指標之間, 則應用程式不需要呼叫**SQLFetch**或**SQLFetchScroll** , 就可以由書簽進行更新。 它可以使用從上一個資料指標儲存的書簽。 如果書簽不會跨資料指標保存, 應用程式必須呼叫**SQLFetch**或**SQLFetchScroll**來取得書簽。  
  
 如果**SQLBulkOperations**(具有 SQL_UPDATE_BY_BOOKMARK 的*Operation*引數) 在包含重復資料行的資料指標上呼叫, 則此行為是驅動程式定義的。 驅動程式可以傳回驅動程式定義的 SQLSTATE、更新結果集中顯示的第一個資料行, 或執行其他驅動程式定義的行為。  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>使用書簽執行大量提取  
 若要使用書簽搭配**SQLBulkOperations**來執行大量提取, 應用程式會依序執行下列步驟:  
  
1.  將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。  
  
2.  執行傳回結果集的查詢。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為它想要提取的資料列數目。  
  
4.  呼叫**SQLBindCol**來系結它想要提取的資料。 資料會系結至大小等於 SQL_ATTR_ROW_ARRAY_SIZE 值的陣列。 它也會呼叫**SQLBindCol**來系結資料行 0 (書簽資料行)。  
  
5.  將想要提取的資料列書簽複製到系結至資料行0的陣列。 (這會假設應用程式已分別取得書簽)。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的陣列大小應該等於 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 應該是 null 指標。  
  
6.  呼叫**SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK)。  
  
7.  如果應用程式已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性, 它就可以檢查此陣列, 以查看作業的結果。  
  
 如果書簽保存在資料指標之間, 則應用程式不需要呼叫**SQLFetch**或**SQLFetchScroll** , 就可以由書簽提取。 它可以使用從上一個資料指標儲存的書簽。 如果書簽不會跨資料指標保存, 應用程式必須呼叫**SQLFetch**或**SQLFetchScroll**一次來抓取書簽。  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>使用書簽執行大量刪除  
 若要使用書簽搭配**SQLBulkOperations**來執行大量刪除, 應用程式會依序執行下列步驟:  
  
1.  將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。  
  
2.  執行傳回結果集的查詢。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為它想要刪除的資料列數目。  
  
4.  呼叫**SQLBindCol**來系結資料行 0 (書簽資料行)。  
  
5.  將想要刪除之資料列的書簽複製到系結至資料行0的陣列。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的陣列大小應該等於 SQL_ATTR_ROW_ARRAY_SIZE 或 SQL_ATTR_ROW_STATUS_PTR 應該是 null 指標。  
  
6.  呼叫**SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK)。  
  
7.  如果應用程式已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性, 它就可以檢查此陣列, 以查看作業的結果。  
  
 如果書簽跨游標保存, 應用程式就不需要在書簽刪除之前呼叫**SQLFetch**或**SQLFetchScroll** 。 它可以使用從上一個資料指標儲存的書簽。 如果書簽不會跨資料指標保存, 應用程式必須呼叫**SQLFetch**或**SQLFetchScroll**一次來抓取書簽。  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>提供大量插入和更新的長資料  
 長資料可提供給**SQLBulkOperations**的呼叫所執行的大量插入和更新。 若要插入或更新長資料, 應用程式會執行下列步驟, 以及本主題前面「執行大量插入」和「使用書簽執行大量更新」一節中所述的步驟。  
  
1.  當它使用**SQLBindCol**來系結資料時, 應用程式會將 *\** 應用程式定義的值 (例如資料行編號) 放在 TargetValuePtr 緩衝區中, 以用於資料執行中的資料行。 稍後可以使用此值來識別資料行。  
  
     應用程式會將 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果放在 *\*StrLen_or_IndPtr*緩衝區中。 如果資料行的 SQL 資料類型為 SQL_LONGVARBINARY、SQL_LONGVARCHAR 或 long 資料來源特定的資料類型, 而驅動程式針對**SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型傳回 "Y", *length*就是要在其中寫入的位元組數目。針對參數傳送;否則, 它必須是非負值, 而且會被忽略。  
  
2.  呼叫**SQLBulkOperations**時, 如果有執行中的資料行, 此函式會傳回 SQL_NEED_DATA 並繼續進行步驟 3, 如下所示。 (如果沒有任何執行中的資料行, 則程式已完成)。  
  
3.  應用程式會呼叫**SQLParamData** , 以取得要處理之第一個資料執行中資料行的 *\*TargetValuePtr*緩衝區位址。 **SQLParamData**會傳回 SQL_NEED_DATA。 應用程式會從 *\*TargetValuePtr*緩衝區捕獲應用程式定義的值。  
  
    > [!NOTE]  
    >  雖然資料執行中的參數與資料執行中的資料行相似, 但每個**SQLParamData**所傳回的值都不同。  
  
     資料執行中的資料行是資料列集中的資料行, 當使用**SQLBulkOperations**更新或插入資料列時, 資料會與**SQLPutData**一起傳送。 它們會與**SQLBindCol**系結。 **SQLParamData**傳回的值是要處理之 **TargetValuePtr*緩衝區中資料列的位址。  
  
4.  應用程式會呼叫**SQLPutData**一次或多次來傳送資料行的資料。 如果無法在**SQLPutData**中指定的 *\*TargetValuePtr*緩衝區內傳回所有資料值, 則需要多個呼叫; 只有在傳送字元 C 資料時, 才允許多次呼叫同一資料行的**SQLPutData**包含字元、二進位或資料來源特定資料類型, 或將二進位 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行。  
  
5.  應用程式會再次呼叫**SQLParamData** , 表示資料行已傳送所有資料。  
  
    -   如果有更多資料執行中的資料行, **SQLParamData**會傳回 SQL_NEED_DATA 和*TargetValuePtr*緩衝區的位址, 以用於下一個要處理的資料執行中資料行。 應用程式會重複步驟4和5。  
  
    -   如果沒有其他資料執行中的資料行, 則程式已完成。 如果語句執行成功, **SQLParamData**會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO;如果執行失敗, 則會傳回 SQL_ERROR。 此時, **SQLParamData**可以傳回**SQLBulkOperations**所能傳回的任何 SQLSTATE。  
  
 如果作業已取消, 或**SQLParamData**或**SQLPutData**在**SQLBulkOperations**傳回 SQL_NEED_DATA 之後發生錯誤, 且在傳送所有資料執行中資料行的資料之前, 應用程式只能呼叫**SQLCancel**、 **SQLGetDiagField**、 **SQLGetDiagRec**、 **SQLGetFunctions**、 **SQLParamData**或**SQLPutData** (適用于語句) 或與語句相關聯的連接。 如果它針對語句或與語句相關聯的連接呼叫任何其他函式, 此函式會傳回 SQL_ERROR 和 SQLSTATE HY010 (函數序列錯誤)。  
  
 如果應用程式在驅動程式仍然需要資料執行中資料行的資料時呼叫**SQLCancel** , 驅動程式會取消作業。 然後, 應用程式就可以再次呼叫**SQLBulkOperations** ;取消不會影響資料指標狀態或目前的資料指標位置。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 在呼叫**SQLBulkOperations**之後, 資料列狀態陣列會包含資料列集中每個資料列的狀態值。 驅動程式會在呼叫**SQLFetch**、 **SQLFetchScroll**、 **SQLSetPos**或**SQLBulkOperations**之後, 設定此陣列中的狀態值。 如果**SQLFetch**或**SQLFetchScroll**在**SQLBulkOperations**之前尚未呼叫, 此陣列一開始會填入**SQLBulkOperations**的呼叫。 SQL_ATTR_ROW_STATUS_PTR 語句屬性會指向這個陣列。 資料列狀態陣列中的元素數目必須等於資料列集中的資料列數目 (如 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性所定義)。 如需有關此資料列狀態陣列的詳細資訊, 請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 下列範例會從 Customers 資料表一次提取10個數據列。 接著, 它會提示使用者輸入要採取的動作。 為了減少網路流量, 範例緩衝區會在系結陣列中本機更新、刪除和插入, 但會在超過資料列集資料的位移上進行。 當使用者選擇將更新、刪除和插入傳送至資料來源時, 程式碼會適當地設定系結位移, 並呼叫**SQLBulkOperations**。 為了簡單起見, 使用者無法緩衝超過10個更新、刪除或插入。  
  
```cpp  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得描述項的單一欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得描述項的多個欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定描述項的單一欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定描述項的多個欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|定位游標、重新整理資料列集中的資料, 或更新或刪除資料列集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
