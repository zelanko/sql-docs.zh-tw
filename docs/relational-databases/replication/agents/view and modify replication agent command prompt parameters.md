---
title: "檢視並修改複寫代理程式命令提示字元參數 (SQL Server Management Studio) | Microsoft Docs"
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
  - "代理程式 [SQL Server 複寫], 命令提示字元參數"
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 檢視並修改複寫代理程式命令提示字元參數 (SQL Server Management Studio)
  複寫代理程式為可接受命令行參數的可執行檔。 根據預設，代理程式執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理程式作業步驟，因此這些參數，您可以檢視並修改使用 **作業屬性-\< 工作>** 對話方塊。 **的** [作業] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 資料夾及複寫監視器的 **[代理程式]** 索引標籤會提供此對話方塊。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
> [!NOTE]  
>  代理程式參數變更會在代理程式下次啟動時生效。 如果代理程式連續執行，則必須停止代理程式，然後重新啟動它。  
  
 雖然可以直接修改參數，但是在更多的情形下透過代理程式設定檔來對其進行修改。 如需詳細資訊，請參閱 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 如果您從 **[作業]** 資料夾存取代理程式作業，則使用下表來決定可用於各代理程式的代理程式作業名稱與參數。  
  
|代理程式|作業名稱|如需參數表，請參閱...|  
|-----------|--------------|------------------------------------|  
|快照集代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 整數>**|[複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|合併式發行集分割區的快照集代理程式|**Dyn_ \< 發行者>-\< u>-\< 發行集>-\< GUID>**|[複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|記錄讀取器代理程式|**\< 發行者>-\< u>-\< 整數>**|[複寫記錄讀取器代理程式](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|提取訂閱的合併代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< u>-\< 整數>**|[複寫合併代理程式](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|發送訂閱的合併代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< 整數>**|[複寫合併代理程式](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|發送訂閱的散發代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< 整數>***|[複寫散發代理程式](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|提取訂閱的散發代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< u>-\< GUID>***\*|[複寫散發代理程式](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|發送訂閱至非 SQL Server 訂閱者的散發代理程式|**\< 發行者>-\< u>-\< 發行集>-\< 訂閱者>-\< 整數>**|[複寫散發代理程式](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|佇列讀取器代理程式|**[\< 散發者>]。\< 整數>**|[複寫佇列讀取器代理程式](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*對於 Oracle 發行集的發送訂閱，它是 **\< 發行者>-\< 發行者**> 而 **\< 發行者>-\< u>**  
  
 \*\*對於 Oracle 發行集的提取訂閱，它是 **\< 發行者>-\< DistributionDatabase**> 而 **\< 發行者>-\< u>**  
  
### 若要從 Management Studio 檢視並修改複寫代理程式命令列參數  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中適當的電腦，然後展開伺服器節點：  
  
    -   對於提取訂閱的「散發代理程式」與「合併代理程式」，則連接到「訂閱者」。  
  
    -   對於所有其他代理程式，則連接到「散發者」。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下作業，然後按一下 **屬性**。  
  
4.  在 **步驟** 頁面 **作業屬性-\< 工作>** 對話方塊方塊中，選取步驟 **執行代理程式**, ，然後按一下 [ **編輯**。  
  
5.  在 **作業步驟屬性-執行代理程式** 對話方塊中，編輯 **命令** 欄位。  
  
6.  同時在兩個對話方塊中按一下 **[確定]** 。  
  
### 若要從複寫監視器檢視並修改散發代理程式與合併代理程式命令列參數  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  訂閱中，按一下滑鼠右鍵，然後按一下 **檢視詳細資料**。  
  
4.  在 **訂閱 \< SubscriptionName >** ] 視窗中，按一下 [ **動作**, ，然後按一下 [ **\< AgentName> 作業屬性**。  
  
5.  在 **步驟** 頁面 **作業屬性-\< 工作>** 對話方塊方塊中，選取步驟 **執行代理程式**, ，然後按一下 [ **編輯**。  
  
6.  在 **作業步驟屬性-執行代理程式** 對話方塊中，編輯 **命令** 欄位。  
  
7.  同時在兩個對話方塊中按一下 **[確定]** 。  
  
### 若要從複寫監視器檢視並修改快照集代理程式、記錄讀取器代理程式與佇列讀取器代理程式命令列參數  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[代理程式]** 索引標籤。  
  
3.  在方格中，代理程式上按一下滑鼠右鍵，然後按一下 **屬性**。  
  
4.  在 **步驟** 頁面 **作業屬性-\< 工作>** 對話方塊方塊中，選取步驟 **執行代理程式**, ，然後按一下 [ **編輯**。  
  
5.  在 **作業步驟屬性-執行代理程式** 對話方塊中，編輯 **命令** 欄位。  
  
6.  同時在兩個對話方塊中按一下 **[確定]** 。  
  
## 另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [複寫代理程式概觀](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  