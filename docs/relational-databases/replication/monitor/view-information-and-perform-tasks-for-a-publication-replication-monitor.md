---
title: "檢視發行集的資訊並執行工作 (複寫監視器) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "檢視發行集資訊"
  - "發行集 [SQL Server 複寫], 檢視資訊"
  - "發行集 [SQL Server 複寫], 複寫監視器工作"
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 檢視發行集的資訊並執行工作 (複寫監視器)
  「複寫監視器」提供下列包含所選取發行集之資訊的索引標籤：  
  
-   **所有訂閱**  
  
     這個索引標籤會顯示有關選取之發行集的所有訂閱資訊。  
  
-   **代理程式**  
  
     此索引標籤會顯示複寫所使用之所有代理程式的相關資訊：  
  
    -   所有發行集所使用的快照集代理程式。  
  
    -   所有交易式發行集所使用的記錄讀取器代理程式。  
  
    -   「佇列讀取器代理程式」，由已佇列更新訂閱的交易式發行集使用。  
  
-   **警告** (散發者執行的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本)  
  
    -   這個索引標籤可用來為代理程式指定警告和警示。  
  
-   **追蹤 Token** (交易式複寫，散發者執行的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本)  
  
     這個索引標籤能讓您測量延遲，在發行者端所認可之交易與在訂閱者端所認可之對應交易之間經過的時間。  
  
 如需有關每個索引標籤上的選項的詳細資訊，請按一下右窗格中的索引標籤，然後按一下 [ **幫助** 在功能表列上。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 若要檢視發行集的資訊並執行工作  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  若要檢視和修改發行集屬性，以滑鼠右鍵按一下發行集，以及 [ **屬性**。  
  
3.  若要檢視訂閱的相關資訊，請按一下 [ **所有訂閱** ] 索引標籤。  
  
     若要檢視及修改訂閱屬性，以滑鼠右鍵按一下訂閱，以及 [ **屬性**。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。 如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
4.  若要檢視有關代理程式的詳細資訊，請按一下 **[代理程式]** 索引標籤。 您也可以透過這個索引標籤存取更多詳細資訊並可執行工作。 如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的發行集與 #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
5.  若要檢視代理程式警告與臨界值的相關資訊，請按一下 [ **警告** ] 索引標籤。 如需詳細資訊，請參閱 [設定臨界值和複寫監視器 」 中的警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
6.  若要檢視追蹤 token 的相關資訊，請按一下 [ **追蹤 Token** ] 索引標籤。 如需如何使用追蹤 token 的詳細資訊，請參閱 [測量延遲及驗證連線的交易式複寫](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
## 另請參閱  
 [檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  