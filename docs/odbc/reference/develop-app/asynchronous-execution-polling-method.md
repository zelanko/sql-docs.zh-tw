---
title: 非同步執行(輪詢方法) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca7b3d5fa16be44bf4c2ef8f8df8953ae081235d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293398"
---
# <a name="asynchronous-execution-polling-method"></a>非同步執行 (輪詢方法)
在 ODBC 3.8 和 Windows 7 SDK 之前,僅允許在語句函數上執行非同步操作。 關於詳細資訊,請參閱本主題後面的**執行敘述 。**  
  
 Windows 7 SDK 中的 ODBC 3.8 引入了連接相關操作的非同步執行。 有關詳細資訊,請參閱本主題後面的 **「同步執行連接操作**」部分。  
  
 在 Windows 7 SDK 中,對於非同步語句或連接操作,應用程式確定非同步操作是否已完成使用輪詢方法。 從 Windows 8 SDK 開始,可以使用通知方法確定非同步操作是否已完成。 有關詳細資訊,請參閱[非同步執行(通知方法)。](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)  
  
 默認情況下,驅動程式同步執行ODBC函數;也就是說,應用程式調用一個函數,驅動程式在完成執行函數之前不會將控制件返回到應用程式。 但是,某些函數可以非同步執行;也就是說,應用程式調用函數,驅動程式在最少的處理后返回對應用程式的控制。 然後,應用程式可以在第一個函數仍在執行時調用其他函數。  
  
 大多數主要在數據源上執行的函數都支援非同步執行,例如建立連接、準備和執行 SQL 語句、檢索元資料、提取資料和提交事務的函數。 當在數據源上執行的任務需要很長時間(如登錄過程或針對大型資料庫的複雜查詢)時,它最有用。  
  
 當應用程式執行具有為非同步處理啟用的語句或連接的函數時,驅動程式執行最少的處理量(例如檢查錯誤參數)、對資料源的句柄處理,以及使用SQL_STILL_EXECUTING返回代碼將控制權返回到應用程式。 然後,應用程式執行其他任務。 要確定非同步函數何時完成,應用程式透過呼叫與最初使用的參數相同的參數,定期輪詢驅動程式。 如果函數仍在執行,它將返回SQL_STILL_EXECUTING;如果已完成執行,它將返回如果同步執行的代碼,例如SQL_SUCCESS、SQL_ERROR或SQL_NEED_DATA。  
  
 函數是同步執行還是非同步執行是特定於驅動程式的。 例如,假設結果集元數據緩存在驅動程式中。 在這種情況下,執行**SQLDescribeCol**的時間非常少,驅動程式應該簡單地執行該函數,而不是人為地延遲執行。 另一方面,如果驅動程式需要從數據源檢索元數據,則應在執行此操作時將控制權返回到應用程式。 因此,應用程式在首次非同步執行函數時必須能夠處理SQL_STILL_EXECUTING以外的返回代碼。  
  
## <a name="executing-statement-operations-asynchronously"></a>非同步執行敘述  
 以下語句函數對資料來源運行,可以非同步執行:  
  
||||  
|-|-|-|  
|[SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 非同步語句執行基於每個語句或每個連接進行控制,具體取決於資料源。 也就是說,應用程式指定的不是要非同步執行特定函數,而是指定對特定語句執行的任何函數都將異步執行。 要瞭解支援哪個應用程式,應用程式呼叫[SQLGetInfo,](../../../odbc/reference/syntax/sqlgetinfo-function.md)選項為 SQL_ASYNC_MODE。 如果支援連接級非同步執行(對於語句句柄),則返回SQL_AM_CONNECTION;如果支援語句級非同步執行,SQL_AM_STATEMENT。  
  
 要指定使用特定語句執行的函數要非同步執行,應用程式使用SQL_ATTR_ASYNC_ENABLE屬性調用**SQLSetStmtAttr**並將其設置為SQL_ASYNC_ENABLE_ON。 如果支援連接級非同步處理,則SQL_ATTR_ASYNC_ENABLE語句屬性為唯讀,其值與分配語句的連接的連接屬性相同。 它是特定於驅動程式的,無論語句屬性的值是在語句分配時間設置還是更高版本。 嘗試設置它將返回SQL_ERROR和 SQLSTATE HYC00(未實現可選功能)。  
  
 要指定使用特定連接執行的函數要非同步執行,應用程式使用SQL_ATTR_ASYNC_ENABLE屬性調用**SQLSetConnectAttr**並將其設定為SQL_ASYNC_ENABLE_ON。 將在連接上分配的所有語句句柄都將啟用以進行非同步執行;它是驅動程式定義的,是否將此操作啟用現有語句句柄。 如果將SQL_ATTR_ASYNC_ENABLE設置為SQL_ASYNC_ENABLE_OFF,則連接上的所有語句都處於同步模式。 如果在連接上有活動語句時啟用了非同步執行,則返回錯誤。  
  
 要確定驅動程式在給定連接上可以支援的非同步模式下活動並發語句的最大數量,應用程式使用SQL_MAX_ASYNC_CONCURRENT_STATEMENTS選項呼叫**SQLGetInfo。**  
  
 以下代碼演示了輪詢模型的工作原理:  
  
```  
SQLHSTMT  hstmt1;  
SQLRETURN rc;  
  
// Specify that the statement is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute a SELECT statement asynchronously.  
while ((rc=SQLExecDirect(hstmt1,"SELECT * FROM Orders",SQL_NTS))==SQL_STILL_EXECUTING) {  
   // While the statement is still executing, do something else.  
   // Do not use hstmt1, because it is being used asynchronously.  
}  
  
// When the statement has finished executing, retrieve the results.  
```  
  
 當函數非同步執行時,應用程式可以在任何其他語句上調用函數。 應用程式還可以調用任何連接上的函數,但與非同步語句關聯的連接除外。 但是,在語句操作返回SQL_STILL_EXECUTING后,應用程式只能調用原始函數和以下函數(具有語句句柄或其關聯的連接、環境句柄):  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle(](../../../odbc/reference/syntax/sqlcancelhandle-function.md)在語句句柄上)  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLData來源](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 如果應用程式使用非同步語句或與該語句關聯的連接呼叫任何其他函數,則函數將返回 SQLSTATE HY010(函數序列錯誤)。  
  
```  
SQLHDBC       hdbc1, hdbc2;  
SQLHSTMT      hstmt1, hstmt2, hstmt3;  
SQLCHAR *     SQLStatement = "SELECT * FROM Orders";  
SQLUINTEGER   InfoValue;  
SQLRETURN     rc;  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt2);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc2, &hstmt3);  
  
// Specify that hstmt1 is to be executed asynchronously.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_ASYNC_ENABLE, SQL_ASYNC_ENABLE_ON, 0);  
  
// Execute hstmt1 asynchronously.  
while ((rc = SQLExecDirect(hstmt1, SQLStatement, SQL_NTS)) == SQL_STILL_EXECUTING) {  
   // The following calls return HY010 because the previous call to  
   // SQLExecDirect is still executing asynchronously on hstmt1. The  
   // first call uses hstmt1 and the second call uses hdbc1, on which  
   // hstmt1 is allocated.  
   SQLExecDirect(hstmt1, SQLStatement, SQL_NTS);   // Error!  
   SQLGetInfo(hdbc1, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // Error!  
  
   // The following calls do not return errors. They use a statement  
   // handle other than hstmt1 or a connection handle other than hdbc1.  
   SQLExecDirect(hstmt2, SQLStatement, SQL_NTS);   // OK  
   SQLTables(hstmt3, NULL, 0, NULL, 0, NULL, 0, NULL, 0);   // OK  
   SQLGetInfo(hdbc2, SQL_UNION, (SQLPOINTER) &InfoValue, 0, NULL);   // OK  
}  
```  
  
 當應用程式調用函數以確定它是否仍在非同步執行時,它必須使用原始語句句柄。 這是因為非同步執行是按語句追蹤的。 應用程式還必須為其他參數(原始參數將執行)提供有效值,以在驅動程式管理器中通過錯誤檢查。 但是,在驅動程式檢查語句句柄並確定語句以非同步方式執行後,它將忽略所有其他參數。  
  
 當函數以非同步方式執行時(即,在返回SQL_STILL_EXECUTING後,並在返回其他代碼之前,應用程式可以透過使用相同的語句句柄呼叫**SQLCancel**或**SQLCancelHandle**來取消它。 這不能保證取消函數執行。 例如,函數可能已完成。 此外 **,SQLCancel**或**SQLCancelHandle**返回的代碼僅指示取消函數的嘗試是否成功,而不是是否實際取消了該函數。 要確定函數是否已取消,應用程式將再次調用該函數。 如果函數已取消,它將返回SQL_ERROR和 SQLSTATE HY008(操作已取消)。 如果未取消該函數,它將返回另一個代碼,如SQL_SUCCESS、SQL_STILL_EXECUTING或具有其他 SQLSTATE 的SQL_ERROR。  
  
 要禁用在驅動程式支援語句級非同步處理時對特定語句的非同步執行,應用程式使用SQL_ATTR_ASYNC_ENABLE屬性調用**SQLSetStmtAttr**並將其設置為SQL_ASYNC_ENABLE_OFF。 如果驅動程式支援連接級非同步處理,應用程式將調用**SQLSetConnectAttr**將SQL_ATTR_ASYNC_ENABLE設定為SQL_ASYNC_ENABLE_OFF,從而禁用對連接上所有語句的非同步執行。  
  
 應用程式應在原始函數的重複迴圈中處理診斷記錄。 如果在執行非同步函數時呼叫**SQLGetDiagField**或**SQLGetDiagRec,** 它將返回當前診斷記錄清單。 每次重複原始函數調用時,它都會清除以前的診斷記錄。  
  
## <a name="executing-connection-operations-asynchronously"></a>非同步執行連線操作  
 在 ODBC 3.8 之前,允許非同步執行語句相關操作,如準備、執行和提取,以及目錄中資料操作。 從 ODBC 3.8 開始,對於連接相關操作(如連接、斷開連接、提交和回滾)也可以執行異步執行。  
  
 有關 ODBC 3.8 的詳細資訊,請參閱[ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
 在以下情況下,非同步執行連線操作非常有用:  
  
-   當少量線程管理具有極高數據速率的大量設備時。 為了最大限度地提高回應性和可擴充性,所有操作都是異步的。  
  
-   如果要在多個連接上重疊資料庫操作以減少已用傳輸時間。  
  
-   高效的非同步ODBC調用和取消連接操作的能力使應用程式允許使用者取消任何慢速操作,而無需等待超時。  
  
 以下函數在連接句柄上操作,現在可以非同步執行:  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQL 斷線](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 要確定驅動程式是否支援對這些函數的非同步操作,應用程式使用SQL_ASYNC_DBC_FUNCTIONS調用**SQLGetInfo。** 如果支援非同步操作,則返回SQL_ASYNC_DBC_CAPABLE。 如果不支援非同步操作,則返回SQL_ASYNC_DBC_NOT_CAPABLE。  
  
 要指定使用特定連接執行的函數要非同步執行,應用程式將調用**SQLSetConnectAttr**並將SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE屬性設置為SQL_ASYNC_DBC_ENABLE_ON。 在建立連接之前設置連接屬性始終同步執行。 此外,使用**SQLSetConnectAttr** SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE連接屬性設置的操作始終同步執行。  
  
 應用程式可以在建立連接之前啟用非同步操作。 由於驅動程式管理員無法確定在建立連接之前要使用的驅動程式,因此驅動程式管理員將始終在**SQLSetConnectAttr**中傳回成功。 但是,如果 ODBC 驅動程式不支援非同步操作,則可能無法連接。  
  
 通常,最多只能有一個與特定連接句柄或語句句柄關聯的非同步執行函數。 但是,連接句柄可以有多個關聯的語句句柄。 如果連接句柄上沒有執行非同步操作,則關聯的語句句柄可以執行非同步操作。 同樣,如果任何關聯的語句句柄上沒有正在進行的非同步操作,則可以對連接句柄執行異步操作。 嘗試使用當前正在執行非同步操作的句柄執行非同步操作將返回 HY010,「函數序列錯誤」。  
  
 如果連線操作傳回SQL_STILL_EXECUTING,則應用程式只能呼叫該連線句柄的原始函數和以下函數:  
  
-   **SQLCancelHandle(** 在連接句柄上)  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle(** 分配 ENV/DBC)  
  
-   **SQLAllocHandleStd(** 分配 ENV/ DBC )  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLData來源**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 應用程式應在原始函數的重複迴圈中處理診斷記錄。 如果在執行非同步函數時呼叫 SQLGetDiagField 或 SQLGetDiagRec,它將返回當前診斷記錄清單。 每次重複原始函數調用時,它都會清除以前的診斷記錄。  
  
 如果以非同步方式打開或關閉連接,則當應用程式在原始函數調用中收到SQL_SUCCESS或SQL_SUCCESS_WITH_INFO時,操作將完成。  
  
 新函數已新增到 ODBC **3.8,SQLCancelHandle**。 此函數取消六個連接函數 **(SQLBrowseConnect、SQLConnect、SQL****斷開連接****、SQLDriverConnect、SQLEndTran**和**SQLSetConnectAttr)。** **SQLConnect** **SQLEndTran** 應用程式應呼叫**SQLGet 函數**以確定驅動程式是否支援**SQLCancelHandle**。 與**SQLCancel**一樣,如果**SQLCancelHandle**返回成功,並不意味著操作已取消。 應用程式應再次調用原始函數以確定操作是否已取消。 **SQLCancelHandle**允許您取消連接句柄或語句句柄上的非同步操作。 使用**SQLCancelHandle**取消文句句柄上的操作與調用**SQLCancel**相同。  
  
 不必同時支援**SQLCancelHandle**和非同步連接操作。 驅動程式可以支援非同步連接操作,但不能支援**SQLCancelHandle,** 反之亦然。  
  
 具有 ODBC 3.8 驅動程式和 ODBC 3.8 驅動程式管理員的 ODBC 3.x 和 ODBC 2.x 應用程式也可以使用非同步連線操作和**SQLCancelHandle。** 有關如何啟用較舊的應用程式在更高版本的 ODBC 版本中使用新功能的資訊,請參閱[相容性矩陣](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
### <a name="connection-pooling"></a>連接共用  
 每當啟用連接池時,非同步操作僅受最小支援,用於建立連接(使用**SQLConnect**和**SQLDriverConnect),** 並關閉與**SQLDisconnect**的連接。 但是,應用程式仍然能夠處理來自 SQLConnect、SQLDriverConnect**SQLConnect**和**SQLDisconnect**的**SQLDriverConnect**SQL_STILL_EXECUTING返回值。  
  
 啟用連接池後,非同步操作支援**SQLEndTran**和**SQLSetConnectAttr。**  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 下面的範例展示如何使用**SQLSetConnectAttr**為連接相關的函數啟用非同步執行。  
  
### <a name="code"></a>程式碼  
  
```  
BOOL AsyncConnect (SQLHANDLE hdbc)   
{  
   SQLRETURN r;  
   SQLHANDLE hdbc;  
  
   // Enable asynchronous execution of connection functions.  
   // This must be executed synchronously, that is r != SQL_STILL_EXECUTING  
   r = SQLSetConnectAttr(  
         hdbc,   
         SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,  
         reinterpret_cast<SQLPOINTER> (SQL_ASYNC_DBC_ENABLE_ON),  
         0);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=AsyncDemo");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
  
   if (r == SQL_ERROR)   
   {  
      // Use SQLGetDiagRec to process the error.  
      // If SQLState is HY114, the driver does not support asynchronous execution.  
      return FALSE;  
   }  
  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion, with the same set of arguments.  
      r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
  
   return TRUE;  
}  
  
```  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 此示例顯示非同步提交操作。 回滾操作也可以以這種方式完成。  
  
### <a name="code"></a>程式碼  
  
```  
BOOL AsyncCommit ()   
{  
   SQLRETURN r;   
  
   // Assume that SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE is SQL_ASYNC_DBC_ENABLE_ON.  
  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   while (r == SQL_STILL_EXECUTING)   
   {  
      // Do something else.  
  
      // Check for completion with the same set of arguments.  
      r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   }  
  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO)   
   {  
      return FALSE;  
   }  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行敘述的 ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
