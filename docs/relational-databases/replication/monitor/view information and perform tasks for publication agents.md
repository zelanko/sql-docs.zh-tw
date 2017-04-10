---
title: "檢視與發行集相關聯之代理程式的資訊並執行工作 (複寫監視器) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "代理程式 [SQL Server 複寫], 檢視資訊"
  - "檢視複寫代理程式資訊"
  - "代理程式 [SQL Server 複寫], 複寫監視器中的工作"
ms.assetid: 2a420da2-66f4-4650-9bdd-1992221ed3fd
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 檢視與發行集相關聯之代理程式的資訊並執行工作 (複寫監視器)
  複寫監視器提供 **[代理程式]** 索引標籤，其中包含與選取的發行集相關聯之代理程式的資訊。 散發代理程式 」 和 「 合併代理程式與相關聯的訂閱。如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
 這個索引標籤會顯示下列代理程式的相關資訊：  
  
-   所有發行集所使用的快照集代理程式。  
  
-   所有交易式發行集所使用的記錄讀取器代理程式。  
  
-   針對佇列更新訂閱啟用之交易式發行集所使用的佇列讀取器代理程式。  
  
 若要檢視有關這個索引標籤之選項的詳細資訊，請按一下功能表列上的 **[說明]** 。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 若要檢視與發行集相關聯之代理程式的資訊並執行工作  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  若要檢視代理程式的相關資訊，請按一下 **[代理程式]** 索引標籤。 您也可以在這個索引標籤上存取更詳細的資訊及執行工作：  
  
    -   若要檢視代理程式 （例如提示訊息及任何錯誤訊息） 的詳細的資訊，代理程式，以滑鼠右鍵按一下，然後按一下 **檢視詳細資料**。  
  
    -   若要檢視工作執行的代理程式 （例如排程、 作業步驟詳細資料，等等） 的詳細的資訊，以滑鼠右鍵按一下代理程式，以及 [ **屬性**。  
  
    -   代理程式管理設定檔，以滑鼠右鍵按一下代理程式，以及 [ **代理程式設定檔**。 如需詳細資訊，請參閱 [使用複寫代理程式設定檔](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)。  
  
    -   若要啟動的代理程式未執行，代理程式，以滑鼠右鍵按一下，然後按一下 [ **啟動代理程式**。  
  
    -   若要停止正在執行的代理程式，代理程式，以滑鼠右鍵按一下，然後按一下 [ **停止代理程式**。  
  
## 另請參閱  
 [在複寫監視器中設定臨界值和警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)   
 [檢視資訊並執行工作的發行集與 #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  