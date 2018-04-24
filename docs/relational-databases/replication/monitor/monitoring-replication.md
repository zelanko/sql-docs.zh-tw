---
title: 監視 (複寫) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2de987fc0dd3a0a06039cb74b4bb1814a4345868
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="monitoring-replication"></a>監視 (複寫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  監控複寫拓撲是部署複寫時很重要的層面。 由於已散發複寫活動，因此必須跨越所有複寫相關的電腦，追蹤活動和狀態 下列工具可用來監視複寫：  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫監視器  
  
     「複寫監視器」是最重要的複寫監視工具，可呈現所有複寫活動以發行者為焦點的檢視。 如需詳細資訊，請參閱 [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)。  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 提供「複寫監視器」的存取權。 還允許您檢視下列代理程式記錄的目前狀態和上一條訊息，並允許您啟動及停止每一個代理程式：「記錄讀取器代理程式」、「快照代理程式」、「合併代理程式」及「散發代理程式」。 如需相關資訊，請參閱 [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md)。  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] 和 Replication Management Objects (RMO)  
  
     兩個介面均可讓您監視「散發者」端所有類型的複寫。 合併式複寫還提供了監視「訂閱者」端複寫的能力。  
  
-   複寫代理程式事件的警示  
  
     複寫提供了一些複寫代理程式事件的預先定義警示，必要時您還可以建立其他警示。 警示可用於觸發對事件的自動回應及 (或) 通知管理員。 如需詳細資訊，請參閱[使用複寫代理程式事件的警示](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)。  
  
-   系統監視器  
  
     「系統監視器」提供了許多複寫計數器，有助於監視效能。 如需相關資訊，請參閱 [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理 &#40;複寫&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
