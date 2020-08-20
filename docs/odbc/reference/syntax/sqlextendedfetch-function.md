---
description: SQLExtendedFetch 函式
title: SQLExtendedFetch 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac19d017baf4a3f0e873be64cd2eb812ca1b05e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476108"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性：已淘汰  
  
 **總結**  
 **SQLExtendedFetch** 會從結果集中提取指定的資料列集，並傳回所有系結資料行的資料。 您可以在絕對或相對位置或依書簽來指定資料列集。  
  
> [!NOTE]
>  在 ODBC 3.x*中，* **SQLExtendedFetch** 已由 **SQLFetchScroll**取代。 ODBC 3.x*應用程式不* 應呼叫 **SQLExtendedFetch**;相反地，它們應該呼叫 **SQLFetchScroll**。 當使用 ODBC*2.x 驅動程式*時，驅動程式管理員會將**SQLFetchScroll**對應至**SQLExtendedFetch** 。 如果 ODBC*3.x 驅動程式*想要使用呼叫它的 odbc 2.x 應用程式，*.x*則應支援**SQLExtendedFetch** 。 如需詳細資訊，請參閱附錄 G：適用于回溯相容性的驅動程式指導方針中的「批註」和 [區塊資料指標、可滾動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *FetchOrientation*  
 輸出提取的類型。 這與**SQLFetchScroll**中的*FetchOrientation*相同。  
  
 *FetchOffset*  
 輸出要提取的資料列數目。 這與**SQLFetchScroll**中的*FetchOffset*相同，但有一個例外狀況。 當 SQL_FETCH_BOOKMARK *FetchOrientation* 時， *FetchOffset* 是固定長度的書簽，而不是書簽的位移。 換句話說， **SQLExtendedFetch** 會從這個引數抓取書簽，而不是 SQL_ATTR_FETCH_BOOKMARK_PTR 的語句屬性。 它不支援可變長度的書簽，也不支援在 (從書簽中的 0) 以外的位移提取資料列集。  
  
 *RowCountPtr*  
 出緩衝區的指標，此緩衝區會傳回實際提取的資料列數目。 這個緩衝區的使用方式與 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性所指定的緩衝區相同。 此緩衝區僅供 **SQLExtendedFetch**使用。 **SQLFetch**或**SQLFetchScroll**不會使用它。  
  
 *RowStatusArray*  
 出陣列的指標，要在其中傳回每個資料列的狀態。 這個陣列的使用方式與 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指定的陣列相同。  
  
 不過，此陣列的位址不會儲存在 IRD 的 [SQL_DESC_STATUS_ARRAY_PTR] 欄位中。 此外，只有**SQLExtendedFetch**和**SQLBulkOperations**會使用這個陣列，並在**SQLExtendedFetch**之後呼叫 SQL_ADD 或**SQLSetPos** 。 *Operation* **SQLFetch**或**SQLFetchScroll**不會使用它，而且**SQLBulkOperations**或**SQLSetPos**在**SQLFetch**或**SQLFetchScroll**之後呼叫時，不會使用它。 在呼叫任何 fetch 函數之前呼叫*SQL_ADD 的* **SQLBulkOperations**時，也不會使用它。 換句話說，它只會在語句狀態 S7 中使用。 它不會在語句狀態中使用，而是使用 S5 或 S6。 如需詳細資訊，請參閱附錄 B： ODBC 狀態轉換資料表中的 [語句轉換](../../../odbc/reference/appendixes/statement-transitions.md) 。  
  
 應用程式應該在 *RowStatusArray* 引數中提供有效的指標;如果沒有，則 **SQLExtendedFetch** 的行為以及 **SQLBulkOperations** 或 **SQLSetPos** 在資料指標定位之後的 **行為未定義** 。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當 **SQLExtendedFetch** 傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫 **SQLError**來取得相關聯的 SQLSTATE 值。 下表列出 **SQLExtendedFetch** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。 如果在單一資料行上發生錯誤，則可以使用 SQL_DIAG_COLUMN_NUMBER 的*以*來呼叫**SQLGetDiagField** ，以判斷發生錯誤的資料行;您可以使用 SQL_DIAG_ROW_NUMBER 的*以*來呼叫和**SQLGetDiagField** ，以判斷包含該資料行的資料列。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|針對資料行傳回的字串或二進位資料會截斷非空白字元或非 Null 的二進位資料。 如果是字串值，就會以正確的方式截斷。 如果是數值，則會截斷數位的小數部分。   (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01S01|資料列發生錯誤|提取一或多個資料列時發生錯誤。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01S06|在結果集傳回第一個資料列集之前嘗試提取|當目前的位置超出第一個資料列，而且 *FetchOrientation* 是 SQL_PRIOR 或 *FetchOrientation* SQL_RELATIVE 是以負 *FetchOffset* 的絕對值小於或等於目前的 SQL_ROWSET_SIZE 時，要求的資料列集會重迭結果集的開頭。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01S07|小數截斷|為數據行傳回的資料已截斷。 若為數值資料類型，則會截斷數位的小數部分。 若是時間、時間戳記和包含時間元件的間隔資料類型，時間的小數部分會被截斷。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07006|限制的資料類型屬性違規|無法將資料值轉換成**SQLBindCol**中*TargetType*所指定的 C 資料類型。|  
|07009|描述元索引無效|資料行0系結了 **SQLBindCol**，且 SQL_ATTR_USE_BOOKMARKS 語句屬性已設為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|22002|需要指標變數，但未提供|Null 資料已提取至資料行，而該資料行的 *StrLen_or_IndPtr* 由 **SQLBindCol** 設定為 null 指標。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|22003|數值超出範圍|將數值或字串) 傳回 (為一個或多個資料行的數值或字串，會導致整個 (與要截斷之數位) 部分的分數相反。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) <br /><br /> 如需詳細資訊，請參閱附錄 D：資料類型中 [的間隔和數值資料類型的指導方針](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) 。|  
|22007|不正確日期時間格式|結果集中的字元資料行系結至日期、時間或時間戳記 C 結構，而資料行中的值分別是不正確日期、時間或時間戳記。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|22012|零除|傳回算術運算式的值，導致零除。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|22015|間隔欄位溢位|從確切數值或間隔 SQL 類型指派至間隔 C 類型，會導致在前置欄位中遺失有效位數。<br /><br /> 將資料提取到間隔 C 類型時，間隔 C 類型中沒有 SQL 類型的值表示。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|22018|轉換規格的字元值無效|C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;且資料行中的值不是系結 C 類型的有效常值。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|24000|指標狀態無效|*StatementHandle*處於執行中狀態，但沒有與*StatementHandle*相關聯的結果集。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 * \* MessageText*緩衝區中的**SQLError**所傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 已呼叫函式，並在它完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** ，然後在*StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLExtendedFetch** 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 指定的 *StatementHandle* 未處於執行中狀態。 在未先呼叫 **SQLExecDirect**、 **SQLExecute**或 catalog 函數的情況下呼叫函式。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br /> 在呼叫**SQLFetch**或**SQLFetchScroll**之後，以及使用 SQL_CLOSE 選項呼叫**SQLFreeStmt**之前，會呼叫*StatementHandle*的 (DM) **SQLExtendedFetch** 。<br /><br /> 在呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLExtendedFetch**之前呼叫語句的 (DM) **SQLBulkOperations** ，然後在使用 SQL_CLOSE 選項呼叫**SQLExtendedFetch**之前呼叫**SQLFreeStmt** 。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY106|提取類型超出範圍| (DM) 引數 *FetchOrientation* 指定的值無效。  (請參閱「批註」。) <br /><br /> 已 SQL_FETCH_BOOKMARK 引數 *FetchOrientation* ，且 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_OFF。<br /><br /> SQL_CURSOR_FORWARD_ONLY SQL_CURSOR_TYPE 語句選項的值，且未 SQL_FETCH_NEXT 引數 *FetchOrientation* 的值。<br /><br /> 已 SQL_FETCH_RESUME 引數 *FetchOrientation* 。|  
|HY107|資料列值超出範圍|已 SQL_CURSOR_KEYSET_DRIVEN 使用 SQL_CURSOR_TYPE 語句選項指定的值，但以 SQL_KEYSET_SIZE 語句屬性指定的值大於0，且小於 SQL_ROWSET_SIZE 語句屬性指定的值。|  
|HY111|不正確書簽值|已 SQL_FETCH_BOOKMARK 引數 *FetchOrientation* ，且 *FetchOffset* 引數中指定的書簽無效。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|驅動程式或資料來源不支援指定的提取類型。<br /><br /> 驅動程式或資料來源不支援**SQLBindCol**中的*TargetType*組合所指定的轉換，以及對應資料行的 SQL 資料類型。 只有當資料行的 SQL 資料類型對應至驅動程式特定的 SQL 資料類型時，才會套用這個錯誤。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回結果集之前過期。 Timeout 期限是透過 **SQLSetStmtOption**、SQL_QUERY_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 **SQLExtendedFetch**的行為與**SQLFetchScroll**的行為完全相同，但有下列例外狀況：  
  
-   **SQLExtendedFetch** 和 **SQLFetchScroll** 會使用不同的方法來傳回提取的資料列數目。 **SQLExtendedFetch**會傳回在* \* RowCountPtr*中提取的資料列數目;**SQLFetchScroll**會傳回直接提取到 SQL_ATTR_ROWS_FETCHED_PTR 所指向之緩衝區的資料列數目。 如需詳細資訊，請參閱 *RowCountPtr* 引數。  
  
-   **SQLExtendedFetch** 和 **SQLFetchScroll** 會傳回不同陣列中每個資料列的狀態。 如需詳細資訊，請參閱 *RowStatusArray* 引數。  
  
-   **SQLExtendedFetch** 和 **SQLFetchScroll** 會使用不同的方法來取得 *FetchOrientation* SQL_FETCH_BOOKMARK 時的書簽。 **SQLExtendedFetch** 不支援可變長度的書簽，也不支援從書簽以0為位移的資料列集提取資料列集。 如需詳細資訊，請參閱 *FetchOffset* 引數。  
  
-   **SQLExtendedFetch** 和 **SQLFetchScroll** 使用不同的資料列集大小。 **SQLExtendedFetch** 會使用 SQL_ROWSET_SIZE 語句屬性的值，而 **SQLFetchScroll** 則會使用 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性的值。  
  
-   **SQLExtendedFetch** 的錯誤處理語義與 **SQLFetchScroll**稍有不同。 如需詳細資訊，請參閱 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)的「批註」一節中的「錯誤處理」。  
  
-   **SQLExtendedFetch** 不支援) SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性 (系結位移。  
  
-   呼叫 **SQLExtendedFetch** 時，不能與對 **SQLFetch** 或 **SQLFetchScroll**的呼叫混合，而且如果在呼叫任何 fetch 函式之前呼叫 **SQLBulkOperations** ，則在關閉並重新開啟資料指標之前，無法呼叫 **SQLExtendedFetch** 。 也就是說， **SQLExtendedFetch** 只能在語句狀態 S7 中呼叫。 如需詳細資訊，請參閱附錄 B： ODBC 狀態轉換資料表中的 [語句轉換](../../../odbc/reference/appendixes/statement-transitions.md) 。  
  
 當應用程式在使用 ODBC*2.x 驅動程式*時呼叫**SQLFetchScroll**時，驅動程式管理員會將此呼叫對應至**SQLExtendedFetch**。 如需詳細資訊，請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)中的「SQLFETCHSCROLL 與 ODBC*2.x 驅動程式*」。  
  
 在 ODBC 2.x*中，* 呼叫 **SQLExtendedFetch** 以提取多個資料列，並呼叫 **SQLFetch** 來提取單一資料列。 另一方面 *，在*ODBC 3.x 中，可以呼叫 **SQLFetch** 來提取多個資料列。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行大量插入、更新或刪除作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集中資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回結果集資料行的數目|[SQLNumResultCols 函數](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位資料指標、重新整理資料列集內的資料，或更新或刪除結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
