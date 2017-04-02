---
title: "啟動追蹤 | Microsoft Docs"
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
  - "SQL Server Profiler, 停止追蹤"
  - "暫停追蹤"
  - "分析工具 [SQL Server Profiler], 停止追蹤"
  - "分析工具 [SQL Server Profiler], 啟動追蹤"
  - "追蹤 [SQL Server], 啟動"
  - "SQL Server Profiler, 暫停追蹤"
  - "追蹤 [SQL Server], 停止"
  - "分析工具 [SQL Server Profiler], 暫停追蹤"
  - "追蹤 [SQL Server], 暫停"
  - "SQL Server Profiler, 啟動追蹤"
  - "停止追蹤"
  - "啟動追蹤"
ms.assetid: aeeb38eb-229a-4c8b-ad66-57e9ce45fb6a
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# 啟動追蹤
  在您使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來定義新追蹤或建立範本之後，即可使用新的追蹤定義或範本來啟動、暫停或停止擷取資料。  
  
## 啟動追蹤  
 當您啟動追蹤，而且所定義的來源是 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 便會建立一個佇列，以提供暫存空間來放置所擷取的伺服器事件。  
  
 當您使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來存取 SQL 追蹤時，啟動追蹤時就會開啟新的追蹤視窗 (如果尚未開啟)，並立即擷取資料。  
  
 當您使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系統預存程序來存取 SQL 追蹤時，您必須在每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時啟動追蹤，以便擷取資料。 啟動追蹤後，您只能修改追蹤的名稱。  
  
> [!NOTE]  
>  使用現有的追蹤時，您可以檢視屬性，但是不能修改屬性。 若要修改屬性，請停止或暫停追蹤。  
  
## 另請參閱  
 [在連接伺服器之後自動啟動追蹤 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [暫停追蹤 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/pause-a-trace-sql-server-profiler.md)   
 [停止追蹤 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/stop-a-trace-sql-server-profiler.md)   
 [清除追蹤視窗 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/clear-a-trace-window-sql-server-profiler.md)   
 [在追蹤暫停或停止之後執行追蹤 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  