---
title: 快取、重新整理和複寫監視器效能 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- cache [SQL Server], replication
- Replication Monitor, caching
- refreshing data
- Replication Monitor, refreshing
ms.assetid: a2d8b666-ed41-4f86-b2b8-c8e118416ab7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: afa70f42c2ea5602bf549a4d5596bff2c8bbff66
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54123878"
---
# <a name="caching-refresh-and-replication-monitor-performance"></a>快取、重新整理和複寫監視器效能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  「[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫監視器」設計成能有效地監視發行集系統中的大量電腦。 會定期快取和重新整理「複寫監視器」用作執行計算和收集資料的查詢。 快取可減少您在「複寫監視器」中檢視不同頁面時的查詢和計算次數，並可使監視範圍擴大到多個使用者。  
  
 快取重新整理由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業 (即 **散發的複寫監視重新整理器**) 處理。 此作業連續執行，但快取重新整理排程需要在上一次重新整理後等候一段時間：  
  
-   如果自上次建立快取之後有發生代理程式記錄變更，則最短的等候時間是：4 秒；或建立先前快取所花費的時間。  
  
-   如果自上次建立快取之後沒有發生任何代理程式記錄變更 (可能有發生其他變更)，則最長的等候時間是：30 秒；或建立先前快取所花費的時間。  
  
## <a name="refreshing-the-replication-monitor-user-interface"></a>重新整理複寫監視器使用者介面  
 「複寫監視器」使用者介面可以按下列方式重新整理：  
  
-   依預設，「複寫監視器」主視窗 (包括所有索引標籤) 將每隔五秒鐘自動進行重新整理。 自動重新整理不會強制重新整理快取；使用者介面將顯示快取最新版本的資料。 您可以透過編輯「發行者」設定來自訂用於所有「發行者」相關視窗的重新整理速率。 您還可以停用「發行者」的自動重新整理。  
  
-   依預設，透過「複寫監視器」啟動的詳細資料視窗不會自動重新整理，正在同步處理的合併訂閱的相關視窗除外。 如果您將詳細資料視窗指定為應自動重新整理，則它們將按照與「複寫監視器」主視窗相同的排程重新整理。  
  
-   可以透過按 F5 或以滑鼠右鍵按一下「複寫監視器」樹狀目錄中的節點，再按一下 **[重新整理]**，手動重新整理所有視窗。 手動重新整理會強制重新整理快取。  
  
 如需詳細資訊，請參閱[在複寫監視器中重新整理資料](../../../relational-databases/replication/monitor/refresh-data-in-replication-monitor.md)。  
  
## <a name="performance-considerations"></a>效能考量  
 雖然「複寫監視器」設計成可高效地執行，但仍應注意下列問題：  
  
-   如果您有大量的發行集或訂閱，請考慮為使用者介面設定頻率較低的自動重新整理排程。  
  
-   避免同時執行多個「複寫監視器」執行個體。  
  
-   避免註冊大量的「散發者」，同時避免將「複寫監視器」設定為自動連接到所有「散發者」。  
  
## <a name="see-also"></a>另請參閱  
 [執行複寫維護作業 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
