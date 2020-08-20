---
description: SQLSetPos 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55741fba1dca898e087f4a992dfd7affbf3bcfcb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491228"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **總結**  
 **SQLSetPos** 會將資料指標位置設定為數據列集，並允許應用程式重新整理資料列集內的資料，或更新或刪除結果集中的資料。  
  
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
 輸出語句控制碼。  
  
 *RowNumber*  
 輸出要執行 *作業引數所指定* 之作業的資料列集中的資料列位置。 如果 *RowNumber* 是0，則作業會套用至資料列集內的每個資料列。  
  
 如需詳細資訊，請參閱「批註」。  
  
 *運算*  
 輸出要執行的作業：  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  ODBC 3.x 的*Operation*引數 SQL_ADD 值已被*取代。* ODBC *3.x* 驅動程式必須支援 SQL_ADD，以提供回溯相容性。 這項功能已由*SQL_ADD 的作業*所呼叫的**SQLBulkOperations**取代。 當 ODBC 3.x*應用程式**與 odbc 2.x*驅動程式搭配使用時，驅動程式管理員會將 SQLBulkOperations 的呼叫對應至具有 SQL_ADD*作業的 SQL_ADD* **SQLBulkOperations**作業，**以進行**的*操作*。  
  
 如需詳細資訊，請參閱「批註」。  
  
 *LockType*  
 輸出指定在執行 *operation* 引數中指定的作業之後，如何鎖定資料列。  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 如需詳細資訊，請參閱「批註」。  
  
## <a name="returns"></a>傳回  
  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetPos**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLSetPos** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
 對於可以傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR (（除了 01xxx SQLSTATEs) 以外）的所有 SQLSTATEs，如果一或多個（但不是全部）多資料列作業的資料列發生錯誤，則會傳回 SQL_SUCCESS_WITH_INFO，如果單一資料列作業發生錯誤，則會傳回 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01001|資料指標操作衝突|作業 *引數* SQL_DELETE 或 SQL_UPDATE，而且沒有刪除或更新一個或多個資料列。  (如需多個資料列更新的詳細資訊，請參閱**SQLSetStmtAttr**中 SQL_ATTR_SIMULATE_CURSOR*屬性*的描述。 )  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) <br /><br /> 作業 *引數是 SQL_DELETE* 或 SQL_UPDATE，因此作業失敗，因為開放式平行存取。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料右截斷|SQL_REFRESH *作業引數* ，以及為資料類型為 SQL_C_CHAR 或 SQL_C_BINARY 的資料行或資料行傳回字串或二進位資料，而導致截斷非空白字元或非 Null 的二進位資料。|  
|01S01|資料列發生錯誤|*RowNumber*引數為0，而且在執行以*operation*引數指定的作業時，一或多個資料列中發生錯誤。<br /><br /> 如果一或多個（但不是全部）多資料列作業的資料列發生錯誤，則會傳回 (SQL_SUCCESS_WITH_INFO，而且如果單一資料列作業發生錯誤，則會傳回 SQL_ERROR。 ) <br /><br />  (只有在**SQLExtendedFetch**之後呼叫**SQLSetPos**時，如果*驅動程式是 ODBC 2.x*驅動程式，且未使用資料指標程式庫，則會傳回此 SQLSTATE。 ) |  
|01S07|小數截斷|作業 *引數是 SQL_REFRESH* ，未 SQL_C_CHAR 或 SQL_C_BINARY 應用程式緩衝區的資料類型，且已截斷針對一或多個資料行傳回給應用程式緩衝區的資料。 若為數值資料類型，則會截斷數位的小數部分。 若是時間、時間戳記和包含時間元件的間隔資料類型，時間的小數部分會被截斷。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07006|限制的資料類型屬性違規|在**SQLBindCol**的呼叫中，無法將結果集內資料行的資料值轉換成*TargetType*所指定的資料類型。|  
|07009|描述元索引無效|*引數*作業是 SQL_REFRESH 或 SQL_UPDATE，而且資料行的資料行編號大於結果集中的資料行數目。|  
|21S02|衍生資料表的程度與資料行清單不相符|*引數*作業已 SQL_UPDATE，且沒有可更新的資料行，因為所有資料行都是未系結、唯讀，或已 SQL_COLUMN_IGNORE 系結長度/指標緩衝區中的值。|  
|22001|字串資料，右截斷|SQL_UPDATE *作業引數* ，並將字元或二進位值的指派指派給資料行，而導致在二進位) 字元或位元組中截斷非 null (的字元) 或非 null (。|  
|22003|數值超出範圍|SQL_UPDATE 自 *變數* 作業，並將數值指派給結果集中的資料行，會導致整個 (，而不是數位的小數) 部分會被截斷。<br /><br /> *引數*作業已 SQL_REFRESH，且傳回一或多個系結資料行的數值，會導致有效位數遺失。|  
|22007|不正確日期時間格式|*引數*作業已 SQL_UPDATE，並將日期或時間戳記值指派給結果集中的資料行，導致 year、month 或 day 欄位超出範圍。<br /><br /> *引數*作業已 SQL_REFRESH，且傳回一或多個系結資料行的日期或時間戳記值會導致 year、month 或 day 欄位超出範圍。|  
|22008|日期/時間欄位溢位|SQL_UPDATE *作業引數* ，而且在結果集中傳送給資料行之資料的日期時間算術效能，會產生 datetime 欄位，)  (結果超出欄位的允許值範圍，或是根據西曆的日期時間自然規則而不正確日期時間欄位，則為不正確日期時間欄位。<br /><br /> 作業 *引數是 SQL_REFRESH 的，* 而從結果集抓取之資料的日期時間算術效能，會產生 datetime 欄位， (結果超出欄位的允許值範圍，或根據西曆的日期時間自然規則而不正確日期時間欄位) 的日期時間欄位，或其無效。|  
|22015|間隔欄位溢位|作業 *引數是 SQL_UPDATE* ，且將精確數值或間隔 C 類型指派給間隔 SQL 資料類型，導致遺失有效位數。<br /><br /> 作業 *引數是 SQL_UPDATE* ;指派至間隔 SQL 類型時，不會在間隔 SQL 類型中表示 C 類型的值。<br /><br /> SQL_REFRESH 作業 *引數，* 並從精確數值或間隔 SQL 類型指派至間隔 C 類型，而導致前置欄位中的有效位數遺失。<br /><br /> 作業引數 SQL_ 重新 *整理* ;當指派給間隔 C 類型時，不會在間隔 C 類型中表示 SQL 類型的值。|  
|22018|轉換規格的字元值無效|作業 *引數是 SQL_REFRESH* ;C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;且資料行中的值不是系結 C 類型的有效常值。<br /><br /> *引數*作業已 SQL_UPDATE;SQL 類型是精確或近似的數值、日期時間或間隔資料類型;C 類型為 SQL_C_CHAR;且資料行中的值不是系結 SQL 類型的有效常值。|  
|23000|完整性條件約束違規|*引數*作業是 SQL_DELETE 或 SQL_UPDATE，而且違反了完整性條件約束。|  
|24000|指標狀態無效|*StatementHandle*處於執行中狀態，但沒有與*StatementHandle*相關聯的結果集。<br /><br />  (DM) 在 *StatementHandle*上開啟資料指標，但尚未呼叫 **SQLFetch** 或 **SQLFetchScroll** 。<br /><br /> 資料指標已在 *StatementHandle*上開啟，而且已呼叫 **SQLFetch** 或 **SQLFetchScroll** ，但資料指標位於結果集的開頭或結果集結尾之後。<br /><br /> *引數*作業為 SQL_DELETE、SQL_REFRESH 或 SQL_UPDATE，且資料指標位於結果集的開頭或結果集結尾之後。|  
|40001|序列化失敗|因為另一個交易發生資源鎖死，所以已回復交易。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|42000|語法錯誤或存取違規|驅動程式無法視需要鎖定資料列，以 *執行引數*作業所要求的作業。<br /><br /> 驅動程式無法在引數 *LockType*中鎖定要求的資料列。|  
|44000|WITH CHECK OPTION 違規|已 SQL_UPDATE *作業引數* ，並且在已查看的資料表或衍生自所查看資料表（藉由指定 **WITH CHECK OPTION**所建立）的資料表上執行更新，如此一來，受更新影響的一或多個資料列就不會再出現在已查看的資料表中。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 已呼叫函式，並在它完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** ，然後在*StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 SQLSetPos 函式時，仍在執行此非同步函式。<br /><br />  (DM) 指定的 *StatementHandle* 未處於執行中狀態。 在未先呼叫 **SQLExecDirect**、 **SQLExecute**或 catalog 函數的情況下呼叫函式。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) *驅動程式是 ODBC 2.x*驅動程式，而在呼叫**SQLFetch**之後，會呼叫**SQLSetPos**來進行*StatementHandle* 。|  
|HY011|無法立即設定屬性| (DM) *驅動程式是 ODBC 2.x*驅動程式;已設定 SQL_ATTR_ROW_STATUS_PTR 語句屬性;然後在呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLExtendedFetch**之前呼叫**SQLSetPos** 。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度|作業 *引數* 是 SQL_UPDATE、資料值為 null 指標，且資料行長度值不是0、SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_Null_DATA 或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 作業 *引數是 SQL_UPDATE* ;資料值不是 null 指標;C 資料類型 SQL_C_BINARY 或 SQL_C_CHAR;且資料行長度值小於0，但不等於 SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS 或 SQL_Null_DATA，或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 長度/指標緩衝區中的值為 SQL_DATA_AT_EXEC;SQL 類型可能是 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定的資料類型;而 **SQLGetInfo** 中的 SQL_NEED_LONG_DATA_LEN 資訊類型為 "Y"。|  
|HY092|不正確屬性識別碼| (DM) 為 *操作* 引數指定的值無效。<br /><br />  (DM) 為 *LockType* 引數指定的值無效。<br /><br /> 作業 *引數是 SQL_UPDATE* 或 SQL_DELETE，而且 SQL_ATTR_CONCURRENCY 語句屬性 SQL_ATTR_CONCUR_READ_ONLY。|  
|HY107|資料列值超出範圍|為引數 *RowNumber* 指定的值大於資料列集中的資料列數目。|  
|HY109|不正確資料指標位置|與 *StatementHandle* 相關聯的資料指標已定義為順向，因此資料指標無法放在資料列集內。 請參閱 **SQLSetStmtAttr**中的 SQL_ATTR_CURSOR_TYPE 屬性的描述。<br /><br /> 作業 *引數為 SQL_UPDATE* 、SQL_DELETE 或 SQL_REFRESH，且 *RowNumber* 引數所識別的資料列已被刪除或尚未提取。<br /><br />  (DM) *RowNumber* 引數為0，且作業 *引數* 是 SQL_POSITION。<br /><br /> 呼叫**SQLBulkOperations**之後，以及在呼叫**SQLFetchScroll**或**SQLFetch**之前，會呼叫**SQLSetPos** 。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|驅動程式或資料來源不支援在 *operation* 引數或 *LockType* 引數中要求的作業。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回結果集之前過期。 您可以使用 SQL_ATTR_QUERY_TIMEOUT 的*屬性*，透過**SQLSetStmtAttr**設定超時時間。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
  
> [!CAUTION]
>  如需語句的詳細資訊，請參閱 **SQLSetPos** 可以在中呼叫，以及它需要如何 *針對 ODBC 2.x* 應用程式進行相容性的資訊，請參閱 [區塊資料指標、可滾動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
## <a name="rownumber-argument"></a>RowNumber 引數  
 *RowNumber*引數會指定資料列集中要執行*作業引數所指定*之作業的資料列編號。 如果 *RowNumber* 是0，則作業會套用至資料列集內的每個資料列。 *RowNumber* 必須是從0到資料列集中的資料列數目的值。  
  
> [!NOTE]  
>  在 C 語言中，陣列是以0為基礎，而 *RowNumber* 引數是以1為基礎。 例如，若要更新資料列集的第五個數據列，應用程式會修改陣列索引4的資料列集緩衝區，但會指定5的 *RowNumber* 。  
  
 所有作業都會將資料指標放在 *RowNumber*指定的資料列上。 下列作業需要資料指標位置：  
  
-   定位的 update 和 delete 語句。  
  
-   呼叫 **SQLGetData**。  
  
-   使用 SQL_DELETE、SQL_REFRESH 和 SQL_UPDATE 選項來呼叫 **SQLSetPos** 。  
  
 例如，如果使用*SQL_DELETE 的作業*呼叫**SQLSetPos**的*RowNumber*為2，則資料指標位於資料列集的第二個數據列，而且該資料列會被刪除。 在第二個數據列中，第二個數據列的 [執行資料列狀態陣列] (所) SQL_ATTR_ROW_STATUS_PTR 指向的專案會變更為 SQL_ROW_DELETED。  
  
 當應用程式呼叫 **SQLSetPos**時，可以指定資料指標的位置。 一般而言，它會使用 SQL_POSITION 或 SQL_REFRESH 作業來呼叫 **SQLSetPos** ，以便在執行定位的 update 或 delete 語句或呼叫 **SQLGetData**之前放置游標。  
  
## <a name="operation-argument"></a>Operation 引數  
 *Operation*引數支援下列作業。 為了判斷資料來源所支援的選項，應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊類型來呼叫 **SQLGetInfo** ，視資料指標 (的類型而定) 。  
  
|*運算*<br /><br /> 引數|作業|  
|------------------------------|---------------|  
|SQL_POSITION|驅動程式會將游標置於 *RowNumber*指定的資料列上。<br /><br /> *SQL_POSITION 作業*會忽略 SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向的資料列狀態陣列內容。|  
|SQL_REFRESH|驅動程式會將游標置於 *RowNumber* 指定的資料列，並在該資料列的資料列集緩衝區中重新整理資料。 如需有關驅動程式如何傳回資料列集緩衝區中資料的詳細資訊，請參閱 **SQLBindCol**中的資料列和資料行取向的描述。<br /><br /> **SQLSetPos** 具有 SQL_REFRESH *的作業* 會更新目前所提取資料列集內資料列的狀態和內容。 這包括重新整理書簽。 因為緩衝區中的資料會重新整理，但無法根據，所以資料列集中的成員資格是固定的。 這與 **SQLFetchScroll** 的呼叫所執行的重新整理不同，其 *FetchOrientation* 為 SQL_FETCH_RELATIVE，而 *RowNumber* 等於0，則會從結果集中 refetches 資料列集，以便在驅動程式和資料指標支援這些作業時，顯示所加入的資料並移除已刪除的資料。<br /><br /> 成功重新整理 with **SQLSetPos** 不會變更 SQL_ROW_DELETED 的資料列狀態。 資料列集內已刪除的資料列將會在下一次提取之前，繼續標示為已刪除。 如果資料指標支援封裝 (（後續 **SQLFetch** 或 **SQLFetchScroll** 不會傳回已刪除的資料) 列），則資料列將會在下一次提取時消失。<br /><br /> 當執行重新整理 with **SQLSetPos** 時，不會顯示新增的資料列。 此行為不同于 **SQLFetchScroll** 與 *FetchType* 的 SQL_FETCH_RELATIVE，而 *RowNumber* 等於0，這也會重新整理目前的資料列集，但如果資料指標支援這些作業，則會顯示新增的記錄或封裝刪除的記錄。<br /><br /> 如果資料列狀態陣列存在) ，則使用 **SQLSetPos** 的成功重新整理會將 SQL_ROW_ADDED 的資料列狀態變更為 SQL_ROW_SUCCESS (。<br /><br /> 成功重新整理 with **SQLSetPos** 會將資料列狀態 SQL_ROW_UPDATED 變更為資料列的新狀態 (如果資料列狀態陣列存在) 。<br /><br /> 如果資料列的 **SQLSetPos** 作業發生錯誤，資料列狀態會設定為 SQL_ROW_ERROR (如果資料列狀態陣列存在) 。<br /><br /> 針對使用 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES 的 SQL_ATTR_CONCURRENCY 語句屬性開啟的資料指標， **SQLSetPos** 的 refresh 可能會更新資料來源所使用的開放式平行存取值，以偵測資料列已變更。 如果發生這種情況，就會在從伺服器重新整理資料列集緩衝區時，更新用來確保資料指標並行的資料列版本。 重新整理的每個資料列都會發生這種情況。<br /><br /> *SQL_REFRESH 作業*會忽略 SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向的資料列狀態陣列內容。|  
|SQL_UPDATE|驅動程式會將游標置於*RowNumber*指定的資料列，並以資料列集緩衝區中的值更新資料的基礎資料列， (**SQLBindCol**) 中的*TargetValuePtr*引數。 它會從**SQLBindCol**) 中的*StrLen_or_IndPtr*引數 (長度/指標緩衝區中取出資料的長度。 如果 SQL_COLUMN_IGNORE 任何資料行的長度，則不會更新資料行。 更新資料列之後，如果資料列狀態陣列存在) ，驅動程式就會將資料列狀態陣列的對應元素變更為 SQL_ROW_UPDATED 或 SQL_ROW_SUCCESS_WITH_INFO (。<br /><br /> 如果 **SQLSetPos** *的作業引數* 是在包含重復資料行的資料指標上呼叫 SQL_UPDATE 的作業引數，則為驅動程式定義的行為。 驅動程式可以傳回驅動程式定義的 SQLSTATE、可以更新結果集中出現的第一個資料行，或執行其他驅動程式定義的行為。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向的資料列作業陣列可以用來表示在大量更新期間應忽略目前資料列集中的資料列。 如需詳細資訊，請參閱此函數參考中稍後的「狀態和作業陣列」。|  
|SQL_DELETE|驅動程式會將游標置於 *RowNumber* 指定的資料列，並刪除基礎資料列。 它會將資料列狀態陣列的對應元素變更為 SQL_ROW_DELETED。 在刪除資料列之後，下列資料列對資料列無效：定位 update 和 delete 語句、呼叫**SQLGetData**，以及將作業設定為除了 SQL_POSITION 以外*的作業*的**SQLSetPos**呼叫。 針對支援封裝的驅動程式，從資料來源取出新資料時，會從資料指標中刪除資料列。<br /><br /> 資料列是否仍會顯示，視資料指標類型而定。 例如，靜態和索引鍵集驅動資料指標可看到已刪除的資料列，但動態資料指標看不到這些資料列。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向的資料列作業陣列可以用來表示在大量刪除期間應忽略目前資料列集中的資料列。 如需詳細資訊，請參閱此函數參考中稍後的「狀態和作業陣列」。|  
  
## <a name="locktype-argument"></a>LockType 引數  
 *LockType*引數提供應用程式控制平行存取的方法。 在大多數情況下，支援平行存取層級和交易的資料來源只會支援 *LockType* 引數的 SQL_LOCK_NO_CHANGE 值。 *LockType*引數通常僅用於以檔案為基礎的支援。  
  
 *LockType*引數會指定在執行**SQLSetPos**之後，資料列的鎖定狀態。 如果驅動程式無法鎖定資料列來執行要求的作業，或是要滿足 *LockType* 引數，則會傳回 SQL_ERROR 和 SQLSTATE 42000 (語法錯誤或存取違規) 。  
  
 雖然已針對單一語句指定 *LockType* 引數，但鎖定會 accords 與連接上所有語句相同的許可權。 尤其是，在連接上由一個語句所取得的鎖定，可以透過相同連接上的不同語句來解除鎖定。  
  
 透過**SQLSetPos**鎖定的資料列會保持鎖定，直到應用程式針對*LockType*設定為 SQL_LOCK_UNLOCK 的資料列呼叫**SQLSetPos** ，或直到應用程式使用 SQL_CLOSE 選項來呼叫語句或**SQLFreeStmt**的**SQLFreeHandle**為止。 **若為**支援交易的驅動程式，在認可或回復交易時，透過**SQLSetPos**鎖定的資料列就會解除鎖定， (如果在認可或回復交易時關閉資料指標，則是由**SQLGetInfo**) 所傳回的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊類型所表示。  
  
 *LockType*引數支援下列類型的鎖定。 為了判斷資料來源所支援的鎖定，應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊類型來呼叫 **SQLGetInfo** ，視資料指標 (的類型而定) 。  
  
|*LockType* 引數|鎖定類型|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|驅動程式或資料來源可確保資料列的鎖定或解除鎖定狀態，與呼叫 **SQLSetPos** 之前相同。 此 *LockType* 的值可讓不支援明確資料列層級鎖定的資料來源使用目前的平行存取和交易隔離等級所需的任何鎖定。|  
|SQL_LOCK_EXCLUSIVE|驅動程式或資料來源會以獨佔方式鎖定資料列。 不同連接或不同應用程式中的語句不能用來取得資料列的任何鎖定。|  
|SQL_LOCK_UNLOCK|驅動程式或資料來源會解除鎖定資料列。|  
  
 如果驅動程式支援 SQL_LOCK_EXCLUSIVE 但不支援 SQL_LOCK_UNLOCK，則鎖定的資料列將會維持鎖定狀態，直到上一個段落所述的其中一個函式呼叫發生為止。  
  
 如果驅動程式支援 SQL_LOCK_EXCLUSIVE 但不支援 SQL_LOCK_UNLOCK，則鎖定的資料列會保持鎖定，直到應用程式使用 SQL_CLOSE 選項來呼叫語句或**SQLFreeStmt**的**SQLFreeHandle**為止。 如果驅動程式支援交易，並在認可或回復交易時關閉資料指標，則應用程式會呼叫 **SQLEndTran**。  
  
 針對 **SQLSetPos**中的更新和刪除作業，應用程式會使用 *LockType* 引數，如下所示：  
  
-   為了保證在抓取資料列之後，資料列不會變更，應用程式會呼叫 **SQLSetPos** ，並將 *Operation* 設定為 SQL_REFRESH，並將 *LockType* 設定為 SQL_LOCK_EXCLUSIVE。  
  
-   如果應用程式將 *LockType* 設定為 SQL_LOCK_NO_CHANGE，則驅動程式會保證只有當應用程式針對 SQL_ATTR_CONCURRENCY 語句屬性指定 SQL_CONCUR_LOCK 時，更新或刪除作業才會成功。  
  
-   如果應用程式為 SQL_ATTR_CONCURRENCY 語句屬性指定 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，驅動程式會比較資料列版本或值，並在應用程式提取資料列之後變更資料列時拒絕作業。  
  
-   如果應用程式指定 SQL_ATTR_CONCURRENCY 語句屬性 SQL_CONCUR_READ_ONLY，驅動程式就會拒絕任何 update 或 delete 作業。  
  
 如需 SQL_ATTR_CONCURRENCY 語句屬性的詳細資訊，請參閱 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="status-and-operation-arrays"></a>狀態和運算元組  
 呼叫 **SQLSetPos**時，會使用下列狀態和運算元組：  
  
-   資料列狀態陣列 (由 IRD 中的 SQL_DESC_ARRAY_STATUS_PTR 欄位所指向，而 SQL_ATTR_ROW_STATUS_ARRAY 語句屬性) 包含資料列集中每個資料列的狀態值。 驅動程式會在呼叫 **SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations**或 **SQLSetPos**之後，設定此陣列中的狀態值。 這個陣列是由 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向。  
  
-   資料列作業陣列 (由 ARD 中的 SQL_DESC_ARRAY_STATUS_PTR 欄位所指向，而 SQL_ATTR_ROW_OPERATION_ARRAY 語句屬性) 包含資料列集中每個資料列的值，指出是否忽略或執行大量作業的 **SQLSetPos** 呼叫。 陣列中的每個元素都會設定為 SQL_ROW_PROCEED (預設) 或 SQL_ROW_IGNORE。 這個陣列是由 SQL_ATTR_ROW_OPERATION_PTR 語句屬性所指向。  
  
 Status 和 operation 陣列中的元素數目必須等於資料列集中的資料列數目 (如 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性) 所定義。  
  
 如需資料列狀態陣列的詳細資訊，請參閱 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。 如需有關資料列作業陣列的詳細資訊，請參閱本節稍後的「忽略大量作業中的資料列」。  
  
## <a name="using-sqlsetpos"></a>使用 SQLSetPos  
 在應用程式呼叫 **SQLSetPos**之前，它必須執行下列一連串的步驟：  
  
1.  如果應用程式會呼叫 **SQLSetPos** ，並將 *Operation* 設定為 SQL_UPDATE，請針對每個資料行呼叫 **SQLBindCol** (或 **SQLSetDescRec**) ，以指定其資料類型，並將資料行的資料和長度系結到緩衝區。  
  
2.  如果應用程式將*作業設定為*SQL_DELETE 或 SQL_UPDATE 來呼叫**SQLSetPos** ，請呼叫**SQLColAttribute**以確定要刪除或更新的資料行是可更新的。  
  
3.  呼叫 **SQLExecDirect**、 **SQLExecute**或類別目錄函數，以建立結果集。  
  
4.  呼叫 **SQLFetch** 或 **SQLFetchScroll** 來取出資料。  
  
 如需使用 **SQLSetPos**的詳細資訊，請參閱 [使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
## <a name="deleting-data-using-sqlsetpos"></a>使用 SQLSetPos 刪除資料  
 若要使用 **SQLSetPos**刪除資料，應用程式會呼叫 **SQLSetPos** ，並將 *RowNumber* 設定為要刪除的資料列數目 *，並將* 作業設定為 SQL_DELETE。  
  
 刪除資料之後，驅動程式會將適當資料列的 [執行資料列狀態] 陣列中的值變更為 SQL_ROW_DELETED (或 SQL_ROW_ERROR) 。  
  
## <a name="updating-data-using-sqlsetpos"></a>使用 SQLSetPos 更新資料  
 應用程式可以傳遞系結資料緩衝區中的資料行值，或使用一或多個 **SQLPutData**呼叫。 以**SQLPutData**傳遞資料的資料行稱為「*資料執行中資料**行*」。 這些通常用來傳送 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 資料行的資料，而且可以與其他資料行混合使用。  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>若要使用 SQLSetPos （應用程式）更新資料：  
  
1.  將資料和長度/指標緩衝區中的值放在與 **SQLBindCol**系結的位置：  
  
    -   若為一般資料行，應用程式會將新的資料行值放在* \* TargetValuePtr*緩衝區，並將該值的長度放在* \* StrLen_or_IndPtr*緩衝區中。 如果不應該更新資料列，應用程式就會將 SQL_ROW_IGNORE 放在資料列作業陣列的該資料列元素中。  
  
    -   針對資料執行中資料行，應用程式會在* \* TargetValuePtr*緩衝區中放置應用程式定義的值，例如資料行編號。 此值稍後可以用來識別資料行。  
  
         應用程式會將 SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果放在 **StrLen_or_IndPtr* 緩衝區中。 如果資料行的 SQL 資料類型為 SQL_LONGVARBINARY、SQL_LONGVARCHAR 或 long 資料來源特定的資料類型，且驅動程式會在 **SQLGetInfo**中傳回 SQL_NEED_LONG_DATA_LEN 資訊類型的 "Y"，則 *length* 是要為參數傳送的資料位元組數;否則，它必須是非負值，而且會被忽略。  
  
2.  呼叫 **SQLSetPos** ，並將 *Operation* 引數設定為 SQL_UPDATE 來更新資料列。  
  
    -   如果沒有執行中的資料行，則程式已完成。  
  
    -   如果有任何資料執行中資料行，此函數會傳回 SQL_NEED_DATA 並繼續進行步驟3。  
  
3.  呼叫**SQLParamData** ，以針對要處理的第一個資料執行中資料行，取得* \* TargetValuePtr*緩衝區的位址。 **SQLParamData** 會傳回 SQL_NEED_DATA。 應用程式會從* \* TargetValuePtr*緩衝區取出應用程式定義的值。  
  
    > [!NOTE]  
    >  雖然資料執行中的參數與資料執行中資料行類似，但每個資料行所傳回的 **SQLParamData** 值都不同。  
  
    > [!NOTE]  
    >  資料執行中參數是 SQL 語句中的參數，當使用**SQLExecDirect**或**SQLExecute**來執行語句時，資料會以**SQLPutData**傳送。 它們會與 **SQLBindParameter** 系結，或藉由設定 **SQLSetDescRec**的描述項來系結。 **SQLParamData**傳回的值是在*ParameterValuePtr*引數中傳遞給**SQLBindParameter**的32位值。  
  
    > [!NOTE]  
    >  資料執行中資料行是資料列集中的資料行，當資料列更新為**SQLSetPos**時，資料將會與**SQLPutData**一起傳送。 它們會與 **SQLBindCol**系結。 **SQLParamData**傳回的值是要處理之 **TargetValuePtr*緩衝區中資料列的位址。  
  
4.  呼叫 **SQLPutData** 一次或多次，以傳送資料行的資料。 如果在**SQLPutData**中指定的* \* TargetValuePtr*緩衝區中無法傳回所有資料值，則需要一個以上的呼叫; 只有在將字元 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行，或將二進位 c 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行時，才允許多個對相同資料行的**SQLPutData**呼叫。  
  
5.  再次呼叫 **SQLParamData** ，以指示資料行的所有資料都已傳送。  
  
    -   如果有多個資料執行中資料行， **SQLParamData** 會傳回要處理之下一個資料執行中資料行的 SQL_NEED_DATA 以及 *TargetValuePtr* 緩衝區的位址。 應用程式會重複步驟4和5。  
  
    -   如果沒有其他資料執行中資料行，程式就會完成。 如果語句執行成功， **SQLParamData** 會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO;如果執行失敗，則會傳回 SQL_ERROR。 此時， **SQLParamData** 可以傳回 **SQLSetPos**可傳回的任何 SQLSTATE。  
  
 如果資料已更新，驅動程式會將適當資料列的 [執行資料列狀態] 陣列中的值變更為 SQL_ROW_UPDATED。  
  
 如果作業已取消，或在 **SQLParamData** 或 **SQLPutData**中發生錯誤，則在 **SQLSetPos** 傳回 SQL_NEED_DATA，且在傳送所有資料執行中資料行的資料之前，應用程式只能針對語句或與語句相關聯的連接呼叫 **SQLCancel**、 **SQLGetDiagField**、 **SQLGetDiagRec**、 **SQLGetFunctions**、 **SQLParamData**或 **SQLPutData** 。 如果它針對語句或與語句相關聯的連接呼叫任何其他函式，此函式會傳回 SQL_ERROR，且 SQLSTATE HY010 (函數順序錯誤) 。  
  
 如果應用程式在驅動程式仍需要資料執行中資料行的資料時呼叫 **SQLCancel** ，驅動程式就會取消作業。 然後，應用程式可以再次呼叫 **SQLSetPos** ;取消不會影響資料指標狀態或目前的資料指標位置。  
  
 當與資料指標相關聯之查詢規格的選取清單包含相同資料行的多個參考時，是否產生錯誤，或驅動程式忽略重複的參考，並執行所要求的作業為驅動程式定義。  
  
## <a name="performing-bulk-operations"></a>執行大量作業  
 如果 *RowNumber* 引數為0，則驅動程式會針對資料列集中的每個資料列，在資料列集內的每個資料列中，針對資料 SQL_ATTR_ROW_OPERATION_PTR 列 SQL_ROW_PROCEED 集內的每個資料列執行 *作業引數* 中所指定的作業 這是 SQL_DELETE、SQL_REFRESH 或*SQL_UPDATE 的作業引數*之*RowNumber*引數的有效值，但不是 SQL_POSITION 的值。 **SQLSetPos** *操作* SQL_POSITION，且 *RowNumber* 等於0將會傳回 SQLSTATE HY109 (不正確資料指標位置) 。  
  
 如果發生與整個資料列集相關的錯誤，例如 SQLSTATE HYT00 (Timeout 過期) ，驅動程式會傳回 SQL_ERROR 和適當的 SQLSTATE。 資料列集緩衝區的內容是未定義的，而且資料指標的位置不會改變。  
  
 如果發生與單一資料列相關的錯誤，驅動程式：  
  
-   針對 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指向之資料列狀態陣列中的資料列，設定要 SQL_ROW_ERROR 的元素。  
  
-   針對錯誤佇列中的錯誤張貼一或多個額外的 SQLSTATEs，並設定診斷資料結構中的 SQL_DIAG_ROW_NUMBER 欄位。  
  
 在處理錯誤或警告之後，如果驅動程式完成資料列集中其餘資料列的作業，則會傳回 SQL_SUCCESS_WITH_INFO。 因此，針對每個傳回錯誤的資料列，錯誤佇列會包含零個或更多的其他 SQLSTATEs。 如果驅動程式在處理錯誤或警告之後停止操作，就會傳回 SQL_ERROR。  
  
 如果驅動程式傳回任何警告，例如 SQLSTATE 01004 (資料被截斷) ，它會傳回套用至整個資料列集或資料列集中未知資料列的警告，然後再傳回適用于特定資料列的錯誤資訊。 它會傳回特定資料列的警告，以及有關這些資料列的任何其他錯誤資訊。  
  
 如果 *RowNumber* 等於 0 *，而且作業* 是 SQL_UPDATE、SQL_REFRESH 或 SQL_DELETE，則 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性會指向 **SQLSetPos** 操作的資料列數目。  
  
 如果 *RowNumber* 等於0，而且 *運算* 是 SQL_DELETE、SQL_REFRESH 或 SQL_UPDATE，則作業之後的目前資料列與作業之前的目前資料列相同。  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>忽略大量作業中的資料列  
 資料列作業陣列可以用來表示在使用 **SQLSetPos**的大量作業期間，應該忽略目前資料列集中的資料列。 若要在大量作業期間指示驅動程式忽略一或多個資料列，應用程式應該執行下列步驟：  
  
1.  呼叫 **SQLSetStmtAttr** ，將 SQL_ATTR_ROW_OPERATION_PTR 語句屬性設定為指向 SQLUSMALLINTs 的陣列。 您也可以呼叫 **SQLSetDescField** 來設定此欄位，以設定 ARD 的 SQL_DESC_ARRAY_STATUS_PTR 標頭欄位，這會要求應用程式取得描述項控制碼。  
  
2.  將資料列作業陣列的每個元素設定為下列兩個值的其中一個：  
  
    -   SQL_ROW_IGNORE，表示已排除大量作業的資料列。  
  
    -   SQL_ROW_PROCEED，表示資料列包含在大量作業中。 (這是預設值)。  
  
3.  呼叫 **SQLSetPos** 來執行大量作業。  
  
 下列規則適用于資料列作業陣列：  
  
-   SQL_ROW_IGNORE 和 SQL_ROW_PROCEED 只會影響使用 **SQLSetPos** 與 SQL_DELETE 或 SQL_UPDATE *作業的大量* 作業。 它們不會影響 SQL_REFRESH 或 SQL_POSITION*作業的* **SQLSetPos**呼叫。  
  
-   根據預設，指標會設定為 null。  
  
-   如果指標為 null，則會更新所有的資料列，就像所有元素都設定為 SQL_ROW_PROCEED 一樣。  
  
-   將專案設定為 SQL_ROW_PROCEED 不保證會在該特定資料列上進行作業。 例如，如果資料列集中的某個資料列具有狀態 SQL_ROW_ERROR，則不論應用程式是否 SQL_ROW_PROCEED 指定，驅動程式都可能無法更新該資料列。 應用程式必須一律檢查資料列狀態陣列，以查看作業是否成功。  
  
-   標頭檔中的 SQL_ROW_PROCEED 定義為0。 應用程式可以將資料列作業陣列初始化為0，以便處理所有資料列。  
  
-   如果資料列作業陣列中的元素編號 "n" 設定為 SQL_ROW_IGNORE，且呼叫 **SQLSetPos** 來執行大量更新或刪除作業，則在呼叫 **SQLSetPos**之後，資料列集中的第 n 個數據列會維持不變。  
  
-   應用程式應該會自動將唯讀資料行設定為 SQL_ROW_IGNORE。  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>忽略大量作業中的資料行  
 為了避免嘗試更新一或多個唯讀資料行而產生不必要的處理診斷，應用程式可以將系結長度/指標緩衝區中的值設定為 SQL_COLUMN_IGNORE。 如需詳細資訊，請參閱 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式可讓使用者流覽 ORDERS 資料表並更新訂單狀態。 資料指標是以資料列集大小20為導向的索引鍵集，並使用開放式並行存取控制來比較資料列版本。 提取每個資料列集之後，應用程式會列印它，並讓使用者選取和更新訂單的狀態。 應用程式會使用 **SQLSetPos** 將游標放置在選取的資料列上，並執行該資料列的定點更新。 為了清楚起見，會省略 (錯誤處理。 )   
  
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
  
 如需更多範例，請參閱 [定位 Update 和 Delete 語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) ，以及 [使用 SQLSetPos 更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行與區塊資料指標位置無關的大量作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得描述項的單一欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得描述項的多個欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定描述項的單一欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定描述項的多個欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
