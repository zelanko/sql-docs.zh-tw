---
title: "SQLExtendedFetch 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6c0336d9f7d3495e7e2ef925b86d47c472ff2ec
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 函式
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： 已被取代  
  
 **摘要**  
 **SQLExtendedFetch**從結果集提取資料之指定資料列集，並傳回所有的繫結資料行的資料。 在絕對或相對的位置或書籤，可以指定資料列集。  
  
> [!NOTE]  
>  在 ODBC 3*.x*， **SQLExtendedFetch**已被取代**SQLFetchScroll**。 ODBC 3*.x*應用程式不應該呼叫**SQLExtendedFetch**; 請改呼叫**SQLFetchScroll**。 驅動程式管理員會將對應**SQLFetchScroll**至**SQLExtendedFetch**時使用的 ODBC 2*.x*驅動程式。 ODBC 3*.x*驅動程式應支援**SQLExtendedFetch**如果他們想要使用的 ODBC 2*.x*呼叫它的應用程式。 如需詳細資訊，請參閱 「 註解 」 和[區塊資料指標，可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中附錄 g： 驅動程式的指導方針回溯相容性。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *Sqlfetchscroll*  
 [輸入]擷取的類型。 這是與相同*Sqlfetchscroll*中**SQLFetchScroll**。  
  
 *FetchOffset*  
 [輸入]要擷取的資料列數目。 這是與相同*FetchOffset*中**SQLFetchScroll**，有一個例外狀況。 當*Sqlfetchscroll*是要使用 SQL_FETCH_BOOKMARK， *FetchOffset*是固定長度的書籤，從書籤的位移。 換句話說， **SQLExtendedFetch**從這個引數不 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性擷取的書籤。 它不支援可變長度的書籤，並不支援從書籤擷取資料列集 （不是 0) 的位移。  
  
 *RowCountPtr*  
 [輸出]這是要傳回的實際擷取資料列數目的緩衝區指標。 這個緩衝區會用於相同的方式將 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性所指定的緩衝區。 這個緩衝區僅供**SQLExtendedFetch**。 它不由**SQLFetch**或**SQLFetchScroll**。  
  
 *RowStatusArray*  
 [輸出]陣列中要傳回的每個資料列狀態指標。 這個陣列可用於將 sql_attr_row_status_ptr 設定陳述式屬性所指定之陣列相同的方式。  
  
 不過，這個陣列的位址不會儲存 SQL_DESC_STATUS_ARRAY_PTR IRD 欄位中。 此外，這個陣列僅供**SQLExtendedFetch**和**SQLBulkOperations**與*作業*的 SQL_ADD 或**SQLSetPos**當之後呼叫**SQLExtendedFetch**。 它不由**SQLFetch**或**SQLFetchScroll**，它不是使用**SQLBulkOperations**或**SQLSetPos**之後的呼叫時**SQLFetch**或**SQLFetchScroll**。 它也不是時，使用**SQLBulkOperations**與*作業*SQL_ADD 的呼叫之前呼叫任何提取函式。 換句話說，它是只能用在陳述式狀態 S7。 在陳述式狀態 S5 或 S6 不使用它。 如需詳細資訊，請參閱[陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)附錄 b: ODBC 狀態轉換表中。  
  
 應用程式應該提供中的有效指標*RowStatusArray*引數; 如果沒有，行為**SQLExtendedFetch**和呼叫行為**SQLBulkOperations**或**SQLSetPos**已由維持資料指標之後**SQLExtendedFetch**是未定義。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLExtendedFetch**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLError**。 下表列出通常所傳回的 SQLSTATE 值**SQLExtendedFetch** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。 如果在單一資料行，就會發生錯誤**SQLGetDiagField**可以使用呼叫*Sqlgetdiagfield* SQL_DIAG_COLUMN_NUMBER 來判斷發生錯誤; 資料行的和**SQLGetDiagField**可以使用呼叫*Sqlgetdiagfield*的 SQL_DIAG_ROW_NUMBER 來判斷包含該資料行的資料列。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|字串或資料行所傳回的二進位資料會導致非空白的字元或二進位資料為非 NULL 的截斷。 如果是字串值，它就是向右截斷。 如果它是數字的值，已截斷的數字的小數部分。  （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S01|資料列中的錯誤|擷取一或多個資料列時發生錯誤。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S06|嘗試擷取結果集傳回第一個資料列集之前|要求的資料列集重疊之結果集目前位置的時間超過第一個資料列，然後開始*Sqlfetchscroll*已 SQL_PRIOR 或*Sqlfetchscroll*已與 SQL_RELATIVE負數*FetchOffset*絕對值是小於或等於目前的 SQL_ROWSET_SIZE。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S07|小數位數截斷|傳回資料行的資料已遭截斷。 數值資料類型已截斷的數字的小數部分。 時間、 時間戳記，和間隔資料型別包含時間元件，已截斷的小數部分的時間。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|資料值無法轉換成 C 資料類型所指定*TargetType*中**SQLBindCol**。|  
|07009|無效的描述元索引|使用繫結資料行 0 **SQLBindCol**，並且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22002|需要指標變數，但是未提供|NULL 的資料提取到資料行的*StrLen_or_IndPtr*設定**SQLBindCol**為 null 指標。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22003|數值超出範圍|傳回一或多個資料行 （做為數值或字串） 的數值可能已造成要截斷的數字 （相對於小數） 的整數部分。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> 如需詳細資訊，請參閱[間隔與數值資料類型的指導方針](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)附錄 d： 資料型別中。|  
|22007|無效的 datetime 格式|在結果集中的字元資料行已繫結至日期、 時間或時間戳記 C 結構，但資料行的值，分別無效的日期、 時間戳記。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22012|除數為零|算術運算式中的值傳回，因而導致除數為零。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22015|間隔欄位溢位|C 間隔類型指派從精確數值或 SQL 類型的間隔 [前置] 欄位中造成有效位數的遺失。<br /><br /> 當資料擷取至 C 間隔類型，時發生沒有 C 間隔類型中的 SQL 型別值的表示。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22018|轉換規格的字元值無效|C 類型為精確或大約的數字、 日期時間或間隔資料類型。資料行的 SQL 類型是字元資料類型。和資料行中的值不是有效的常值的繫結 C 類型。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|24000|指標狀態無效|*StatementHandle*目前處於執行狀態，但任何結果集與*StatementHandle*。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLError**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*，然後被呼叫函式上一次*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLExtendedFetch**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> (DM) 指定*StatementHandle*不處於執行狀態。 呼叫此函式時未先呼叫**SQLExecDirect**， **SQLExecute**，或類別目錄函式。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) **SQLExtendedFetch**針對呼叫*StatementHandle*之後**SQLFetch**或**SQLFetchScroll**呼叫之前**SQLFreeStmt** SQL_CLOSE 選項呼叫。<br /><br /> (DM) **SQLBulkOperations**陳述式之前呼叫**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**呼叫，並然後**SQLExtendedFetch**之前已呼叫**SQLFreeStmt** SQL_CLOSE 選項呼叫。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY106|提取類型超出範圍|(DM) 指定的引數的值*Sqlfetchscroll*無效。 （請參閱 「 註解。"）<br /><br /> 引數*Sqlfetchscroll*所要使用 SQL_FETCH_BOOKMARK，並且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_OFF。<br /><br /> SQL_CURSOR_TYPE 陳述式選項的值已 SQL_CURSOR_FORWARD_ONLY 和引數的值*Sqlfetchscroll*未 SQL_FETCH_NEXT。<br /><br /> 引數*Sqlfetchscroll*已 SQL_FETCH_RESUME。|  
|HY107|資料列值超出範圍|SQL_CURSOR_TYPE 陳述式選項所指定的值 SQL_CURSOR_KEYSET_DRIVEN，但 SQL_KEYSET_SIZE 陳述式屬性具有指定的值是大於 0 且小於 SQL_ROWSET_SIZE 陳述式屬性具有指定的值.|  
|HY111|無效的書籤值|引數*Sqlfetchscroll* SQL_FETCH_BOOKMARK，且書籤中指定*FetchOffset*引數無效。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援指定的提取型態。<br /><br /> 驅動程式或資料來源不支援的組合所指定的轉換*TargetType*中**SQLBindCol**和對應的資料行的 SQL 資料類型。 SQL 資料類型的資料行對應至驅動程式專屬 SQL 資料類型時，才會發生這個錯誤。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 逾時期限透過設定**SQLSetStmtOption**，SQL_QUERY_TIMEOUT。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 行為**SQLExtendedFetch**等同於**SQLFetchScroll**，但有下列例外狀況：  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**使用不同方法來傳回提取的資料列數目。 **SQLExtendedFetch**傳回中提取的資料列數目 *\*RowCountPtr*;**SQLFetchScroll**傳回直接至 SQL_ATTR_ROWS_FETCHED_PTR 所指向的緩衝區中提取的資料列數目。 如需詳細資訊，請參閱*RowCountPtr*引數。  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**不同陣列中傳回的每個資料列狀態。 如需詳細資訊，請參閱*RowStatusArray*引數。  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**使用不同方法來擷取書籤時*Sqlfetchscroll*是要使用 SQL_FETCH_BOOKMARK。 **SQLExtendedFetch**不支援可變長度的書籤或擷取的資料列集，從書籤 0 以外的位移。 如需詳細資訊，請參閱*FetchOffset*引數。  
  
-   **SQLExtendedFetch**和**SQLFetchScroll**使用不同的資料列集大小。 **SQLExtendedFetch**使用 SQL_ROWSET_SIZE 陳述式屬性的值和**SQLFetchScroll**使用 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性的值。  
  
-   **SQLExtendedFetch**有稍微不同的錯誤處理語意上的與**SQLFetchScroll**。 如需詳細資訊，請參閱 「 錯誤處理 」 的 [意見] 區段中[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
-   **SQLExtendedFetch**不支援繫結的位移 （SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性）。  
  
-   呼叫**SQLExtendedFetch**呼叫不能混合**SQLFetch**或**SQLFetchScroll**，而且如果**SQLBulkOperations**稱為在呼叫任何提取函式前， **SQLExtendedFetch**直到資料指標已關閉並重新開啟，無法呼叫。 也就是說， **SQLExtendedFetch**可以只在陳述式狀態 S7 呼叫。 如需詳細資訊，請參閱[陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)附錄 b: ODBC 狀態轉換表中。  
  
 當應用程式呼叫**SQLFetchScroll**時使用的 ODBC 2*.x*驅動程式，驅動程式管理員會對應至這個呼叫**SQLExtendedFetch**。 如需詳細資訊，請參閱 「 SQLFetchScroll 和 ODBC 2*.x*驅動程式 」 在[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 ODBC 2*.x*， **SQLExtendedFetch**已呼叫以擷取多個資料列和**SQLFetch**呼叫來提取單一資料列。 在 ODBC 3*.x*，相反地， **SQLFetch**可以呼叫以擷取多個資料列。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集內的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行大量插入、 更新或刪除作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集內的資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回結果集資料行|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位資料指標，重新整理此資料列集中，或更新或刪除在結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

