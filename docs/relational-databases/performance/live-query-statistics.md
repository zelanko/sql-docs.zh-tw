---
title: "即時查詢統計資料 | Microsoft Docs"
ms.custom: 
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bff144ba100fe72dcc036299138e656362977b96
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="live-query-statistics"></a>即時查詢統計資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可供檢視作用中查詢的即時執行計畫。 這個即時查詢計畫會隨著控制項在查詢計畫運算子之間流動，提供查詢執行程序的即時深入資訊。 即時查詢計畫會顯示整體的查詢進度，以及運算子層級的執行階段執行統計資料，如產生的資料列數目、耗用時間、運算子進度等等。因為這份資料是即時提供，不需要等待查詢完成，所以這些執行統計資料在偵錯查詢效能問題方面非常有用。 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 開始即提供這項功能，但它也可以搭配 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 使用。  
  
**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
> [!WARNING]  
>  這項功能主要用在疑難排解。 使用這項功能不會過度降低整體查詢效能。 這項功能可以搭配 [TRANSACT-SQL 偵錯工具](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)使用。  
  
#### <a name="to-view-live-query-statistics"></a>檢視即時查詢統計資料  
  
1.  若要檢視即時查詢執行計畫，請在 [工具] 功能表上按一下 **即時查詢統計資料** 圖示。  
  
     ![在工具列上的 [即時查詢統計資料] 按鈕](../../relational-databases/performance/media/livequerystatstoolbar.png "在工具列上的 [即時查詢統計資料] 按鈕")  
  
     您也可以用滑鼠右鍵按一下 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中選取的查詢，檢視存取即時查詢執行計畫，然後按一下 [包含即時查詢統計資料] 。  
  
     ![在快顯功能表上的 [即時查詢統計資料] 按鈕](../../relational-databases/performance/media/livequerystatsmenu.png "在快顯功能表上的 [即時查詢統計資料] 按鈕")  
  
2.  現在執行查詢。 即時查詢計劃會顯示查詢計劃運算子的整體查詢進度，以及執行階段的執行統計資料 (例如已耗用時間、進度等)。 在進行查詢執行時，會定期更新查詢進度資訊和執行統計資料。 使用這項資訊來了解整體的查詢執行處理程序，以及偵錯長時間執行的查詢、無限期執行的查詢、會造成 tempdb 溢位的查詢和逾時問題。  
  
     ![執行程序表中的 [即時查詢統計資料] 按鈕](../../relational-databases/performance/media/livequerystatsplan.png "執行程序表中的 [即時查詢統計資料] 按鈕")  
  
 以滑鼠右鍵按一下 [使用中的高成本查詢]  資料表中的查詢，也可以從 [活動監視器]  存取即時執行計畫。  
  
 ![在 [活動監視器] 的 [即時查詢統計資料] 按鈕](../../relational-databases/performance/media/livequerystatsactmon.png "在 [活動監視器] 的 [即時查詢統計資料] 按鈕")  
  
## <a name="remarks"></a>Remarks  
 必須先啟用統計資料設定檔基礎結構，即時查詢統計資料才可以擷取查詢進度資訊。 指定 **中的 [Include Live Query Statistics (包括即時查詢統計資料)]**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ，可啟用目前查詢工作階段的統計資料基礎結構。 
 
在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]之前，還有兩種其他方式可啟用統計資料基礎結構，用以檢視其他工作階段 (如活動監視器) 的即時查詢統計資料：  
  
-   在目標工作階段中執行 `SET STATISTICS XML ON;` 或 `SET STATISTICS PROFILE ON;` 。  
  
 中的多個  
  
-   啟用 **query_post_execution_showplan** 擴充事件。 這是在所有工作階段啟用即時查詢統計資料的全伺服器設定。 若要啟用擴充事件，請參閱 [使用擴充事件監視系統活動](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。  

從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 開始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含輕量型版本的統計資料設定檔基礎結構。 還有兩種方式可啟用輕量型統計資料基礎結構，用以檢視其他工作階段 (如活動監視器) 的即時查詢統計資料：

-   使用全域追蹤旗標 7412。  
  
 中的多個  
  
-   啟用 **query_thread_profile** 擴充事件。 這是在所有工作階段啟用即時查詢統計資料的全伺服器設定。 若要啟用擴充事件，請參閱 [使用擴充事件監視系統活動](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。
  
 > [!NOTE]
 > 不支援原生編譯的預存程序。  
  
## <a name="permissions"></a>Permissions  
 填入 [即時查詢統計資料]  結果頁面需要資料庫層級的 **SHOWPLAN** 權限，查看即時統計資料需要伺服器層級的 **VIEW SERVER STATE** 權限，而執行查詢則需要任何必要權限。  
  
## <a name="see-also"></a>另請參閱  
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [效能監視及微調工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [開啟活動監視器 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)   
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)   
 [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
