---
title: SQLFreeHandle 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f63af414d59afed2bbe2e8eed3fba7a1362bb4bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061476"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 函數
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLFreeHandle**釋出與特定的環境、 連接、 陳述式或描述元控制代碼相關聯的資源。  
  
> [!NOTE]
>  此函式會釋放控制代碼的泛型函式。 它會取代 ODBC 2.0 函式**SQLFreeConnect** （適用於釋放連接控制代碼） 及**SQLFreeEnv** （適用於釋放環境控制代碼）。 **SQLFreeConnect**並**SQLFreeEnv**都不再支援的 ODBC 3 *.x*。 **SQLFreeHandle**也會取代 ODBC 2.0 函式**SQLFreeStmt** (使用 SQL_DROP*選項*) 釋放陳述式控制代碼。 如需詳細資訊，請參閱 「 註解。 」 如需有關什麼驅動程式管理員會對應到此函式時 ODBC 3 *.x*應用程式正在使用的 ODBC 2 *.x*驅動程式，請參閱[對應為向後取代函式應用程式的相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]若要釋放的控制代碼的型別**SQLFreeHandle**。 必須是下列值之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 只在驅動程式管理員和驅動程式會使用 SQL_HANDLE_DBC_INFO_TOKEN 控制代碼。 應用程式不應使用此控制代碼型別。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 如果*HandleType*不是其中一個值， **SQLFreeHandle**傳回 SQL_INVALID_HANDLE。  
  
 *Handle*  
 [輸入]要釋放控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
 如果**SQLFreeHandle**傳回 SQL_ERROR，控制代碼是否仍然有效。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFreeHandle**會傳回 SQL_ERROR，相關聯的 SQLSTATE 值可能取自之診斷的資料結構的控制代碼所**SQLFreeHandle**嘗試免費，但無法。 下表列出通常所傳回的 SQLSTATE 值**SQLFreeHandle** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) *HandleType*引數為 SQL_HANDLE_ENV，和至少一個連線處於已配置或已連線狀態。 **SQLDisconnect**並**SQLFreeHandle**具有*HandleType*利用 SQL_HANDLE_DBC 的必須呼叫每個連線，然後再呼叫**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_ENV。<br /><br /> (DM) *HandleType*引數是利用 SQL_HANDLE_DBC，和呼叫的函式呼叫之前，先**SQLDisconnect**連接。<br /><br /> (DM) *HandleType*引數是利用 SQL_HANDLE_DBC。 以非同步方式執行的函式呼叫與*處理*和函式仍執行時呼叫此函式。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_STMT。 **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**且已使用陳述式控制代碼呼叫和傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_STMT。 陳述式控制代碼上或在相關聯的連接控制代碼上呼叫以非同步方式執行的函式和函式仍執行時呼叫此函式。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_DESC。 以非同步方式執行的函式呼叫相關聯的連接控制代碼;和函式仍執行時呼叫此函式。<br /><br /> (DM) 所有分公司的控制代碼和其他資源就不會釋放之前**SQLFreeHandle**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對其中一個相關聯的陳述式控制代碼呼叫*處理*並*HandleType*已設定為 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC 傳回 SQL_PARAM_DATA_AVAILABLE。 資料已擷取所有的資料流參數前呼叫此函式。|  
|HY013|記憶體管理錯誤|*HandleType*引數為 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，以及無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY017|使用自動配置描述項控制代碼無效。|(DM)*處理*引數設定為自動配置描述項控制代碼。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) *HandleType*引數是 SQL_HANDLE_DESC，且驅動程式的 ODBC 2 *.x*驅動程式。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_STMT，和驅動程式不是有效的 ODBC 驅動程式。|  
  
## <a name="comments"></a>註解  
 **SQLFreeHandle**用來釋放控制代碼的環境、 連接、 陳述式，以及描述元，如下列各節中所述。 如需控制代碼的一般資訊，請參閱[控制代碼](../../../odbc/reference/develop-app/handles.md)。  
  
 釋出; 之後，應用程式不應使用的控制代碼驅動程式管理員不會檢查函式呼叫中的控制代碼的有效性。  
  
## <a name="freeing-an-environment-handle"></a>釋放環境控制代碼  
 它會呼叫之前**SQLFreeHandle**具有*HandleType* SQL_HANDLE_ENV，應用程式必須呼叫**SQLFreeHandle**具有*HandleType*配置的環境下的所有連線的利用 SQL_HANDLE_DBC。 否則，呼叫**SQLFreeHandle**傳回 SQL_ERROR 並在環境中，任何使用中連接仍然有效。 如需詳細資訊，請參閱 <<c0> [ 環境處理](../../../odbc/reference/develop-app/environment-handles.md)並[配置環境處理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 如果環境是共用的環境中，應用程式，會呼叫**SQLFreeHandle**具有*HandleType*利用 SQL_HANDLE_ENV 的不再具有存取權的環境呼叫之後，但環境不一定被釋放資源。 若要在呼叫**SQLFreeHandle**遞減參考計數的環境。 參考計數會維護由驅動程式管理員。 如果它不會到達零，共用的環境不會釋放，因為它仍正由另一個元件。 如果參考計數到達零時，會釋放共用的環境中的資源。  
  
## <a name="freeing-a-connection-handle"></a>釋放連接控制代碼  
 它會呼叫之前**SQLFreeHandle**具有*HandleType*利用 SQL_HANDLE_DBC 的應用程式必須呼叫**SQLDisconnect**如果沒有這個連接的連接處理 *。* 否則，呼叫**SQLFreeHandle**傳回 SQL_ERROR，而且連接會保持有效。  
  
 如需詳細資訊，請參閱 <<c0> [ 連接控制代碼](../../../odbc/reference/develop-app/connection-handles.md)並[中斷資料來源或驅動程式](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="freeing-a-statement-handle"></a>釋放陳述式控制代碼  
 呼叫**SQLFreeHandle**具有*HandleType*利用 SQL_HANDLE_STMT 的釋出所有的呼叫所配置的資源**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_STMT。 當應用程式呼叫**SQLFreeHandle**釋放具有暫止的結果陳述式，會刪除暫止的結果。 當應用程式會釋放陳述式控制代碼時，驅動程式會釋放該控制代碼相關聯的四個自動配置描述元。 如需詳細資訊，請參閱 <<c0> [ 陳述式會處理](../../../odbc/reference/develop-app/statement-handles.md)並[釋放陳述式控制代碼](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 請注意， **SQLDisconnect**會自動在連接上卸除任何陳述式和開啟的描述元。  
  
## <a name="freeing-a-descriptor-handle"></a>釋放描述項控制代碼  
 呼叫**SQLFreeHandle**具有*HandleType* SQL_HANDLE_DESC 的釋放描述項控制代碼，在*處理*。 若要在呼叫**SQLFreeHandle**不會釋放任何可能由指標欄位 （包括 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 參考的應用程式所配置任何記憶體描述項記錄*處理*。 不是指標欄位的欄位的驅動程式所配置的記憶體釋放控制代碼已釋放時。 當使用者配置描述項控制代碼已釋放時，釋放控制代碼必須與相關聯的所有陳述式還原成其各自的自動配置描述項控制代碼。  
  
> [!NOTE]
>  ODBC 2 *.x*驅動程式不會支援釋放描述項控制代碼，就像它們不支援配置描述項控制代碼。  
  
 請注意， **SQLDisconnect**會自動在連接上卸除任何陳述式和開啟的描述元。 當應用程式會釋放陳述式控制代碼時，驅動程式會釋放該控制代碼相關聯的所有自動產生描述元。  
  
 如需描述項的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>程式碼範例  
 如需額外的程式碼範例，請參閱[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)並[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
