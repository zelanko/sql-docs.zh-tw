---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e312bcbc6efcb96ff02657b98034f0340ae377dc
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345181"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 函數
**標準**  
 引進的版本:ODBC 3.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLFreeHandle**會釋出與特定環境、連接、語句或描述項控制碼相關聯的資源。  
  
> [!NOTE]
>  此函式是用來釋放控制碼的泛型函式。 它會取代 ODBC 2.0 函數**SQLFreeConnect** (用於釋放連接控制碼) 和**SQLFreeEnv** (用於釋放環境控制碼)。 **SQLFreeConnect**和**SQLFreeEnv**在 ODBC 3.x 中都已  被取代。 **SQLFreeHandle**也會取代 ODBC 2.0 函數**SQLFREESTMT** (使用 SQL_DROP*選項*) 來釋放語句控制碼。 如需詳細資訊, 請參閱「批註」。 如需 ODBC 3.x 應用程式與 ODBC 2.x 驅動程式搭配使用時, 驅動  程式管理員將此函式對應至哪個  功能的詳細資訊, 請參閱對應取代函式[以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 源要由**SQLFreeHandle**釋放的控制碼類型。 必須是下列其中一個值:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 控制碼僅供驅動程式管理員和驅動程式使用。 應用程式不應使用此控制碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊, 請參閱[在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 如果*HandleType*不是這些值的其中一個, **SQLFREEHANDLE**會傳回 SQL_INVALID_HANDLE。  
  
 *Handle*  
 源要釋放的控制碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
 如果**SQLFreeHandle**傳回 SQL_ERROR, 控制碼仍然有效。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFreeHandle**傳回 SQL_ERROR 時, 可能會從**SQLFreeHandle**嘗試釋放的控制碼的診斷資料結構中取得相關聯的 SQLSTATE 值, 但無法取得。 下表列出通常由**SQLFreeHandle**所傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|說明|  
|--------------|-----------|-----------------|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|(DM) *HandleType*引數已 SQL_HANDLE_ENV, 且至少有一個連接處於已配置或已連線的狀態。 必須先針對每個連接呼叫具有*HANDLETYPE* SQL_HANDLE_DBC 的**SQLDisconnect**和**SQLFreeHandle** , 才能  呼叫 SQLFreeHandle HandleType  SQL_HANDLE_ENV。<br /><br /> (DM) *HandleType*引數已 SQL_HANDLE_DBC, 且在呼叫**SQLDisconnect**以進行連線之前已呼叫過函數。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_DBC。 以*控制碼*呼叫非同步執行的函式, 而且呼叫此函式時, 函數仍在執行中。<br /><br /> (DM) *HandleType*引數為 handletype 來。 使用語句控制碼呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。<br /><br /> (DM) *HandleType*引數為 handletype 來。 在語句控制碼或相關聯的連接控制碼上呼叫非同步執行的函式, 而且呼叫此函式時, 函數仍在執行中。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_DESC。 在相關聯的連接控制碼上呼叫了非同步執行的函式;呼叫這個函式時, 函數仍在執行。<br /><br /> (DM) 在呼叫**SQLFreeHandle**之前, 不會釋放所有子公司控制碼和其他資源。<br /><br /> 已針對與*控制碼*相關聯的其中一個語句控制碼呼叫 (DM) **SQLExecute**、 **SQLExecDirect**或**SQLMORERESULTS** , 而*HandleType*已設定為 handletype 來或 SQL_HANDLE_DESC 傳回 SQL_PARAM_DATA_只有. 在抓取所有資料流程參數的資料之前, 會呼叫這個函式。|  
|HY013|記憶體管理錯誤|*HandleType*引數是 HANDLETYPE 來或 SQL_HANDLE_DESC, 而且無法處理函式呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY017|使用自動設定的描述項控制碼不正確。|(DM) *handle*引數已設定為自動設定描述元的控制碼。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) *HandleType*引數是 SQL_HANDLE_DESC, 而驅動程式是 ODBC 2.x 驅動  程式。<br /><br /> (DM) *HandleType*引數是 handletype 來, 而驅動程式不是有效的 ODBC 驅動程式。|  
  
## <a name="comments"></a>註解  
 **SQLFreeHandle**是用來釋放環境、連接、語句和描述元的控制碼, 如下列各節所述。 如需控制碼的一般資訊, 請參閱[控制碼](../../../odbc/reference/develop-app/handles.md)。  
  
 應用程式在釋放之後, 不應該使用控制碼;驅動程式管理員不會檢查函式呼叫中控制碼的有效性。  
  
## <a name="freeing-an-environment-handle"></a>釋放環境控制碼  
 在呼叫具有*HANDLETYPE* SQL_HANDLE_ENV 的**SQLFreeHandle**之前, 應用程式必須針對環境中配置的所有連線, 使用 HandleType *SQL_HANDLE_DBC*呼叫**SQLFreeHandle** 。 否則, 對**SQLFreeHandle**的呼叫會傳回 SQL_ERROR, 而環境和任何使用中的連接仍然有效。 如需詳細資訊, 請參閱[環境控制碼](../../../odbc/reference/develop-app/environment-handles.md)和配置[環境控制碼](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 如果環境是共用環境, 則呼叫具有*HANDLETYPE* SQL_HANDLE_ENV 之**SQLFreeHandle**的應用程式在呼叫之後就不再具有環境的存取權, 但不一定會釋放環境的資源。 **SQLFreeHandle**的呼叫會遞減環境的參考計數。 參考計數是由驅動程式管理員維護。 如果沒有到達零, 就不會釋放共用的環境, 因為它仍由另一個元件使用中。 如果參考計數達到零, 則會釋放共用環境的資源。  
  
## <a name="freeing-a-connection-handle"></a>釋放連接控制碼  
 在呼叫具有*HANDLETYPE* SQL_HANDLE_DBC 的**SQLFreeHandle**之前, 如果此控制碼上有連接, 應用程式必須呼叫**SQLDisconnect**以取得連接 *。* 否則, 對**SQLFreeHandle**的呼叫會傳回 SQL_ERROR, 且連接仍然有效。  
  
 如需詳細資訊, 請參閱[連接控制碼](../../../odbc/reference/develop-app/connection-handles.md)和[從資料來源或驅動程式中斷](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)連線。  
  
## <a name="freeing-a-statement-handle"></a>釋放陳述式控制代碼  
 呼叫*HandleType*為 Handletype 來的**SQLFreeHandle** , 會釋出**SQLAllocHandle**與 HandleType handletype 來的呼叫所配置的所有資源。  當應用程式呼叫**SQLFreeHandle**來釋放具有暫止結果的語句時, 就會刪除暫止的結果。 當應用程式釋放語句控制碼時, 驅動程式會釋放與該控制碼相關聯的四個自動設定描述元。 如需詳細資訊, 請參閱[語句控制碼](../../../odbc/reference/develop-app/statement-handles.md)和[釋放語句控制碼](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 請注意, **SQLDisconnect**會自動卸載在連接上開啟的任何語句和描述項。  
  
## <a name="freeing-a-descriptor-handle"></a>釋放描述項控制碼  
 呼叫*HandleType*為 SQL_HANDLE_DESC 的**SQLFreeHandle**會釋出*控制碼*中的描述項控制碼。 對**SQLFreeHandle**的呼叫不會釋出應用程式所配置的任何記憶體, 這些是由任何描述項記錄的*指標欄位 (包括 SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR) 所參考。控制碼*。 釋放控制碼時, 會釋出驅動程式所配置的記憶體給不是指標欄位的欄位。 釋放使用者配置的描述項控制碼時, 已與釋放的控制碼相關聯的所有語句都會還原為各自自動設定的描述項控制碼。  
  
> [!NOTE]
>  ODBC 2.x  驅動程式不支援釋放描述項控制碼, 就如同它們不支援配置描述項控制碼一樣。  
  
 請注意, **SQLDisconnect**會自動卸載在連接上開啟的任何語句和描述項。 當應用程式釋放語句控制碼時, 驅動程式會釋出所有與該控制碼相關聯的自動產生描述元。  
  
 如需描述項的詳細資訊, 請參閱[描述](../../../odbc/reference/develop-app/descriptors.md)元。  
  
## <a name="code-example"></a>程式碼範例  
 如需其他程式碼範例, 請參閱[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)和[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
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
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消語句處理|[SQLCance Functionl](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
