---
title: 監視複寫 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 615582b2d961f87a2d3df151175d7bd5d06e305f
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000382"
---
# <a name="monitoring-replication"></a>監視 (複寫)
  監控複寫拓撲是部署複寫時很重要的層面。 由於已散發複寫活動，因此必須跨越所有複寫相關的電腦，追蹤活動和狀態 下列工具可用來監視複寫：  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)]複寫 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 監視器  
  
     「複寫監視器」是最重要的複寫監視工具，可呈現所有複寫活動以發行者為焦點的檢視。 如需詳細資訊，請參閱[使用複寫監視器監視效能](monitor/monitor-performance-with-replication-monitor.md)。  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssManStudioFull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 提供「複寫監視器」的存取權。 還允許您檢視下列代理程式記錄的目前狀態和上一條訊息，並允許您啟動及停止每一個代理程式：「記錄讀取器代理程式」、「快照代理程式」、「合併代理程式」及「散發代理程式」。 如需相關資訊，請參閱 [Monitor Replication Agents](monitor/monitor-replication-agents.md)。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Replication Management Objects (RMO)  
  
     兩個介面均可讓您監視「散發者」端所有類型的複寫。 合併式複寫還提供了監視「訂閱者」端複寫的能力。  
  
-   複寫代理程式事件的警示  
  
     複寫提供了一些複寫代理程式事件的預先定義警示，必要時您還可以建立其他警示。 警示可用於觸發對事件的自動回應及 (或) 通知管理員。 如需詳細資訊，請參閱[使用複寫代理程式事件的警示](agents/use-alerts-for-replication-agent-events.md)。  
  
-   系統監視器  
  
     「系統監視器」提供了許多複寫計數器，有助於監視效能。 如需相關資訊，請參閱 [Monitoring Replication with System Monitor](monitor/monitoring-replication-with-system-monitor.md)。  
  
## <a name="see-also"></a>另請參閱  
 [複寫管理常見問題集](administration/frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](administration/best-practices-for-replication-administration.md)   

  
  
