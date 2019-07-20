---
title: SQLSetPos 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80f14b99d2c7dac91116186fdcf53ff77ee6c2c0
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343071"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 函式
**標準**  
 引進的版本:ODBC 1.0 標準合規性:ODBC  
  
 **摘要**  
 **SQLSetPos**會在資料列集中設定游標位置, 並允許應用程式重新整理資料列集中的資料, 或更新或刪除結果集中的資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *RowNumber*  
 源資料列集的位置, 要在其上執行使用*operation*引數所指定的作業。 如果*RowNumber*是 0, 則作業會套用至資料列集中的每個資料列。  
  
 如需其他資訊, 請參閱「批註」。  
  
 *運算*  
 源要執行的作業:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  ODBC 3.x 的*Operation*引數的 SQL_ADD 值已被取代  。 ODBC  3.x 驅動程式必須支援 SQL_ADD 以提供回溯相容性。 這項功能已由呼叫**SQLBulkOperations**與 SQL_ADD 的作業取代  。 當 ODBC 3.x  應用程式與 odbc 2.x 驅動程式搭配  使用時, 驅動程式管理員會使用 SQL_ADD 的作業, 將對**SQLBulkOperations**的呼叫對應至**SQLSetPos**的作業  。   
  
 如需詳細資訊, 請參閱「批註」。  
  
 *LockType*  
 源指定在執行*operation*引數中指定的作業之後, 如何鎖定資料列。  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 如需詳細資訊, 請參閱「批註」。  
  
 **傳回**  
  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetPos**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫 SQLGetDiagRec 和 HandleType 的  Handletype 來和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。  下表列出**SQLSetPos**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
 對於可傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 的所有 SQLSTATEs (01xxx SQLSTATEs 除外), 如果一或多個 (但非全部) SQL_SUCCESS_WITH_INFO 作業的資料列發生錯誤, 則會傳回多資料列, 如果發生錯誤, 則會傳回 SQL_ERROR單一資料列作業。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01001|資料指標操作衝突|*Operation*引數為 SQL_DELETE 或 SQL_UPDATE, 且未刪除或更新任何資料列或有一個以上的資料列。 (如需有關多個資料列更新的詳細資訊, 請參閱**SQLSetStmtAttr**中 SQL_ATTR_SIMULATE_CURSOR*屬性*的描述。)(函數會傳回 SQL_SUCCESS_WITH_INFO)。<br /><br /> *Operation*引數為 SQL_DELETE 或 SQL_UPDATE, 且作業因開放式平行存取而失敗。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01004|字串資料右側截斷|*Operation*引數為 SQL_REFRESH, 且資料類型為 SQL_C_CHAR 或 SQL_C_BINARY 的一或多個資料行傳回的字串或二進位資料, 導致截斷非空白字元或非 Null 的二進位資料。|  
|01S01|資料列發生錯誤|*RowNumber*引數為 0, 且在執行以*operation*引數指定的作業時, 在一或多個資料列中發生錯誤。<br /><br /> (如果一個或多個 (但非全部) 多資料列作業的資料列發生錯誤, 則會傳回 SQL_SUCCESS_WITH_INFO, 而如果單一資料列作業發生錯誤, 則會傳回 SQL_ERROR)。<br /><br /> (只有在**SQLExtendedFetch**之後呼叫**SQLSetPos**時, 如果驅動程式是 ODBC 2.x 驅動程式, 且  未使用資料指標程式庫, 才會傳回此 SQLSTATE)。|  
|01S07|小數截斷|*Operation*引數為 SQL_REFRESH, 應用程式緩衝區的資料類型不是 SQL_C_CHAR 或 SQL_C_BINARY, 而且已截斷一或多個資料行的應用程式緩衝區傳回的資料。 若為數值資料類型, 則會截斷數位的小數部分。 若為包含時間元件的時間、時間戳記和間隔資料類型, 則會截斷時間的小數部分。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|07006|限制的資料類型屬性違規|在**SQLBindCol**的呼叫中, 無法將結果集中資料行的資料值轉換成*TargetType*所指定的資料類型。|  
|07009|不正確描述項索引|引數  作業為 SQL_REFRESH 或 SQL_UPDATE, 且資料行系結的資料行編號大於結果集中的資料行數目。|  
|21S02|衍生資料表的程度與資料行清單不符|引數  作業已 SQL_UPDATE, 而且沒有任何資料行是可更新的, 因為所有資料行都是未系結、唯讀, 或系結長度/指標緩衝區中的值是 SQL_COLUMN_IGNORE。|  
|22001|字串資料, 右截斷|*Operation*引數已 SQL_UPDATE, 而將字元或二進位值指派給資料行時, 導致截斷非空白 (字元) 或非 null (二進位) 字元或位元組。|  
|22003|數值超出範圍|SQL_UPDATE 自  變數作業, 而將數值指派給結果集中的資料行, 會導致整個 (而不是小數) 部分的數位被截斷。<br /><br /> 引數  作業已 SQL_REFRESH, 而傳回一個或多個系結資料行的數值可能會造成有效位數遺失。|  
|22007|不正確日期時間格式|SQL_UPDATE 自  變數作業, 並將日期或時間戳記值指派給結果集中的資料行, 導致 year、month 或 day 欄位超出範圍。<br /><br /> 引數  作業已 SQL_REFRESH, 而傳回一或多個系結資料行的日期或時間戳記值, 會導致 year、month 或 day 欄位超出範圍。|  
|22008|日期/時間欄位溢位|*Operation*引數已 SQL_UPDATE, 而傳送至結果集中資料行的日期時間算術效能, 導致結果超出允許的日期時間欄位 (年、月、日、小時、分鐘或第二個欄位)欄位的值範圍, 或根據西曆的日期時間自然規則而無效。<br /><br /> *Operation*引數已 SQL_REFRESH, 而從結果集取得之資料的日期時間算術效能, 導致結果超出允許的日期時間欄位 (年、月、日、小時、分鐘或第二個欄位)欄位的值範圍, 或根據西曆的日期時間自然規則而無效。|  
|22015|間隔欄位溢位|*Operation*引數已 SQL_UPDATE, 且將精確數值或間隔 C 類型指派給 interval SQL 資料類型會造成有效位數遺失。<br /><br /> *Operation*引數為 SQL_UPDATE;指派至間隔 SQL 類型時, 不會在 interval SQL 類型中表示 C 類型的值。<br /><br /> *Operation*引數已 SQL_REFRESH, 且從精確的數值或間隔 SQL 類型指派到間隔 C 類型, 導致前置欄位中的有效位數遺失。<br /><br /> *Operation*引數為 SQL_ REFRESH;指派至間隔 C 類型時, 不會在間隔 C 類型中表示 SQL 類型的值。|  
|22018|轉換規格的字元值無效|*Operation*引數為 SQL_REFRESH;C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;而資料行中的值不是系結 C 類型的有效常值。<br /><br /> 引數  作業已 SQL_UPDATE;SQL 類型是精確或近似的數值、日期時間或間隔資料類型;C 類型為 SQL_C_CHAR;而資料行中的值不是系結 SQL 類型的有效常值。|  
|23000|完整性條件約束違規|引數  作業為 SQL_DELETE 或 SQL_UPDATE, 且已違反完整性條件約束。|  
|24000|指標狀態無效|*StatementHandle*處於已執行狀態, 但沒有與*StatementHandle*相關聯的結果集。<br /><br /> (DM) 已在*StatementHandle*上開啟資料指標, 但尚未呼叫**SQLFetch**或**SQLFetchScroll** 。<br /><br /> 已在*StatementHandle*上開啟資料指標, 且已呼叫**SQLFetch**或**SQLFetchScroll** , 但資料指標位於結果集開頭之前或結果集結束之後。<br /><br /> 引數  作業為 SQL_DELETE、SQL_REFRESH 或 SQL_UPDATE, 且資料指標位於結果集開頭之前或結果集結尾的後面。|  
|40001|序列化失敗|因為另一筆交易發生資源鎖死, 所以交易已回復。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗, 無法判斷交易的狀態。|  
|42000|語法錯誤或存取違規|驅動程式無法視需要鎖定資料列, 以執行引數作業中要求的作業  。<br /><br /> 驅動程式無法在引數*LockType*中鎖定要求的資料列。|  
|44000|WITH CHECK OPTION 違規|作業  引數已 SQL_UPDATE, 且已在已查看的資料表上執行更新, 或已透過指定**WITH CHECK 選項**來建立的資料表, 讓更新所影響的一或多個資料列將不再是出現在已查看的表格中。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|作業已取消|已啟用*StatementHandle*的非同步處理。 已呼叫函式, 並在完成執行之前, 在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** , 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式, 並在完成執行之前, 從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|(DM) 已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫 SQLSetPos 函數時, 這個非同步函式仍在執行中。<br /><br /> (DM) 指定的*StatementHandle*不是處於執行中狀態。 在未先呼叫**SQLExecDirect**、 **SQLExecute**或目錄函式的情況下呼叫函數。<br /><br /> (DM) 已針對*StatementHandle*呼叫非同步執行的函式 (而非這個函式), 而且在呼叫這個函數時仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。<br /><br /> (DM) 驅動程式是 ODBC 2.x  驅動程式, 在呼叫**SQLFetch**之後, 會針對*StatementHandle*呼叫**SQLSetPos** 。|  
|HY011|無法立即設定屬性|(DM) 驅動程式是 ODBC 2.x  驅動程式;已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性;然後呼叫**SQLSetPos** , 然後呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLExtendedFetch** 。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|*Operation*引數為 SQL_UPDATE, 資料值為 null 指標, 且資料行長度值不是0、SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_Null_DATA 或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> *Operation*引數為 SQL_UPDATE;資料值不是 null 指標;C 資料類型為 SQL_C_BINARY 或 SQL_C_CHAR;而資料行長度值小於 0, 但不等於 SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS 或 SQL_Null_DATA, 或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 長度/指標緩衝區中的值是 SQL_DATA_AT_EXEC;SQL 類型可能是 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定資料類型;而**SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型是 "Y"。|  
|HY092|不正確屬性識別碼|(DM) 為*Operation*引數指定的值無效。<br /><br /> (DM) 為*LockType*引數指定的值無效。<br /><br /> *Operation*引數為 SQL_UPDATE 或 SQL_DELETE, 而 SQL_ATTR_CONCURRENCY 語句屬性為 SQL_ATTR_CONCUR_READ_ONLY。|  
|HY107|資料列值超出範圍|為引數*RowNumber*指定的值大於資料列集中的資料列數目。|  
|HY109|不正確資料指標位置|與*StatementHandle*相關聯的資料指標已定義為順向, 因此資料指標無法放在資料列集內。 請參閱**SQLSetStmtAttr**中 SQL_ATTR_CURSOR_TYPE 屬性的描述。<br /><br /> *Operation*引數是 SQL_UPDATE、SQL_DELETE 或 SQL_REFRESH, 而*RowNumber*引數所識別的資料列已被刪除或尚未提取。<br /><br /> (DM) *RowNumber*引數為 0, 且*Operation*引數為 SQL_POSITION。<br /><br /> 呼叫**SQLBulkOperations**之後, 以及在呼叫**SQLFetchScroll**或**SQLFetch**之前, 會呼叫**SQLSetPos** 。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援*操作*引數或*LockType*引數中所要求的作業。|  
|HYT00|已超過逾時的設定|在資料來源傳回結果集之前, 查詢超時時間已過期。 您可使用 SQL_ATTR_QUERY_TIMEOUT 的*屬性*, 透過**SQLSetStmtAttr**來設定超時時間。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時, 就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING, 而且如果啟用通知模式, 則必須在控制碼上呼叫**SQLCompleteAsync** , 才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
  
> [!CAUTION]
>  如需語句的詳細資訊, 說明可以在中呼叫**SQLSetPos** , 以及它需要如何處理 ODBC 2.x 應用  程式的相容性, 請參閱[區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
## <a name="rownumber-argument"></a>RowNumber 引數  
 *RowNumber*引數會指定要在資料列集中執行*operation*引數所指定之作業的資料列編號。 如果*RowNumber*是 0, 則作業會套用至資料列集中的每個資料列。 *RowNumber*必須是從0到資料列集中的資料列數目的值。  
  
> [!NOTE]  
>  在 C 語言中, 陣列是以0為基礎, 而*RowNumber*引數是以1為基礎。 例如, 若要更新資料列集的第五個數據列, 應用程式會修改位於陣列索引4的資料列集緩衝區, 但指定了5的*RowNumber* 。  
  
 所有作業會將資料指標放在*RowNumber*所指定的資料列上。 下列作業需要資料指標位置:  
  
-   定位 update 和 delete 語句。  
  
-   呼叫**SQLGetData**。  
  
-   使用 SQL_DELETE、SQL_REFRESH 和 SQL_UPDATE 選項來呼叫**SQLSetPos** 。  
  
 例如, 如果*RowNumber*是 2, 用於呼叫具有 SQL_DELETE 作業的**SQLSetPos** , 則資料指標會位於資料列集的第二個數據列上, 而且該資料列會被刪除。  第二個數據列的執行資料列狀態陣列中的專案 (由 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向) 會變更為 SQL_ROW_DELETED。  
  
 當應用程式呼叫**SQLSetPos**時, 可以指定游標位置。 一般來說, 它會呼叫具有 SQL_POSITION 或 SQL_REFRESH 作業的**SQLSetPos** , 以在執行定位的 update 或 delete 語句之前放置游標, 或呼叫**SQLGetData**。  
  
## <a name="operation-argument"></a>Operation 引數  
 *Operation*引數支援下列作業。 若要判斷資料來源支援哪些選項, 應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 呼叫**SQLGetInfo**資訊類型 (視游標的類型而定)。  
  
|*運算*<br /><br /> Argument - 引數|運算|  
|------------------------------|---------------|  
|SQL_POSITION|驅動程式會將資料指標置於*RowNumber*所指定的資料列上。<br /><br /> SQL_POSITION 作業會忽略 SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向之資料列狀態陣列的內容。 |  
|SQL_REFRESH|驅動程式會將游標放在*RowNumber*所指定的資料列上, 並重新整理該資料列之資料列集緩衝區中的資料。 如需有關驅動程式如何傳回資料列集緩衝區中資料的詳細資訊, 請參閱**SQLBindCol**中的資料列取向和資料行取向的描述。<br /><br /> 具有 SQL_REFRESH 作業  的**SQLSetPos**會更新目前所提取資料列集內的資料列狀態和內容。 這包括重新整理書簽。 由於緩衝區中的資料會重新整理, 但不會根據, 因此會修正資料列集中的成員資格。 這不同于呼叫**SQLFetchScroll**時所執行的重新整理, *FetchOrientation*為 SQL_FETCH_RELATIVE, 而*RowNumber*等於 0, 這會從結果集 refetches 資料列集, 以便顯示新增的資料和移除如果驅動程式和資料指標支援這些作業, 就會刪除該資料。<br /><br /> 使用**SQLSetPos**成功重新整理不會變更資料列狀態 SQL_ROW_DELETED。 在下一次提取之前, 資料列集內已刪除的資料列將會繼續標示為已刪除。 如果資料指標支援封裝 (其中後續的**SQLFetch**或**SQLFetchScroll**不會傳回已刪除的資料列), 則資料列將會在下一次提取時消失。<br /><br /> 當執行具有**SQLSetPos**的重新整理時, 不會顯示已加入的資料列。 此行為不同于**SQLFetchScroll** , *FetchType*為 SQL_FETCH_RELATIVE, 而*RowNumber*等於 0, 這也會重新整理目前的資料列集, 但如果這些作業為, 則會顯示已新增的記錄或套件刪除的記錄。資料指標支援。<br /><br /> 使用**SQLSetPos**成功重新整理會將資料列狀態從 SQL_ROW_ADDED 變更為 SQL_ROW_SUCCESS (如果資料列狀態陣列存在)。<br /><br /> 使用**SQLSetPos**成功重新整理會將 SQL_ROW_UPDATED 的資料列狀態變更為資料列的新狀態 (如果資料列狀態陣列存在的話)。<br /><br /> 如果資料列的**SQLSetPos**作業發生錯誤, 資料列狀態會設定為 SQL_ROW_ERROR (如果資料列狀態陣列存在)。<br /><br /> 對於以 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES 的 SQL_ATTR_CONCURRENCY 語句屬性開啟的資料指標, 使用**SQLSetPos**的重新整理可能會更新資料來源所使用的開放式並行值, 以偵測資料列已變更。 如果發生這種情況, 則每當從伺服器重新整理資料列集緩衝區時, 就會更新用來確保資料指標平行存取的資料列版本。 重新整理的每個資料列都會發生這種情況。<br /><br /> SQL_REFRESH 作業會忽略 SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向之資料列狀態陣列的內容。 |  
|SQL_UPDATE|驅動程式會將游標放在*RowNumber*所指定的資料列上, 並使用資料列集緩衝區中的值 ( **SQLBindCol**中的*TargetValuePtr*引數) 來更新資料的基礎資料列。 它會從長度/指標緩衝區 ( **SQLBindCol**中的*StrLen_or_IndPtr*引數) 抓取資料的長度。 如果 SQL_COLUMN_IGNORE 任何資料行的長度, 則不會更新資料行。 更新資料列之後, 驅動程式會將資料列狀態陣列的對應元素變更為 SQL_ROW_UPDATED 或 SQL_ROW_SUCCESS_WITH_INFO (如果資料列狀態陣列存在的話)。<br /><br /> 如果在包含重復資料行的資料指標上呼叫具有 SQL_UPDATE 之*Operation*引數的**SQLSetPos** , 則此為驅動程式定義的行為。 驅動程式可能會傳回驅動程式定義的 SQLSTATE、可以更新結果集中出現的第一個資料行, 或執行其他驅動程式定義的行為。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向的資料列作業陣列, 可以用來表示在大量更新期間應該忽略目前資料列集內的資料列。 如需詳細資訊, 請參閱本函數參考後面的「狀態和作業陣列」。|  
|SQL_DELETE|驅動程式會將游標放在*RowNumber*所指定的資料列上, 並刪除基礎資料列。 它會將資料列狀態陣列的對應元素變更為 SQL_ROW_DELETED。 在刪除資料列之後, 下列資料列無效: 定位 update 和 delete 語句、呼叫**SQLGetData**, 以及呼叫**SQLSetPos**並將作業設定為 SQL_POSITION 以外的  任何專案。 對於支援封裝的驅動程式, 當從資料來源抓取新資料時, 會從資料指標中刪除資料列。<br /><br /> 資料列是否維持可見, 取決於資料指標類型。 例如, 靜態和索引鍵集導向的資料指標可以看到已刪除的資料列, 但動態資料指標看不到。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向的資料列作業陣列, 可以用來表示在大量刪除期間, 應該忽略目前資料列集內的資料列。 如需詳細資訊, 請參閱本函數參考後面的「狀態和作業陣列」。|  
  
## <a name="locktype-argument"></a>LockType 引數  
 *LockType*引數提供應用程式控制並行的方式。 在大部分情況下, 支援並行層級和交易的資料來源只會支援*LockType*引數的 SQL_LOCK_NO_CHANGE 值。 *LockType*引數通常僅用於以檔案為基礎的支援。  
  
 *LockType*引數會指定在執行**SQLSetPos**之後, 資料列的鎖定狀態。 如果驅動程式無法鎖定資料列來執行要求的作業, 或要滿足*LockType*引數, 它會傳回 SQL_ERROR 和 SQLSTATE 42000 (語法錯誤或存取違規)。  
  
 雖然已針對單一語句指定*LockType*引數, 但鎖定會 accords 連接上所有語句的相同許可權。 特別是, 在連接上的一個語句所取得的鎖定, 可以由相同連接上的不同語句解除鎖定。  
  
 透過**SQLSetPos**鎖定的資料列會保持鎖定, 直到應用程式針對*LOCKTYPE*設定為 SQL_LOCK_UNLOCK 的資料列呼叫**SQLSetPos** , 或直到應用程式呼叫語句或 SQLFreeHandle 的**SQLFreeStmt**為止  使用 SQL_CLOSE 選項。 對於支援交易的驅動程式, 當應用程式呼叫**SQLEndTran**來認可或回復連接上的交易時 (如果資料指標在認可或回復交易時已關閉, 則會解除鎖定通過**SQLSetPos**的資料列)。如**SQLGetInfo**所傳回的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊類型所指示)。  
  
 *LockType*引數支援下列類型的鎖定。 若要判斷資料來源支援哪些鎖定, 應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 呼叫**SQLGetInfo**資訊類型 (視游標的類型而定)。  
  
|*LockType*引數|鎖定類型|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|驅動程式或資料來源會確保資料列與呼叫**SQLSetPos**之前的鎖定或解除鎖定狀態相同。 這個*LockType*值可讓不支援明確資料列層級鎖定的資料來源使用目前平行存取和交易隔離等級所需的任何鎖定。|  
|SQL_LOCK_EXCLUSIVE|驅動程式或資料來源會以獨佔方式鎖定資料列。 不同連接或不同應用程式中的語句不能用來取得資料列的任何鎖定。|  
|SQL_LOCK_UNLOCK|驅動程式或資料來源會解除鎖定資料列。|  
  
 如果驅動程式支援 SQL_LOCK_EXCLUSIVE, 但不支援 SQL_LOCK_UNLOCK, 則已鎖定的資料列將會保持鎖定, 直到上一個段落中所述的其中一個函式呼叫發生為止。  
  
 如果驅動程式支援 SQL_LOCK_EXCLUSIVE, 但不支援 SQL_LOCK_UNLOCK, 則已鎖定的資料列會保持鎖定, 直到應用程式使用 SQL_CLOSE 選項呼叫語句或**SQLFreeStmt**的**SQLFreeHandle**為止。 如果驅動程式支援交易, 並在認可或回復交易時關閉資料指標, 應用程式會呼叫**SQLEndTran**。  
  
 針對**SQLSetPos**中的更新和刪除作業, 應用程式會使用*LockType*引數, 如下所示:  
  
-   若要保證資料列在抓取之後不會變更, 應用程式會呼叫**SQLSetPos**並將*OPERATION*設定為 SQL_REFRESH, 並將*LockType*設定為 SQL_LOCK_EXCLUSIVE。  
  
-   如果應用程式將*LockType*設定為 SQL_LOCK_NO_CHANGE, 則只有在應用程式指定了 SQL_ATTR_CONCURRENCY 語句屬性的 SQL_CONCUR_LOCK 時, 驅動程式才會保證更新或刪除作業才會成功。  
  
-   如果應用程式針對 SQL_ATTR_CONCURRENCY 語句屬性指定 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES, 則此驅動程式會比較資料列版本或值, 並在應用程式提取資料列之後, 變更資料列時拒絕作業。  
  
-   如果應用程式為 SQL_ATTR_CONCURRENCY 語句屬性指定 SQL_CONCUR_READ_ONLY, 驅動程式會拒絕任何更新或刪除作業。  
  
 如需 SQL_ATTR_CONCURRENCY 語句屬性的詳細資訊, 請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="status-and-operation-arrays"></a>狀態和運算元組  
 呼叫**SQLSetPos**時, 會使用下列狀態和作業陣列:  
  
-   資料列狀態陣列 (由 IRD 和 SQL_ATTR_ROW_STATUS_ARRAY 語句屬性中的 SQL_DESC_ARRAY_STATUS_PTR 欄位所指向) 包含資料列集中每個資料列的狀態值。 驅動程式會在呼叫**SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations**或**SQLSetPos**之後, 設定此陣列中的狀態值。 SQL_ATTR_ROW_STATUS_PTR 語句屬性會指向這個陣列。  
  
-   資料列作業陣列 (由 ARD 和 SQL_ATTR_ROW_OPERATION_ARRAY 語句屬性中的 SQL_DESC_ARRAY_STATUS_PTR 欄位所指向) 包含資料列集中每一個資料列的值, 指出是否有大量作業的**SQLSetPos**呼叫會忽略或執行。 陣列中的每個元素都會設定為 SQL_ROW_PROCEED (預設值) 或 SQL_ROW_IGNORE。 SQL_ATTR_ROW_OPERATION_PTR 語句屬性會指向這個陣列。  
  
 「狀態」和「作業」陣列中的元素數目必須等於資料列集中的資料列數目 (如 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性所定義)。  
  
 如需資料列狀態陣列的詳細資訊, 請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。 如需資料列作業陣列的詳細資訊, 請參閱本節稍後的「忽略大量作業中的資料列」。  
  
## <a name="using-sqlsetpos"></a>使用 SQLSetPos  
 在應用程式呼叫**SQLSetPos**之前, 它必須執行下列步驟順序:  
  
1.  如果應用程式會呼叫**SQLSetPos**並將*OPERATION*設定為 SQL_UPDATE, 請針對每個資料行呼叫**SQLBindCol** (或**SQLSetDescRec**), 以指定其資料類型, 以及系結資料行的資料和長度的緩衝區。  
  
2.  如果應用程式會呼叫**SQLSetPos** , 並將*OPERATION*設定為 SQL_DELETE 或 SQL_UPDATE, 請呼叫**SQLColAttribute**以確保要刪除或更新的資料行是可更新的。  
  
3.  呼叫**SQLExecDirect**、 **SQLExecute**或 catalog 函數來建立結果集。  
  
4.  呼叫**SQLFetch**或**SQLFetchScroll**以取得資料。  
  
 如需使用**SQLSetPos**的詳細資訊, 請參閱使用[SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
## <a name="deleting-data-using-sqlsetpos"></a>使用 SQLSetPos 刪除資料  
 若要使用**SQLSetPos**刪除資料, 應用程式會呼叫**SQLSetPos**並將*RowNumber*設定為要刪除的資料列  數目, 並將作業設定為 SQL_DELETE。  
  
 刪除資料之後, 驅動程式會將 [執行列狀態] 陣列中的值變更為要 SQL_ROW_DELETED 的適當資料列 (或 SQL_ROW_ERROR)。  
  
## <a name="updating-data-using-sqlsetpos"></a>使用 SQLSetPos 更新資料  
 應用程式可以在系結的資料緩衝區中, 或對**SQLPutData**的一或多個呼叫, 傳遞資料行的值。 資料會以**SQLPutData**傳遞的資料行稱為「*資料執行中」資料* *行*。 這些通常用來傳送 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 資料行的資料, 而且可以與其他資料行混合使用。  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>若要使用 SQLSetPos (應用程式) 更新資料:  
  
1.  將值放入與**SQLBindCol**系結的資料和長度/指標緩衝區中:  
  
    -   針對一般資料行, 應用程式 *\** 會將新的資料行值放在 *\*TargetValuePtr*緩衝區, 並將該值的長度置於 StrLen_or_IndPtr 緩衝區中。 如果資料列不應更新, 應用程式會將 SQL_ROW_IGNORE 放置在資料列作業陣列的該資料列元素中。  
  
    -   針對資料執行中的資料行, 應用程式會在 *\*TargetValuePtr*緩衝區中放置應用程式定義的值, 例如欄號。 稍後可以使用此值來識別資料行。  
  
         應用程式會將 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果放在 **StrLen_or_IndPtr*緩衝區中。 如果資料行的 SQL 資料類型為 SQL_LONGVARBINARY、SQL_LONGVARCHAR 或 long 資料來源特定的資料類型, 而驅動程式針對**SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型傳回 "Y", *length*就是要在其中寫入的位元組數目。針對參數傳送;否則, 它必須是非負值的值, 而且會被忽略。  
  
2.  呼叫**SQLSetPos**並將*Operation*引數設定為 SQL_UPDATE, 以更新資料列。  
  
    -   如果沒有執行中的資料行, 則程式已完成。  
  
    -   如果有任何執行中的資料行, 此函式會傳回 SQL_NEED_DATA 並繼續進行步驟3。  
  
3.  呼叫**SQLParamData** , 以取得要處理之第一個資料執行中資料行的 *\*TargetValuePtr*緩衝區位址。 **SQLParamData**會傳回 SQL_NEED_DATA。 應用程式會從 *\*TargetValuePtr*緩衝區捕獲應用程式定義的值。  
  
    > [!NOTE]  
    >  雖然資料執行中的參數與資料執行中的資料行類似, 但每個**SQLParamData**所傳回的值都不同。  
  
    > [!NOTE]  
    >  資料執行中參數是 SQL 語句中的參數, 當使用**SQLExecDirect**或**SQLExecute**執行語句時, 資料會與**SQLPutData**一起傳送。 它們會與**SQLBindParameter**系結, 或藉由使用**SQLSetDescRec**來設定描述元。 **SQLParamData**傳回的值是在*ParameterValuePtr*引數中傳遞至**SQLBindParameter**的32位值。  
  
    > [!NOTE]  
    >  資料執行中的資料行是資料列集中的資料行, 會在使用**SQLSetPos**更新資料列時, 使用**SQLPutData**來傳送資料。 它們會與**SQLBindCol**系結。 **SQLParamData**傳回的值是要處理之 **TargetValuePtr*緩衝區中資料列的位址。  
  
4.  會呼叫**SQLPutData**一次或多次來傳送資料行的資料。 如果無法在**SQLPutData**中指定的 *\*TargetValuePtr*緩衝區內傳回所有資料值, 則需要多個呼叫; 只有在傳送字元 C 資料時, 才允許多次呼叫同一資料行的**SQLPutData**包含字元、二進位或資料來源特定資料類型, 或將二進位 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行。  
  
5.  再次呼叫**SQLParamData** , 表示資料行已傳送所有資料。  
  
    -   如果有更多資料執行中的資料行, **SQLParamData**會傳回 SQL_NEED_DATA 和*TargetValuePtr*緩衝區的位址, 以用於下一個要處理的資料執行中資料行。 應用程式會重複步驟4和5。  
  
    -   如果沒有其他資料執行中的資料行, 則程式已完成。 如果語句執行成功, **SQLParamData**會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO;如果執行失敗, 則會傳回 SQL_ERROR。 此時, **SQLParamData**可以傳回**SQLSetPos**所能傳回的任何 SQLSTATE。  
  
 如果資料已更新, 驅動程式會將「執行列狀態」陣列中的值變更為要 SQL_ROW_UPDATED 的適當資料列。  
  
 如果作業已取消或在**SQLParamData**或**SQLPutData**中發生錯誤, 則在**SQLSetPos**傳回 SQL_NEED_DATA 之後, 以及在傳送所有資料執行中資料行的資料之前, 應用程式只能呼叫**SQLCancel**, **SQLGetDiagField**、 **SQLGetDiagRec**、 **SQLGetFunctions**、 **SQLParamData**或**SQLPutData** (適用于語句) 或與語句相關聯的連接。 如果它針對語句或與語句相關聯的連接呼叫任何其他函式, 此函式會傳回 SQL_ERROR 和 SQLSTATE HY010 (函數序列錯誤)。  
  
 如果應用程式在驅動程式仍然需要資料執行中資料行的資料時呼叫**SQLCancel** , 驅動程式會取消作業。 然後, 應用程式就可以再次呼叫**SQLSetPos** ;取消不會影響資料指標狀態或目前的資料指標位置。  
  
 當與資料指標相關聯的查詢規格的選取清單包含相同資料行的多個參考時, 是否產生錯誤, 或驅動程式忽略重複的參考, 並執行所要求的作業是驅動程式定義的。  
  
## <a name="performing-bulk-operations"></a>執行大量作業  
 如果*RowNumber*引數為 0, 驅動程式會針對資料列集中的  每個資料列, 在其欄位的 SQL_ROW_PROCEED 中, 針對資料列集內的每個資料列執行作業引數中指定的作業, SQL_ATTR_ROW_OPERATION_PTR語句屬性。 這是 SQL_DELETE、SQL_REFRESH 或 SQL_UPDATE 之*Operation*引數的*RowNumber*引數有效值, 但不是 SQL_POSITION。 具有 SQL_POSITION 作業  的**SQLSetPos**和等於0的*RowNumber*會傳回 SQLSTATE HY109 (不正確資料指標位置)。  
  
 如果發生與整個資料列集相關的錯誤, 例如 SQLSTATE HYT00 (超時時間已過期), 驅動程式會傳回 SQL_ERROR 和適當的 SQLSTATE。 資料列集緩衝區的內容未定義, 且資料指標位置不變。  
  
 如果發生與單一資料列相關的錯誤, 驅動程式:  
  
-   在 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的資料列狀態陣列中, 將資料列的元素設定為 SQL_ROW_ERROR。  
  
-   在錯誤佇列中張貼錯誤的一個或多個額外 SQLSTATEs, 並在診斷資料結構中設定 SQL_DIAG_ROW_NUMBER 欄位。  
  
 在處理錯誤或警告之後, 如果驅動程式針對資料列集的其餘資料列完成作業, 它會傳回 SQL_SUCCESS_WITH_INFO。 因此, 對於每個傳回錯誤的資料列, 錯誤佇列會包含零個或多個額外的 SQLSTATEs。 如果驅動程式在處理錯誤或警告之後停止作業, 它會傳回 SQL_ERROR。  
  
 如果驅動程式傳回任何警告, 例如 SQLSTATE 01004 (資料已截斷), 它會在傳回適用于特定資料列的錯誤資訊之前, 傳回套用至整個資料列集的警告, 或傳回給資料列集內的未知資料列。 它會傳回特定資料列的警告, 以及與這些資料列相關的任何其他錯誤資訊。  
  
 如果*RowNumber*等於 0, 而*Operation*為 SQL_UPDATE、SQL_REFRESH 或 SQL_DELETE, 則 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性會指向**SQLSetPos**操作所在的資料列數目。  
  
 如果*RowNumber*等於 0, 而*operation*是 SQL_DELETE、SQL_REFRESH 或 SQL_UPDATE, 則作業之後的目前資料列會與作業之前的目前資料列相同。  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>忽略大量作業中的資料列  
 「資料列作業」陣列可以用來表示在使用**SQLSetPos**進行大量作業期間, 應該忽略目前資料列集中的資料列。 若要指示驅動程式在大量作業期間忽略一或多個資料列, 應用程式應該執行下列步驟:  
  
1.  呼叫**SQLSetStmtAttr** , 將 SQL_ATTR_ROW_OPERATION_PTR 語句屬性設定為指向 SQLUSMALLINTs 的陣列。 藉由呼叫**SQLSetDescField**來設定 ARD 的 SQL_DESC_ARRAY_STATUS_PTR 標頭欄位 (需要應用程式取得描述項控制碼), 也可以設定此欄位。  
  
2.  將資料列作業陣列的每個元素設定為兩個值的其中一個:  
  
    -   SQL_ROW_IGNORE, 表示已排除大量作業的資料列。  
  
    -   SQL_ROW_PROCEED, 表示資料列包含在大量作業中。 (這是預設值)。  
  
3.  呼叫**SQLSetPos**來執行大量作業。  
  
 下列規則適用于資料列作業陣列:  
  
-   SQL_ROW_IGNORE 和 SQL_ROW_PROCEED 只會影響使用**SQLSetPos**與 SQL_DELETE 或  SQL_UPDATE 的大量作業。 它們不會影響**SQLSetPos**的呼叫與 SQL_REFRESH  或 SQL_POSITION 的作業。  
  
-   根據預設, 指標會設定為 null。  
  
-   如果指標是 null, 則所有的資料列都會更新, 如同所有元素都已設定為 SQL_ROW_PROCEED。  
  
-   將元素設定為 SQL_ROW_PROCEED, 並不保證會在該特定資料列上執行作業。 例如, 如果資料列集中的某個資料列具有狀態 SQL_ROW_ERROR, 不論應用程式是否指定 SQL_ROW_PROCEED, 驅動程式都可能無法更新該資料列。 應用程式必須一律檢查資料列狀態陣列, 以查看作業是否成功。  
  
-   SQL_ROW_PROCEED 在標頭檔中定義為0。 應用程式可以將資料列作業陣列初始化為 0, 以便處理所有的資料列。  
  
-   如果資料列作業陣列中的元素編號 "n" 設定為 SQL_ROW_IGNORE, 而呼叫**SQLSetPos**來執行大量更新或刪除作業, 則在呼叫**SQLSetPos**之後, 資料列集中的第 n 個數據列會維持不變。  
  
-   應用程式應該會自動將唯讀資料行設定為 SQL_ROW_IGNORE。  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>忽略大量作業中的資料行  
 若要避免嘗試更新為一或多個唯讀資料行所產生的不必要處理診斷, 應用程式可以將系結長度/指標緩衝區中的值設定為 SQL_COLUMN_IGNORE。 如需詳細資訊, 請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中, 應用程式可讓使用者流覽 ORDERS 資料表並更新訂單狀態。 資料指標是資料列集大小為20的索引鍵集驅動, 並使用開放式並行存取控制來比較資料列版本。 提取每個資料列集之後, 應用程式會列印它, 並允許使用者選取和更新訂單的狀態。 應用程式會使用**SQLSetPos**將游標放在選取的資料列上, 並執行資料列的定點更新。 (為了清楚起見, 會省略錯誤處理)。  
  
```cpp  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 如需更多範例, 請參閱[定位 Update 和 Delete 語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)和[使用 SQLSetPos 更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行與區塊資料指標位置無關的大量作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得描述項的單一欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得描述項的多個欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定描述項的單一欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定描述項的多個欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
