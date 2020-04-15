---
title: SQL 延伸取得功能 :微軟文件
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
ms.openlocfilehash: dc832e5a20b1d3c0a1ad63b3e2a070563de2b46d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285978"
---
# <a name="sqlextendedfetch-function"></a>SQLExtendedFetch 函式
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: 已棄用  
  
 **摘要**  
 **SQLExtendedFetch**從結果集中獲取指定的數據列集,並返回所有綁定列的數據。 行集可以在絕對或相對位置或通過書籤指定。  
  
> [!NOTE]
>  在 ODBC 3 *.x*中 **,SQL 擴展獲取**已被**SQLFetchScroll**替換。 ODBC 3 *.x*應用程式不應呼叫**SQL 延伸取得**;相反,他們應該調用**SQLFetchScroll。** 使用 ODBC 2 *.x*驅動程式時,驅動程式管理員將**SQLFetchScroll**映射到**SQL 延伸 。** 如果 ODBC 3 *.x*驅動程式想要與呼叫它的 ODBC 2 *.x*應用程式配合使用,則應支援**SQLExtendedFetch。** 有關詳細資訊,請參閱附錄 G 中的「註釋」和[塊游標、可滾動游標和向後相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md):向後相容性的驅動程式指南。  
  
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
 *語句句柄*  
 [輸入]語句句柄。  
  
 *擷取方向*  
 [輸入]提取的類型。 這與**SQLFetchScroll**中的 *「獲取方向」* 相同。  
  
 *擷取位移*  
 [輸入]要提取的行數。 這與**SQLFetchScroll**中的*提取偏移*相同,但有一個例外。 當*取取方向*SQL_FETCH_BOOKMARK時 *,FetchOffset*是固定長度的書籤,而不是書籤的偏移量。 換句話說 **,SQLExtendedFetch**從此參數檢索書籤,而不是SQL_ATTR_FETCH_BOOKMARK_PTR語句屬性。 它不支援可變長度書籤,不支援從書籤的偏移量(0 以外的)提取行集。  
  
 *羅( 羅) CountPtr*  
 【輸出]指向要返回實際提取的行數的緩衝區的指標。 此緩衝區的使用方式與SQL_ATTR_ROWS_FETCHED_PTR語句屬性指定的緩衝區相同。 此緩衝區僅由**SQL 擴展獲取**使用。 它不被**SQLFetch**或**SQLFetchScroll**使用。  
  
 *行狀態陣列*  
 【輸出]指向要返回每行狀態的陣列的指標。 此陣列的使用方式與SQL_ATTR_ROW_STATUS_PTR語句屬性指定的陣列相同。  
  
 但是,此陣列的位址不會存儲在 IRD 中SQL_DESC_STATUS_ARRAY_PTR欄位中。 此外,此陣列僅在**SQL****擴充取得**後調用時由*Operation*SQL 擴充獲取和**SQLBulk 操作**使用,操作SQL_ADD或**SQLSetPos。** 它不由**SQLFetch**或**SQLFetchScroll**使用,並且**SQLBulk 操作**或**SQLSetPos**在**SQLFetch**或**SQLFetchScroll**之後調用時不使用它。 在調用任何提取函數之前調用具有SQL_ADD*操作*的**SQLBulk 操作**時,也不會使用它。 換句話說,它僅在語句狀態 S7 中使用。 它不用於語句狀態 S5 或 S6。 有關詳細資訊,請參閱附錄 B[中的語句轉換](../../../odbc/reference/appendixes/statement-transitions.md):ODBC 狀態轉換表。  
  
 應用程式應在*RowStatusArray*參數中提供有效的指標;否則 **,SQL擴展獲取**的行為以及**SQL 擴展獲取**定位游標後對**SQLBulk 操作**或**SQLSetPos**的調用行為未定義。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLExtendedFetch**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以通過調用**SQLError**獲得關聯的 SQLSTATE 值。 下表列出了**SQLAofFetch**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。 如果單個列上發生錯誤,可以使用 SQL_DIAG_COLUMN_NUMBER*的 Diag 標識符*調用**SQLGetDiagField**以確定錯誤發生的列;和**SQLGetDiagField**可以使用SQL_DIAG_ROW_NUMBER*的 Diag 識別符*調用,以確定包含該列的行。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|為列返回的字串或二進位資料導致非空白字元或非 NULL 二進位資料的截斷。 如果它是一個字串值,它是右截斷的。 如果是數值,則數位的小數部分將被截斷。  (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S01|行中的錯誤|獲取一個或多個行時出錯。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S06|嘗試在結果集傳回第一個行集之前擷取|當當前位置超出第一行時,請求的行集與結果集的開始重疊,要麼*Fetch方向*SQL_PRIOR,要麼*Fetch 方向*SQL_RELATIVE,其絕對值小於或等於當前SQL_ROWSET_SIZE的負*FetchOffset。* (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S07|分數截斷|為列返回的數據被截斷。 對於數位數據類型,數位的小數部分被截斷。 對於包含時間元件的時間、時間戳和間隔數據類型,時間的小數部分被截斷。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|數據值無法轉換為**SQLBindCol**中*TargetType*指定的 C 資料類型。|  
|07009|不合法的描述符索引|列 0 與**SQLBindCol**綁定,SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_OFF。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|22002|需要指標變數,但未提供|NULL 資料被提取到一個列中,該列*的 StrLen_or_IndPtr*由**SQLBindCol**設置為空指標。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|22003|數值超範圍|返回一個或多個列的數值(作為數位或字串)將導致數字的整個部分(而不是小數)被截斷。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。<br /><br /> 有關詳細資訊,請參閱附錄 D:資料類型中[間隔和數位資料類型的準則](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md)。|  
|22007|不合法日期時間格式|結果集中的字元列綁定到日期、時間或時間戳 C 結構,並且列中的值分別是無效的日期、時間或時間戳。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|22012|除零|返回算術表達式中的值,結果除以零。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|22015|間隔欄位溢出|從精確數位或間隔 SQL 類型分配給間隔 C 類型會導致前導欄位中的重要數位丟失。<br /><br /> 將資料提取到間隔 C 類型時,間隔 C 類型中沒有 SQL 類型的值表示形式。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|22018|強制轉換規範的不合法字元值|C 類型是精確或近似的數位、日期時間或間隔數據類型;列的 SQL 類型是字元數據類型;列中的值不是綁定 C 型態的有效文字。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|24000|指標狀態無效|*語句句柄*處於已執行狀態,但沒有與*語句句柄*關聯的結果集。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLError**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫該函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**在*語句句柄*上調用 ,然後在*語句句柄*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQL 擴展獲取**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 指定的*語句句柄*未處於執行狀態。 調用該函數時沒有首先調用**SQLExecDirect、SQLExecute**或目錄函**SQLExecute**數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) SQLExtendedFetch 在調用**SQLFetch**或**SQLFetchScroll**後,在使用SQL_CLOSE選項調用**SQLFreeStmt**之前,為*語句處理*調用了**SQLAa,** 用於語句處理。<br /><br /> (DM) **SQLBulk 操作**在呼叫**SQLFetch、SQLFetchScroll**或 SQL**擴充取得**之前呼叫您的敘述,然後在使用SQL_CLOSE選項呼叫**SQLFreeStmt**之前呼叫 SQL**延伸取得**。 **SQLFetchScroll**|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY106|擷取類型範圍外|(DM) 為參數 Fetch*方向*指定的值無效。 (請參閱"註釋」。。<br /><br /> 參數*Fetch 方向*已SQL_FETCH_BOOKMARK,並且SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_OFF。<br /><br /> SQL_CURSOR_TYPE語句選項的值SQL_CURSOR_FORWARD_ONLY,並且參數*Fetch 方向*的值不SQL_FETCH_NEXT。<br /><br /> 爭論*Fetch定向*是SQL_FETCH_RESUME。|  
|HY107|行值範圍外|使用SQL_CURSOR_TYPE語句選項指定的值SQL_CURSOR_KEYSET_DRIVEN,但使用SQL_KEYSET_SIZE語句屬性指定的值大於 0,小於使用 SQL_ROWSET_SIZE 語句屬性指定的值。|  
|HY111|不合法的書籤值|SQL_FETCH_BOOKMARK,在*FetchOffset*參數中指定的書籤*FetchOffset*無效。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或數據源不支援指定的提取類型。<br /><br /> 驅動程式或資料來源不支援**SQLBindCol**中的*TargetType*和相應列的 SQL 資料類型的組合指定的轉換。 僅當列的 SQL 資料類型映射到特定於驅動程式的 SQL 資料類型時,此錯誤才適用。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回結果集之前已過期。 超時期間通過**SQLSetStmtOption**SQL_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 **SQLExfetch**的行為與**SQLFetchScroll**的行為相同,但有以下例外:  
  
-   **SQL擴展獲取**和**SQLFetch**使用不同的方法來返回提取的行數。 **SQLExtendedFetch**傳回*\*在 RowCountPtr*中獲取的行數;**SQLFetchScroll**返回直接提取到SQL_ATTR_ROWS_FETCHED_PTR指向的緩衝區的行數。 有關詳細資訊,請參閱*RowCountPtr*參數。  
  
-   **SQL擴展取得**和**SQLFetchScroll**傳回不同陣列中每行的狀態。 有關詳細資訊,請參閱*行狀態陣列*參數。  
  
-   **SQL擴展取得**和**SQLScroll**使用不同的方法來檢索書籤,當*取取方向*SQL_FETCH_BOOKMARK。 **SQLExtendedFetch**不支援可變長度書籤或從書籤中從 0 以外的偏移量提取行集。 有關詳細資訊,請參閱*提取偏移參數*。  
  
-   **SQL 延伸取得**和**SQLFetch**使用不同的行集大小。 **SQLExtendedFetch**使用SQL_ROWSET_SIZE語句屬性的值 **,SQLFetchScroll**使用SQL_ATTR_ROW_ARRAY_SIZE語句屬性的值。  
  
-   **SQLExtendedFetch**具有與**SQLFetchScroll**略有不同的錯誤處理語義。 有關詳細資訊,請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)的「註釋」部分中的「錯誤處理」。  
  
-   **SQLExtendedFetch**不支援綁定偏移量(SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性)。  
  
-   對**SQL 延伸提取的**呼叫不能與**SQLFetch**或**SQLFetchScroll**的呼叫混合,如果在呼叫任何提取函數之前調用**SQLBulk 操作,** 則在關閉和重新打開游標之前無法呼叫**SQLExtendedFetch。** 也就是說 **,SQLExtendedFetch**只能在語句狀態 S7 下調用。 有關詳細資訊,請參閱附錄 B[中的語句轉換](../../../odbc/reference/appendixes/statement-transitions.md):ODBC 狀態轉換表。  
  
 當應用程式使用 ODBC 2 *.x*驅動程式呼叫**SQLFetchScroll**時,驅動程式管理員將此呼叫映射到**SQL 延伸 。** 有關詳細資訊,請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)中的"SQLFetchScroll 和 ODBC 2 *.x*驅動程式"。  
  
 在 ODBC 2 *.x*中,呼叫**SQL 延伸獲取**以獲取多行,並調用**SQLFetch**來取得一行。 另一方面,在 ODBC 3 *.x*中,可以調用**SQLFetch**來獲取多行。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行批次插入、更新或移除操作|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回有關結果集中的資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回結果集欄數|[SQLNumResultCols 函數](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位游標、刷新列集中的資料或更新或刪除結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
