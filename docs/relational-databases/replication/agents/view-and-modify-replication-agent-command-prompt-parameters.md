---
title: 檢視並修改複寫代理程式命令提示字元參數 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce887109d154f2d0940507d06950bf918ff2ab4b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters"></a>檢視並修改複寫代理程式命令提示字元參數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  複寫代理程式為可接受命令行參數的可執行檔。 根據預設，代理程式會在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理程式作業步驟下執行，因此這些參數便可透過 [作業屬性 - \<作業>] 對話方塊進行檢視並修改。 **的** [作業] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 資料夾及複寫監視器的 **[代理程式]** 索引標籤會提供此對話方塊。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
> [!NOTE]  
>  代理程式參數變更會在代理程式下次啟動時生效。 如果代理程式連續執行，則必須停止代理程式，然後重新啟動它。  
  
 雖然可以直接修改參數，但是在更多的情形下透過代理程式設定檔來對其進行修改。 如需相關資訊，請參閱 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 如果您從 **[作業]** 資料夾存取代理程式作業，則使用下表來決定可用於各代理程式的代理程式作業名稱與參數。  
  
|Agent|作業名稱|如需參數表，請參閱...|  
|-----------|--------------|------------------------------------|  
|快照集代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<整數>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|合併式發行集分割區的快照集代理程式|**Dyn_\<發行者>-\<發行集資料庫>-\<發行集>-\<GUID>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|記錄讀取器代理程式|**\<發行者>-\<發行集資料庫>-\<整數>**|[複寫記錄讀取器代理程式](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|提取訂閱的合併代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<訂閱資料庫>-\<整數>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|發送訂閱的合併代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|發送訂閱的散發代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>***|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|提取訂閱的散發代理程式|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>***\*|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|發送訂閱至非 SQL Server 訂閱者的散發代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|佇列讀取器代理程式|**[\<散發者>].\<整數>**|[複寫佇列讀取器代理程式](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*如果是 Oracle 發行集的發送訂閱，其作業名稱會是 **\<發行者>-\<發行者**>，而不是 **\<發行者>-\<發行集資料庫>**  
  
 \*\*如果是 Oracle 發行集的提取訂閱，其作業名稱會是 **\<發行者>-\<散發資料庫**>，而不是 **\<發行者>-\<發行集資料庫>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>若要從 Management Studio 檢視並修改複寫代理程式命令列參數  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中適當的電腦，然後展開伺服器節點：  
  
    -   對於提取訂閱的「散發代理程式」與「合併代理程式」，則連接到「訂閱者」。  
  
    -   對於所有其他代理程式，則連接到「散發者」。  
  
2.  展開 **[SQL Server Agent]** 資料夾，然後展開 **[作業]** 資料夾。  
  
3.  以滑鼠右鍵按一下作業，然後按一下 **[屬性]**。  
  
4.  在 [作業屬性 - \<作業>] 對話方塊的 [步驟] 頁面上，選取步驟 [執行代理程式]，然後按一下 [編輯]。  
  
5.  在 **[作業步驟屬性 - 執行代理程式]** 對話方塊中，編輯 **[命令]** 欄位。  
  
6.  同時在兩個對話方塊中按一下 **[確定]** 。  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>若要從複寫監視器檢視並修改散發代理程式與合併代理程式命令列參數  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]**。  
  
4.  在 [訂閱 <訂閱名稱>] 視窗中，按一下 [動作]，然後按一下 [\<代理程式名稱> 作業屬性]。  
  
5.  在 [作業屬性 - \<作業>] 對話方塊的 [步驟] 頁面上，選取步驟 [執行代理程式]，然後按一下 [編輯]。  
  
6.  在 **[作業步驟屬性 - 執行代理程式]** 對話方塊中，編輯 **[命令]** 欄位。  
  
7.  同時在兩個對話方塊中按一下 **[確定]** 。  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>若要從複寫監視器檢視並修改快照集代理程式、記錄讀取器代理程式與佇列讀取器代理程式命令列參數  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[代理程式]** 索引標籤。  
  
3.  以滑鼠右鍵按一下方格內的代理程式，然後按一下 **[屬性]**。  
  
4.  在 [作業屬性 - \<作業>] 對話方塊的 [步驟] 頁面上，選取步驟 [執行代理程式]，然後按一下 [編輯]。  
  
5.  在 **[作業步驟屬性 - 執行代理程式]** 對話方塊中，編輯 **[命令]** 欄位。  
  
6.  同時在兩個對話方塊中按一下 **[確定]** 。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Replication Agents Overview](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
