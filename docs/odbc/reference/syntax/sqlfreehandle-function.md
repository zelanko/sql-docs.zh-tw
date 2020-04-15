---
title: SQLFreeHandle 功能 |微軟文件
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
ms.openlocfilehash: 0b136dec98a19676aa67c78615d8fe931f62aafa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285769"
---
# <a name="sqlfreehandle-function"></a>SQLFreeHandle 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLFreeHandle**釋放與特定環境、連接、語句或描述符句柄關聯的資源。  
  
> [!NOTE]
>  此函數是用於釋放句柄的泛型函數。 它取代了 ODBC 2.0 函數**SQLFreeConnect(** 用於釋放連接句柄)和**SQLFreeEnv(** 用於釋放環境句柄)。 **SQLFreeConnect**和**SQLFreeEnv**都在 ODBC 3 *.x*中棄用。 **SQLFreeHandle**還替換了 ODBC 2.0 函數**SQLFreeStmt(** 使用SQL_DROP*選項*),用於釋放語句句柄。 有關詳細資訊,請參閱"註釋"。 有關驅動程式管理員將此功能映射到 ODBC 3 *.x*應用程式使用 ODBC 2 *.x*驅動程式時的詳細資訊,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFreeHandle(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]要由**SQLFreeHandle**釋放的句柄的類型。 必須為下列其中一個值：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN句柄僅由驅動程式管理器和驅動程式使用。 應用程式不應使用此句柄類型。 有關SQL_HANDLE_DBC_INFO_TOKEN的詳細資訊,請參閱在[ODBC 驅動程式中開發連接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 如果*HandleType*不是這些值之一 **,SQLFreeHandle**將返回SQL_INVALID_HANDLE。  
  
 *Handle*  
 [輸入]要釋放的句柄。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_ERROR或SQL_INVALID_HANDLE。  
  
 如果**SQLFreeHandle**返回SQL_ERROR,則句柄仍然有效。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFreeHandle**返回SQL_ERROR時,可以從**SQLFreeHandle**嘗試釋放但無法釋放的句柄的診斷數據結構中獲取關聯的 SQLSTATE 值。 下表列出了**SQLFreeHandle**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) *HandleType*參數SQL_HANDLE_ENV,並且至少有一個連接處於已分配或連接狀態。 在使用*SQL_HANDLE_ENV的句柄類型*呼叫**SQLFreeHandle**之前,必須為每個連接呼叫具有 SQL_HANDLE_DBC*句柄類型的* **SQLDisconnect**和**SQLFreeHandle。**<br /><br /> (DM) *handleType*參數SQL_HANDLE_DBC,在調用**SQLDisconnect**進行連接之前調用該函數。<br /><br /> (DM)*句柄類型*參數SQL_HANDLE_DBC。 使用*Handle*調用了非同步執行函數,並且調用此函數時該函數仍在執行。<br /><br /> (DM)*句柄類型*參數SQL_HANDLE_STMT。 **SQLExecute、SQLExecDirect、SQLBulk****操作**或**SQLSetPos**被調用語句句柄**SQLExecute**並返回SQL_NEED_DATA。 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM)*句柄類型*參數SQL_HANDLE_STMT。 在語句句柄或關聯的連接句柄上調用了異步執行函數,並且在調用此函數時,該函數仍在執行。<br /><br /> (DM)*句柄類型*參數SQL_HANDLE_DESC。 在關聯的連接句柄上調用了非同步執行函數;調用此函數時,該函數仍在執行。<br /><br /> (DM) 在調用**SQLFreeHandle**之前,未釋放所有輔助句柄和其他資源。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用,其中一個語句句柄與*句柄*和*句柄類型***SQLExecDirect**設置為SQL_HANDLE_STMT或SQL_HANDLE_DESC返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|*HandleType*參數SQL_HANDLE_STMT或SQL_HANDLE_DESC,無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY017|自動分配的描述符句柄的使用無效。|(DM) *Handle*參數已設置為自動分配描述符的句柄。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) *handleType*參數SQL_HANDLE_DESC,驅動程式是 ODBC 2 *.x*驅動程式。<br /><br /> (DM) *HandleType*參數SQL_HANDLE_STMT,驅動程式不是有效的 ODBC 驅動程式。|  
  
## <a name="comments"></a>註解  
 **SQLFreeHandle**用於釋放環境、連接、語句和描述符的句柄,如以下各節所述。 有關句柄的一般資訊,請參閱[句柄](../../../odbc/reference/develop-app/handles.md)。  
  
 應用程式在釋放句柄后不應使用句柄;驅動程式管理員不檢查函數調用中句柄的有效性。  
  
## <a name="freeing-an-environment-handle"></a>釋放環境句柄  
 在使用*SQL_HANDLE_ENV的句柄類型*調用**SQLFreeHandle**之前,應用程式必須調用**SQLFreeHandle,** 該*句柄具有*SQL_HANDLE_DBC的句柄類型,用於環境下分配的所有連接。 否則,對**SQLFreeHandle 的**調用將返回SQL_ERROR和環境,並且任何活動連接都仍然有效。 有關詳細資訊,請參閱[環境句柄](../../../odbc/reference/develop-app/environment-handles.md)和[分配環境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 如果環境是共享環境,則使用*handletype*調用**SQLFreeHandle**的應用程式SQL_HANDLE_ENV調用後不再有權訪問環境,但環境的資源不一定被釋放。 對**SQLFreeHandle 的**呼叫會取消環境的引用計數。 引用計數由驅動程式管理器維護。 如果未達到零,則不會釋放共享環境,因為它仍被另一個元件使用。 如果引用計數達到零,則釋放共享環境的資源。  
  
## <a name="freeing-a-connection-handle"></a>釋放連接句柄  
 在使用 *「 句柄類型*SQL_HANDLE_DBC呼叫**SQLFreeHandle**之前,如果此句柄」 上存在連線,則應用程式必須呼叫**SQLDisconnect**連線 *。* 否則,對**SQLFreeHandle 的**調用將返回SQL_ERROR並且連接仍然有效。  
  
 有關詳細資訊,請參閱[連接句柄](../../../odbc/reference/develop-app/connection-handles.md)與[斷開與資料來源或驅動程式](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="freeing-a-statement-handle"></a>釋放陳述式控制代碼  
 使用*句柄類型*SQL_HANDLE_STMT對**SQLFreeHandle**的調用會釋放通過調用**SQLAllocHandle**分配的具有 SQL_HANDLE_STMT*的句柄類型*的所有資源。 當應用程式調用**SQLFreeHandle**以釋放具有掛起結果的語句時,掛起的結果將被刪除。 當應用程式釋放語句句柄時,驅動程式將釋放與該句柄關聯的四個自動分配的描述符。 有關詳細資訊,請參閱[語句句柄](../../../odbc/reference/develop-app/statement-handles.md)和[釋放敘述句柄](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)。  
  
 請注意 **,SQLDisconnect**會自動刪除連接上打開的任何語句和描述符。  
  
## <a name="freeing-a-descriptor-handle"></a>釋放描述符句柄  
 使用*handle 類型的* **SQLFreeHandle**調用SQL_HANDLE_DESC釋放*句柄*中的描述符句柄。 對**SQLFreeHandle 的**呼叫不會釋放應用程式分配的任何記憶體,這些記憶體可能由*句柄*的任何描述元記錄的指標欄位(包括SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR)引用。 釋放句柄時,驅動程式為不是指標欄位的欄位分配的記憶體將被釋放。 釋放使用者分配的描述符句柄時,釋放的句柄與其各自自動分配的描述符句柄關聯的所有語句都恢復到其各自的自動分配描述符句柄。  
  
> [!NOTE]
>  ODBC 2 *.x*驅動程式不支援釋放描述符句柄,就像它們不支援分配描述符句柄一樣。  
  
 請注意 **,SQLDisconnect**會自動刪除連接上打開的任何語句和描述符。 當應用程式釋放語句句柄時,驅動程式將釋放與該句柄關聯的所有自動生成的描述符。  
  
 有關描述符的詳細資訊,請參閱[描述子](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>程式碼範例  
 有關其他代碼示例,請參閱[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)和[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
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
|配置控點|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|解除敘述處理|[SQLCance 函數](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|設定游標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
