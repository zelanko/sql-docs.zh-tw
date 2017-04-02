---
title: "SQL Server Profiler 範本和權限 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Profiler [SQL Server Profiler], 關於 SQL Server Profiler"
  - "SQL Server Profiler, 關於 SQL Server Profiler"
ms.assetid: 6d00378a-5d74-463b-9ed6-a2685306a9d2
caps.latest.revision: 34
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 34
---
# SQL Server Profiler 範本和權限
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何在內部解析查詢。 這可讓系統管理員確切地查看哪些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或「多維度運算式」已提交給伺服器，以及伺服器如何存取資料庫或 Cube，以傳回結果集。  
  
 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以執行下列動作：  
  
-   建立根據可重複使用範本的追蹤  
  
-   在追蹤執行時監視追蹤結果  
  
-   將追蹤結果儲存在資料表  
  
-   視需要啟動、停止、暫停和修改追蹤結果  
  
-   重新執行追蹤結果  
  
 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 時，只需監視您有興趣的事件。 如果追蹤變得太大，您可以根據所要的資訊加以篩選，以便只收集事件資料的子集。 監視太多事件會增加伺服器與監視處理序的負擔，且會使得追蹤檔案或追蹤資料表增長過大，尤其是需要花費長時間的監視處理序更是如此。  
  
> [!NOTE]  
>  大於 1GB 的追蹤資料行值會傳回錯誤，並在追蹤輸出中截斷。  
  
## 本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[SQL Server Profiler 範本](../../tools/sql-server-profiler/sql-server-profiler-templates.md)|包含 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 隨附之預先定義追蹤範本的相關資訊。|  
|[執行 SQL Server Profiler 所需的權限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)|包含執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 所需權限的相關資訊。|  
|[儲存追蹤及追蹤範本](../../tools/sql-server-profiler/save-traces-and-trace-templates.md)|包含儲存追蹤輸出以及將追蹤定義儲存到範本的相關資訊。|  
|[修改追蹤範本](../../tools/sql-server-profiler/modify-trace-templates.md)|包含使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 或使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 修改追蹤範本的相關資訊。|  
|[啟動追蹤](../../tools/sql-server-profiler/start-a-trace.md)|包含當啟動、暫停或停止追蹤時所發生情況的相關資訊。|  
|[使追蹤與 Windows 效能記錄資料相互關聯](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data.md)|包含使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler，讓 Windows 效能記錄資料與追蹤產生關聯的相關資訊。|  
|[使用 SQL Server Profiler 檢視和分析追蹤](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)|包含使用追蹤來進行資料的疑難排解、在追蹤中顯示物件名稱，以及在追蹤中尋找事件的相關資訊。|  
|[使用 SQL Server Profiler 分析死結](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)|包含使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來識別死結原因的相關資訊。|  
|[在 SQL Server Profiler 中使用 SHOWPLAN 結果分析查詢](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)|包含使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來收集並顯示顯示計畫與顯示計畫統計結果的相關資訊。|  
|[使用 SQL Server Profiler 篩選追蹤](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md)|包含使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 對資料行設定篩選，用來篩選追蹤輸出的相關資訊。|  
|[重新執行追蹤](../../tools/sql-server-profiler/replay-traces.md)|包含說明重新執行追蹤的意義，以及重新執行追蹤的必要條件等之相關資訊。|  
  
## 另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [啟動 SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  