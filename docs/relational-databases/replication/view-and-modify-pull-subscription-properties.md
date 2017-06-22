---
title: "檢視及修改提取訂閱屬性 | Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying subscriptions
- viewing replication properties
- modifying replication properties, pull subscriptions
- pull subscriptions [SQL Server replication], modifying
- subscriptions [SQL Server replication], pull
- pull subscriptions [SQL Server replication], properties
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e62ba6a0d4aebf9cb6c929e5564645e8407da3ee
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="view-and-modify-pull-subscription-properties"></a>檢視及修改提取訂閱屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視及修改提取訂閱屬性。  
  
 **本主題內容**  
  
-   **若要檢視及修改提取訂閱屬性，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [訂閱屬性 - \<發行者>: \<發行集資料庫>] 對話方塊中檢視發行者或訂閱者的提取訂閱屬性，該對話方塊可從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 取得。 「訂閱者」可看見更多屬性，而屬性可於「訂閱者」端修改。 您也可以從 **[所有訂閱]** 索引標籤上的「發行者」檢視屬性，該索引標籤位於「複寫監視器」中。 如需啟動複寫監視器的資訊，請參閱[啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-management-studio"></a>從 Management Studio 中的發行者檢視提取訂閱屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開適當的發行集，以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]**。  
  
4.  檢視屬性，然後按一下 **[確定]**。  
  
#### <a name="to-view-and-modify-pull-subscription-properties-from-the-subscriber-in-management-studio"></a>從 Management Studio 中的訂閱者檢視和修改提取訂閱屬性  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]**。  
  
4.  必要時修改任何屬性，然後按一下 **[確定]**。  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-replication-monitor"></a>從複寫監視器中的發行者檢視提取訂閱屬性  
  
1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  以滑鼠右鍵按一下訂閱，然後按一下 **[屬性]**。  
  
4.  檢視屬性，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式修改提取訂閱及存取其屬性。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>檢視快照式或交易式發行集之提取訂閱的屬性  
  
1.  在訂閱者上，執行 [sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)。 指定 **@publisher**或 Replication Management Objects (RMO)，在 **@publisher_db**和 **@publication**取得。 這樣會傳回儲存於訂閱者上之系統資料表內的訂閱相關資訊。  
  
2.  在訂閱者上，執行 [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)。 指定 **@publisher**或 Replication Management Objects (RMO)，在 **@publisher_db**或 Replication Management Objects (RMO)，在 **@publication**及 **@publication_type**的下列其中一個值：  
  
    -   **0** - 訂閱屬於交易式發行集。  
  
    -   **1** - 訂閱屬於快照式發行集。  
  
3.  在發行者上，執行 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。 指定 **@publication** 和 **@subscriber**取得。  
  
4.  在發行者上，執行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)，指定 **@subscriber**取得。 這樣會顯示與訂閱者有關的資訊。  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>變更快照式或交易式發行集之提取訂閱的屬性  
  
1.  在訂閱者上，執行 [sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)，指定 **@publisher**或 Replication Management Objects (RMO)，在 **@publisher_db**或 Replication Management Objects (RMO)，在 **@publication**、 **0** 的 **1** (交易式) 或 **@publication_type**(快照式) 的值、變更為 **@property**的訂閱屬性，以及當做 **@value**取得。  
  
2.  (選擇性) 在訂閱資料庫的訂閱者上，執行 [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md)。 針對 **@jobid**指定散發代理程式作業的識別碼以及下列 Data Transformation Services (DTS) 封裝屬性：  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     這樣會變更訂閱的 DTS 封裝屬性。  
  
    > [!NOTE]  
    >  可以執行 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)來取得作業識別碼。  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>檢視合併式發行集之提取訂閱的屬性  
  
1.  在訂閱者上，執行 [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)。 指定 **@publisher**或 Replication Management Objects (RMO)，在 **@publisher_db**和 **@publication**取得。  
  
2.  在訂閱者上，執行 [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)。 指定 **@publisher**或 Replication Management Objects (RMO)，在 **@publisher_db**或 Replication Management Objects (RMO)，在 **@publication**及 **@publication_type**取得。  
  
3.  在發行者上執行 [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md) ，以顯示訂閱資訊。 若要傳回特定訂閱的相關資訊，您必須指定 **@publication**或 Replication Management Objects (RMO)，在 **@subscriber**及 **@subscription_type** 的 **@subscription_type**取得。  
  
4.  在發行者上，執行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)，指定 **@subscriber**取得。 這樣會顯示與訂閱者有關的資訊。  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>變更合併式發行集之提取訂閱的屬性  
  
1.  在訂閱者上，執行 [sp_changemergepullsubscription](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)。 指定 **@publication**或 Replication Management Objects (RMO)，在 **@publisher**或 Replication Management Objects (RMO)，在 **@publisher_db**(快照式) 的值、變更為 **@property**的訂閱屬性，以及當做 **@value**取得。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 用於檢視或修改提取訂閱屬性的 RMO 類別，將取決於該提取訂閱所訂閱的發行集類型而定。  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>檢視或修改快照式或交易式發行集之提取訂閱的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與訂閱者的連線。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A> 和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連線。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在於伺服器上。  
  
6.  (選擇性) 若要變更屬性，請為可以設定的其中一個 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 屬性設定新值，然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  (選擇性) 若要檢視新的設定，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法，重新載入發行項的屬性。  
  
8.  關閉所有連接。  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-merge-publication"></a>檢視或修改合併式發行集之提取訂閱的屬性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與訂閱者的連線。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A> 和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連線。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在於伺服器上。  
  
6.  (選擇性) 若要變更屬性，請為可以設定的其中一個 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 屬性設定新值，然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  (選擇性) 若要檢視新的設定，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法，重新載入發行項的屬性。  
  
8.  關閉所有連接。  
  
## <a name="see-also"></a>另請參閱  
 [檢視訂閱的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [訂閱發行集集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
