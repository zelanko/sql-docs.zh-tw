---
description: 分析 ODBC 驅動程式效能
title: 分析 ODBC 驅動程式效能 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- profiling ODBC driver performance data [SQL Server Native Client]
- performance [ODBC]
- application statistics [ODBC]
- time statistics [ODBC]
- ODBC, performance data
- SQL Server Native Client ODBC driver, profiling performance data
- SQLPERF data structure
- statistical information [ODBC]
ms.assetid: 8f44e194-d556-4119-a759-4c9dec7ecead
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 172557586f7198bcc6151fd58f12faa0683f4fc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428120"
---
# <a name="profiling-odbc-driver-performance"></a>分析 ODBC 驅動程式效能
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式可以分析兩種類型的效能資料：  
  
-   長時間執行的查詢。  
  
     驅動程式可以將指定時間內，沒有從伺服器取得回應的任何查詢寫入記錄檔中。 接著，應用程式的程式設計師或資料庫管理員可以研究每個記錄的 SQL 陳述式來決定改善其效能的方式。  
  
-   驅動程式效能資料。  
  
     驅動程式可以記錄效能統計資料，然後將其寫入檔案中，或透過名稱為 SQLPERF 的驅動程式專屬資料結構，提供給應用程式。 包含效能統計資料的檔案是一個以 Tab 分隔的檔案，可以利用支援以 Tab 分隔之檔案的任何試算表 (例如，Microsoft Excel) 輕鬆進行分析。  
  
 每種分析類型都可以透過下列方式開啟：  
  
-   連接至指定記錄的資料來源。  
  
-   呼叫 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 可設定控制分析的驅動程式特定屬性。  
  
 每個應用程式處理序都可以取得自己的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式複本，而且分析通用於驅動程式複本和應用程式處理序的組合。 當應用程式中的任何項目開啟分析時，分析會記錄來自該應用程式的驅動程式中，所有作用中連接的資訊。 甚至是沒有特別針對分析呼叫的連接也包含在內。  
  
 驅動程式開啟分析記錄 (效能資料或長時間執行的查詢記錄) 後，如果應用程式釋放它在驅動程式中開啟的所有環境控制代碼，它不會關閉記錄，直到 ODBC 驅動程式管理員卸載該驅動程式為止。 如果應用程式開啟一個新的環境控制代碼，就會載入驅動程式的新複本。 如果應用程式接著連接到指定相同記錄檔的資料來源，或將驅動程式專屬屬性設定為記錄到相同的檔案，驅動程式就會覆寫舊的記錄。  
  
 如果應用程式開始記錄檔的分析，而且有另一個應用程式嘗試開始相同記錄檔的分析，則第二個應用程式無法記錄任何分析資料。 如果第二個應用程式在第一個應用程式卸載其驅動程式後開始分析，第二個應用程式會覆寫來自第一個應用程式的記錄檔。  
  
 如果應用程式連接到已啟用分析的資料來源，則驅動程式會在應用程式呼叫 **SQLSetConnectOption** 來開始記錄時，傳回 SQL_ERROR。 呼叫 **SQLGetDiagRec** ，然後傳回下列內容：  
  
```  
SQLState: 01000, pfNative = 0  
ErrorMsg: [Microsoft][SQL Server Native Client]  
   An error has occurred during the attempt to access  
   the log file, logging disabled.  
```  
  
 當環境控制代碼關閉時，驅動程式會停止蒐集效能資料。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 應用程式有多個連接，而且每個連接都有自己的環境控制代碼，當任何相關聯的環境控制代碼關閉時，驅動程式將會停止蒐集效能資料。  
  
 驅動程式的效能資料可以儲存在 SQLPERF 資料結構中，也可以記錄到以 Tab 分隔的檔案中。 此資料包括下列類別的統計資料：  
  
-   應用程式設定檔  
  
-   Connection  
  
-   Network (網路)  
  
-   Time  
  
 在下表中，SQLPERF 資料結構內的欄位描述也會套用到效能記錄檔中記錄的統計資料。  
  
### <a name="application-profile-statistics"></a>應用程式設定檔統計資料  
  
|SQLPERF 欄位|描述|  
|-------------------|-----------------|  
|TimerResolution|伺服器時間的最小解析 (以毫秒為單位)。 這通常會報告為 0 (零)，而且只有在報告的數字很大時，才考慮使用。 如果伺服器時間的最小解析大於某些以計時器為基礎之統計資料的可能間隔，這些統計資料可能會擴大。|  
|SQLidu|SQL_PERF_START 之後的 INSERT、DELETE 或 UPDATE 陳述式數目。|  
|SQLiduRows|SQL_PERF_START 之後的 INSERT、DELETE 或 UPDATE 陳述式數目。|  
|SQLSelects|在 SQL_PERF_START 之後處理的 SELECT 陳述式數目。|  
|SQLSelectRows|在 SQL_PERF_START 之後選取的資料列數目。|  
|交易|SQL_PERF_START 之後的使用者交易數目，包括回復。 當 ODBC 應用程式使用 SQL_AUTOCOMMIT_ON 執行時，會將每個命令視為交易。|  
|SQLPrepares|SQL_PERF_START 後的 [SQLPrepare 函數](https://go.microsoft.com/fwlink/?LinkId=59360) 調用數目。|  
|ExecDirects|SQL_PERF_START 之後的 **SQLExecDirect** 呼叫數目。|  
|SQLExecutes|SQL_PERF_START 之後的 **SQLExecute** 呼叫數目。|  
|CursorOpens|驅動程式在 SQL_PERF_START 之後已經開啟伺服器資料指標的次數。|  
|CursorSize|在 SQL_PERF_START 之後，資料指標開啟之結果集中的資料列數目。|  
|CursorUsed|在 SQL_PERF_START 之後，透過驅動程式從資料指標實際擷取的資料列數目。|  
|PercentCursorUsed|等於 CursorUsed/CursorSize。 例如，如果應用程式使驅動程式開啟伺服器資料指標來執行 "SELECT COUNT(*) FROM Authors"，SELECT 陳述式的結果集中將有 23 個資料列。 接著，如果應用程式只提取其中三個資料列，CursorUsed/CursorSize 為 3/23，因此 PercentCursorUsed 為 13.043478。|  
|AvgFetchTime|等於 SQLFetchTime/SQLFetchCount。|  
|AvgCursorSize|等於 CursorSize/CursorOpens。|  
|AvgCursorUsed|等於 CursorUsed/CursorOpens。|  
|SQLFetchTime|根據伺服器資料指標完成提取所需的累計時間。|  
|SQLFetchCount|在 SQL_PERF_START 之後，根據伺服器資料指標完成的提取數目。|  
|CurrentStmtCount|目前在驅動程式中開啟的所有連接上開啟的陳述式控制代碼數目。|  
|MaxOpenStmt|在 SQL_PERF_START 之後，同時開啟之陳述式控制代碼的最大數目。|  
|SumOpenStmt|在 SQL_PERF_START 之後，已經開啟之陳述式控制代碼的數目。|  
|**連接統計資料**||  
|CurrentConnectionCount|應用程式已經在伺服器上開啟之作用中連接控制代碼的目前數目。|  
|MaxConnectionsOpened|在 SQL_PERF_START 之後開啟之並行連接控制代碼的最大數目。|  
|SumConnectionsOpened|在 SQL_PERF_START 之後，已經開啟之連接控制代碼的數目總和。|  
|SumConnectionTime|在 SQL_PERF_START 之後，已經開啟之所有連接的時間總和。 例如，如果應用程式開啟 10 個連接，而且每個連接維持 5 秒鐘，則 SumConnectionTime 為 50 秒。|  
|AvgTimeOpened|等於 SumConnectionsOpened/SumConnectionTime。|  
|**網路統計資料：**||  
|ServerRndTrips|驅動程式將命令傳送到伺服器並得到回覆的次數。|  
|BuffersSent|SQL_PERF_START 之後，驅動程式傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的表格式資料流 (TDS) 封包數目。 大型命令可以佔用多個緩衝區，因此，如果將大型命令傳送到伺服器，而且填滿六個封包，ServerRndTrips 會以 1 遞增，而 BuffersSent 則會以 6 遞增。|  
|BuffersRec|應用程式使用驅動程式啟動後，從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之驅動程式接收的 TDS 封包數目。|  
|BytesSent|應用程式使用驅動程式啟動後，以 TDS 封包將資料傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的位元組數目。|  
|BytesRec|應用程式使用驅動程式啟動後，從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之驅動程式接收的 TDS 封包資料位元組數目。|  
  
### <a name="time-statistics"></a>時間統計資料  
  
|SQLPERF 欄位|描述|  
|-------------------|-----------------|  
|msExecutionTime|驅動程式在 SQL_PERF_START 之後，花在處理上的累計時間，包括花在等待伺服器回覆的時間。|  
|msNetworkServerTime|驅動程式花在等待伺服器回覆的累計時間。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [&#40;ODBC&#41;分析 ODBC 驅動程式效能的使用說明主題 ](../../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)  
  
  
