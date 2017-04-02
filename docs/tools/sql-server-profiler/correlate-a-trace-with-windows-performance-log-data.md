---
title: "使追蹤與 Windows 效能記錄資料相互關聯 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "使追蹤與記錄資料相互關聯"
  - "記錄 [SQL Server], 追蹤"
  - "Profiler [SQL Server Profiler], 使追蹤與記錄資料相互關聯"
  - "追蹤 [SQL Server], 記錄"
  - "SQL Server Profiler, 使追蹤與記錄資料相互關聯"
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# 使追蹤與 Windows 效能記錄資料相互關聯
  使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以開啟 Microsoft Windows 效能記錄，選擇要與追蹤相互關連的計數器，而且在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 圖形化使用者介面中，讓選取的效能計數器顯示在追蹤的旁邊。 選取追蹤視窗中的事件後，[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的 [系統監視器] 資料窗格中的紅色直條，表示與選取的追蹤事件相互關聯的效能記錄資料。  
  
 若要使追蹤與效能計數器相互關聯，請開啟包含 **StartTime** 與 **EndTime** 資料行的追蹤檔案或資料表，然後在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] [檔案] 功能表上，按一下 [匯入效能資料]。 接著可以開啟效能記錄，然後選取要與追蹤相互關聯的「系統監視器」物件與計數器。  
  
## 另請參閱  
 [使追蹤與 Windows 效能記錄資料相互關聯 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  