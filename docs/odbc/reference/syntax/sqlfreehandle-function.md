---
description: SQLFreeHandle 函數
title: SQLFreeHandle 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeHandle
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
ms.assetid: 17a6fcdc-b05a-4de7-be93-a316f39696a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e90be541b73e0a5fefb7a082bad27f29c3a6d2a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491269"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 函數
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLFreeHandle** 會釋出與特定環境、連接、語句或描述項控制碼相關聯的資源。  
  
> [!NOTE]
>  這個函式是用來釋放控制碼的泛型函數。 它取代了 ODBC 2.0 函式 **SQLFreeConnect** (來釋出連接控制碼) 和 **SQLFreeEnv** (釋放環境控制碼) 。 **SQLFreeConnect**和**SQLFreeEnv**都已在 ODBC 3.x 中*淘汰。* **SQLFreeHandle** 也會將 ODBC 2.0 函數 **SQLFreeStmt** (取代為釋放語句控制碼) 的 SQL_DROP *選項* 。 如需詳細資訊，請參閱「批註」。 如需當 ODBC 3.x 應用程式與 ODBC 2.x*驅動程式搭配*使用時，驅動程式管理員會將此函式對應 *.x*至的詳細資訊，請參閱對應取代函式[以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 輸出要由 **SQLFreeHandle**釋放的控制碼類型。 必須為下列其中一個值：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 控制碼只能由驅動程式管理員和驅動程式使用。 應用程式不應該使用這個控制碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱 [在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 如果 *HandleType* 不是下列其中一個值，則 **SQLFreeHandle** 會傳回 SQL_INVALID_HANDLE。  
  
 *Handle*  
 輸出要釋放的控制碼。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
 如果 **SQLFreeHandle** 傳回 SQL_ERROR，控制碼仍然有效。  
  
## <a name="diagnostics"></a>診斷  
 當 **SQLFreeHandle** 傳回 SQL_ERROR 時，可能會從 **SQLFreeHandle** 嘗試釋放但無法釋放之控制碼的診斷資料結構取得相關聯的 SQLSTATE 值。 下表列出 **SQLFreeHandle** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤| (DM) *HandleType* 引數是 SQL_HANDLE_ENV 的，而且至少有一個連線處於已配置或已線上狀態。 您必須針對每個*HandleType*連接呼叫**SQLDisconnect**和 SQL_HANDLE_DBC **SQLFreeHandle** ，才能呼叫*HandleType*為 SQL_HANDLE_ENV 的**SQLFreeHandle** 。<br /><br />  (DM) *HandleType* 引數是 SQL_HANDLE_DBC 的，而且在呼叫 **SQLDisconnect** 以進行連接之前，會呼叫此函數。<br /><br />  (DM) *HandleType* 引數是 SQL_HANDLE_DBC 的。 以非同步方式執行的函式是以 *控制碼* 呼叫，且函式在呼叫此函式時仍在執行中。<br /><br />  (DM) *HandleType* 引數是 SQL_HANDLE_STMT 的。 **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或 **SQLSetPos** 是利用語句控制碼來呼叫，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) *HandleType* 引數是 SQL_HANDLE_STMT 的。 在語句控制碼或相關聯的連接控制碼上呼叫非同步執行的函式，但呼叫這個函式時，函式仍在執行中。<br /><br />  (DM) *HandleType* 引數是 SQL_HANDLE_DESC 的。 在相關聯的連接控制碼上呼叫非同步執行的函式;而且函式在呼叫此函式時仍在執行中。<br /><br />  (DM) 在呼叫 **SQLFreeHandle** 之前，不會釋放所有的子公司控制碼和其他資源。<br /><br />  (DM) **SQLExecute**、 **SQLExecDirect**或 **SQLMoreResults** 與 *控制碼* 相關聯的其中一個語句控制碼，而且 *HandleType* 設定為 SQL_HANDLE_STMT，或 SQL_HANDLE_DESC 傳回的 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|*HandleType*引數 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，而且無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY017|使用自動設定的描述項控制碼無效。| (DM) *控制碼* 引數已設定為自動設定的描述項的控制碼。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) *HandleType* 引數是 SQL_HANDLE_DESC 的，而且*驅動程式是 ODBC 2.x 驅動程式* 。<br /><br />  (DM) *HandleType* 引數是 SQL_HANDLE_STMT 的，而驅動程式並不是有效的 ODBC 驅動程式。|  
  
## <a name="comments"></a>註解  
 **SQLFreeHandle** 可用來釋放環境、連接、語句和描述項的控制碼，如下列各節所述。 如需控制碼的一般資訊，請參閱 [控制碼](../../../odbc/reference/develop-app/handles.md)。  
  
 應用程式在釋放後不應使用控制碼;驅動程式管理員不會檢查函式呼叫中控制碼的有效性。  
  
## <a name="freeing-an-environment-handle"></a>釋放環境控制碼  
 在使用 SQL_HANDLE_ENV *HandleType*呼叫**SQLFreeHandle**之前，應用程式必須針對在環境下配置的所有連線，呼叫**SQLFreeHandle**和*HandleType* SQL_HANDLE_DBC。 否則，對 **SQLFreeHandle** 的呼叫會傳回 SQL_ERROR，且環境和任何使用中的連接都會保持有效。 如需詳細資訊，請參閱 [環境](../../../odbc/reference/develop-app/environment-handles.md) 控制碼和配置 [環境控制碼](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 如果環境是共用的環境，以*HandleType*的 SQL_HANDLE_ENV 呼叫**SQLFreeHandle**的應用程式在呼叫之後將不再具有環境的存取權，但不一定會釋放環境的資源。 對 **SQLFreeHandle** 的呼叫會遞減環境的參考計數。 參考計數由驅動程式管理員維護。 如果未達到零，就不會釋放共用環境，因為另一個元件仍在使用它。 如果參考計數到達零，則會釋放共用環境的資源。  
  
## <a name="freeing-a-connection-handle"></a>釋放連接控制碼  
 當這個控制碼上有連接時，應用程式必須呼叫**SQLDisconnect**進行連接，然後再以 SQL_HANDLE_DBC 的*HandleType*呼叫**SQLFreeHandle** *。* 否則，呼叫 **SQLFreeHandle** 會傳回 SQL_ERROR，且連接會保持有效。  
  
 如需詳細資訊，請參閱 [連接控制碼](../../../odbc/reference/develop-app/connection-handles.md) 和 [從資料來源或驅動程式中斷](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)連接。  
  
## <a name="freeing-a-statement-handle"></a>釋放陳述式控制代碼  
 以 SQL_HANDLE_STMT 的*HandleType*呼叫**SQLFreeHandle** ，會釋出呼叫**SQLAllocHandle**的所有資源（ *HandleType*為 SQL_HANDLE_STMT）。 當應用程式呼叫 **SQLFreeHandle** 來釋放具有暫止結果的語句時，就會刪除暫止的結果。 當應用程式釋放語句控制碼時，驅動程式會釋放與該控制碼相關聯的四個自動設定的描述項。 如需詳細資訊，請參閱 [語句](../../../odbc/reference/develop-app/statement-handles.md) 控制碼和 [釋放語句控制碼](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 請注意， **SQLDisconnect** 會自動卸載在連接上開啟的任何語句和描述項。  
  
## <a name="freeing-a-descriptor-handle"></a>釋放描述項控制碼  
 以 SQL_HANDLE_DESC 的*HandleType*呼叫**SQLFreeHandle**會釋放*控制碼*中的描述項控制碼。 對 **SQLFreeHandle** 的呼叫不會釋放由指標欄位所參考之應用程式所配置的任何記憶體 (包括 *控制碼*之任何描述項記錄的 SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR) 。 釋放控制碼時，驅動程式針對非指標欄位所配置的記憶體會釋放。 當使用者配置的描述項控制碼釋出時，已釋放的控制碼相關聯的所有語句都會還原為各自自動設定的描述項控制碼。  
  
> [!NOTE]
>  ODBC 2.x*驅動程式* 不支援釋放描述項控制碼，因為它們不支援配置描述項控制碼。  
  
 請注意， **SQLDisconnect** 會自動卸載在連接上開啟的任何語句和描述項。 當應用程式釋放語句控制碼時，驅動程式會釋出與該控制碼相關聯的所有自動產生的描述項。  
  
 如需描述項的詳細資訊，請參閱 [描述](../../../odbc/reference/develop-app/descriptors.md)項。  
  
## <a name="code-example"></a>程式碼範例  
 如需其他程式碼範例，請參閱 [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) 和 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
### <a name="code"></a>程式碼  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消語句處理|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
