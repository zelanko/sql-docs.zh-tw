---
title: "使用複寫監視器監視效能 |Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Log Reader Agent, monitoring
- Replication Monitor, performance
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication]
ms.assetid: f212397d-1bfd-496b-a246-668952891d09
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 590c82fa430be2c34796b6ae5201a0ef7efba7c1
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="monitor-performance-with-replication-monitor"></a>使用複寫監視器監視效能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  「[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫監視器」可讓您使用下列方法來監視異動複寫與合併式複寫的效能：  
  
-   設定警告和臨界值  
  
-   檢視效能度量  
  
-   以追蹤 Token 決定延遲 (異動複寫)  
  
-   檢視詳細的同步處理統計資料 (合併式複寫)  
  
-   檢視交易和傳遞時間 (異動複寫)  
  
## <a name="set-warnings-and-thresholds"></a>設定警告和臨界值  
 「複寫監視器」允許您啟用一些效能條件的警告。 在您啟用警告時，必須指定臨界值。 當達到或超過該臨界值時，會在訂閱和與之同步的發行集之 **[狀態]** 資料行中顯示警告 (除非需要顯示優先權更高的問題)。 除了在複寫監視器顯示警告外，達到臨界值也會觸發警示。 您可以啟用下列效能條件的警告：  
  
-   超過指定的延遲 (交易受發行者認可與對應交易受訂閱者認可之間所經過的時間)。  
  
     這可以套用於異動複寫。 若已達到或超過指定臨界值，狀態顯示為 **[效能嚴重不足]**。  
  
-   超過指定的同步處理時間。  
  
     這可以套用於合併式複寫。 若已達到或超過指定臨界值，狀態顯示為 **[長期執行合併]**。 您可以為撥號連接和區域網路 (LAN) 連接指定不同的臨界值。  
  
-   在給定時間內處理的資料列數達不到指定數目。  
  
     這可以套用於合併式複寫。 若已達到或超過指定臨界值，狀態顯示為 **[效能嚴重不足]**。 您可以為撥號連接和 LAN 連接指定不同的臨界值。  
  
 如需相關資訊，請參閱 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
## <a name="view-performance-measurements"></a>檢視效能度量  
 複寫監視器在發行集的 **[目前的平均效能]** 和 **[目前最差效能]** 資料行，以及訂閱的 **[效能]** 資料行，顯示異動複寫與合併式複寫的效能品質的值。 這些值為：  
  
-   非常好  
  
-   好  
  
-   普通  
  
-   差  
  
-   嚴重不足 (僅限於異動複寫)  
  
 使用下列方法判斷這些值：  
  
-   對於異動複寫，效能品質由延遲臨界值決定。 如果不設定臨界值，則不顯示值。 下表顯示了臨界值和效能品質值之間的交互關聯。 例如，如果將臨界值設定為 60 秒，而實際延遲為 30 秒，則延遲為臨界值的 50%，結果值為「好」。  
  
    |非常好|好|普通|差|嚴重|  
    |---------------|----------|----------|----------|--------------|  
    |0 – 34%|35 – 59%|60 – 84%|85 – 99%|100% +|  
  
-   對於合併式複寫，效能品質與臨界值無關 (如果在 **[狀態]** 資料行中顯示的值為 **[效能嚴重不足]** ，則資料列處理臨界值將不作判斷)。 透過將個別訂閱效能與具有相同連接類型 (撥號或 LAN) 之發行集訂閱的平均記錄效能進行比較，對效能品質進行判斷。 在相同連接類型上發生過五次同步處理，且每次同步處理都具有 50 或更多個變更之後，複寫監視器才會顯示值。 如果發生 50 個 (含) 以上變更的同步處理不及五個，或者最近一次同步處理少於 50 個變更，則「複寫監視器」不會顯示值。  
  
     下表顯示了平均效能和效能品質值之間的交互關聯。 例如，如果十個「訂閱者」透過 LAN 連接以每秒平均 100 個資料列的速率進行同步處理，而其中一個訂閱則是以每秒 125 個資料列的速率進行同步處理，這個「訂閱者」的同步處理效能平均為 125%，結果值為「好」。  
  
    |非常好|好|普通|差|  
    |---------------|----------|----------|----------|  
    |151+%|76 – 150%|26 – 75%|0 – 25%|  
  
 如需檢視訂閱資訊的詳細資訊，請參閱[檢視訂閱的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)。  
  
## <a name="determine-latency-with-tracer-tokens"></a>使用追蹤 Token 判斷延遲  
 異動複寫可允許您藉由在發行集資料庫的交易記錄中插入 Token (少量資料)，並記錄到達散發者和訂閱者所需花費的時間，以測量系統中的延遲。 Token 亦可讓您識別資料是否未到達散發者或訂閱者。 如需相關資訊，請參閱 [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
## <a name="view-detailed-synchronization-performance-for-merge-replication"></a>檢視合併式複寫的詳細同步處理效能  
 針對合併式複寫，複寫監視器於同步處理時顯示每個已處理發行項的詳細資訊，包括每個處理階段花費的時間 (上傳變更、下載變更等等)。 這樣有助於找出導致過慢的特定資料表，同時也是解決合併訂閱效能問題的最佳地點。 如需檢視詳細統計資料的詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
## <a name="view-transactions-and-delivery-time-for-transactional-replication"></a>檢視異動複寫的交易和傳遞時間  
 對於異動複寫，「複寫監視器」會顯示有關下列內容的資訊：尚未散發到「訂閱者」之散發資料庫中的交易數，以及散發這些交易的預估時間。 如需詳細資訊，請參閱[檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
