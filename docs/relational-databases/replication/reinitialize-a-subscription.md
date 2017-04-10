---
title: "重新初始化訂閱 | Microsoft Docs"
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
  - "初始化訂閱 [SQL Server 複寫], 重新初始化"
  - "訂閱 [SQL Server 複寫], 重新初始化"
  - "重新初始化訂閱"
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 重新初始化訂閱
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO) 來重新初始化 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的訂閱。 個別訂閱可標示為要重新初始化，好讓下一次同步處理期間會套用新的快照集。  
  
 **本主題內容**  
  
-   **若要重新初始化訂閱，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 重新初始化訂閱處理分為兩部份：  
  
1.  *「標示」* 要重新初始化之發行集的單個或所有訂閱。 將訂閱標示為重新初始化在 **重新初始化訂閱** 對話方塊中，可從 **本機發行集** 資料夾和 **本機訂閱** 資料夾中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您也可以從「複寫監視器」中的 **[所有訂閱]** 索引標籤和發行集節點中標示訂閱。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。 當您要標示訂閱進行重新初始化時，可用的選項如下：  
  
     **使用目前的快照集**  
     選取即可將目前的快照集套用至散發代理程式或合併代理程式下一次將執行的訂閱者。 如果沒有任何有效的快照集可以使用，則不可以選取此選項。  
  
     **使用新的快照集**  
     選取即可使用新的快照集重新初始化訂閱。 唯有在快照集代理程式產生快照集之後，該快照集才能套用至訂閱者。 如果設定「快照集代理程式」根據排程執行，則只有在下一個排程的「快照集代理程式」執行後，訂閱才會重新初始化。 選取 **[立即產生新的快照集]** ，即可立即啟動快照集代理程式。  
  
     **重新初始化之前，先上傳尚未同步處理的變更**  
     僅限合併式複寫。 選取即可在使用快照集覆寫訂閱者端的資料之前，從訂閱資料庫上傳任何暫止變更。  
  
     如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
2.  訂閱會在下一次同步處理時重新初始化：(異動複寫的)「散發代理程式」或 (合併式複寫的)「合併代理程式」，為含有標示要重新初始化訂閱的每個「訂閱者」套用最新的快照集。 如需同步處理訂閱的詳細資訊，請參閱 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 和 [同步處理提取訂閱](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 若要在 Management Studio (在發行者端) 中標示要重新初始化的單一發送訂閱或提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開含有您要重新初始化之訂閱的發行集。  
  
4.  在訂閱中，以滑鼠右鍵按一下，然後按一下 **重新初始化**。  
  
5.  在 **重新初始化訂閱** 對話方塊中，選取 [選項]，然後按一下 **標示為重新初始化**。  
  
#### 若要在 Management Studio (在訂閱者端) 中標示要重新初始化的單一提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  在訂閱中，以滑鼠右鍵按一下，然後按一下 **重新初始化**。  
  
4.  在顯示的確認對話方塊中，按一下 **[是]**。  
  
#### 若要在 Management Studio 中標示要重新初始化的所有訂閱  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要重新初始化，然後按一下 [的訂閱發行集中 **重新初始化所有訂閱**。  
  
4.  在 **重新初始化訂閱** 對話方塊中，選取 [選項]，然後按一下 **標示為重新初始化**。  
  
#### 若要在複寫監視器中標示要重新初始化的單一發送或提取訂閱  
  
1.  在複寫監視器中，展開左窗格裡的發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  以滑鼠右鍵按一下您想要重新初始化，然後按一下 [的訂閱 **重新初始化訂閱**。  
  
4.  在 **重新初始化訂閱** 對話方塊中，選取 [選項]，然後按一下 **標示為重新初始化**。  
  
#### 若要在複寫監視器中標示要重新初始化的所有訂閱  
  
1.  在複寫監視器的左窗格中展開發行者群組，然後展開發行者。  
  
2.  以滑鼠右鍵按一下您想要重新初始化，然後按一下 [的訂閱發行集中 **重新初始化所有訂閱**。  
  
3.  在 **重新初始化訂閱** 對話方塊中，選取 [選項]，然後按一下 **標示為重新初始化**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用複寫預存程序來以程式設計的方式重新初始化訂閱。 使用的預存程序取決於訂閱的類型 (發送訂閱或提取訂閱) 以及訂閱所屬的發行集類型而定。  
  
#### 重新初始化交易式發行集的提取訂閱  
  
1.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_reinitpullsubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。 這樣會標示此訂閱，在下次執行散發代理程式時重新初始化。  
  
2.  (選擇性) 在訂閱者上啟動散發代理程式，以同步處理此訂閱。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 重新初始化交易式發行集的發送訂閱  
  
1.  在 「 發行者 」 執行 [sp_reinitsubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，和 **@destination_db**。 這樣會標示此訂閱，在下次執行散發代理程式時重新初始化。  
  
2.  (選擇性) 在散發者上啟動散發代理程式，以同步處理此訂閱。 如需詳細資訊，請參閱 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
#### 重新初始化合併式發行集的提取訂閱  
  
1.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_reinitmergepullsubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。 若要將變更從 「 訂閱者 」 上傳重新初始化之前，指定其值為 **true** 的 **@upload_first**。 這樣會標示此訂閱，在下次執行合併代理程式時重新初始化。  
  
    > [!IMPORTANT]  
    >  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
2.  (選擇性) 在訂閱者上啟動合併代理程式，以同步處理此訂閱。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 重新初始化合併式發行集的發送訂閱  
  
1.  在 「 發行者 」 執行 [sp_reinitmergesubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，和 **@subscriber_db**。 若要將變更從 「 訂閱者 」 上傳重新初始化之前，指定其值為 **true** 的 **@upload_first**。 這樣會標示此訂閱，在下次執行散發代理程式時重新初始化。  
  
    > [!IMPORTANT]  
    >  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
2.  (選擇性) 在散發者上啟動合併代理程式，以同步處理此訂閱。 如需詳細資訊，請參閱 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
#### 在建立新的合併式發行集時，設定重新初始化原則  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), ，指定下列其中一個值 **@automatic_reinitialization_policy**:  
  
    -   **1** -上傳變更從 「 訂閱者 」 會自動重新初始化訂閱之前視需要發行集的變更。  
  
    -   **0** -訂閱者端的變更都會被捨棄，自動重新初始化訂閱時視需要發行集的變更。  
  
    > [!IMPORTANT]  
    >  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
     如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 針對現有的合併式發行集變更重新初始化原則  
  
1.  在發行集資料庫的發行者，執行 [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，並指定 **automatic_reinitialization_policy** 的 **@property** 和下列其中一個值 **@value**:  
  
    -   **1** -上傳變更從 「 訂閱者 」 會自動重新初始化訂閱之前視需要發行集的變更。  
  
    -   **0** -訂閱者端的變更都會被捨棄，自動重新初始化訂閱時視需要發行集的變更。  
  
    > [!IMPORTANT]  
    >  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
     如需詳細資訊，請參閱 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 個別訂閱可標示為要重新初始化，好讓下一次同步處理期間會套用新的快照集。 您可以使用 Replication Management Objects (RMO) 以程式設計的方式重新初始化訂閱。 使用的類別取決於訂閱所屬的發行集類型及訂閱的類型 (發送訂閱或提取訂閱) 而定。  
  
#### 重新初始化交易式發行集的提取訂閱  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別，並設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>, ，以及步驟 1 的連線 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。  
  
    > [!NOTE]  
    >  如果這個方法會傳回 **false**, ，步驟 2 中的訂閱屬性定義不正確或提取訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> 方法。 此方法會標示要重新初始化的訂閱。  
  
5.  同步處理提取訂閱。 如需詳細資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 重新初始化交易式發行集的發送訂閱  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別，並設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, ，以及步驟 1 的連線 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。  
  
    > [!NOTE]  
    >  如果這個方法會傳回 **false**, ，步驟 2 中的訂閱屬性定義不正確或發送訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> 方法。 此方法會標示要重新初始化的訂閱。  
  
5.  同步處理發送訂閱。 如需詳細資訊，請參閱 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
#### 重新初始化合併式發行集的提取訂閱  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別，並設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>, ，以及步驟 1 的連線 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。  
  
    > [!NOTE]  
    >  如果這個方法會傳回 **false**, ，步驟 2 中的訂閱屬性定義不正確或提取訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> 方法。 傳遞 **true** 的值可在重新初始化之前上傳訂閱者上的變更，或者傳遞 **false** 的值可重新初始化及遺失訂閱者上的任何暫止變更。 此方法會標示要重新初始化的訂閱。  
  
    > [!NOTE]  
    >  如果此訂閱已過期，將無法上傳變更。 如需詳細資訊，請參閱 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)。  
  
5.  同步處理提取訂閱。 如需詳細資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 重新初始化合併式發行集的發送訂閱  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別，並設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, ，以及步驟 1 的連線 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。  
  
    > [!NOTE]  
    >  如果這個方法會傳回 **false**, ，步驟 2 中的訂閱屬性定義不正確或發送訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> 方法。 傳遞 **true** 的值可在重新初始化之前上傳訂閱者上的變更，或者傳遞 **false** 的值可重新初始化及遺失訂閱者上的任何暫止變更。 此方法會標示要重新初始化的訂閱。  
  
    > [!NOTE]  
    >  如果此訂閱已過期，將無法上傳變更。 如需詳細資訊，請參閱 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)。  
  
5.  同步處理發送訂閱。 如需詳細資訊，請參閱 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會重新初始化交易式發行集的提取訂閱。  
  
 [!code-csharp[HowTo#rmo_ReinitTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 此範例會在初次上傳訂閱者上的暫止變更之後，重新初始化合併式發行集的提取訂閱。  
  
 [!code-csharp[HowTo#rmo_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## 另請參閱  
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Replication Management Objects 概念。](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  