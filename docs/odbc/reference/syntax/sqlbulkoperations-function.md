---
description: SQLBulkOperations 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e065bc06150c3b12e469489c4d115d02c2142f14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421292"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 函式
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ODBC  
  
 **總結**  
 **SQLBulkOperations** 會執行大量插入和大量書簽作業，包括依書簽更新、刪除和提取。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *運算*  
 輸出要執行的作業：  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 如需詳細資訊，請參閱「批註」。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBulkOperations**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLBulkOperations** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
 對於可以傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR (（除了 01xxx SQLSTATEs) 以外）的所有 SQLSTATEs，如果一或多個（但不是全部）多資料列作業的資料列發生錯誤，則會傳回 SQL_SUCCESS_WITH_INFO，如果單一資料列作業發生錯誤，則會傳回 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料右截斷|SQL_FETCH_BY_BOOKMARK *作業引數* ，以及為資料類型為 SQL_C_CHAR 或 SQL_C_BINARY 的資料行或資料行傳回字串或二進位資料，而導致截斷非空白字元或非 Null 的二進位資料。|  
|01S01|資料列發生錯誤|SQL_ADD *作業引數* ，而且在執行此作業時，一或多個資料列中發生錯誤，但至少有一個資料列已成功加入。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) <br /><br />  (只有當應用程式正在使用 ODBC 2 時，才會引發此錯誤。*x* 驅動程式。 ) |  
|01S07|小數截斷|作業 *引數是 SQL_FETCH_BY_BOOKMARK* ，未 SQL_C_CHAR 或 SQL_C_BINARY 應用程式緩衝區的資料類型，且已截斷針對一或多個資料行傳回給應用程式緩衝區的資料。 數位 C 資料類型的 (，數位的小數部分會被截斷。 如果是包含時間元件的時間、時間戳記和間隔 C 資料類型，時間的小數部分會被截斷。 ) <br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07006|限制的資料類型屬性違規|SQL_FETCH_BY_BOOKMARK*作業引數*，而且結果集中資料行的資料值無法轉換成呼叫**SQLBindCol**時， *TargetType*引數所指定的資料類型。<br /><br /> 作業 *引數是 SQL_UPDATE_BY_BOOKMARK* 或 SQL_ADD，而且應用程式緩衝區中的資料值無法轉換成結果集中資料行的資料類型。|  
|07009|描述元索引無效|*引數*作業已 SQL_ADD，且資料行的資料行編號大於結果集中的資料行數目。|  
|21S02|衍生資料表的程度與資料行清單不相符|*引數*作業已 SQL_UPDATE_BY_BOOKMARK;而且沒有任何資料行是可更新的，因為所有資料行都是未系結或唯讀，或已 SQL_COLUMN_IGNORE 系結長度/指標緩衝區中的值。|  
|22001|字串資料右截斷|將字元或二進位值指派給結果集內的資料行，會導致截斷非 null 的 (字元) 或二進位) 字元或位元組的非 null (。|  
|22003|數值超出範圍|SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK *作業引數* ，並將數值指派給結果集中的資料行，會導致整個 (與要截斷之數位) 部分的分數相反。<br /><br /> *引數*作業已 SQL_FETCH_BY_BOOKMARK，且傳回一或多個系結資料行的數值，會導致有效位數遺失。|  
|22007|不正確日期時間格式|SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK *作業引數* ，並將日期或時間戳記值指派給結果集中的資料行，導致 year、month 或 day 欄位超出範圍。<br /><br /> *引數*作業已 SQL_FETCH_BY_BOOKMARK，且傳回一或多個系結資料行的日期或時間戳記值會導致 year、month 或 day 欄位超出範圍。|  
|22008|日期/時間欄位溢位|作業 *引數* 是 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，而將資料傳送至結果集中資料行的日期時間算術的效能，會產生 datetime 欄位， (結果落在欄位的允許值範圍之外，或是根據西曆的日期時間自然規則而不正確日期時間欄位) 的結果。<br /><br /> 作業 *引數是* SQL_FETCH_BY_BOOKMARK，而從結果集抓取之資料的日期時間算術效能，會產生 datetime 欄位 (該欄位在允許的欄位值範圍之外的年份、月份、日、小時、分鐘或第二個欄位) ，或根據西曆的日期時間自然規則而無效。|  
|22015|間隔欄位溢位|作業 *引數是 SQL_ADD* 或 SQL_UPDATE_BY_BOOKMARK，而且將精確數值或間隔 C 類型指派給間隔 SQL 資料類型，導致遺失有效位數。<br /><br /> *Operation*引數是 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK;指派至間隔 SQL 類型時，不會在間隔 SQL 類型中表示 C 類型的值。<br /><br /> SQL_FETCH_BY_BOOKMARK 作業 *引數，* 並從精確數值或間隔 SQL 類型指派至間隔 C 類型，而導致前置欄位中的有效位數遺失。<br /><br /> 作業 *引數是 SQL_FETCH_BY_BOOKMARK* ;當指派給間隔 C 類型時，不會在間隔 C 類型中表示 SQL 類型的值。|  
|22018|轉換規格的字元值無效|作業 *引數是 SQL_FETCH_BY_BOOKMARK* ;C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;且資料行中的值不是系結 C 類型的有效常值。<br /><br /> *引數*作業是 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK;SQL 類型是精確或近似的數值、日期時間或間隔資料類型;C 類型為 SQL_C_CHAR;且資料行中的值不是系結 SQL 類型的有效常值。|  
|23000|完整性條件約束違規|作業 *引數為 SQL_ADD* 、SQL_DELETE_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK，但違反了完整性條件約束。<br /><br /> SQL_ADD *作業引數* ，而且未系結的資料行定義為 not Null，且沒有預設值。<br /><br /> 作業 *引數* 是 SQL_ADD，在系結 *StrLen_or_IndPtr* 緩衝區中指定的長度是 SQL_COLUMN_IGNORE 的，而且資料行沒有預設值。|  
|24000|指標狀態無效|*StatementHandle*處於執行中狀態，但沒有與*StatementHandle*相關聯的結果集。|  
|40001|序列化失敗|交易已復原，因為另一個交易發生資源鎖死。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|42000|語法錯誤或存取違規|驅動程式無法視需要鎖定資料列，以執行 *操作* 引數中所要求的作業。|  
|44000|WITH CHECK OPTION 違規|SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK *作業引數* ，並且在已查看的 (資料表上執行 insert 或 UPDATE，或是藉由指定 **WITH CHECK OPTION**所建立的資料表) 衍生自已查看資料表，如此一來，就不會再有一或多個受插入或更新影響的資料列會出現在已查看的資料表中。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 呼叫函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在 *StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLBulkOperations** 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 指定的 *StatementHandle* 未處於執行中狀態。 在未先呼叫 **SQLExecDirect**、 **SQLExecute**或 catalog 函數的情況下呼叫函式。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLSetPos** () DM，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) 驅動程式是 ODBC 2。在呼叫**SQLFetchScroll**或**SQLFetch**之前，會針對*StatementHandle*呼叫*x*驅動程式和**SQLBulkOperations** 。<br /><br /> 在*StatementHandle*上呼叫**SQLExtendedFetch**之後，會呼叫 (DM) **SQLBulkOperations** 。|  
|HY011|無法立即設定屬性| (DM) 驅動程式是 ODBC 2。*x* 驅動程式和 SQL_ATTR_ROW_STATUS_PTR 語句屬性是在呼叫 **SQLFetch** 或 **SQLFetchScroll** 和 **SQLBulkOperations**之間設定。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度|*Operation*引數是 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK;資料值不是 null 指標;C 資料類型 SQL_C_BINARY 或 SQL_C_CHAR;且資料行長度值小於0，但不等於 SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS 或 SQL_Null_DATA，或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 長度/指標緩衝區中的值為 SQL_DATA_AT_EXEC;SQL 類型可能是 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定的資料類型;而 **SQLGetInfo** 中的 SQL_NEED_LONG_DATA_LEN 資訊類型為 "Y"。<br /><br /> 作業 *引數* 已 SQL_ADD、SQL_ATTR_USE_BOOKMARK 語句屬性設定為 SQL_UB_VARIABLE，且資料行0系結至長度不等於此結果集之書簽長度上限的緩衝區。  (此長度可在 IRD 的 [SQL_DESC_OCTET_LENGTH] 欄位中取得，而且可以藉由呼叫 **SQLDescribeCol**、 **SQLColAttribute**或 **SQLGetDescField**來取得。 ) |  
|HY092|不正確屬性識別碼| (DM) 為 *操作* 引數指定的值無效。<br /><br /> 作業 *引數是 SQL_ADD* 、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，且 SQL_ATTR_CONCURRENCY 語句屬性已設定為 SQL_CONCUR_READ_ONLY。<br /><br /> 作業 *引數為 SQL_DELETE_BY_BOOKMARK* 、SQL_FETCH_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK，且書簽資料行未系結或 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_OFF。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|驅動程式或資料來源不支援 *操作* 引數中所要求的作業。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回結果集之前過期。 使用 SQL_ATTR_QUERY_TIMEOUT 的*屬性*引數，透過**SQLSetStmtAttr**設定超時時間。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
  
> [!CAUTION]  
>  如需可在其中呼叫哪些語句狀態 **SQLBulkOperations** 的相關資訊，以及它必須如何針對 ODBC 2 進行相容性的資訊。*x* 應用程式的詳細說明，請參閱附錄 G：驅動程式指導方針中的 [區塊資料指標、可滾動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 一節。  
  
 應用程式會使用 **SQLBulkOperations** ，在與目前查詢對應的基表或視圖上執行下列作業：  
  
-   加入新的資料列。  
  
-   更新一組資料列，其中每個資料列都是由書簽識別。  
  
-   刪除一組資料列，其中每個資料列都是由書簽識別。  
  
-   提取一組資料列，其中每個資料列都是由書簽識別。  
  
 呼叫 **SQLBulkOperations**之後，區塊資料指標位置是未定義的。 應用程式必須呼叫 **SQLFetchScroll** 來設定資料指標的位置。 應用程式只能使用 SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE 或 SQL_FETCH_BOOKMARK 的*FetchOrientation*引數來呼叫**SQLFetchScroll** 。 如果應用程式使用 SQL_FETCH_PRIOR、SQL_FETCH_NEXT 或 SQL_FETCH_RELATIVE 的*FetchOrientation*引數來呼叫**SQLFetch**或**SQLFetchScroll** ，則資料指標位置是未定義的。  
  
 藉由將對**SQLBindCol**的呼叫所指定的資料行長度/指標緩衝區設定為 SQL_COLUMN_IGNORE，可以在呼叫**SQLBulkOperations**所執行的大量作業中略過資料行。  
  
 應用程式不需要在呼叫 **SQLBulkOperations** 時設定 SQL_ATTR_ROW_OPERATION_PTR 語句屬性，因為使用此函數執行大量作業時，無法忽略資料列。  
  
 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性所指向的緩衝區包含受 **SQLBulkOperations**呼叫影響的資料列數目。  
  
 當 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK *作業引數* ，而且與資料指標相關聯之查詢規格的選取清單包含相同資料行的多個參考時，就會定義驅動程式是否產生錯誤，或是驅動程式是否忽略重複的參考並執行要求的作業。  
  
 如需如何使用 **SQLBulkOperations**的詳細資訊，請參閱 [使用 SQLBulkOperations 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。  
  
## <a name="performing-bulk-inserts"></a>執行大量插入  
 若要使用 **SQLBulkOperations**插入資料，應用程式會執行下列一連串的步驟：  
  
1.  執行傳回結果集的查詢。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為想要插入的資料列數目。  
  
3.  呼叫 **SQLBindCol** 來系結它想要插入的資料。 資料會系結至大小等於 SQL_ATTR_ROW_ARRAY_SIZE 值的陣列。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的陣列大小應等於 SQL_ATTR_ROW_ARRAY_SIZE，或 SQL_ATTR_ROW_STATUS_PTR 應該是 null 指標。  
  
4.  呼叫 **SQLBulkOperations** (*StatementHandle，* SQL_ADD) 來執行插入。  
  
5.  如果應用程式已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性，它可以檢查這個陣列以查看作業的結果。  
  
 如果應用程式在使用*SQL_ADD 的作業引數*呼叫**SQLBulkOperations**之前系結資料行0，驅動程式將會使用新插入之資料列的書簽值來更新系結資料行0緩衝區。 若要進行這種情況，應用程式必須在執行語句之前，先將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。  (這無法與 ODBC 2 搭配使用。*x* 驅動程式。 )   
  
 您可以使用 SQLParamData 和 SQLPutData 的呼叫，以 SQLBulkOperations 的方式將長資料新增至元件。 如需詳細資訊，請參閱此函數參考稍後的「提供大量插入和更新的長資料」。  
  
 應用程式不需要在呼叫 **SQLFetch** 或 **SQLFetchScroll** 之前呼叫 **SQLBULKOPERATIONS** (，除非對 ODBC 2 進行。*x* 驅動程式;請參閱回溯 [相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)) 。  
  
 如果 **SQLBulkOperations**（具有 *SQL_ADD 的作業引數* ）在包含重復資料行的資料指標上呼叫，則此行為為驅動程式定義。 驅動程式可以傳回驅動程式定義的 SQLSTATE、將資料新增至出現在結果集中的第一個資料行，或執行其他驅動程式定義的行為。  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>使用書簽執行大量更新  
 若要使用書簽搭配 **SQLBulkOperations**來執行大量更新，應用程式會依序執行下列步驟：  
  
1.  將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。  
  
2.  執行傳回結果集的查詢。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為想要更新的資料列數目。  
  
4.  呼叫 **SQLBindCol** 來系結它想要更新的資料。 資料會系結至大小等於 SQL_ATTR_ROW_ARRAY_SIZE 值的陣列。 它也會呼叫 **SQLBindCol** 來系結資料行 0 (書簽資料行) 。  
  
5.  將感興趣更新之資料列的書簽複製到系結至資料行0的陣列。  
  
6.  更新系結緩衝區中的資料。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的陣列大小應等於 SQL_ATTR_ROW_ARRAY_SIZE，或 SQL_ATTR_ROW_STATUS_PTR 應該是 null 指標。  
  
7.  呼叫 **SQLBulkOperations** (*StatementHandle、* SQL_UPDATE_BY_BOOKMARK) 。  
  
    > [!NOTE]  
    >  如果應用程式已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性，它可以檢查這個陣列以查看作業的結果。  
  
8.  選擇性地呼叫 **SQLBulkOperations** (*StatementHandle*，SQL_FETCH_BY_BOOKMARK) 將資料提取到系結的應用程式緩衝區，以確認是否發生更新。  
  
9. 如果資料已更新，驅動程式會將資料列狀態陣列中的值變更為要 SQL_ROW_UPDATED 的適當資料列。  
  
 **SQLBulkOperations**所執行的大量更新可以使用**SQLParamData**和**SQLPutData**的呼叫來包含長資料。 如需詳細資訊，請參閱此函數參考稍後的「提供大量插入和更新的長資料」。  
  
 如果書簽跨資料指標保存，則應用程式不需要在依書簽更新之前呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 它可以使用從上一個資料指標儲存的書簽。 如果書簽不會跨資料指標保存，則應用程式必須呼叫 **SQLFetch** 或 **SQLFetchScroll** 來取得書簽。  
  
 如果 **SQLBulkOperations**（具有 *SQL_UPDATE_BY_BOOKMARK 的作業引數* ）在包含重復資料行的資料指標上呼叫，則此行為為驅動程式定義。 驅動程式可以傳回驅動程式定義的 SQLSTATE、更新結果集中出現的第一個資料行，或執行其他驅動程式定義的行為。  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>使用書簽執行大量提取  
 若要使用書簽搭配 **SQLBulkOperations**來執行大量提取，應用程式會依序執行下列步驟：  
  
1.  將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。  
  
2.  執行傳回結果集的查詢。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為它想要提取的資料列數目。  
  
4.  呼叫 **SQLBindCol** 來系結它想要提取的資料。 資料會系結至大小等於 SQL_ATTR_ROW_ARRAY_SIZE 值的陣列。 它也會呼叫 **SQLBindCol** 來系結資料行 0 (書簽資料行) 。  
  
5.  將感興趣提取的資料列的書簽複製到系結至資料行0的陣列中。  (這會假設應用程式已分別取得書簽。 )   
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的陣列大小應等於 SQL_ATTR_ROW_ARRAY_SIZE，或 SQL_ATTR_ROW_STATUS_PTR 應該是 null 指標。  
  
6.  呼叫 **SQLBulkOperations** (*StatementHandle、* SQL_FETCH_BY_BOOKMARK) 。  
  
7.  如果應用程式已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性，它可以檢查這個陣列以查看作業的結果。  
  
 如果書簽跨資料指標保存，則應用程式不需要在依書簽提取之前呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 它可以使用從上一個資料指標儲存的書簽。 如果書簽不會跨資料指標保存，則應用程式必須呼叫 **SQLFetch** 或 **SQLFetchScroll** 一次，才能取得書簽。  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>使用書簽執行大量刪除  
 若要使用書簽搭配 **SQLBulkOperations**來執行大量刪除，應用程式會依序執行下列步驟：  
  
1.  將 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_VARIABLE。  
  
2.  執行傳回結果集的查詢。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為想要刪除的資料列數目。  
  
4.  呼叫 **SQLBindCol** 來系結資料行 0 (書簽資料行) 。  
  
5.  將有興趣刪除之資料列的書簽複製到系結至資料行0的陣列。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向的陣列大小應等於 SQL_ATTR_ROW_ARRAY_SIZE，或 SQL_ATTR_ROW_STATUS_PTR 應該是 null 指標。  
  
6.  呼叫 **SQLBulkOperations** (*StatementHandle、* SQL_DELETE_BY_BOOKMARK) 。  
  
7.  如果應用程式已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性，它可以檢查這個陣列以查看作業的結果。  
  
 如果書簽跨資料指標保存，則在刪除書簽之前，應用程式不需要呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 它可以使用從上一個資料指標儲存的書簽。 如果書簽不會跨資料指標保存，則應用程式必須呼叫 **SQLFetch** 或 **SQLFetchScroll** 一次，才能取得書簽。  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>提供大量插入和更新的長資料  
 您可以針對 **SQLBulkOperations**呼叫所執行的大量插入和更新，提供完整的資料。 若要插入或更新較長的資料，應用程式除了本主題稍早的「執行大量插入」和「使用書簽執行大量更新」一節中所述的步驟之外，還會執行下列步驟。  
  
1.  當它使用**SQLBindCol**系結資料時，應用程式會將應用程式定義的值（例如資料行編號）放在資料執行中資料行的* \* TargetValuePtr*緩衝區中。 此值稍後可以用來識別資料行。  
  
     應用程式會將 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果放在* \* StrLen_or_IndPtr*緩衝區中。 如果資料行的 SQL 資料類型為 SQL_LONGVARBINARY、SQL_LONGVARCHAR 或 long 資料來源特定的資料類型，且驅動程式會在 **SQLGetInfo**中傳回 SQL_NEED_LONG_DATA_LEN 資訊類型的 "Y"，則 *length* 是要為參數傳送的資料位元組數;否則，它必須是非負值，而且會被忽略。  
  
2.  當呼叫 **SQLBulkOperations** 時，如果有資料執行中資料行，此函式會傳回 SQL_NEED_DATA 並繼續進行步驟3，如下所示。  (如果沒有任何資料執行中資料行，程式就會完成。 )   
  
3.  應用程式會呼叫**SQLParamData** ，以針對要處理的第一個資料執行中資料行，取得* \* TargetValuePtr*緩衝區的位址。 **SQLParamData** 會傳回 SQL_NEED_DATA。 應用程式會從* \* TargetValuePtr*緩衝區取出應用程式定義的值。  
  
    > [!NOTE]  
    >  雖然資料執行中的參數與資料執行中資料行類似，但每個資料行的 **SQLParamData** 所傳回的值都不同。  
  
     資料執行中資料行是資料列集中的資料行，當資料列已更新或使用**SQLBulkOperations**插入時，資料將會以**SQLPutData**傳送。 它們會與 **SQLBindCol**系結。 **SQLParamData**傳回的值是要處理之 **TargetValuePtr*緩衝區中資料列的位址。  
  
4.  應用程式會呼叫 **SQLPutData** 一次或多次，以傳送資料行的資料。 如果在**SQLPutData**中指定的* \* TargetValuePtr*緩衝區中無法傳回所有資料值，則需要一個以上的呼叫; 只有在將字元 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行，或將二進位 c 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行時，才允許多個對相同資料行的**SQLPutData**呼叫。  
  
5.  應用程式會再次呼叫 **SQLParamData** ，以指示資料行的所有資料都已傳送。  
  
    -   如果有多個資料執行中資料行， **SQLParamData** 會傳回要處理之下一個資料執行中資料行的 SQL_NEED_DATA 以及 *TargetValuePtr* 緩衝區的位址。 應用程式會重複步驟4和5。  
  
    -   如果沒有其他資料執行中資料行，程式就會完成。 如果語句執行成功， **SQLParamData** 會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO;如果執行失敗，則會傳回 SQL_ERROR。 此時， **SQLParamData** 可以傳回 **SQLBulkOperations**可傳回的任何 SQLSTATE。  
  
 如果作業已取消，或在 **SQLParamData** 或 **SQLPutData** 中發生錯誤，則 **SQLBulkOperations** 會傳回 SQL_NEED_DATA，且在傳送所有資料執行中資料行的資料之前，應用程式只能針對語句或與語句相關聯的連接呼叫 **SQLCancel**、 **SQLGetDiagField**、 **SQLGetDiagRec**、 **SQLGetFunctions**、 **SQLParamData**或 **SQLPutData** 。 如果它針對語句或與語句相關聯的連接呼叫任何其他函式，此函式會傳回 SQL_ERROR，且 SQLSTATE HY010 (函數順序錯誤) 。  
  
 如果應用程式在驅動程式仍需要資料執行中資料行的資料時呼叫 **SQLCancel** ，驅動程式就會取消作業。 然後，應用程式可以再次呼叫 **SQLBulkOperations** ;取消不會影響資料指標狀態或目前的資料指標位置。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 資料列狀態陣列包含呼叫 **SQLBulkOperations**之後，資料列集中每個資料列的狀態值。 驅動程式會在呼叫 **SQLFetch**、 **SQLFetchScroll**、 **SQLSetPos**或 **SQLBulkOperations**之後，設定此陣列中的狀態值。 如果未在**SQLBulkOperations**之前呼叫**SQLFetch**或**SQLFetchScroll** ，此陣列一開始會填入**SQLBulkOperations**的呼叫。 這個陣列是由 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向。 資料列狀態陣列中的元素數目必須等於資料列集 (中的資料列數目，如 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性) 所定義。 如需此資料列狀態陣列的詳細資訊，請參閱 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 下列範例會從 Customers 資料表一次提取10個數據列。 然後，它會提示使用者採取動作。 若要減少網路流量，範例緩衝區會在系結陣列中的本機更新、刪除和插入，但在超過資料列集資料的位移。 當使用者選擇傳送更新、刪除和插入資料來源時，此程式碼會適當地設定系結位移並呼叫 **SQLBulkOperations**。 為了簡單起見，使用者無法緩衝超過10個更新、刪除或插入。  
  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得描述項的單一欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得描述項的多個欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定描述項的單一欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定描述項的多個欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|定位資料指標、重新整理資料列集內的資料，或更新或刪除資料列集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
