---
title: 非同步執行 （輪詢方法） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- asynchronous execution [ODBC]
ms.assetid: 8cd21734-ef8e-4066-afd5-1f340e213f9c
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d64874a4633e7bede14051d882925f633dadc36c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913823"
---
# <a name="asynchronous-execution-polling-method"></a>非同步執行 （輪詢方法）
ODBC 3.8 和 Windows 7 SDK 之前, 才被允許陳述式的函式的非同步作業。 如需詳細資訊，請參閱**非同步執行陳述式作業**稍後在本主題中。  
  
 Windows 7 SDK 中的 ODBC 3.8 導入了連接相關作業的非同步執行。 如需詳細資訊，請參閱**非同步執行連線作業**區段中，本主題稍後的。  
  
 在 Windows 7 SDK 中，非同步的陳述式或連接作業，應用程式會判斷非同步作業已完成使用輪詢方法。 從 Windows 8 SDK 開始，您可以判斷非同步作業已完成使用的通知方法。 如需詳細資訊，請參閱[非同步執行 （通知方法）](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)。  
  
 依預設，驅動程式執行 ODBC 函數以同步方式;也就是說，應用程式呼叫的函式，而且驅動程式不會將控制權傳回給應用程式完成執行函式之前。 不過，以非同步的方式; 執行某些函式也就是說，應用程式呼叫函式，而且驅動程式，最少經過處理後，控制權傳回給應用程式。 第一個函式仍在執行時，應用程式就可以呼叫其他函式。  
  
 對於大部分的資料來源執行的大部分函式支援非同步執行，例如建立連接、 準備及執行 SQL 陳述式，函式會擷取中繼資料，擷取資料，以及認可的交易。 當資料來源上正在執行的工作需要較長的時間，例如登入程序或複雜的查詢，對大型資料庫，它便最有用。  
  
 當應用程式執行的陳述式或連接已啟用非同步處理的函式時，驅動程式執行最少量的處理 （例如，檢查有錯誤的引數）、 交給處理到資料來源，並傳回控制 SQL_STILL_EXECUTING 傳回程式碼在應用程式。 接著，應用程式會執行其他工作。 若要判斷完成的非同步函式時，應用程式的驅動程式會定期輪詢藉由呼叫具有相同的引數，因為它原本使用的函式。 如果函式仍在執行中，它會傳回 SQL_STILL_EXECUTING。如果它已完成執行時，它會傳回它會傳回具有它以同步方式執行，例如 SQL_SUCCESS、 SQL_ERROR 或 SQL_NEED_DATA 的程式碼。  
  
 函式是執行以同步或非同步方式，是特定的驅動程式。 例如，假設結果集中繼資料會快取中的驅動程式。 在此情況下，需要極少的時間才能執行**SQLDescribeCol**和驅動程式應該只執行該函式，而延遲執行，以人為方式。 相反地，如果驅動程式必須從資料來源擷取中繼資料，應該要傳回控制項至應用程式時，它會執行此動作。 因此，應用程式必須能夠處理 SQL_STILL_EXECUTING 以外的傳回碼，當它第一次執行的函式以非同步的方式。  
  
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
  
 每個陳述式或以每個連線為基礎，視資料來源上控制非同步陳述式執行。 也就是應用程式指定不特定函式是以非同步方式執行，但在特定陳述式上執行任何函式是以非同步方式執行。 若要尋找支援哪一個超出，應用程式呼叫[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) SQL_ASYNC_MODE 選擇。 如果支援連接層級 （適用於陳述式控制代碼） 的非同步執行，則會傳回 SQL_AM_CONNECTIONSQL_AM_STATEMENT 支援非同步執行的陳述式層級。  
  
 若要指定執行特定陳述式的函式是要以非同步方式執行，應用程式會呼叫**SQLSetStmtAttr** SQL_ATTR_ASYNC_ENABLE 與屬性，並將其設為請。 如果支援連接層級的非同步處理，SQL_ATTR_ASYNC_ENABLE 陳述式屬性是唯讀的且其值為陳述式會配置所在連接的連接屬性相同。 它是驅動程式專屬的陳述式屬性值是否設定陳述式配置的時間或更新版本。 嘗試將其設定將會傳回 SQL_ERROR 並 SQLSTATE HYC00 （未實作的選擇性功能）。  
  
 若要指定特定的連接來執行的函式是要以非同步方式執行，應用程式會呼叫**SQLSetConnectAttr** SQL_ATTR_ASYNC_ENABLE 與屬性，並將其設為請。 在此連接上配置的所有未來的陳述式控制代碼都將啟用非同步執行。它是驅動程式定義的這個動作是否啟用現有的陳述式控制代碼。 如果 SQL_ATTR_ASYNC_ENABLE 設定為 SQL_ASYNC_ENABLE_OFF，連接上的所有陳述式就會處於同步模式。 如果在連接上的作用中陳述式時，已啟用非同步執行，則會傳回錯誤。  
  
 若要判斷在驅動程式可支援給定連接的非同步模式的作用中並行陳述式的最大數目，應用程式呼叫**SQLGetInfo** SQL_MAX_ASYNC_CONCURRENT_STATEMENTS 選項。  
  
 下列程式碼說明如何使用輪詢模型：  
  
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
  
 當函式以非同步方式執行時，應用程式可以呼叫函式的任何其他陳述式。 應用程式也可以呼叫函式，除了非同步陳述式相關聯的任何連線。 但是，應用程式可以只呼叫原始函式和下列函式 （具有陳述式控制代碼或其相關聯的連接，環境控制代碼） 之後的陳述式作業傳回 SQL_STILL_EXECUTING:  
  
-   [SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) (on 陳述式控制代碼）  
  
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
  
 如果應用程式呼叫其他任何函式使用非同步的陳述式，或與該陳述式相關聯的連接，則函數會傳回 SQLSTATE HY010 （函數順序錯誤），例如。  
  
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
  
 當應用程式呼叫的函式來判斷是否仍在執行以非同步方式時，它必須使用原始陳述式控制代碼。 這是因為非同步執行會追蹤每個陳述式為基礎。 應用程式也必須提供有效的引數的值 — 原始引數會進行 — 取得以前的錯誤檢查驅動程式管理員。 不過，驅動程式會檢查陳述式控制代碼，並判斷以非同步方式執行的陳述式之後，它就會忽略所有其他引數。  
  
 函式以非同步方式執行時，也就是它已傳回 SQL_STILL_EXECUTING 之後之前, 它會傳回不同的程式碼，應用程式可以藉由呼叫取消它**SQLCancel**或**SQLCancelHandle**具有相同的陳述式控制代碼。 這不保證取消函式執行。 例如，函式可能已經完成。 此外，程式碼傳回**SQLCancel**或**SQLCancelHandle**只表示嘗試取消函式是否成功，不是否確實已取消函式。 若要判斷函數是否已取消，應用程式會再次呼叫函式。 如果函式已取消，則會傳回 SQL_ERROR 並 SQLSTATE HY008 （取消作業）。 如果未取消函式，它會傳回另一個程式碼，例如 SQL_SUCCESS、 SQL_STILL_EXECUTING 或 sql_error，其中包含不同的 SQLSTATE。  
  
 若要停用特定的陳述式的非同步執行時，驅動程式支援陳述式層級非同步處理，應用程式會呼叫**SQLSetStmtAttr** SQL_ATTR_ASYNC_ENABLE 與屬性，並將其設為 SQL_ASYNC_ENABLE_OFF。 如果驅動程式支援連接層級的非同步處理，應用程式呼叫**SQLSetConnectAttr**將 SQL_ATTR_ASYNC_ENABLE 設定為 SQL_ASYNC_ENABLE_OFF，會非同步執行的所有陳述式停用連接。  
  
 應用程式應該會處理重複的原始函式的迴圈中的診斷記錄。 如果**SQLGetDiagField**或**SQLGetDiagRec**稱為時執行的非同步函式時，它會傳回目前的診斷記錄的清單。 每次重複的原始函式呼叫時，它會清除先前的診斷記錄。  
  
## <a name="executing-connection-operations-asynchronously"></a>以非同步方式執行連線作業  
 ODBC 3.8 之前請允許非同步執行，例如準備陳述式相關的作業、 執行和擷取，也與目錄中繼資料作業。 從開始 ODBC 3.8，非同步執行，也可以針對連線相關的作業，例如當連線時，中斷連線、 commit 和 rollback。  
  
 如需有關 ODBC 3.8 的詳細資訊，請參閱[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。  
  
 以非同步方式執行連接作業是在下列案例中很有用：  
  
-   當少量執行緒管理大量的裝置使用非常高資料速率。 若要最大化回應性和延展性最好是非同步的所有作業。  
  
-   當您想要重疊資料庫作業，透過多個連線，以減少整體的傳輸時間。  
  
-   有效率的非同步 ODBC 呼叫和取消連接作業的能力可讓應用程式可讓使用者取消任何很慢的作業，而不必等候逾時。  
  
 下列函式，在連接控制代碼運作，現在可以在以非同步方式執行：  
  
||||  
|-|-|-|  
|[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
 若要判斷驅動程式是否支援這些函式的非同步作業，應用程式呼叫**SQLGetInfo** SQL_ASYNC_DBC_FUNCTIONS 與。 如果支援非同步作業，則會傳回 SQL_ASYNC_DBC_CAPABLE。 如果不支援非同步作業，則會傳回 SQL_ASYNC_DBC_NOT_CAPABLE。  
  
 若要指定特定的連接來執行的函式是要以非同步方式執行，應用程式會呼叫**SQLSetConnectAttr** ，設 SQL_ASYNC_DBC_ENABLE SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 屬性_ON。 設定連接屬性之前建立的連接一律會以同步方式執行。 此外，設定連接的作業屬性 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 與**SQLSetConnectAttr**一律以同步方式執行。  
  
 應用程式可以啟用非同步作業之前進行連接。 因為驅動程式管理員無法判斷哪一個驅動程式以使用，才能建立連接，驅動程式管理員一律會傳回成功的**SQLSetConnectAttr**。 不過，它可能無法連接如果 ODBC 驅動程式不支援非同步作業。  
  
 一般情況下，可以有最多一個以非同步方式執行函式相關聯的特定連接控制代碼或陳述式控制代碼。 不過，在連接控制代碼可以有多個相關聯的陳述式控制代碼。 如果沒有在連接控制代碼上執行非同步作業，相關聯的陳述式控制代碼可以執行非同步作業。 同樣地，您可以有連接控制代碼上的非同步作業，如果沒有任何相關聯的陳述式控制代碼上非同步作業進行中。 嘗試執行非同步作業使用的控制代碼，目前正在執行非同步作業會傳回 HY010，「 函數順序錯誤 」。  
  
 如果連接作業傳回 SQL_STILL_EXECUTING 時，應用程式可以只針對該連接控制代碼呼叫原始函式與下列函式：  
  
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
  
 應用程式應該會處理重複的原始函式的迴圈中的診斷記錄。 SQLGetDiagField 或 SQLGetDiagRec 稱為非同步函式執行時，它會傳回目前的診斷記錄的清單。 每次重複的原始函式呼叫時，它會清除先前的診斷記錄。  
  
 如果連接是開啟或關閉以非同步方式，當應用程式收到 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 原始函式呼叫中的作業已完成。  
  
 新的函式已加入至 ODBC 3.8 **SQLCancelHandle**。 此函式取消的六個連接函式 (**SQLBrowseConnect**， **SQLConnect**， **SQLDisconnect**， **SQLDriverConnect**，**SQLEndTran**，和**SQLSetConnectAttr**)。 應用程式應該呼叫**SQLGetFunctions**決定驅動程式是否支援**SQLCancelHandle**。 如同**SQLCancel**，如果**SQLCancelHandle**傳回成功，並不表示已取消作業。 應用程式應該呼叫一次來判斷已取消作業的原始函數。 **SQLCancelHandle**可讓您取消非同步作業，在連接控制代碼或陳述式控制代碼。 使用**SQLCancelHandle**取消作業的陳述式控制代碼等同於呼叫**SQLCancel**。  
  
 不需要同時支援**SQLCancelHandle**和非同步連線作業一次。 驅動程式可以支援非同步連接作業，但不是**SQLCancelHandle**，反之亦然。  
  
 非同步連接作業和**SQLCancelHandle**也可由 ODBC 3.x 和 ODBC 2.x 應用程式使用 ODBC 3.8 驅動程式和 ODBC 3.8 驅動程式管理員。 如需瞭解如何讓舊版應用程式使用較新的 ODBC 版本中的新功能的相關資訊，請參閱[相容性比較表](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
### <a name="connection-pooling"></a>連接共用  
 每當啟用連接共用時，只使用最低限度支援非同步作業建立之連接 (使用**SQLConnect**和**SQLDriverConnect**) 和關閉的連線**SQLDisconnect**。 應用程式應該仍然能夠處理來自 SQL_STILL_EXECUTING 傳回值，但是**SQLConnect**， **SQLDriverConnect**，和**SQLDisconnect**。  
  
 啟用連接共用時， **SQLEndTran**和**SQLSetConnectAttr**支援非同步作業。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>Description  
 下列範例示範如何使用**SQLSetConnectAttr**啟用連線相關的函式的非同步執行。  
  
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
  
### <a name="description"></a>Description  
 這個範例示範非同步認可作業。 回復作業也可以透過這種方式。  
  
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
