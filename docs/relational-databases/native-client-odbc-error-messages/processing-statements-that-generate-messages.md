---
title: 處理產生訊息的陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-error-messages
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9475afda740b4c2b2d6b279c0ea0a454fd397bf0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32946703"
---
# <a name="processing-statements-that-generate-messages"></a>處理產生訊息的陳述式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] SET 陳述式選項 STATISTICS TIME 和 STATISTICS IO 用於取得協助診斷長時間執行之查詢的資訊。 舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也支援 SHOWPLAN 選項來分析查詢計畫。 ODBC 應用程式可以執行下列陳述式來設定這些選項：  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 當 SET STATISTICS TIME 或 SET SHOWPLAN 為 ON， **SQLExecute**和**SQLExecDirect**傳回 SQL_SUCCESS_WITH_INFO，而且此時，應用程式可以擷取 SHOWPLAN 或 STATISTICS 時間輸出藉由呼叫**SQLGetDiagRec**直到傳回 sql_no_data 為止。 SHOWPLAN 資料的每一行都會以下列格式傳回：  
  
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
  
 在結果集結束之前，不會提供 SET STATISTICS IO 的輸出。 若要取得 STATISTICS IO 輸出，應用程式會呼叫**SQLGetDiagRec**當時**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)傳回 sql_no_data 為止。 STATISTICS IO 的輸出會以下列格式傳回：  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>使用 DBCC 陳述式  
 DBCC 陳述式會傳回其資料做為訊息，而非結果集。 **SQLExecDirect**或**SQLExecute**傳回 SQL_SUCCESS_WITH_INFO，而且應用程式擷取輸出，藉由呼叫**SQLGetDiagRec**直到傳回 sql_no_data 為止。  
  
 例如，下列陳述式會傳回 SQL_SUCCESS_WITH_INFO：  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 呼叫**SQLGetDiagRec**傳回：  
  
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
 [!INCLUDE[tsql](../../includes/tsql-md.md)] PRINT 和 RAISERROR 陳述式也會傳回資料藉由呼叫**SQLGetDiagRec**。 PRINT 陳述式會使 SQL 陳述式執行傳回 SQL_SUCCESS_WITH_INFO，而且後續呼叫**SQLGetDiagRec**傳回*SQLState*的 01000。 嚴重性為 10 或更低之 RAISERROR 陳述式的行為與 PRINT 相同。 嚴重性為 11 或更高的 RAISERROR 會使執行傳回 SQL_ERROR，而且後續呼叫**SQLGetDiagRec**傳回*SQLState* 42000。 例如，下列陳述式會傳回 SQL_SUCCESS_WITH_INFO：  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 呼叫**SQLGetDiagRec**傳回：  
  
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
  
 呼叫**SQLGetDiagRec**傳回：  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 下列陳述式會傳回 SQL_ERROR：  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 呼叫**SQLGetDiagRec**傳回：  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 呼叫時機**SQLGetDiagRec**時來自 PRINT 或 RAISERROR 陳述式的輸出結果集中包含非常重要。 若要呼叫**SQLGetDiagRec**擷取 PRINT 或 RAISERROR 輸出必須接收 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 的陳述式之後立即進行。 僅執行單一 SQL 陳述式時，這是相當直接的，如以上的範例所示。 在這些情況下，呼叫**SQLExecDirect**或**SQLExecute**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**便可以呼叫。 當編碼使用迴圈處理 SQL 陳述式的批次輸出時，或執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序時，比較不直接。  
  
 在此情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對批次或預存程序中執行的每個 SELECT 陳述式傳回一個結果集。 如果批次或程序包含 PRINT 或 RAISERROR 陳述式，這些陳述式的輸出會與 SELECT 陳述式結果集交錯。 如果批次或程序中的第一個陳述式為 PRINT 或 RAISERROR， **SQLExecute**或**SQLExecDirect**傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，而且應用程式需要呼叫**SQLGetDiagRec**直到傳回 SQL_NO_DATA 來擷取 PRINT 或 RAISERROR 資訊。  
  
 如果 PRINT 或 RAISERROR 陳述式是在 SQL 陳述式 （例如 SELECT 陳述式） 之後, 則 PRINT 或 RAISERROR 資訊時，會傳回[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)位置的結果集，其中包含錯誤。 **SQLMoreResults**根據訊息的嚴重性會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR。 訊息藉由呼叫擷取**SQLGetDiagRec**直到傳回 sql_no_data 為止。  
  
## <a name="see-also"></a>另請參閱  
 [處理錯誤與訊息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
