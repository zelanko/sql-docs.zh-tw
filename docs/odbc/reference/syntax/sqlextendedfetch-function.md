---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12c64be42c921a4dff57ccca6278e1f84bd717ef
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345205"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 函式
**標準**  
 引進的版本:ODBC 1.0 標準合規性:已被取代  
  
 **摘要**  
 **SQLExtendedFetch**會從結果集提取指定的資料列集, 並傳回所有系結資料行的資料。 資料列集可以在絕對或相對位置或依書簽指定。  
  
> [!NOTE]
>  在 ODBC 3.x  中, **SQLExtendedFetch**已由**SQLFetchScroll**取代。 ODBC 3.x  應用程式不應呼叫**SQLExtendedFetch**;相反地, 他們應該呼叫**SQLFetchScroll**。 使用 ODBC 2.x 驅動程式時, 驅動程式管理員會將**SQLFetchScroll**對應至**SQLExtendedFetch** 。  如果 ODBC   3.x 驅動程式想要使用呼叫它的 odbc 2.x 應用程式,  就應該支援**SQLExtendedFetch** 。 如需詳細資訊, 請參閱附錄 G 中的「批註」和[區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md):回溯相容性的驅動程式方針。  
  
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
 源語句控制碼。  
  
 *FetchOrientation*  
 源Fetch 的類型。 這與**SQLFetchScroll**中的*FetchOrientation*相同。  
  
 *FetchOffset*  
 源要提取的資料列數目。 這與**SQLFetchScroll**中的*FetchOffset*相同, 但有一個例外狀況。 當*FetchOrientation*是 SQL_FETCH_BOOKMARK 時, *FetchOffset*是固定長度的書簽, 而不是書簽的位移。 換句話說, **SQLExtendedFetch**會從這個引數抓取書簽, 而不是 SQL_ATTR_FETCH_BOOKMARK_PTR 語句屬性。 它不支援可變長度的書簽, 也不支援從書簽提取位移 (不是 0) 的資料列集。  
  
 *RowCountPtr*  
 輸出緩衝區的指標, 要在其中傳回實際提取的資料列數目。 這個緩衝區的使用方式與 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性所指定的緩衝區相同。 這個緩衝區僅供**SQLExtendedFetch**使用。 **SQLFetch**或**SQLFetchScroll**不會使用它。  
  
 *RowStatusArray*  
 輸出陣列的指標, 要在其中傳回每個資料列的狀態。 此陣列的使用方式與 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指定的陣列相同。  
  
 不過, 此陣列的位址不會儲存在 IRD 的 SQL_DESC_STATUS_ARRAY_PTR 欄位中。 此外, 只有**SQLExtendedFetch**和**SQLBulkOperations**搭配 SQL_ADD 或**SQLSetPos**的作業在**SQLExtendedFetch**之後呼叫時, 才會使用這個陣列。  **SQLFetch**或**SQLFetchScroll**不會使用它, 而且**SQLBulkOperations**或**SQLSetPos**在**SQLFetch**或**SQLFetchScroll**之後呼叫時, 不會使用它。 在呼叫任何 fetch 函數之前呼叫 SQL_ADD 的  作業**SQLBulkOperations**時, 也不會使用它。 換句話說, 它只會在語句狀態 S7 中使用。 它不會在語句狀態 S5 或 S6 中使用。 如需詳細資訊, 請參閱附錄 B 中的[語句轉換](../../../odbc/reference/appendixes/statement-transitions.md):ODBC 狀態轉換資料表。  
  
 應用程式應該在*RowStatusArray*引數中提供有效的指標;如果不是, 則**SQLExtendedFetch**的行為和呼叫**SQLBulkOperations**或**SQLSetPos**的行為會在**SQLExtendedFetch**的定位點之後未定義。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLExtendedFetch**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫**SQLError**來取得相關聯的 SQLSTATE 值。 下表列出**SQLExtendedFetch**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。 如果單一資料行發生錯誤, 則可以使用 SQL_DIAG_COLUMN_NUMBER 的*以*來呼叫**SQLGetDiagField** , 以判斷發生錯誤的資料行;您可以使用 SQL_DIAG_ROW_NUMBER 的*以*來呼叫和**SQLGetDiagField** , 以判斷包含該資料行的資料列。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01004|字串資料, 右邊已截斷|傳回資料行的字串或二進位資料導致截斷非空白字元或非 Null 的二進位資料。 如果它是字串值, 則會被右截斷。 如果是數值, 則會截斷數位的小數部分。  (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01S01|資料列發生錯誤|提取一或多個資料列時發生錯誤。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01S06|嘗試在結果集傳回第一個資料列集之前提取|當目前的位置超出第一個資料列時, 要求的資料列集會重迭結果集的開頭, 而*FetchOrientation*是 SQL_PRIOR 或*FetchOrientation* Was SQL_RELATIVE 的負*FetchOffset* , 其絕對值小於或等於目前的 SQL_ROWSET_SIZE。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01S07|小數截斷|針對資料行傳回的資料已被截斷。 若為數值資料類型, 則會截斷數位的小數部分。 若為包含時間元件的時間、時間戳記和間隔資料類型, 則會截斷時間的小數部分。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|07006|限制的資料類型屬性違規|資料值無法轉換成**SQLBindCol**中*TargetType*所指定的 C 資料類型。|  
|07009|不正確描述項索引|資料行0已與**SQLBindCol**系結, 且 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|在函式完成處理之前, 驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|22002|需要指標變數, 但未提供|已將 Null 資料提取到**SQLBindCol**中, 其*StrLen_or_IndPtr*設定為 null 指標。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|22003|數值超出範圍|傳回一或多個資料行的數值 (以數值或字串表示) 會導致截斷的整數部分 (相對於分數)。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。<br /><br /> 如需詳細資訊, 請參閱附錄 D: 中[的間隔和數值資料類型的方針](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)資料類型。|  
|22007|不正確日期時間格式|結果集中的字元資料行已系結至日期、時間或時間戳記 C 結構, 而且資料行中的值分別為不正確日期、時間或時間戳記。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|22012|除數為零|傳回算術運算式的值, 導致零除。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|22015|間隔欄位溢位|從精確的數值或間隔 SQL 類型指派到間隔 C 類型, 會導致前置欄位中的有效位數遺失。<br /><br /> 將資料提取到 interval C 類型時, 不會在間隔 C 類型中表示 SQL 類型的值。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|22018|轉換規格的字元值無效|C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;而資料行中的值不是系結 C 類型的有效常值。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|24000|指標狀態無效|*StatementHandle*處於已執行狀態, 但沒有與*StatementHandle*相關聯的結果集。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLError**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|作業已取消|已啟用*StatementHandle*的非同步處理。 已呼叫函式, 並在完成執行之前, 在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** , 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式, 並在完成執行之前, 從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|(DM) 已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLExtendedFetch**函數時, 這個非同步函式仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** , 並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前, 會呼叫這個函式。<br /><br /> (DM) 指定的*StatementHandle*不是處於執行中狀態。 在未先呼叫**SQLExecDirect**、 **SQLExecute**或目錄函式的情況下呼叫函數。<br /><br /> (DM) 已針對*StatementHandle*呼叫非同步執行的函式 (而非這個函式), 而且在呼叫這個函數時仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。<br /><br /> (DM) 在呼叫**SQLFetch**或**SQLFetchScroll**之後, 以及使用 SQLFreeStmt 選項呼叫**SQL_CLOSE**之前, 會呼叫*StatementHandle*的**SQLExtendedFetch** 。<br /><br /> (DM) 在呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLExtendedFetch**之前, 已呼叫語句的**SQLBulkOperations** , 然後在使用 SQLExtendedFetch 呼叫 SQLFreeStmt 之前  呼叫**SQL_** 關閉選項。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY106|提取類型超出範圍|(DM) 為引數*FetchOrientation*指定的值無效。 (請參閱「留言」)。<br /><br /> 引數*FetchOrientation*是 SQL_FETCH_BOOKMARK, 而 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_OFF。<br /><br /> SQL_CURSOR_TYPE 語句選項的值是 SQL_CURSOR_FORWARD_ONLY, 而 argument *FetchOrientation*的值不是 SQL_FETCH_NEXT。<br /><br /> 引數*FetchOrientation*是 SQL_FETCH_RESUME。|  
|HY107|資料列值超出範圍|以 SQL_CURSOR_TYPE 語句選項指定的值是 SQL_CURSOR_KEYSET_DRIVEN, 但是以 SQL_KEYSET_SIZE 語句屬性指定的值大於0且小於以 SQL_ROWSET_SIZE 語句屬性指定的值.|  
|HY111|不正確書簽值|引數*FetchOrientation*是 SQL_FETCH_BOOKMARK, 而*FetchOffset*引數中指定的書簽無效。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援指定的 fetch 類型。<br /><br /> 驅動程式或資料來源不支援**SQLBindCol**中的*TargetType*組合和對應資料行的 SQL 資料類型所指定的轉換。 只有當資料行的 SQL 資料類型對應到驅動程式特有的 SQL 資料類型時, 此錯誤才適用。|  
|HYT00|已超過逾時的設定|在資料來源傳回結果集之前, 查詢超時時間已過期。 超時期間是透過**SQLSetStmtOption**, SQL_QUERY_TIMEOUT 來設定。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*StatementHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 **SQLExtendedFetch**的行為等同于**SQLFetchScroll**, 但有下列例外狀況:  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**會使用不同的方法來傳回所提取的資料列數目。 **SQLExtendedFetch**會傳回在 *\*RowCountPtr*中提取的資料列數目;**SQLFetchScroll**會傳回 SQL_ATTR_ROWS_FETCHED_PTR 所指向的緩衝區直接提取的資料列數目。 如需詳細資訊, 請參閱*RowCountPtr*引數。  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**會傳回不同陣列中每個資料列的狀態。 如需詳細資訊, 請參閱*RowStatusArray*引數。  
  
-   當*FetchOrientation*為 SQL_FETCH_BOOKMARK 時, **SQLExtendedFetch**和**SQLFetchScroll**會使用不同的方法來抓取書簽。 **SQLExtendedFetch**不支援可變長度的書簽, 或從書簽在0以外的位移提取資料列集。 如需詳細資訊, 請參閱*FetchOffset*引數。  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**使用不同的資料列集大小。 **SQLExtendedFetch**會使用 SQL_ROWSET_SIZE 語句屬性的值, 而**SQLFETCHSCROLL**會使用 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性的值。  
  
-   **SQLExtendedFetch**的錯誤處理語義與**SQLFetchScroll**略有不同。 如需詳細資訊, 請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)的「批註」一節中的「錯誤處理」。  
  
-   **SQLExtendedFetch**不支援系結位移 (SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性)。  
  
-   呼叫**SQLExtendedFetch**時, 不能與**SQLFetch**或**SQLFetchScroll**的呼叫混合, 而且如果在呼叫任何 fetch 函數之前呼叫**SQLBulkOperations** , 就無法呼叫**SQLExtendedFetch** , 直到資料指標為已關閉並重新開啟。 也就是說, **SQLExtendedFetch**只能在語句狀態 S7 中呼叫。 如需詳細資訊, 請參閱附錄 B 中的[語句轉換](../../../odbc/reference/appendixes/statement-transitions.md):ODBC 狀態轉換資料表。  
  
 當應用程式在使用 ODBC 2.x 驅動程式呼叫  **SQLFetchScroll**時, 驅動程式管理員會將此呼叫對應至**SQLExtendedFetch**。 如需詳細資訊, 請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)中的  < SQLFetchScroll 和 ODBC 2.x 驅動程式》。  
  
 在 ODBC 2.x  中, 會呼叫**SQLExtendedFetch**來提取多個資料列, 並呼叫**SQLFetch**來提取單一資料列。 另一方面, 在  ODBC 3.x 中, 可以呼叫**SQLFetch**來提取多個資料列。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行 bulk insert、update 或 delete 作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集中資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回結果集資料行的數目|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位游標、重新整理資料列集中的資料, 或更新或刪除結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
