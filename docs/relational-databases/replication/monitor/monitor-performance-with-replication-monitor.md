---
title: "使用複寫監視器監視效能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "監視效能 [SQL Server 複寫], 複寫監視器"
  - "記錄讀取器代理程式, 監視"
  - "複寫監視器, 效能"
  - "合併代理程式, 監視"
  - "佇列讀取器代理程式, 監視"
  - "快照集代理程式, 監視"
  - "散發代理程式, 監視"
  - "監視效能 [SQL Server 複寫]"
ms.assetid: f212397d-1bfd-496b-a246-668952891d09
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 使用複寫監視器監視效能
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 「複寫監視器」可讓您使用下列方法來監視異動複寫與合併式複寫的效能：  
  
-   設定警告和臨界值  
  
-   檢視效能度量  
  
-   以追蹤 Token 決定延遲 (異動複寫)  
  
-   檢視詳細的同步處理統計資料 (合併式複寫)  
  
-   檢視交易和傳遞時間 (異動複寫)  
  
## 設定警告和臨界值  
 「複寫監視器」允許您啟用一些效能條件的警告。 在您啟用警告時，必須指定臨界值。 當達到或超過該臨界值時，會顯示警告 **狀態** 訂用帳戶和與之同步 （除非需要顯示優先順序較高的問題） 的發行集的資料行。 除了在複寫監視器顯示警告外，達到臨界值也會觸發警示。 您可以啟用下列效能條件的警告：  
  
-   超過指定的延遲 (交易受發行者認可與對應交易受訂閱者認可之間所經過的時間)。  
  
     這可以套用於異動複寫。 若已達到或超過指定臨界值，狀態顯示為 **[效能嚴重不足]**。  
  
-   超過指定的同步處理時間。  
  
     這可以套用於合併式複寫。 如果達到或超過指定的閾值，狀態會顯示為 **長時間執行的合併**。 您可以為撥號連接和區域網路 (LAN) 連接指定不同的臨界值。  
  
-   在給定時間內處理的資料列數達不到指定數目。  
  
     這可以套用於合併式複寫。 若已達到或超過指定臨界值，狀態顯示為 **[效能嚴重不足]**。 您可以為撥號連接和 LAN 連接指定不同的臨界值。  
  
 如需詳細資訊，請參閱 [設定臨界值和複寫監視器 」 中的警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
## 檢視效能度量  
 複寫監視器 」 會顯示在交易式複寫和合併式複寫的效能品質值 **目前的平均效能** 和 **目前最差效能** 的發行集的資料行和 **效能** 訂閱的資料行。 這些值為：  
  
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
  
-   合併式複寫，效能品質無關的臨界值 (若其值為資料列處理臨界值將不作判斷 **效能嚴重不足** 會顯示在 **狀態** 資料行)。 透過將個別訂閱效能與具有相同連接類型 (撥號或 LAN) 之發行集訂閱的平均記錄效能進行比較，對效能品質進行判斷。 在相同連接類型上發生過五次同步處理，且每次同步處理都具有 50 或更多個變更之後，複寫監視器才會顯示值。 如果發生 50 個 (含) 以上變更的同步處理不及五個，或者最近一次同步處理少於 50 個變更，則「複寫監視器」不會顯示值。  
  
     下表顯示了平均效能和效能品質值之間的交互關聯。 例如，如果十個「訂閱者」透過 LAN 連接以每秒平均 100 個資料列的速率進行同步處理，而其中一個訂閱則是以每秒 125 個資料列的速率進行同步處理，這個「訂閱者」的同步處理效能平均為 125%，結果值為「好」。  
  
    |非常好|好|普通|差|  
    |---------------|----------|----------|----------|  
    |151+%|76 – 150%|26 – 75%|0 – 25%|  
  
 如需檢視訂閱資訊的詳細資訊，請參閱 [檢視資訊並執行工作訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)。  
  
## 使用追蹤 Token 判斷延遲  
 異動複寫可允許您藉由在發行集資料庫的交易記錄中插入 Token (少量資料)，並記錄到達散發者和訂閱者所需花費的時間，以測量系統中的延遲。 Token 亦可讓您識別資料是否未到達散發者或訂閱者。 如需詳細資訊，請參閱 [測量延遲及驗證連線的交易式複寫](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
## 檢視合併式複寫的詳細同步處理效能  
 針對合併式複寫，複寫監視器於同步處理時顯示每個已處理發行項的詳細資訊，包括每個處理階段花費的時間 (上傳變更、下載變更等等)。 這樣有助於找出導致過慢的特定資料表，同時也是解決合併訂閱效能問題的最佳地點。 如需檢視詳細統計資料的詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
## 檢視異動複寫的交易和傳遞時間  
 對於異動複寫，「複寫監視器」會顯示有關下列內容的資訊：尚未散發到「訂閱者」之散發資料庫中的交易數，以及散發這些交易的預估時間。 如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
## 另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [在複寫監視器中設定臨界值和警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  