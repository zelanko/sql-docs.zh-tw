---
title: 監視 (複寫) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
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
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: b35b7ecc21497e7b8c458b6d0e46c410f96d5d21
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68767132"
---
# <a name="monitoring-replication"></a>監視 (複寫)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  監控複寫拓撲是部署複寫時很重要的層面。 由於已散發複寫活動，因此必須跨越所有複寫相關的電腦，追蹤活動和狀態 藉由使用各種監視工具，您將可回答諸如以下的常見問題： 

-   我的複寫系統狀況是否良好？
-   哪些訂閱的速度慢？
-   我的交易式訂閱落後多少？
-   目前一個認可的交易要到達異動複寫中的訂閱者需花多久的時間？
-   為何我的合併訂閱速度很慢？
-   代理程式為何沒有執行？  
  

下列工具可用來監視複寫：  
  
-   **SQL Server 複寫監視器** - 最重要的複寫監視工具，能夠呈現以「發行者」為焦點的所有複寫活動檢視。 如需詳細資訊，請參閱 [Monitoring Replication](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。 
-   **SQL Server Management Studio** - 可讓您存取「複寫監視器」。 它也可讓您檢視下列代理程式所記錄的目前狀態和最後訊息，並可讓您啟動和停止每個代理程式：記錄讀取器代理程式、快照集代理程式、合併代理程式，以及散發代理程式。 如需相關資訊，請參閱 [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md)。  
  
-   **Transact-SQL (T-SQL) 和 Replication Management Objects (RMO)** - 兩個介面都可讓您監視來自「散發者」之所有類型的複寫。 合併式複寫還提供了監視「訂閱者」端複寫的能力。  
  
-   **複寫代理程式事件的警示** -「複寫」針對複寫代理程式事件提供了一些預先定義的警示，如有必要，您還可以建立額外的警示。 警示可用於觸發對事件的自動回應及 (或) 通知管理員。 如需詳細資訊，請參閱[使用複寫代理程式事件的警示](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)。  
  
-   **系統監視器** - 針對複寫提供了一些計數器，有助於監視效能。 如需相關資訊，請參閱 [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md)。  
  

## <a name="see-also"></a>另請參閱  
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   

  
  
