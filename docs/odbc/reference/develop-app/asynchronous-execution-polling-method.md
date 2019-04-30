---
title: 非同步執行 （輪詢方法） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ca0a5094e40f13aef4b4f87d5642e51e7a9b765
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306295"
---
# <a name="asynchronous-execution-polling-method"></a>非同步執行 (輪詢方法)
之前 ODBC 3.8，而且 Windows 7 SDK，只被允許陳述式的函式的非同步作業。 如需詳細資訊，請參閱 <<c0>  **非同步執行陳述式作業**稍後在本主題中。  
  
 Windows 7 SDK 中的 ODBC 3.8 導入了連接相關作業的非同步執行。 如需詳細資訊，請參閱 <<c0>  **非同步執行連線作業**區段中的，稍後在本主題中。  
  
 在 Windows 7 SDK 中，針對非同步的陳述式或連接作業，應用程式會判斷非同步作業已完成使用輪詢方法。 從 Windows 8 SDK 中，您就可以判斷非同步作業已完成使用的通知方法。 如需詳細資訊，請參閱 <<c0> [ 非同步執行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
 根據預設，驅動程式執行 ODBC 函數以同步方式;也就是說，應用程式呼叫的函式，而且驅動程式不會將控制權傳回給應用程式直到它完成時執行函式。 不過，某些函數可以非同步執行;也就是應用程式呼叫函式，並驅動程式，最少處理後，控制權傳回給應用程式。 應用程式在第一個函式仍在執行時，就可以呼叫其他函式。  
  
 非同步執行支援的主要資料來源執行的大部分函式，例如，建立連線、 準備及執行 SQL 陳述式，函式擷取中繼資料，擷取資料，以及認可交易。 資料來源上執行工作花較長的時間，例如登入程序或複雜的查詢，對大型資料庫時，它是最有用。  
  
 當應用程式執行的陳述式或連接已啟用非同步處理的函式時，驅動程式執行最少量的處理 （例如，檢查有錯誤的引數）、 實際操作處理至資料來源，並傳回控制應用程式並 SQL_STILL_EXECUTING 傳回碼。 接著，應用程式會執行其他工作。 若要判斷完成的非同步函式時，應用程式會輪詢驅動程式，定期呼叫具有相同的引數，因為它原本使用的函式。 如果函式仍在執行中，它會傳回 SQL_STILL_EXECUTING;如果它已完成執行時，它會傳回它會傳回有它以同步方式執行，例如 SQL_SUCCESS、 SQL_ERROR 或 SQL_NEED_DATA 的程式碼。  
  
 同步或非同步函式會執行的是否是特定的驅動程式。 例如，假設驅動程式中快取的結果集中繼資料。 在此情況下，它會很短的時間來執行**SQLDescribeCol**和驅動程式應該直接執行函式而不是以人為方式延遲執行。 相反地，如果驅動程式需要從資料來源擷取中繼資料，它應該傳回控制應用程式時它會執行此動作。 因此，應用程式必須能夠處理 SQL_STILL_EXECUTING 以外的傳回碼，當它第一次執行的函式以非同步的方式。  
  
## <a name="executing-statement-operations-asynchronously"></a>以非同步方式執行陳述式的作業  
 下列陳述式函式在資料來源上運作，並能夠以非同步方式執行：  
  
||||  
|-|-|-|  
|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
 執行非同步的陳述式被控制每個陳述式或以每個連線為基礎，根據資料來源。 也就是應用程式指定不特定的函式會以非同步方式執行，但任何特定陳述式上執行的函式是以非同步方式執行。 若要尋找哪一個支援的外，應用程式呼叫[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) SQL_ASYNC_MODE 選擇。 如果支援的連接層級 （適用於陳述式控制代碼） 的非同步執行;，則會傳回 SQL_AM_CONNECTION如果支援非同步執行的陳述式層級，SQL_AM_STATEMENT。  
  
 若要指定要使用特定的陳述式執行的函式以非同步方式執行，應用程式會呼叫**SQLSetStmtAttr** SQL_ATTR_ASYNC_ENABLE 屬性，並將它設定為 sql_async_enable_on，然後。 如果支援非同步處理的連接層級，則請 SQL_ATTR_ASYNC_ENABLE 陳述式屬性是唯讀的且其值為的連接的陳述式所配置的連接屬性相同。 它是驅動程式特有的陳述式屬性值是否設定在陳述式配置階段或更新版本。 嘗試設定它將會傳回 SQL_ERROR 並 SQLSTATE HYC00 （未實作選擇性功能）。  
  
 若要指定要使用特定的連接執行的函式以非同步方式執行，應用程式會呼叫**SQLSetConnectAttr** SQL_ATTR_ASYNC_ENABLE 屬性，並將它設定為 sql_async_enable_on，然後。 在此連接上配置的所有未來的陳述式控制代碼將讓非同步執行;它是驅動程式-定義此動作是否啟用現有的陳述式控制代碼。 如果 SQL_ATTR_ASYNC_ENABLE 設定為 SQL_ASYNC_ENABLE_OFF，連接上的所有陳述式就會處於同步模式。 如果在連接上的作用中陳述式時，已啟用非同步執行，則會傳回錯誤。  
  
 若要判斷驅動程式可支援指定的連接上的非同步模式的作用中並行陳述式的最大數目，應用程式會呼叫**SQLGetInfo** SQL_MAX_ASYNC_CONCURRENT_STATEMENTS 選項。  
  
 下列程式碼示範輪詢模式的運作方式：  
  
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
  
 函式執行時以非同步方式，應用程式可以呼叫函式的任何其他陳述式。 應用程式也可以在相關聯的非同步的陳述式以外的任何連線，呼叫函式。 但是，應用程式可以只呼叫原始函式和下列函式 （使用陳述式控制代碼或其相關聯的連線，環境控制代碼） 之後的陳述式作業傳回 SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) （在陳述式控制代碼）  
  
-   [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
 如果應用程式呼叫任何其他函式以非同步的陳述式，或與該陳述式相關聯的連接，則函數會傳回 SQLSTATE HY010 （函數順序錯誤），例如。  
  
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
  
 當應用程式呼叫的函式，來判斷是否仍在執行以非同步方式時，它必須使用原始的陳述式控制代碼。 這是因為非同步執行會追蹤每個陳述式為基礎。 應用程式也必須提供有效的值，其他引數： 原始的引數的作用為何-通過檢查驅動程式管理員時發生錯誤。 不過，驅動程式會檢查陳述式控制代碼，並判斷該陳述式會以非同步方式執行之後，它就會忽略所有其他引數。  
  
 以非同步方式-執行函式時，也就是它已傳回 SQL_STILL_EXECUTING 後之前它會傳回不同的程式碼-, 應用程式可以取消它藉由呼叫**SQLCancel**或**SQLCancelHandle**具有相同的陳述式控制代碼。 這不保證取消函式執行。 例如，可能已經完成函式。 此外，程式碼會由**SQLCancel**或是**SQLCancelHandle**只會指出是否要取消此函式的嘗試成功，不是它實際取消函式是否。 若要判斷函式是否已取消，應用程式會再次呼叫此函式。 如果函式已取消，則會傳回 SQL_ERROR，而且 SQLSTATE HY008 （已取消的作業）。 如果未取消函式，它會傳回另一個程式碼，例如 SQL_SUCCESS、 SQL_STILL_EXECUTING 或 sql_error，其中包含不同的 SQLSTATE。  
  
 若要停用的特定陳述式的非同步執行，當驅動程式支援的陳述式層級非同步處理，應用程式會呼叫**SQLSetStmtAttr** SQL_ATTR_ASYNC_ENABLE 屬性，並將它設定為 SQL_ASYNC_ENABLE_OFF。 如果驅動程式支援連接層級非同步處理，應用程式會呼叫**SQLSetConnectAttr**將 SQL_ATTR_ASYNC_ENABLE 設定為 SQL_ASYNC_ENABLE_OFF，停用的所有陳述式的非同步執行連接。  
  
 應用程式應該處理重複的原始函式的迴圈中的診斷記錄。 如果**SQLGetDiagField**或是**SQLGetDiagRec**稱為非同步函式會執行時，它會傳回目前的診斷記錄的清單。 每次重複的原始函式呼叫時，它會清除先前的診斷記錄。  
  
## <a name="executing-connection-operations-asynchronously"></a>以非同步方式執行連線作業  
 ODBC 3.8 之前請允許非同步執行，例如準備陳述式相關的作業、 執行和擷取，也與目錄中繼資料作業。 從符合 ODBC 3.8，非同步執行，也可以針對連線相關的作業，例如當連線時，中斷連線、 commit 和 rollback。  
  
 如需有關 ODBC 3.8 的詳細資訊，請參閱 < [What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
 以非同步方式執行連線作業是適用於下列情況：  
  
-   當少量的執行緒管理大量非常高的資料費率的裝置。 若要最大化回應性和延展性最好都是非同步的所有作業。  
  
-   當您想要透過多個連線，以減少耗用的傳輸時間重疊資料庫作業。  
  
-   有效率的非同步 ODBC 呼叫，並取消連接作業的能力可讓應用程式允許使用者取消任何緩慢的作業，而不必等候逾時。  
  
 下列函式，在連接控制代碼運作，現在可以在以非同步方式執行：  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 若要判斷驅動程式是否支援這些函式的非同步作業，應用程式會呼叫**SQLGetInfo** SQL_ASYNC_DBC_FUNCTIONS 使用。 如果支援非同步作業，則會傳回 SQL_ASYNC_DBC_CAPABLE。 如果不支援非同步作業，則會傳回 SQL_ASYNC_DBC_NOT_CAPABLE。  
  
 若要指定要使用特定的連接執行的函式以非同步方式執行，應用程式會呼叫**SQLSetConnectAttr**並將 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 屬性設定為 SQL_ASYNC_DBC_ENABLE_ON。 設定連接屬性之前建立的連接一律會以同步方式執行。 此外，作業設定連接屬性與 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE **SQLSetConnectAttr**一律會以同步方式執行。  
  
 應用程式可以啟用非同步作業之前進行連接。 由於驅動程式管理員無法判斷哪一個驅動程式以使用，才能進行連接，驅動程式管理員一律會傳回成功**SQLSetConnectAttr**。 不過，它可能無法連線，如果 ODBC 驅動程式不支援非同步作業。  
  
 一般情況下，可以有最多一個以非同步方式執行函式相關聯的特定連接控制代碼或陳述式控制代碼。 不過，在連接控制代碼可以有多個相關聯的陳述式控制代碼。 如果沒有在連接控制代碼上執行非同步作業，相關聯的陳述式控制代碼可以執行非同步作業。 同樣地，您可以有連接控制代碼上的非同步作業，如果沒有任何相關聯的陳述式控制代碼上非同步作業進行中。 嘗試執行使用目前正在執行非同步作業的控制代碼，以非同步作業會傳回 HY010，「 函數順序錯誤 」。  
  
 如果連接的作業會傳回 SQL_STILL_EXECUTING，應用程式可以只針對該連接控制代碼呼叫原始函式和下列函式：  
  
-   **SQLCancelHandle** （在連接控制代碼）  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** （配置 ENV/雙位元組字元）  
  
-   **SQLAllocHandleStd** （配置 ENV/雙位元組字元）  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 應用程式應該處理重複的原始函式的迴圈中的診斷記錄。 如果執行的非同步函式時，會呼叫 SQLGetDiagField 或 SQLGetDiagRec，它會傳回目前的診斷記錄的清單。 每次重複的原始函式呼叫時，它會清除先前的診斷記錄。  
  
 如果連接正在開啟或關閉以非同步方式，當應用程式會在原始的函式呼叫中收到 「 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，表示作業已完成。  
  
 新的函式已加入至 ODBC 3.8 **SQLCancelHandle**。 此函式取消的六個連接函式 (**SQLBrowseConnect**， **SQLConnect**， **SQLDisconnect**， **SQLDriverConnect**，**SQLEndTran**，並**SQLSetConnectAttr**)。 應用程式應該呼叫**SQLGetFunctions**決定驅動程式是否支援**SQLCancelHandle**。 如同**SQLCancel**，如果**SQLCancelHandle**會傳回成功，它並不表示作業已取消。 應用程式應該呼叫原始的函式，以判斷是否取消作業。 **SQLCancelHandle**可讓您取消連接控制代碼或陳述式控制代碼上的非同步作業。 使用**SQLCancelHandle**取消作業的陳述式控制代碼是呼叫相同**SQLCancel**。  
  
 您不需要同時支援**SQLCancelHandle**和非同步連接作業，在相同的時間。 驅動程式可支援非同步連接作業而非**SQLCancelHandle**，反之亦然。  
  
 非同步連接作業並**SQLCancelHandle**也可由 ODBC 3.x 和 ODBC 2.x 應用程式使用 ODBC 3.8 驅動程式和 ODBC 3.8 驅動程式管理員。 如需如何啟用舊版應用程式以使用較新的 ODBC 版本中的新功能的相關資訊，請參閱[相容性比較表](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
### <a name="connection-pooling"></a>連接共用  
 每當啟用連接共用時，只進行最低限度支援非同步作業來建立連線 (與**SQLConnect**並**SQLDriverConnect**) 和關閉的連線**SQLDisconnect**。 應用程式應該仍然能夠處理來自 SQL_STILL_EXECUTING 傳回值，但是**SQLConnect**， **SQLDriverConnect**，並**SQLDisconnect**。  
  
 啟用連線共用時， **SQLEndTran**並**SQLSetConnectAttr**支援非同步作業。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 下列範例示範如何使用**SQLSetConnectAttr**啟用連接相關的函式的非同步執行。  
  
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
 此範例示範非同步認可作業。 回復作業也可以完成這種方式。  
  
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
 [執行陳述式 ODBC](../../../odbc/reference/develop-app/executing-statements-odbc.md)
