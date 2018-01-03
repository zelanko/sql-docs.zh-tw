---
title: "SQLFreeStmt 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLFreeStmt
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLFreeStmt
helpviewer_keywords: SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d758d7ec03a7d67e7f943a01d19c4959aa18bc9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLFreeStmt**停止的特定陳述式相關聯的處理、 關閉任何開啟的資料指標相關聯的陳述式，捨棄暫止的結果，或選擇性地釋放陳述式控制代碼相關聯的所有資源。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼  
  
 *選項*  
 [輸入]下列選項之一：  
  
 SQL_ 關閉： 關閉資料指標相關聯*StatementHandle* （如果已定義），並捨棄所有擱置的結果。 應用程式可以稍後重新開啟這個資料指標執行**選取**再次以相同或不同的參數值的陳述式。 如果任何資料指標開啟時，這個選項就會有任何作用，應用程式。 **SQLCloseCursor**也可以呼叫來關閉資料指標。 如需詳細資訊，請參閱[關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 SQL_DROP： 此選項已被取代。 呼叫**SQLFreeStmt**與*選項*SQL_DROP 的會對應到在驅動程式管理員[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
 SQL_UNBIND： 設定為 0，ARD 釋放所有的資料行緩衝區的 SQL_DESC_COUNT 欄位所繫結**SQLBindCol**針對給定*StatementHandle*。 這不會解除繫結的書籤資料行;若要這樣做，請 ARD 書籤資料行的 SQL_DESC_DATA_PTR 欄位設為 NULL。 請注意，是否共用的多個陳述式的明確配置描述項上執行這項作業，則作業會影響所有共用的描述元的陳述式的繫結。 如需詳細資訊，請參閱[概觀的擷取結果 （基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 SQL_RESET_PARAMS： 將 APD SQL_DESC_COUNT 欄位設定為 0，釋出所有所設定的參數緩衝區**SQLBindParameter**針對給定*StatementHandle*。 如果共用的多個陳述式的明確配置描述項上執行這項作業，則這項作業會影響之共用的描述元的所有陳述式的繫結。 如需詳細資訊，請參閱[繫結參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFreeStmt**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLFreeStmt** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLFreeStmt**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫與*選項*設定為 SQL_RESET_PARAMS，擷取資料的所有資料流處理的參數。<br /><br /> 以非同步方式執行的函式的呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY092|選項類型超出範圍|(DM) 指定的引數的值*選項*不是：<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 呼叫**SQLFreeStmt** SQL_CLOSE 選項是相當於呼叫**SQLCloseCursor**，不同之處在於**SQLFreeStmt**與 SQL_CLOSE 不會影響應用程式如果任何資料指標不是，開啟的陳述式上。 如果任何資料指標不為開啟，請呼叫**SQLCloseCursor**傳回 SQLSTATE 24000 （無效的資料指標狀態）。  
  
 應用程式不應該使用陳述式控制代碼之後釋出。驅動程式管理員不會檢查函式呼叫中的控制代碼的有效性。  
  
## <a name="example"></a>範例  
 它是良好的程式設計作法，以釋放控制代碼。 不過，為了簡單起見，下列範例不包含程式碼，可釋放已配置的控制代碼。 如需如何釋放控制代碼的範例，請參閱[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
```  
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
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|關閉資料指標|[SQLCloseCursor 函式](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|釋放控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
