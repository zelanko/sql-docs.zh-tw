---
title: SQLFreeStmt 函數 |微軟文件
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e252769c26a5491100094b1243b9c2c6bb67d94d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285698"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLFreeStmt**停止與特定語句關聯的處理,關閉與語句關聯的任何打開的游標,丟棄掛起的結果,或者,可以選擇釋放與語句句柄關聯的所有資源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄  
  
 *選項*  
 [輸入]以下選項之一:  
  
 SQL_關閉:關閉與*語句句柄*關聯的游標(如果已定義),並丟棄所有掛起的結果。 應用程式以後可以通過再次使用相同或不同的參數值執行**SELECT**語句來重新打開此遊標。 如果沒有打開遊標,則此選項對應用程式沒有影響。 也可以調用**SQLCloseCursor**來關閉游標。 有關詳細資訊,請參閱[關閉游標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 SQL_DROP:此選項已棄用。 在驅動程式管理器中對應到**SQLFreeStmt**的呼叫,選項為[SQL_DROP。](../../../odbc/reference/syntax/sqlfreehandle-function.md) *Option*  
  
 SQL_UNBIND:將 ARD 的SQL_DESC_COUNT欄位設置為 0,釋放**SQLBindCol**為給定*語句句柄*綁定的所有列緩衝區。 這不會取消綁定書籤列;因此,不會取消綁定書簽列。為此,書籤列的 ARD SQL_DESC_DATA_PTR欄位設置為 NULL。 請注意,如果此操作對由多個語句共用的顯式分配的描述符執行,則該操作將影響共用描述符的所有語句的綁定。 有關詳細資訊,請參閱[檢索結果概述(基本)](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 SQL_RESET_PARAMS:將 APD 的SQL_DESC_COUNT欄位設置為 0,釋放**SQLBind 參數**為給定*語句句柄*設置的所有參數緩衝區。 如果此操作對由多個語句共享的顯式分配的描述符執行,則此操作將影響共用描述符的所有語句的綁定。 有關詳細資訊,請參閱[連結參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFreeStmt**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_STMT的*句柄類型*和*敘述句柄*。 下表列出了**SQLFreeStmt**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLFreeStmt**時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,使用*Option*設置為SQL_RESET_PARAMS調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數,並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY092|選項類型範圍外|(DM) 為參數*選項*指定的值不是:<br /><br /> SQL_CLOSESQL_DROPSQL_UNBINDSQL_RESET_PARAMS|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 使用SQL_CLOSE選項調用**SQLFreeStmt**等效於調用**SQLCloseCursor,** 只不過,如果語句上未打開游標,則具有SQL_CLOSE的**SQLFreeStmt**不會影響應用程式。 如果未打開遊標,則對**SQLCloseCursor 的**呼叫將返回 SQLSTATE 24000(無效游標狀態)。  
  
 應用程式在釋放語句句柄后不應使用它;驅動程式管理員不檢查函數調用中句柄的有效性。  
  
## <a name="example"></a>範例  
 釋放句柄是一種很好的程式設計實踐。 但是,為簡單起見,以下示例不包括釋放分配的句柄的代碼。 有關如何釋放句柄的範例,請參閱[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
```cpp  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控點|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|關閉游標|[SQLCloseCursor 函式](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|釋放手柄|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|設定游標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
