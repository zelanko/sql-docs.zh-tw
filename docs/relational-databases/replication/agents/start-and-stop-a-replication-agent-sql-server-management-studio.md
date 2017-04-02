---
title: "啟動及停止複寫代理程式 (SQL Server Management Studio) | Microsoft Docs"
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
  - "代理程式 [SQL Server 複寫], 停止"
  - "代理程式 [SQL Server 複寫], 啟動"
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 啟動及停止複寫代理程式 (SQL Server Management Studio)
  啟動和停止代理程式從 **工作** 資料夾和 **複寫** 資料夾中的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 以及從 「 複寫監視器。 啟動和停止下列代理程式和作業：  
  
-   所有發行集所使用的快照集代理程式。  
  
-   所有交易式發行集所使用的記錄讀取器代理程式。  
  
-   針對佇列更新訂閱啟用之交易式發行集所使用的佇列讀取器代理程式。  
  
-   散發代理程式，同步處理交易式和快照式發行集的訂閱。  
  
-   合併代理程式，同步處理合併式發行集的訂閱。  
  
-   複寫維護作業。  
  
 如需啟動 「 合併代理程式 」 和 「 散發代理程式的詳細資訊，請參閱 [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md) 和 [同步處理提取訂閱](../../../relational-databases/replication/synchronize-a-pull-subscription.md)。 如需維護工作的詳細資訊，請參閱 [執行複寫維護作業 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)。  
  
 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
### 若要從 Management Studio 啟動和停止快照集代理程式或記錄讀取器代理程式  
  
1.  連接到 「 發行者 」 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], ，然後展開伺服器節點和 **複寫** 資料夾。  
  
2.  展開 **本機發行集** 資料夾，然後再以滑鼠右鍵按一下發行集。  
  
3.  按一下 [ **檢視快照集代理程式狀態** 或 **檢視記錄讀取器代理程式狀態**。  
  
4.  按一下 [ **啟動** 或 **停止**。  
  
### 若要從 Management Studio 啟動和停止「佇列讀取器代理程式」  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的散發者，然後展開伺服器節點。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下代理程式的工作，然後按一下 **啟動作業** 或 **停止工作**。 佇列讀取器代理程式的作業名稱是在表單中 **[\< 散發者>]。 \< 整數>**。  
  
### 若要從「複寫監視器」啟動和停止「快照集代理程式」、「記錄讀取器代理程式」或「佇列讀取器代理程式」  
  
1.  在左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[代理程式]** 索引標籤。  
  
3.  代理程式上按一下滑鼠右鍵，然後按一下 **啟動代理程式** 或 **停止代理程式**。  
  
## 另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [複寫代理程式概觀](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  