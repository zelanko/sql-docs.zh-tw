---
title: "SQLFreeHandle 函數 |Microsoft 文件"
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
apiname: SQLFreeHandle
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLFreeHandle
helpviewer_keywords: SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 96f6d2c94a6b2fb78245c83cbf989e6a707caccc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLFreeHandle**釋出特定的環境、 連接、 陳述式或描述項控制代碼相關聯的資源。  
  
> [!NOTE]  
>  此函式會釋放控制代碼的泛型函式。 它會取代 ODBC 2.0 函式**SQLFreeConnect** （適用於釋放連接控制代碼） 和**SQLFreeEnv** （適用於釋放環境控制代碼）。 **SQLFreeConnect**和**SQLFreeEnv**都不再支援的 ODBC 3*.x*。 **SQLFreeHandle**也會取代 ODBC 2.0 函式**SQLFreeStmt** (與 SQL_DROP*選項*) 釋放陳述式控制代碼。 如需詳細資訊，請參閱 「 註解。 」 如需有關什麼驅動程式管理員會對應到此函式時 ODBC 3*.x*應用程式使用 ODBC 2*.x*驅動程式，請參閱[向後的對應取代函式應用程式的相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]若要釋放的控制代碼的類型**SQLFreeHandle**。 必須是下列值之一：  
  
-   利用 SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   利用 SQL_HANDLE_STMT  
  
 只在驅動程式管理員和驅動程式會使用 SQL_HANDLE_DBC_INFO_TOKEN 控制代碼。 應用程式不應該使用此控制代碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[開發 ODBC 驅動程式中的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 如果*HandleType*不是其中一個值， **SQLFreeHandle**傳回 SQL_INVALID_HANDLE。  
  
 *Handle*  
 [輸入]要釋放控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
 如果**SQLFreeHandle**傳回 SQL_ERROR，控制代碼是否仍然有效。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFreeHandle**傳回 SQL_ERROR，相關聯的 SQLSTATE 值可以取自控制代碼的診斷資料結構， **SQLFreeHandle**嘗試釋出，但不是可以。 下表列出通常所傳回的 SQLSTATE 值**SQLFreeHandle** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) *HandleType*引數為 SQL_HANDLE_ENV，和至少一個連接是在配置或已連線的狀態。 **SQLDisconnect**和**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_DBC 的必須呼叫每個連線然後再呼叫**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_ENV。<br /><br /> (DM) *HandleType*引數以前是利用 SQL_HANDLE_DBC，並會在呼叫之前已呼叫此函式**SQLDisconnect**連接。<br /><br /> (DM) *HandleType*引數以前是利用 SQL_HANDLE_DBC。 以非同步方式執行的函式呼叫與*處理*和函式還在執行時呼叫此函式。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_STMT。 **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**已使用陳述式控制代碼呼叫，並且傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_STMT。 陳述式控制代碼或相關聯的連接控制代碼上呼叫非同步執行的函式和函式還在執行時呼叫此函式。<br /><br /> (DM) *HandleType*引數以前是 SQL_HANDLE_DESC。 以非同步方式執行的函式呼叫相關聯的連接控制代碼。和函式還在執行時呼叫此函式。<br /><br /> (DM) 所有附屬的控制代碼和其他資源並未釋放之前**SQLFreeHandle**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**呼叫其中一個相關聯的陳述式控制代碼*處理*和*HandleType*已設定為 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC 傳回 SQL_PARAM_DATA_AVAILABLE。 此函式呼叫之前的所有資料流處理的參數擷取資料。|  
|HY013|記憶體管理錯誤|*HandleType*引數是 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，和因為基礎記憶體的物件無法存取，可能是因為記憶體不足，無法處理函式呼叫。|  
|HY017|使用自動配置描述項控制代碼無效。|(DM)*處理*引數設定為自動配置描述項的控制代碼。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) *HandleType*引數是 SQL_HANDLE_DESC，且驅動程式的 ODBC 2*.x*驅動程式。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_STMT，且驅動程式不是有效的 ODBC 驅動程式。|  
  
## <a name="comments"></a>註解  
 **SQLFreeHandle**用來釋放控制代碼的環境、 連接、 陳述式，以及描述元，如下列各節中所述。 如需控制代碼的一般資訊，請參閱[控點](../../../odbc/reference/develop-app/handles.md)。  
  
 應用程式不應該使用的控制代碼之後釋出。驅動程式管理員不會檢查函式呼叫中的控制代碼的有效性。  
  
## <a name="freeing-an-environment-handle"></a>釋放環境控制代碼  
 它會呼叫之前**SQLFreeHandle**與*HandleType* SQL_HANDLE_ENV 的應用程式必須呼叫**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_DBC 的配置環境下的所有連線。 否則，呼叫**SQLFreeHandle**傳回 SQL_ERROR 並在環境中，任何使用中連接仍然有效。 如需詳細資訊，請參閱[環境處理](../../../odbc/reference/develop-app/environment-handles.md)和[配置環境處理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 如果環境是共用的環境，應用程式呼叫**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_ENV 的不再擁有呼叫之後，環境，但環境的存取不一定釋放資源。 若要呼叫**SQLFreeHandle**遞減參考計數的環境。 參考計數會維護由驅動程式管理員。 它不會達到零，如果共用的環境不會釋放，因為仍由其他元件所使用。 如果參考計數達到零時，會釋放資源的共用的環境。  
  
## <a name="freeing-a-connection-handle"></a>釋放連接控制代碼  
 它會呼叫之前**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_DBC 的應用程式必須呼叫**SQLDisconnect**如果沒有這個連接的連接處理*。* 否則，呼叫**SQLFreeHandle**傳回 SQL_ERROR，而且連接會保持有效。  
  
 如需詳細資訊，請參閱[連接控制代碼](../../../odbc/reference/develop-app/connection-handles.md)和[中斷資料來源或驅動程式](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="freeing-a-statement-handle"></a>釋放陳述式控制代碼  
 呼叫**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_STMT 的釋出所有的資源所配置的呼叫**SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_STMT。 當應用程式呼叫**SQLFreeHandle**來釋放陳述式具有擱置的結果，會刪除暫止的結果。 當應用程式會釋放陳述式控制代碼時，驅動程式會釋放該控制代碼相關聯的四個自動配置描述元。 如需詳細資訊，請參閱[陳述式會處理](../../../odbc/reference/develop-app/statement-handles.md)和[釋放陳述式控制代碼](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 請注意， **SQLDisconnect**會自動在連接上卸除任何陳述式與開啟的描述。  
  
## <a name="freeing-a-descriptor-handle"></a>釋放的描述項控制代碼  
 呼叫**SQLFreeHandle**與*HandleType* SQL_HANDLE_DESC 的釋放中的描述項控制代碼*處理*。 若要呼叫**SQLFreeHandle**不會釋放任何可能由指標欄位 （包括 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 參考的應用程式所配置任何記憶體描述項記錄的*處理*。 非指標欄位的欄位的驅動程式所配置的記憶體釋放控制代碼已釋放時。 當使用者配置描述項控制代碼已釋放時，釋放控制代碼必須與相關聯的所有陳述式會還原成其各自的自動配置描述項控制代碼。  
  
> [!NOTE]  
>  ODBC 2*.x*驅動程式不會支援釋放描述項控制代碼，就如同它們不支援配置描述項控制代碼。  
  
 請注意， **SQLDisconnect**會自動在連接上卸除任何陳述式與開啟的描述。 當應用程式會釋放陳述式控制代碼時，驅動程式會釋放該控制代碼相關聯的所有自動產生描述元。  
  
 如需描述元的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>程式碼範例  
 如需額外的程式碼範例，請參閱[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)和[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
### <a name="code"></a>程式碼  
  
```  
// SQLFreeHandle.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <stdio.h>  
  
int main() {  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   // Initialize the environment, connection, statement handles.  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   // Allocate the environment.  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set environment attributes.  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
  
   // Allocate the connection.  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Set the login timeout.  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
  
   // Let the user select the data source and connect to the database.  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Free handles, and disconnect.     
   if (hstmt) {   
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
      hstmt = NULL;   
   }  
   if (hdbc) {   
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      hdbc = NULL;   
   }  
   if (henv) {   
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
      henv = NULL;   
   }  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消陳述式處理|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
