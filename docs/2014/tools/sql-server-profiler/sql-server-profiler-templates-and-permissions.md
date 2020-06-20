---
title: SQL Server Profiler 範本和權限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], about SQL Server Profiler
- SQL Server Profiler, about SQL Server Profiler
ms.assetid: 6d00378a-5d74-463b-9ed6-a2685306a9d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4185204a5b511237e3074baf5e9add7e7e2672da
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057639"
---
# <a name="sql-server-profiler-templates-and-permissions"></a>SQL Server Profiler 範本和權限
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
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[SQL Server Profiler 範本](sql-server-profiler-templates.md)|包含 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]隨附之預先定義追蹤範本的相關資訊。|  
|[執行 SQL Server Profiler 所需的權限](permissions-required-to-run-sql-server-profiler.md)|包含執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]所需權限的相關資訊。|  
|[儲存追蹤及追蹤範本](save-traces-and-trace-templates.md)|包含儲存追蹤輸出以及將追蹤定義儲存到範本的相關資訊。|  
|[修改追蹤範本](modify-trace-templates.md)|包含使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 或使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]修改追蹤範本的相關資訊。|  
|[啟動追蹤](start-a-trace.md)|包含當啟動、暫停或停止追蹤時所發生情況的相關資訊。|  
|[使追蹤與 Windows 效能記錄資料相互關聯](correlate-a-trace-with-windows-performance-log-data.md)|包含使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler，讓 Windows 效能記錄資料與追蹤產生關聯的相關資訊。|  
|[使用 SQL Server Profiler 檢視和分析追蹤](view-and-analyze-traces-with-sql-server-profiler.md)|包含使用追蹤來進行資料的疑難排解、在追蹤中顯示物件名稱，以及在追蹤中尋找事件的相關資訊。|  
|[使用 SQL Server Profiler 分析死結](analyze-deadlocks-with-sql-server-profiler.md)|包含使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來識別死結原因的相關資訊。|  
|[在 SQL Server Profiler 中使用 SHOWPLAN 結果分析查詢](analyze-queries-with-showplan-results-in-sql-server-profiler.md)|包含使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來收集並顯示顯示計畫與顯示計畫統計結果的相關資訊。|  
|[使用 SQL Server Profiler 篩選追蹤](filter-traces-with-sql-server-profiler.md)|包含使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]對資料行設定篩選，用來篩選追蹤輸出的相關資訊。|  
|[重新執行追蹤](replay-traces.md)|包含說明重新執行追蹤的意義，以及重新執行追蹤的必要條件等之相關資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [[SQL Server Profiler]](sql-server-profiler.md)   
 [啟動 SQL Server Profiler](start-sql-server-profiler.md)  
  
  
