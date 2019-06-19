---
title: SQLExtendedFetch 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63030b34e4b607b850f25a67357d62a7184467c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537189"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：已被取代  
  
 **摘要**  
 **SQLExtendedFetch**提取從結果集的指定資料列集的資料，並傳回所有繫結的資料行的資料。 在絕對或相對位置或依書籤，則可以指定資料列集。  
  
> [!NOTE]
>  在 ODBC 3 *.x*， **SQLExtendedFetch**已被取代**SQLFetchScroll**。 ODBC 3 *.x*應用程式不應該呼叫**SQLExtendedFetch**; 改為呼叫**SQLFetchScroll**。 驅動程式管理員會將對應**SQLFetchScroll**要**SQLExtendedFetch**時使用的 ODBC 2 *.x*驅動程式。 ODBC 3 *.x*驅動程式應支援**SQLExtendedFetch**如果他們想要使用 ODBC 2 *.x*呼叫它的應用程式。 如需詳細資訊，請參閱 「 註解 」 以及[區塊資料指標、 可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。  
  
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
 [輸入]陳述式控制代碼。  
  
 *FetchOrientation*  
 [輸入]擷取的型別。 這是相同*Sqlfetchscroll*中**SQLFetchScroll**。  
  
 *FetchOffset*  
 [輸入]要擷取的資料列數目。 這是相同*FetchOffset*中**SQLFetchScroll**，有一個例外狀況。 當*Sqlfetchscroll*是要使用 SQL_FETCH_BOOKMARK， *FetchOffset*是固定長度書籤，從書籤的位移。 亦即**SQLExtendedFetch**從這個引數，而不是 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性擷取的書籤。 它不支援可變長度的書籤，並不支援從書籤擷取資料列集 （不是 0) 的位移。  
  
 *RowCountPtr*  
 [輸出]若要在其中傳回的實際提取的資料列數目的緩衝區的指標。 這個緩衝區會在相同的方式為 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性所指定的緩衝區。 這個緩衝區僅供**SQLExtendedFetch**。 它不是由**SQLFetch**或是**SQLFetchScroll**。  
  
 *RowStatusArray*  
 [輸出]若要在其中傳回每個資料列狀態陣列的指標。 這個陣列用在 sql_attr_row_status_ptr 設定陳述式屬性所指定之陣列相同的方式。  
  
 不過，這個陣列的位址不會儲存在 IRD SQL_DESC_STATUS_ARRAY_PTR 欄位中。 此外，這個陣列僅供**SQLExtendedFetch** ，經由**SQLBulkOperations**具有*作業*的 SQL_ADD 或**SQLSetPos**呼叫之後時**SQLExtendedFetch**。 它不是由**SQLFetch**或**SQLFetchScroll**，而且它不會由**SQLBulkOperations**或是**SQLSetPos**之後的呼叫時**SQLFetch**或是**SQLFetchScroll**。 它也不是時，使用**SQLBulkOperations**具有*作業*SQL_ADD 的呼叫之前呼叫任何提取函式。 換句話說，它只適用於陳述式狀態 S7。 在 S5 或 S6 的陳述式狀態中不使用它。 如需詳細資訊，請參閱 <<c0> [ 陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)中附錄 b:狀態轉換資料表。  
  
 應用程式應該提供中的有效指標*RowStatusArray*引數; 如果沒有，行為**SQLExtendedFetch**和 呼叫行為**SQLBulkOperations**或是**SQLSetPos**已藉由維持資料指標之後**SQLExtendedFetch**為未定義。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLExtendedFetch**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLError**。 下表列出通常所傳回的 SQLSTATE 值**SQLExtendedFetch** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。 如果在單一資料行，就會發生錯誤**SQLGetDiagField**也可以呼叫*Sqlgetdiagfield* SQL_DIAG_COLUMN_NUMBER 來判斷發生錯誤; 資料行的和**SQLGetDiagField**也可以呼叫*Sqlgetdiagfield*的 SQL_DIAG_ROW_NUMBER 來決定包含該資料行的資料列。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|字串或二進位資料傳回的資料行導致的非空白的字元或非 NULL 的二進位資料截斷。 如果是字串值，則向右截斷。 如果它是一個數字值，已截斷數字的小數部分。  （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S01|資料列中的錯誤|擷取一或多個資料列時發生錯誤。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S06|嘗試擷取結果集傳回第一個資料列集之前|要求的資料列集重疊時的目前位置是在第一個資料列，而且不是，結果集的開頭*Sqlfetchscroll*已 SQL_PRIOR 或*Sqlfetchscroll*已與 SQL_RELATIVE負*FetchOffset*其絕對值是小於或等於目前的 SQL_ROWSET_SIZE。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S07|小數位數截斷|傳回資料行的資料已遭截斷。 數值資料類型已遭截斷數字的小數部分。 時間、 時間戳記，和包含時間元件的 interval 資料類型，已截斷的小數部分的時間。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|資料值無法轉換成 C 資料類型所指定*TargetType*中**SQLBindCol**。|  
|07009|描述項索引無效|使用繫結資料行 0 **SQLBindCol**，且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22002|指標變數但未提供|NULL 的資料擷取成資料行其*StrLen_or_IndPtr*情況下設**SQLBindCol**是 null 指標。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22003|數值超出範圍|傳回數字的值 （做為數值或字串），一或多個資料行可能已造成要截斷的數字 （相對於小數） 的整數部分。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 間隔和數值資料類型的方針](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)附錄 d:資料類型。|  
|22007|無效的日期時間格式|在結果集中的字元資料行已繫結至日期、 時間或時間戳記 C 結構，但資料行的值，分別無效的日期、 時間戳記。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22012|除數為零|算術運算式的值傳回，因而導致除數為零。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22015|間隔欄位溢位|將指派從精確數值或時間間隔 SQL 型別，給 C 間隔類型造成有效位數的遺失開頭的欄位中。<br /><br /> 當 C 間隔類型以提取資料時，發生 C 間隔類型中的 SQL 類型的值不表示。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22018|轉換規格的字元值無效|C 類型為精確或近似數值、 日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;和資料行中的值不是有效的常值的繫結的 C 類型。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|24000|指標狀態無效|*StatementHandle*處於執行狀態，但與相關聯的任何結果集已*StatementHandle*。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLError**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*，並接著呼叫函式上再次*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLExtendedFetch**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 指定*StatementHandle*不處於執行狀態。 已呼叫的函式，但是未先呼叫**SQLExecDirect**， **SQLExecute**，或目錄函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) **SQLExtendedFetch**針對呼叫*StatementHandle*之後**SQLFetch**或是**SQLFetchScroll**呼叫之前**SQLFreeStmt**以 SQL_CLOSE 選項來呼叫。<br /><br /> (DM) **SQLBulkOperations**陳述式之前呼叫**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**呼叫，以及然後**SQLExtendedFetch**之前已呼叫**SQLFreeStmt**以 SQL_CLOSE 選項來呼叫。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY106|擷取類型超出範圍|(DM) 引數指定的值*Sqlfetchscroll*無效。 （請參閱 「 註解。"）<br /><br /> 引數*Sqlfetchscroll*所要使用 SQL_FETCH_BOOKMARK，且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_OFF。<br /><br /> SQL_CURSOR_TYPE 陳述式選項的值為 SQL_CURSOR_FORWARD_ONLY 和引數的值*Sqlfetchscroll*未 SQL_FETCH_NEXT。<br /><br /> 引數*Sqlfetchscroll*已 SQL_FETCH_RESUME。|  
|HY107|資料列值超出範圍|使用 SQL_CURSOR_TYPE 陳述式選項所指定的值是 SQL_CURSOR_KEYSET_DRIVEN，但 SQL_KEYSET_SIZE 陳述式屬性所指定的值是大於 0 且小於 SQL_ROWSET_SIZE 陳述式屬性所指定的值.|  
|HY111|無效的書籤值|引數*Sqlfetchscroll*是要使用 SQL_FETCH_BOOKMARK，和書籤中指定*FetchOffset*引數無效。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式] 或 [資料來源不支援指定的擷取型別。<br /><br /> 驅動程式或資料來源不支援指定的組合來轉換*TargetType*中**SQLBindCol**和對應的資料行的 SQL 資料類型。 SQL 資料類型資料行的已對應至驅動程式專屬的 SQL 資料型別時，就會適用這項錯誤。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtOption**，SQL_QUERY_TIMEOUT。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 行為**SQLExtendedFetch**等同於**SQLFetchScroll**，但有下列例外狀況：  
  
-   **SQLExtendedFetch**並**SQLFetchScroll**使用不同方法來傳回提取的資料列數目。 **SQLExtendedFetch**會傳回在擷取的資料列數目 *\*RowCountPtr*;**SQLFetchScroll**傳回直接至 SQL_ATTR_ROWS_FETCHED_PTR 所指向的緩衝區中提取的資料列數目。 如需詳細資訊，請參閱 < *RowCountPtr*引數。  
  
-   **SQLExtendedFetch**並**SQLFetchScroll**不同陣列中傳回每個資料列的狀態。 如需詳細資訊，請參閱 < *RowStatusArray*引數。  
  
-   **SQLExtendedFetch**並**SQLFetchScroll**使用不同的方法來擷取書籤時*Sqlfetchscroll*是要使用 SQL_FETCH_BOOKMARK。 **SQLExtendedFetch**不支援可變長度的書籤或擷取的資料列集，從書籤的 0 以外的位移。 如需詳細資訊，請參閱 < *FetchOffset*引數。  
  
-   **SQLExtendedFetch**並**SQLFetchScroll**使用不同的資料列集大小。 **SQLExtendedFetch**會使用 SQL_ROWSET_SIZE 陳述式屬性值，並**SQLFetchScroll**會使用 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性的值。  
  
-   **SQLExtendedFetch**稍有不同的錯誤處理的語意**SQLFetchScroll**。 如需詳細資訊，請參閱 「 錯誤處理 」 的 [註解] 區段中[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
-   **SQLExtendedFetch**不支援繫結位移 （SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性）。  
  
-   呼叫**SQLExtendedFetch**不能呼叫的方式來混合**SQLFetch**或**SQLFetchScroll**，而如果**SQLBulkOperations**稱為呼叫任何提取函式之前，請**SQLExtendedFetch**之前的資料指標已關閉並重新開啟，無法呼叫。 亦即**SQLExtendedFetch**可以只能在陳述式狀態 S7 中呼叫。 如需詳細資訊，請參閱 <<c0> [ 陳述式轉換](../../../odbc/reference/appendixes/statement-transitions.md)中附錄 b:狀態轉換資料表。  
  
 當應用程式呼叫**SQLFetchScroll**時使用的 ODBC 2 *.x*驅動程式，驅動程式管理員會對應至這個呼叫**SQLExtendedFetch**。 如需詳細資訊，請參閱 「 SQLFetchScroll 和 ODBC 2 *.x*驅動程式 」 中[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)。  
  
 ODBC 2 *.x*， **SQLExtendedFetch**呼叫來擷取多個資料列並**SQLFetch**呼叫來擷取單一資料列。 在 ODBC 3 *.x*，相反地， **SQLFetch**可以呼叫以擷取多個資料列。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行大量插入、 更新或刪除作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在結果集中傳回資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回結果集資料行|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|遊標定位、 重新整理此資料列集中，或更新或刪除結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
