---
title: SQLCloseCursor 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef336a4deb734c0e44f9c15ae7f9faf0dcb32d93
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343152"
---
# <a name="sqlclosecursor-function"></a>SQLCloseCursor 函式
**標準**  
 引進的版本:ODBC 3.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLCloseCursor**會關閉已在語句上開啟的資料指標, 並捨棄暫止的結果。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCloseCursor**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫 SQLGetDiagRec 和 HandleType 的  Handletype 來和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。  下表列出**SQLCloseCursor**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|說明|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|24000|指標狀態無效|*StatementHandle*上沒有開啟的資料指標。 (這只會由 ODBC 3 傳回。*x*驅動程式)。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|(DM) 已針對與*StatementHandle*相關聯的連接控制碼呼叫非同步執行的函式, 且在呼叫這個函數時仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫非同步執行的函式, 且在呼叫此函式時仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*StatementHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 如果未開啟任何資料指標, **SQLCloseCursor**會傳回 SQLSTATE 24000 (不正確資料指標狀態)。 呼叫**SQLCloseCursor**相當於使用 SQL_CLOSE 選項呼叫**SQLFreeStmt** , 但如果語句上未開啟任何資料指標,  **則 SQLFreeStmt with SQL_CLOSE 的例外狀況對應用程式沒有任何影響。SQLCloseCursor**會傳回 SQLSTATE 24000 (不正確資料指標狀態)。  
  
> [!NOTE]  
>  如果是 ODBC 3, 則為。使用 ODBC 2 的*x*應用程式。*x*驅動程式在未開啟任何資料指標時呼叫**SQLCloseCursor** , 因為驅動程式管理員會將**SQLCLOSECURSOR**對應至**SQLFreeStmt** with SQL_CLOSE, 所以不會傳回 SQLSTATE 24000 (不正確資料指標狀態)。  
  
 如需詳細資訊, 請參閱[關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)函式和[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|釋放控制碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|處理多個結果集|[SQLMoreResults 函式](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
