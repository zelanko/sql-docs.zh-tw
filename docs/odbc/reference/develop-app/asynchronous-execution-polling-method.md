---
title: 非同步執行（輪詢方法） |Microsoft Docs
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
ms.openlocfilehash: 97fe8af6f02e9797bc14578edda09c420f8f94e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077054"
---
# <a name="asynchronous-execution-polling-method"></a>非同步執行 (輪詢方法)
在 ODBC 3.8 和 Windows 7 SDK 之前，只允許在語句函式上進行非同步作業。 如需詳細資訊，請參閱本主題稍後的**以非同步方式執行語句作業**。  
  
 Windows 7 SDK 中的 ODBC 3.8 在連接相關的作業上引進了非同步執行。 如需詳細資訊，請參閱本主題稍後的**非同步執行連接作業**一節。  
  
 在 Windows 7 SDK 中，針對非同步語句或連接作業，應用程式會使用輪詢方法判定非同步作業已完成。 從 Windows 8 SDK 開始，您可以使用通知方法來判斷非同步作業是否已完成。 如需詳細資訊，請參閱[非同步執行（通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
 根據預設，驅動程式會以同步方式執行 ODBC 函數;也就是說，應用程式會呼叫函式，而驅動程式不會將控制權傳回給應用程式，直到它完成執行函數為止。 不過，有些函數可以非同步執行;也就是說，應用程式會呼叫函式，而驅動程式會在最少處理之後，將控制權傳回給應用程式。 然後，應用程式可以在第一個函式仍在執行時呼叫其他函式。  
  
 大部分大部分在資料來源上執行的函式都支援非同步執行，例如建立連接、準備和執行 SQL 語句、抓取中繼資料、提取資料和認可交易的函數。 在資料來源上執行的工作需要很長的時間，例如登入程式或對大型資料庫的複雜查詢時，這是最有用的。  
  
 當應用程式使用已啟用非同步處理的語句或連接來執行函式時，驅動程式會執行最少量的處理（例如，檢查引數的錯誤）、對資料來源進行手動處理，然後傳回使用 SQL_STILL_EXECUTING 傳回碼來控制應用程式。 然後，應用程式會執行其他工作。 若要判斷非同步函式何時完成，應用程式會呼叫函式，並以原先使用的相同引數，以定期輪詢驅動程式。 如果函數仍在執行，它會傳回 SQL_STILL_EXECUTING;如果它已經完成執行，它會傳回它所傳回的程式碼，它會以同步方式執行，例如 SQL_SUCCESS、SQL_ERROR 或 SQL_NEED_DATA。  
  
 函數是否以同步或非同步方式執行，是驅動程式特有的。 例如，假設驅動程式中快取了結果集中繼資料。 在此情況下，執行**SQLDescribeCol**需要很少的時間，而驅動程式應該只執行函式，而不是人為順延強制。 另一方面，如果驅動程式需要從資料來源抓取中繼資料，它應該會在執行此作業時將控制權傳回給應用程式。 因此，在第一次以非同步方式執行函式時，應用程式必須能夠處理 SQL_STILL_EXECUTING 以外的傳回碼。  
  
## <a name="executing-statement-operations-asynchronously"></a>以非同步方式執行語句作業  
 下列語句函式會在資料來源上運作，而且可以非同步執行：  
  
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
  
 視資料來源而定，非同步語句執行是根據每個語句或每個連接來控制。 也就是說，應用程式不會指定要以非同步方式執行特定函式，但在特定語句上執行的任何函式都會以非同步方式執行。 若要找出支援哪一個，應用程式會使用 SQL_ASYNC_MODE 的選項來呼叫[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 。 如果支援連接層級的非同步執行（適用于語句控制碼），則會傳回 SQL_AM_CONNECTION;如果支援語句層級非同步執行，SQL_AM_STATEMENT。  
  
 若要指定以特定語句執行的函式要以非同步方式執行，應用程式會使用 SQL_ATTR_ASYNC_ENABLE 屬性來呼叫**SQLSetStmtAttr** ，並將它設定為 SQL_ASYNC_ENABLE_ON。 如果支援連接層級的非同步處理，則 SQL_ATTR_ASYNC_ENABLE 語句屬性會是唯讀的，而且其值會與配置語句之連接的連接屬性相同。 無論語句屬性的值是在語句配置時間或更新版本中設定，它都是驅動程式特定的。 嘗試設定它會傳回 SQL_ERROR 和 SQLSTATE HYC00 （未實作為選擇性功能）。  
  
 若要指定以特定連接執行的函式要以非同步方式執行，應用程式會使用 SQL_ATTR_ASYNC_ENABLE 屬性來呼叫**SQLSetConnectAttr** ，並將它設定為 SQL_ASYNC_ENABLE_ON。 在連接上配置的所有未來語句控制碼都將啟用非同步執行;無論此動作是否會啟用現有的語句控制碼，都是由驅動程式定義的。 如果 SQL_ATTR_ASYNC_ENABLE 設定為 SQL_ASYNC_ENABLE_OFF，則連接上的所有語句都會處於同步模式。 當連接上有作用中的語句時，如果啟用非同步執行，則會傳回錯誤。  
  
 若要判斷驅動程式可在指定的連接上支援之非同步模式中的作用中並行語句數目上限，應用程式會使用 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS 選項來呼叫**SQLGetInfo** 。  
  
 下列程式碼示範輪詢模型的運作方式：  
  
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
  
 當函式以非同步方式執行時，應用程式可以在任何其他語句上呼叫函數。 應用程式也可以呼叫任何連接上的函式，但與非同步語句關聯的函式除外。 但是，在語句作業傳回 SQL_STILL_EXECUTING 之後，應用程式只能呼叫原始函式和下列函數（使用語句控制碼或其相關聯的連接，環境控制碼）：  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) （在語句控制碼上）  
  
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
  
 如果應用程式使用非同步語句或與該語句相關聯的連接來呼叫任何其他函式，此函式會傳回 SQLSTATE HY010 （函數順序錯誤），例如。  
  
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
  
 當應用程式呼叫函式以判斷它是否仍以非同步方式執行時，它必須使用原始的語句控制碼。 這是因為非同步執行是根據每個語句來追蹤。 應用程式也必須提供其他引數的有效值，原始引數會執行，以在驅動程式管理員中取得過去的錯誤檢查。 不過，在驅動程式檢查語句控制碼並判斷語句是以非同步方式執行之後，它會忽略所有其他引數。  
  
 當函式以非同步方式執行時，也就是在它傳回 SQL_STILL_EXECUTING 之後，而且在傳回不同的程式碼之前，應用程式可以使用相同的語句控制碼呼叫**SQLCancel**或**SQLCancelHandle**來取消它。 這不保證會取消函式執行。 例如，函數可能已經完成。 此外， **SQLCancel**或**SQLCancelHandle**所傳回的程式碼只會指出是否已成功嘗試取消函式，而不是真的是否已取消函數。 為了判斷函式是否已取消，應用程式會再次呼叫函式。 如果已取消函式，它會傳回 SQL_ERROR 並 SQLSTATE HY008 （作業已取消）。 如果未取消函式，它會傳回另一個程式碼，例如 SQL_SUCCESS、SQL_STILL_EXECUTING 或具有不同 SQLSTATE 的 SQL_ERROR。  
  
 當驅動程式支援語句層級非同步處理時，若要停用特定語句的非同步執行，應用程式會使用 SQL_ATTR_ASYNC_ENABLE 屬性呼叫**SQLSetStmtAttr** ，並將它設定為 SQL_ASYNC_ENABLE_OFF。 如果驅動程式支援連接層級的非同步處理，則應用程式會呼叫**SQLSetConnectAttr** ，將 SQL_ATTR_ASYNC_ENABLE 設定為 SQL_ASYNC_ENABLE_OFF，這會停用連接上所有語句的非同步執行。  
  
 應用程式應該在原始函數的重複迴圈中處理診斷記錄。 如果在非同步函式執行時呼叫**SQLGetDiagField**或**SQLGetDiagRec** ，它會傳回目前的診斷記錄清單。 每當原始函式呼叫重複時，就會清除先前的診斷記錄。  
  
## <a name="executing-connection-operations-asynchronously"></a>以非同步方式執行連接作業  
 在 ODBC 3.8 之前，允許非同步執行用於語句相關的作業，例如準備、執行和提取，以及目錄中繼資料作業。 從 ODBC 3.8 開始，也可以對連接相關的作業（例如 connect、disconnect、commit 和 rollback）進行非同步執行。  
  
 如需 ODBC 3.8 的詳細資訊，請參閱[odbc 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
 在下列案例中，非同步執行連接作業非常有用：  
  
-   當少數的執行緒以非常高的資料速率來管理大量的裝置時。 若要將回應能力和擴充性最大化，所有作業都是非同步。  
  
-   當您想要在多個連接上重迭資料庫作業，以減少經過的傳輸時間。  
  
-   有效率的非同步 ODBC 呼叫和取消連接作業的功能，可讓應用程式允許使用者取消任何緩慢的操作，而不需要等候超時。  
  
 下列在連接控制碼上運作的函式現在可以非同步執行：  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 為了判斷驅動程式是否支援這些函式的非同步作業，應用程式會使用 SQL_ASYNC_DBC_FUNCTIONS 來呼叫**SQLGetInfo** 。 如果支援非同步作業，則會傳回 SQL_ASYNC_DBC_CAPABLE。 如果不支援非同步作業，則會傳回 SQL_ASYNC_DBC_NOT_CAPABLE。  
  
 若要指定以特定連接執行的函式要以非同步方式執行，應用程式會呼叫**SQLSetConnectAttr** ，並將 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 屬性設為 SQL_ASYNC_DBC_ENABLE_ON。 在建立連接之前設定連接屬性一律會以同步方式執行。 此外，使用**SQLSetConnectAttr**設定連接屬性 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 的作業，一律會以同步方式執行。  
  
 應用程式可以在建立連接之前啟用非同步作業。 因為驅動程式管理員無法在建立連線之前判斷要使用哪一個驅動程式，所以驅動程式管理員在**SQLSetConnectAttr**中一律會傳回成功。 不過，如果 ODBC 驅動程式不支援非同步作業，它可能會無法連接。  
  
 一般來說，最多隻能有一個與特定連接控制碼或語句控制碼相關聯的非同步執行函數。 不過，連接控制碼可以有一個以上關聯的語句控制碼。 如果沒有在連接控制碼上執行的非同步作業，相關聯的語句控制碼就可以執行非同步作業。 同樣地，如果任何相關聯的語句控制碼上沒有進行中的非同步作業，您可以在連接控制碼上進行非同步作業。 嘗試使用目前正在執行非同步作業的控制碼來執行非同步作業，將會傳回 HY010，「函數順序錯誤」。  
  
 如果連接作業傳回 SQL_STILL_EXECUTING，應用程式只能針對該連接控制碼呼叫原始函式和下列函數：  
  
-   **SQLCancelHandle** （在連接控制碼上）  
  
-   **SQLGetDiagField**  
  
-   **SQLGetDiagRec**  
  
-   **SQLAllocHandle** （配置 ENV/DBC）  
  
-   **SQLAllocHandleStd** （配置 ENV/DBC）  
  
-   **SQLGetEnvAttr**  
  
-   **SQLGetConnectAttr**  
  
-   **SQLDataSources**  
  
-   **SQLDrivers**  
  
-   **SQLGetInfo**  
  
-   **SQLGetFunctions**  
  
 應用程式應該在原始函數的重複迴圈中處理診斷記錄。 如果在非同步函式執行時呼叫 SQLGetDiagField 或 SQLGetDiagRec，它會傳回目前的診斷記錄清單。 每當原始函式呼叫重複時，就會清除先前的診斷記錄。  
  
 如果以非同步方式開啟或關閉連接，當應用程式接收到原始函數呼叫 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 時，作業就會完成。  
  
 ODBC 3.8 （ **SQLCancelHandle**）已加入新函數。 此函式會取消六個連接函式（**SQLBrowseConnect**、 **SQLConnect**、 **SQLDisconnect**、 **SQLDriverConnect**、 **SQLEndTran**和**SQLSetConnectAttr**）。 應用程式應該呼叫**SQLGetFunctions**來判斷驅動程式是否支援**SQLCancelHandle**。 如同**SQLCancel**，如果**SQLCancelHandle**傳回 success，則不表示作業已取消。 應用程式應該再次呼叫原始函式，以判斷作業是否已取消。 **SQLCancelHandle**可讓您取消連接控制碼或語句控制碼上的非同步作業。 使用**SQLCancelHandle**取消語句控制碼上的作業，與呼叫**SQLCancel**相同。  
  
 不需要同時支援**SQLCancelHandle**和非同步連接作業。 驅動程式可以支援非同步連接作業，但不能**SQLCancelHandle**，反之亦然。  
  
 ODBC 3.x 和 odbc 2.x 應用程式也可以使用非同步連接作業和**SQLCancelHandle**搭配 odbc 3.8 驅動程式和 Odbc 3.8 驅動程式管理員。 如需如何讓繼承應用程式在稍後的 ODBC 版本中使用新功能的相關資訊，請參閱[相容性對照表](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
### <a name="connection-pooling"></a>連接共用  
 每當啟用連接共用時，僅支援非同步作業來建立連接（使用**SQLConnect**和**SQLDriverConnect**），並關閉與**SQLDisconnect**的連接。 但是，應用程式仍然可以處理來自**SQLConnect**、 **SQLDriverConnect**和**SQLDisconnect**的 SQL_STILL_EXECUTING 傳回值。  
  
 啟用連接共用時，非同步作業會支援**SQLEndTran**和**SQLSetConnectAttr** 。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 下列範例示範如何使用**SQLSetConnectAttr** ，為連接相關的函式啟用非同步執行功能。  
  
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
 這個範例會顯示非同步認可作業。 復原作業也可以透過這種方式來完成。  
  
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
