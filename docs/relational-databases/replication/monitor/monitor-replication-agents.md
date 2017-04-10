---
title: "監視複寫代理程式 | Microsoft Docs"
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
  - "監視效能 [SQL Server 複寫], 代理程式"
  - "記錄讀取器代理程式, 監視"
  - "複寫監視器, 代理程式"
  - "合併代理程式, 監視"
  - "佇列讀取器代理程式, 監視"
  - "快照集代理程式, 監視"
  - "代理程式 [SQL Server 複寫], 監視"
  - "散發代理程式, 監視"
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# 監視複寫代理程式
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫監視器 」 可全面檢視複寫活動，但也可以直接尋找特定代理程式的資訊。 下列清單包含每個代理程式、可以在複寫監視器上找到的索引標籤，以及到說明如何存取這些索引標籤之主題的連結：  
  
-   下列代理程式與複寫監視器中的發行集相關聯：  
  
    -   快照集代理程式  
  
    -   記錄讀取器代理程式  
  
    -   佇列讀取器代理程式  
  
     存取資訊和透過下列索引標籤的這些代理程式相關聯的工作︰ **代理程式** （適用於每個發行者和發行集） 和 **警告** （適用於每個發行集）。 如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的發行集與 #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
-   下列代理程式與複寫監視器中的訂閱相關聯：  
  
    -   散發代理程式  
  
    -   [合併代理程式]  
  
     存取資訊和透過下列索引標籤的這些代理程式相關聯的工作︰ **訂閱監看清單** （適用於每個發行者） 或 **所有訂閱** （適用於每個發行集）] 索引標籤。 如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
## 使用 SQL Server Management Studio 監視複寫代理程式  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 監視複寫代理程式提供下列對話方塊︰  
  
-   **檢視快照集代理程式狀態** （適用於所有發行集）  
  
-   **檢視記錄讀取器代理程式狀態** （適用於所有的交易式發行集）  
  
-   **檢視同步處理狀態** （針對所有訂閱; 此對話方塊可讓散發代理程式 」 和 「 合併代理程式存取權）  
  
 「複寫監視器」提供每個代理程式的其他資訊，並提供對「佇列讀取器代理程式」的監視(如果使用的話)。 如需詳細資訊，請參閱 [檢視資訊並執行工作的代理程式相關聯的發行集與 #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), ，[檢視資訊並執行工作與發行集和 #40; 相關聯的代理程式複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md), ，和 [檢視資訊並執行訂閱 & #40; 相關聯的代理程式工作複寫監視器 & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)。  
  
#### 若要監視快照集代理程式和記錄讀取器代理程式  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  發行集，以滑鼠右鍵按一下，然後按一下 [ **檢視記錄讀取器代理程式狀態** 或 **檢視快照集代理程式狀態**。  
  
4.  在 **檢視記錄讀取器代理程式狀態** 或 **檢視快照集代理程式狀態** ] 對話方塊中︰  
  
    -   檢視代理程式狀態。  
  
    -   如有必要，啟動或停止代理程式。  
  
    -   按一下 [ **監視** 啟動 **複寫監視器**。  
  
5.  按一下 [ **關閉**]。  
  
#### 若要監視散發代理程式與合併代理程式 (從發行者)  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開要監視之訂閱的發行集。  
  
4.  在訂閱中，以滑鼠右鍵按一下，然後按一下 **檢視同步處理狀態**。  
  
5.  在 **檢視同步處理狀態** ] 對話方塊中︰  
  
    -   檢視代理程式狀態。  
  
    -   如有必要，啟動或停止代理程式。  
  
    -   對於發送訂閱，按一下 [ **監視** 啟動 **複寫監視器**。  
  
    -   對於提取訂閱，按一下 **檢視作業歷程記錄** 啟動 **記錄檔檢視器**, ，以顯示從代理程式記錄檔的輸出。  
  
6.  按一下 [ **關閉**]。  
  
#### 若要監視散發代理程式與合併代理程式 (從訂閱者)  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要監視，然後按一下 [的訂閱 **檢視同步處理狀態**。  
  
4.  在 **檢視同步處理狀態** ] 對話方塊中︰  
  
    -   檢視代理程式狀態。  
  
    -   如有必要，啟動或停止代理程式。  
  
    -   按一下 [ **檢視作業歷程記錄** 啟動 **記錄檔檢視器**, ，以顯示從代理程式記錄檔的輸出。  
  
5.  按一下 [ **關閉**]。  
  
## 另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [複寫代理程式概觀](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  