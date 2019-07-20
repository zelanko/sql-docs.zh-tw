---
title: SQLNumResultCols 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNumResultCols
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLNumResultCols
helpviewer_keywords:
- SQLNumResultCols function [ODBC]
ms.assetid: d863179f-12a9-4b55-ac6b-7d84202d3da3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43c7f72869cf46fa12f942a3d31399cf3e316520
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343554"
---
# <a name="sqlnumresultcols-function"></a>SQLNumResultCols 函數
**標準**  
 引進的版本:ODBC 1.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLNumResultCols**會傳回結果集內的資料行數目。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLNumResultCols(  
     SQLHSTMT        StatementHandle,  
     SQLSMALLINT *   ColumnCountPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *ColumnCountPtr*  
 輸出要在其中傳回結果集中之資料行數目的緩衝區指標。 此計數不包含系結的書簽資料行。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLNumResultCols**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫 SQLGetDiagRec HandleType Handletype 來和  *StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。  下表列出**SQLNumResultCols**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|08S01|通訊連結失敗|在函式完成處理之前, 驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|作業已取消|已啟用*StatementHandle*的非同步處理。 已呼叫函式, 在完成執行之前, 會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** ;然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式, 並在完成執行之前, 從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|(DM) 已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLNumResultsCols**函數時, 這個非同步函式仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** , 並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前, 會呼叫這個函式。<br /><br /> (DM) 在呼叫*StatementHandle*的**SQLPrepare**或**SQLExecDirect**之前, 已呼叫過函數。<br /><br /> (DM) 已針對*StatementHandle*呼叫非同步執行的函式 (而非這個函式), 而且在呼叫這個函數時仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。<br /><br /> 如需何時可以釋放語句控制碼的詳細資訊, 請參閱[SQLPrepare 函數](../../../odbc/reference/syntax/sqlprepare-function.md)。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時, 就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING, 而且如果啟用通知模式, 則必須在控制碼上呼叫**SQLCompleteAsync** , 才能執行後置處理並完成作業。|  
  
 視資料來源評估 SQL 語句的時間而定, **SQLNumResultCols**可能會傳回**SQLPrepare**或**SQLExecute**在**SQLPrepare**和**SQLExecute**之前所能傳回的任何 SQLSTATE與語句相關聯的。  
  
## <a name="comments"></a>註解  
 只有當語句處於準備、執行或定位狀態時, 才能成功呼叫**SQLNumResultCols** 。  
  
 如果與*StatementHandle*相關聯的語句不會傳回資料行, **SQLNumResultCols**會將 **ColumnCountPtr*設定為0。  
  
 **SQLNumResultCols**所傳回的資料行數目與 IRD 的 SQL_DESC_COUNT 欄位具有相同的值。  
  
 如需詳細資訊, 請參閱[Was 是否已建立結果集？](../../../odbc/reference/develop-app/was-a-result-set-created.md)和[如何使用中繼資料？](../../../odbc/reference/develop-app/how-is-metadata-used.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集中資料行的相關資訊|[SQLColAttribute 函式](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|傳回結果集中資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|正在提取部分或所有資料行|[SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|準備要執行的 SQL 語句|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定資料指標滾動選項|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
