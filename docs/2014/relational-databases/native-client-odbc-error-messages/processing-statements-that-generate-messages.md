---
title: 處理產生訊息的語句 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- PRINT statement
- messages [ODBC], statements generating messages
- statements [ODBC], message generation
- errors [ODBC], statements generating messages
- SQL Server Native Client ODBC driver, errors
- STATISTICS IO option
- STATISTICS TIME option
- DBCC statements
- SQLExecute function
- RAISERROR statement
- SQLGetDiagRec function
- ODBC error handling, statements generating messages
- SQLExecDirect function
ms.assetid: 672ebdc5-7fa1-4ceb-8d52-fd25ef646654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11235979a886e82fa09ca1d1a79fa21550965d0f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205695"
---
# <a name="processing-statements-that-generate-messages"></a>處理產生訊息的陳述式
  
  [!INCLUDE[tsql](../../includes/tsql-md.md)] SET 陳述式選項 STATISTICS TIME 和 STATISTICS IO 用於取得協助診斷長時間執行之查詢的資訊。 舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也支援 SHOWPLAN 選項來分析查詢計畫。 ODBC 應用程式可以執行下列陳述式來設定這些選項：  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 當設定統計資料時間或設定執行程式表是 ON 時， **SQLExecute**和**SQLExecDirect**會傳回 SQL_SUCCESS_WITH_INFO，而此時，應用程式可以藉由呼叫**SQLGetDiagRec**來抓取顯示計畫或統計資料時間輸出，直到它傳回 SQL_NO_DATA 為止。 SHOWPLAN 資料的每一行都會以下列格式傳回：  
  
```  
szSqlState="01000", *pfNativeError=6223,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]   
              Table Scan"  
```  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版會將 SHOWPLAN 選項取代成 SHOWPLAN_ALL 和 SHOWPLAN_TEXT，而且這兩個都會傳回輸出當做結果集，而且一組訊息。  
  
 STATISTICS TIME 資料的每一行都會以下列格式傳回：  
  
```  
szSqlState="01000", *pfNativeError= 3613,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
   SQL Server Parse and Compile Time: cpu time = 0 ms."  
```  
  
 在結果集結束之前，不會提供 SET STATISTICS IO 的輸出。 若要取得統計資料 IO 輸出，應用程式會在**SQLFetch**或[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)傳回 SQL_NO_DATA 時呼叫**SQLGetDiagRec** 。 STATISTICS IO 的輸出會以下列格式傳回：  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>使用 DBCC 陳述式  
 DBCC 陳述式會傳回其資料做為訊息，而非結果集。 **SQLExecDirect**或**SQLExecute**會傳回 SQL_SUCCESS_WITH_INFO，而應用程式會藉由呼叫**SQLGetDiagRec**來抓取輸出，直到傳回 SQL_NO_DATA 為止。  
  
 例如，下列陳述式會傳回 SQL_SUCCESS_WITH_INFO：  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 呼叫**SQLGetDiagRec**會傳回：  
  
```  
szSqlState = "01000", *pfNativeError = 2536,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Checking authors"  
szSqlState = "01000", *pfNativeError = 2579,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   The total number of data pages in this table is 1."  
szSqlState = "01000", *pfNativeError = 7929,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table has 23 data rows."  
szSqlState = "01000", *pfNativeError = 2528  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   DBCC execution completed. If DBCC printed error messages,  
   see your System Administrator."  
```  
  
## <a name="using-print-and-raiserror-statements"></a>使用 PRINT 和 RAISERROR 陳述式  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]PRINT 和 RAISERROR 語句也會藉由呼叫**SQLGetDiagRec**來傳回資料。 PRINT 語句會導致 SQL 語句執行傳回 SQL_SUCCESS_WITH_INFO，後續對**SQLGetDiagRec**的呼叫會傳回01000的*SQLState* 。 嚴重性為 10 或更低之 RAISERROR 陳述式的行為與 PRINT 相同。 嚴重性為11或更高的 RAISERROR 會導致執行傳回 SQL_ERROR，而後續的**SQLGetDiagRec**呼叫會傳回*SQLState* 42000。 例如，下列陳述式會傳回 SQL_SUCCESS_WITH_INFO：  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 呼叫**SQLGetDiagRec**會傳回：  
  
```  
szSQLState = "01000", *pfNative Error = 0,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Some message"  
```  
  
 下列陳述式會傳回 SQL_SUCCESS_WITH_INFO：  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 1.', 10, -1)",  
   SQL_NTS)  
```  
  
 呼叫**SQLGetDiagRec**會傳回：  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 下列陳述式會傳回 SQL_ERROR：  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 呼叫**SQLGetDiagRec**會傳回：  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 當來自 PRINT 或 RAISERROR 語句的輸出包含在結果集中時，呼叫**SQLGetDiagRec**的時機很重要。 **SQLGetDiagRec**用來抓取 PRINT 或 RAISERROR 輸出的呼叫，必須緊接在接收 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 的語句之後才進行。 僅執行單一 SQL 陳述式時，這是相當直接的，如以上的範例所示。 在這些情況下，呼叫**SQLExecDirect**或**SQLExecute**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，然後可以呼叫**SQLGetDiagRec** 。 當編碼使用迴圈處理 SQL 陳述式的批次輸出時，或執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序時，比較不直接。  
  
 在此情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對批次或預存程序中執行的每個 SELECT 陳述式傳回一個結果集。 如果批次或程序包含 PRINT 或 RAISERROR 陳述式，這些陳述式的輸出會與 SELECT 陳述式結果集交錯。 如果批次或程式中的第一個語句是 PRINT 或 RAISERROR，則**SQLExecute**或**SQLExecDirect**會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，而應用程式必須呼叫**SQLGetDiagRec** ，直到它傳回 SQL_NO_DATA 以取得列印或 RAISERROR 資訊為止。  
  
 如果 PRINT 或 RAISERROR 語句位於 SQL 語句（例如 SELECT 語句）之後，則在包含錯誤的結果集上[SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md)位置時，會傳回 PRINT 或 RAISERROR 資訊。 **SQLMoreResults**會根據訊息的嚴重性傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 藉由呼叫**SQLGetDiagRec**來抓取訊息，直到傳回 SQL_NO_DATA 為止。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](handling-errors-and-messages.md)  
  
  
