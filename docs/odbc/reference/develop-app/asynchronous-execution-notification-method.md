---
title: 非同步執行(通知方法) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e509dad9-5263-4a10-9a4e-03b84b66b6b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 250e71dcb47d44a6e437d12c269ea23fa6fb3c2c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306409"
---
# <a name="asynchronous-execution-notification-method"></a>非同步執行 (通知方法)
ODBC 允許非同步執行連接和語句操作。 應用程式線程可以在非同步模式下調用 ODBC 函數,並且該函數可以在操作完成之前返回,從而允許應用程式線程執行其他任務。 在 Windows 7 SDK 中,對於非同步語句或連接操作,應用程式確定非同步操作是否已完成使用輪詢方法。 有關詳細資訊,請參閱[非同步執行(輪詢方法)。](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md) 從 Windows 8 SDK 開始,可以使用通知方法確定非同步操作是否已完成。  
  
 在輪詢方法中,應用程式每次需要操作的狀態時都需要調用異步函數。 通知方法類似於回調和等待ADO.NET。 但是,ODBC 使用 Win32 事件作為通知物件。  
  
 ODBC 游標庫和 ODBC 同步通知不能同時使用。 設置這兩個屬性將返回 SQLSTATE S1119 的錯誤(無法同時啟用游標庫和非同步通知)。  
  
 有關驅動程式開發人員的資訊[,請參閱非同步功能完成通知](../../../odbc/reference/develop-driver/notification-of-asynchronous-function-completion.md)。  
  
> [!NOTE]  
>  游標庫不支援通知方法。 如果應用程式嘗試在啟用通知方法時通過 SQLSetConnectAttr 啟用游標庫,則會收到錯誤消息。  
  
## <a name="overview"></a>概觀  
 當以非同步模式調用ODBC函數時,控制項將立即返回調用應用程式,返回代碼SQL_STILL_EXECUTING。 應用程式必須重複輪詢函數,直到返回SQL_STILL_EXECUTING以外的內容。 輪詢環路提高了 CPU 利用率,導致許多非同步方案中性能不佳。  
  
 每當使用通知模型時,輪詢模型都會被禁用。 應用程式不應再次調用原始函數。 調用[SQLCompleteAsync 函數](../../../odbc/reference/syntax/sqlcompleteasync-function.md)以完成非同步操作。 如果應用程式在非同步操作完成之前再次調用原始函數,則調用將返回SQL_ERROR SQLSTATE IM017(在非同步通知模式下禁用輪詢)。  
  
 使用通知模型時,應用程式可以調用**SQLCancel**或**SQLCancelHandle**來取消語句或連接操作。 如果取消請求成功,ODBC 將返回SQL_SUCCESS。 此消息不指示該函數實際上已取消;因此,該功能未表示該函數已取消。它表示已處理取消請求。 函數是否實際取消取決於驅動程序和數據源。 當操作被取消時,驅動程式管理員仍將發出事件信號。 驅動程式管理員返回返回代碼緩衝區中的SQL_ERROR,狀態為 SQLSTATE HY008(操作已取消),以指示取消成功。 如果函數完成正常處理,驅動程式管理員將返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO。  
  
### <a name="downlevel-behavior"></a>下級行為  
 ODBC 驅動程式管理員版本支援此通知的完整是 ODBC 3.81。  
  
|應用程式 ODBC 版本|驅動程式管理員版本|驅動程式版本|行為|  
|------------------------------|----------------------------|--------------------|--------------|  
|任何 ODBC 版本的新應用|ODBC 3.81|ODBC 3.80 驅動程式|如果驅動程式支援此功能,應用程式可以使用此功能,否則驅動程式管理器將出錯。|  
|任何 ODBC 版本的新應用|ODBC 3.81|ODBC 前 3.80 驅動程式|如果驅動程式不支援此功能,驅動程式管理器將出錯。|  
|任何 ODBC 版本的新應用|ODBC 前 3.81|任意|當應用程式使用此功能時,舊的驅動程式管理器會將新屬性視為特定於驅動程式的屬性,驅動程式應出錯。新的驅動程式管理員不會將這些屬性傳遞給驅動程式。|  
  
 在使用此功能之前,應用程式應檢查驅動程式管理器版本。 否則,如果編寫不良的驅動程式未出錯,並且驅動程式管理器版本是 ODBC 3.81 前版本,則行為未定義。  
  
## <a name="use-cases"></a>使用案例  
 本節顯示異步執行的用例和輪詢機制。  
  
### <a name="integrate-data-from-multiple-odbc-sources"></a>整合來自多個 ODBC 源的資料  
 數據集成應用程式非多個資料來源取得資料。 某些數據來自遠端數據來源,有些數據來自本地檔案。 在完成非同步操作之前,應用程式無法繼續。  
  
 應用程式可以建立事件物件並將其與 ODBC 連接句柄或 ODBC 語句句柄相關聯,而不是重複輪詢操作以確定它是否已完成。 然後,應用程式調用作業系統同步 API 以等待一個事件物件或多個事件物件(包括 ODBC 事件和其他 Windows 事件)。 當相應的 ODBC 非同步操作完成時,ODBC 將發出事件物件信號。  
  
 在 Windows 上,將使用 Win32 事件物件,這將為使用者提供統一的程式設計模型。 其他平臺上的驅動程式管理器可以使用特定於這些平臺的事件對象實現。  
  
 以下代碼範例展示與語句非同步通知的使用:  
  
```  
// This function opens NUMBER_OPERATIONS connections and executes one query on statement of each connection.  
// Asynchronous Notification is used  
  
#define NUMBER_OPERATIONS 5  
int AsyncNotificationSample(void)  
{  
    RETCODE     rc;  
  
    SQLHENV     hEnv              = NULL;  
    SQLHDBC     arhDbc[NUMBER_OPERATIONS]         = {NULL};  
    SQLHSTMT    arhStmt[NUMBER_OPERATIONS]        = {NULL};  
  
    HANDLE      arhDBCEvent[NUMBER_OPERATIONS]    = {NULL};  
    RETCODE     arrcDBC[NUMBER_OPERATIONS]        = {0};  
    HANDLE      arhSTMTEvent[NUMBER_OPERATIONS]   = {NULL};  
    RETCODE     arrcSTMT[NUMBER_OPERATIONS]       = {0};  
  
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &hEnv);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    rc = SQLSetEnvAttr(hEnv,  
        SQL_ATTR_ODBC_VERSION,  
        (SQLPOINTER) SQL_OV_ODBC3_80,  
        SQL_IS_INTEGER);  
    if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
  
    // Connection operations begin here  
  
    // Alloc NUMBER_OPERATIONS connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_DBC, hEnv, &arhDbc[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable DBC Async on all connection handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE, (SQLPOINTER)SQL_ASYNC_DBC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Application must create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhDBCEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhDBCEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all connection handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetConnectAttr(arhDbc[i], SQL_ATTR_ASYNC_DBC_EVENT, arhDBCEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate connect establishing  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLDriverConnect(arhDbc[i], NULL, (SQLTCHAR*)TEXT("Driver={ODBC Driver 11 for SQL Server};SERVER=dp-srv-sql2k;DATABASE=pubs;UID=sa;PWD=XYZ;"), SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE); // Wait All  
  
    // Complete connect API calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], & arrcDBC[i]);  
    }  
  
    BOOL fFail = FALSE; // Whether some connection openning fails.  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcDBC[i]) )   
            fFail = TRUE;  
    }  
  
    // If some SQLDriverConnect() fail, clean up.  
    if (fFail)  
    {  
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {  
                SQLDisconnect(arhDbc[i]); // This is also async  
            }  
            else  
            {  
                SetEvent(arhDBCEvent[i]); // Previous SQLDriverConnect() failed. No need to call SQLDisconnect().  
            }  
        }  
        WaitForMultipleObjects(NUMBER_OPERATIONS, arhDBCEvent, TRUE, INFINITE);   
        for (int i=0; i<NUMBER_OPERATIONS; i++)  
        {  
            if (SQL_SUCCEEDED(arrcDBC[i]) )   
            {     
                SQLCompleteAsync(SQL_HANDLE_DBC, arhDbc[i], &arrcDBC[i]);; // To Complete  
            }  
        }  
  
        goto Cleanup;  
    }  
  
    // Statement Operations begin here  
  
    // Alloc statement handle  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLAllocHandle(SQL_HANDLE_STMT, arhDbc[i], &arhStmt[i]);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Enable STMT Async on all statement handles  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc = SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_ENABLE, (SQLPOINTER)SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Create event objects  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        arhSTMTEvent[i] = CreateEvent(NULL, FALSE, FALSE, NULL); // Auto-reset, initial state is not-signaled  
        if (!arhSTMTEvent[i]) goto Cleanup;  
    }  
  
    // Enable notification on all statement handles  
    // Event  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        rc= SQLSetStmtAttr(arhStmt[i], SQL_ATTR_ASYNC_STMT_EVENT, arhSTMTEvent[i], SQL_IS_POINTER);  
        if ( !SQL_SUCCEEDED(rc) ) goto Cleanup;  
    }  
  
    // Initiate SQLExecDirect() calls  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLExecDirect(arhStmt[i], (SQLTCHAR*)TEXT("select au_lname, au_fname from authors"), SQL_NTS);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE); // Wait All  
  
    // Now, call SQLCompleteAsync to complete the operation and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return values  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        //Do some binding jobs here, set SQL_ATTR_ROW_ARRAY_SIZE   
    }  
  
    // Now, initiate fetching  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLFetch(arhStmt[i]);  
    }  
  
    // Can do some other staff before calling WaitForMultipleObjects  
    WaitForMultipleObjects(NUMBER_OPERATIONS, arhSTMTEvent, TRUE, INFINITE);   
  
    // Now, to complete the operations and get return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        SQLCompleteAsync(SQL_HANDLE_STMT, arhStmt[i], &arrcSTMT[i]);  
    }  
  
    // Check return code  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if ( !SQL_SUCCEEDED(arrcSTMT[i]) ) goto Cleanup;  
    }  
  
    // USE fetched data here!!  
  
Cleanup:  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhStmt[NUMBER_OPERATIONS])  
        {  
            SQLFreeHandle(SQL_HANDLE_STMT, arhStmt[i]);  
            arhStmt[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhSTMTEvent[i])  
        {  
            CloseHandle(arhSTMTEvent[i]);  
            arhSTMTEvent[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDbc[i])  
        {  
            SQLFreeHandle(SQL_HANDLE_DBC, arhDbc[i]);  
            arhDbc[i] = NULL;  
        }  
    }  
  
    for (int i=0; i<NUMBER_OPERATIONS; i++)  
    {  
        if (arhDBCEvent[i])  
        {  
            CloseHandle(arhDBCEvent[i]);  
            arhDBCEvent[i] = NULL;  
        }  
    }  
  
    if (hEnv)  
    {  
        SQLFreeHandle(SQL_HANDLE_ENV, hEnv);  
        hEnv = NULL;  
    }  
  
    return 0;  
}  
  
```  
  
### <a name="determining-if-a-driver-supports-asynchronous-notification"></a>確定驅動程式是否支援非同步通知  
 ODBC 應用程式可以通過調用[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)來確定 ODBC 驅動程式是否支援非同步通知。 因此,ODBC 驅動程式管理器將調用驅動程式的**SQLGetInfo,SQL_ASYNC_NOTIFICATION。**  
  
```  
SQLUINTEGER InfoValue;  
SQLLEN      cbInfoLength;  
  
SQLRETURN retcode;  
retcode = SQLGetInfo (hDbc,   
                      SQL_ASYNC_NOTIFICATION,   
                      &InfoValue,  
                      sizeof(InfoValue),  
                      NULL);  
if (SQL_SUCCEEDED(retcode))  
{  
if (SQL_ASYNC_NOTIFICATION_CAPABLE == InfoValue)  
      {  
          // The driver supports asynchronous notification  
      }  
      else if (SQL_ASYNC_NOTIFICATION_NOT_CAPABLE == InfoValue)  
      {  
          // The driver does not support asynchronous notification  
      }  
}  
```  
  
### <a name="associating-a-win32-event-handle-with-an-odbc-handle"></a>將 Win32 事件句柄與 ODBC 句柄關聯  
 應用程式負責使用相應的 Win32 函數創建 Win32 事件物件。 應用程式可以將一個 Win32 事件句柄與一個 ODBC 連接句柄或一個 ODBC 語句句柄相關聯。  
  
 連接屬性SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE,SQL_ATTR_ASYNC_DBC_EVENT確定 ODBC 是否以非同步模式執行,以及 ODBC 是否啟用連接句柄的通知模式。 語句屬性SQL_ATTR_ASYNC_ENABLE和SQL_ATTR_ASYNC_STMT_EVENT確定 ODBC 是否以非同步模式執行,以及 ODBC 是否啟用語句句柄的通知模式。  
  
|SQL_ATTR_ASYNC_ENABLE或SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE|SQL_ATTR_ASYNC_STMT_EVENT或SQL_ATTR_ASYNC_DBC_EVENT|[模式]|  
|-------------------------------------------------------------------------|-------------------------------------------------------------------|----------|  
|啟用|非空|非同步通知|  
|啟用|null|非同步輪詢|  
|停用|任意|同步|  
  
 應用程式可以暫時禁用非同步操作模式。 如果關閉連接級非同步操作,ODBC將忽略SQL_ATTR_ASYNC_DBC_EVENT值。 如果禁用語句級非同步操作,ODBC將忽略SQL_ATTR_ASYNC_STMT_EVENT值。  
  
 **SQLSetStmtAttr**與**SQLSetConnectAttr**同步呼叫  
 -   **SQLSetConnectAttr**支援非同步操作,但調用**SQLSetConnectAttr**來設定SQL_ATTR_ASYNC_DBC_EVENT始終是同步的。  
  
-   **SQLSetStmtAttr**不支援非同步執行。  
  
 錯誤宣告機制  
 在建立連接之前調用**SQLSetConnectAttr**時,驅動程式管理器無法確定要使用的驅動程式。 因此,驅動程式管理器返回**SQLSetConnectAttr**的成功,但屬性可能尚未準備好在驅動程式中設置。 驅動程式管理員將在應用程式呼叫連接函數時設置這些屬性。 驅動程式管理器可能會出錯,因為驅動程式不支援非同步操作。  
  
 連線屬性的繼承  
 通常,連接的語句將繼承連接屬性。 但是,屬性SQL_ATTR_ASYNC_DBC_EVENT不可繼承,並且僅影響連接操作。  
  
 要將事件句柄與 ODBC 連接句柄關聯,ODBC 應用程式呼叫 ODBC API **SQLSetConnectAttr**並將SQL_ATTR_ASYNC_DBC_EVENT指定為屬性,並將事件句柄指定為屬性值。 新的 ODBC 屬性SQL_ATTR_ASYNC_DBC_EVENT類型為SQL_IS_POINTER。  
  
```  
HANDLE hEvent;  
hEvent = CreateEvent(   
            NULL,                // default security attributes  
            FALSE,               // auto-reset event  
            FALSE,               // initial state is non-signaled  
            NULL                 // no name  
            );  
```  
  
 通常,應用程式創建自動重置事件物件。 ODBC 不會重置事件物件。 在調用任何異步 ODBC 函數之前,應用程式必須確保物件未處於信號狀態。  
  
```  
SQLRETURN retcode;  
retcode = SQLSetConnectAttr ( hDBC,  
                              SQL_ATTR_ASYNC_DBC_EVENT, // Attribute name  
                              (SQLPOINTER) hEvent,      // Win32 Event handle  
                              SQL_IS_POINTER);          // Length Indicator  
```  
  
 SQL_ATTR_ASYNC_DBC_EVENT是驅動程式中不會設置的僅驅動程式管理員屬性。  
  
 SQL_ATTR_ASYNC_DBC_EVENT的預設值為 NULL。 如果驅動程式不支援非同步通知,獲取或設定SQL_ATTR_ASYNC_DBC_EVENT將返回SQL_ERROR SQLSTATE HY092(無效屬性/選項識別符)。  
  
 如果 ODBC 連接句柄上設置的最後一個SQL_ATTR_ASYNC_DBC_EVENT值不是 NULL,並且應用程式通過設置SQL_ASYNC_DBC_ENABLE_ON的屬性SQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE啟用了非同步模式,則呼叫支援非同步模式的任何 ODBC 連接函數都將收到完成通知。 如果 ODBC 連接句柄上設定的最後一個SQL_ATTR_ASYNC_DBC_EVENT值為 NULL,則無論是否啟用非同步模式,ODBC 不會向應用程式發送任何通知。  
  
 應用程式可以在設置屬性之前或之後設置SQL_ATTR_ASYNC_DBC_EVENTSQL_ATTR_ASYNC_DBC_FUNCTION_ENABLE。  
  
 在調用連接函數 **(SQLConnect、SQLBrowseConnect**或**SQLDriverConnect)** 之前,應用程式**SQLBrowseConnect**可以在 ODBC 連接句柄上設置SQL_ATTR_ASYNC_DBC_EVENT屬性。 由於 ODBC 驅動程式管理員不知道應用程式將使用哪個 ODBC 驅動程式,因此它將返回SQL_SUCCESS。 當應用程式呼叫連接函數時,ODBC 驅動程式管理員將檢查驅動程式是否支援非同步通知。 如果驅動程式不支援非同步通知,則 ODBC 驅動程式管理員將返回SQL_ERROR,S1_118 SQLSTATE(驅動程式不支援非同步通知)。 如果驅動程式支援非同步通知,ODBC 驅動程式管理員將調用驅動程式,並設置相應的屬性SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK和SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT。  
  
 同樣,應用程式在 ODBC 語句句柄上調用**SQLSetStmtAttr,** 並指定SQL_ATTR_ASYNC_STMT_EVENT屬性以啟用或禁用語句級別的非同步通知。 由於在建立連接後始終調用語句函數,因此如果相應的驅動程式不支援非同步操作或驅動程式支援非同步操作但不支援非同步通知 **,SQLSetStmtAttr**將立即返回具有 SQLSTATE S1_118(驅動程式不支援非同步通知)SQL_ERROR。  
  
```  
SQLRETURN retcode;  
retcode = SQLSetStmtAttr ( hSTMT,  
                           SQL_ATTR_ASYNC_STMT_EVENT, // Attribute name   
                           (SQLPOINTER) hEvent,       // Win32 Event handle  
                           SQL_IS_POINTER);           // length Indicator  
```  
  
 SQL_ATTR_ASYNC_STMT_EVENT(可以設置為 NULL)是驅動程式中不會設置的僅驅動程式管理員屬性。  
  
 SQL_ATTR_ASYNC_STMT_EVENT的預設值為 NULL。 如果驅動程式不支援非同步通知,獲取或設定SQL_ATTR_ASYNC_STMT_EVENT屬性將返回SQL_ERROR SQLSTATE HY092(無效屬性/選項識別符)。  
  
 應用程式不應將同一事件句柄與多個 ODBC 句柄相關聯。 否則,如果兩個異步 ODBC 函數調用在共用同一事件句柄的兩個句柄上完成,則一個通知將丟失。 為了避免語句句柄從連接句柄繼承同一事件句柄,如果應用程式在連接句柄上設置SQL_ATTR_ASYNC_STMT_EVENT,則 ODBC 返回 SQL_ERROR SQLSTATE IM016(無法將語句屬性設置為連接句柄)。  
  
### <a name="calling-asynchronous-odbc-functions"></a>呼叫非同步 ODBC 函式  
 啟用非同步通知並啟動非同步操作後,應用程式可以調用任何ODBC函數。 如果函數屬於支援非同步操作的函數集,則無論函數是失敗還是成功,應用程式都將在操作完成後收到完成通知。  唯一的例外是應用程式調用具有無效連接或語句句柄的 ODBC 函數。 在這種情況下,ODBC 將不會獲取事件句柄並將其設置為信號狀態。  
  
 在對相應的 ODBC 句柄啟動非同步操作之前,應用程式必須確保關聯的事件物件處於非信號狀態。 ODBC 不會重置事件物件。  
  
### <a name="getting-notification-from-odbc"></a>從 ODBC 取得通知  
 應用程式線程可以調用**WaitForSingleObject**等待一個事件句柄,或調用**WaitForMultiObjects**等待事件句柄陣列,並掛起,直到一個或所有事件物件發出信號或超時間隔結束。  
  
```  
DWORD dwStatus = WaitForSingleObject(  
                        hEvent,  // The event associated with the ODBC handle  
                        5000     // timeout is 5000 millisecond   
);  
  
If (dwStatus == WAIT_TIMEOUT)  
{  
    // time-out interval elapsed before all the events are signaled.   
}  
Else  
{  
    // Call the corresponding Asynchronous ODBC API to complete all processing and retrieve the return code.  
}  
```
