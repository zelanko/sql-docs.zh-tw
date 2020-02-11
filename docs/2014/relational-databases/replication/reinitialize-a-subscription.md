---
title: 重新初始化訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3f148cc75ba7ae1987d0114186b76273f35e8d03
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68199223"
---
# <a name="reinitialize-a-subscription"></a>重新初始化訂閱
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO) 來重新初始化 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的訂閱。 個別訂閱可標示為要重新初始化，好讓下一次同步處理期間會套用新的快照集。  
  
 **本主題內容**  
  
-   **若要重新初始化訂閱，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 重新初始化訂閱處理分為兩部份：  
  
1.  
  *「標示」* 要重新初始化之發行集的單個或所有訂閱。 在 **[重新初始化訂閱]** 對話方塊中標示要進行重新初始化處理的訂閱，此對話方塊在 **** 中的 **[本機發行集]** 資料夾和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 您也可以從「複寫監視器」中的 **[所有訂閱]** 索引標籤和發行集節點中標示訂閱。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](monitor/start-the-replication-monitor.md)。 當您要標示訂閱進行重新初始化時，可用的選項如下：  
  
     **使用目前的快照集**  
     選取即可將目前的快照集套用至散發代理程式或合併代理程式下一次將執行的訂閱者。 如果沒有任何有效的快照集可以使用，則不可以選取此選項。  
  
     **使用新的快照集**  
     選取即可使用新的快照集重新初始化訂閱。 唯有在快照集代理程式產生快照集之後，該快照集才能套用至訂閱者。 如果設定「快照集代理程式」根據排程執行，則只有在下一個排程的「快照集代理程式」執行後，訂閱才會重新初始化。 選取 **[立即產生新的快照集]** ，即可立即啟動快照集代理程式。  
  
     **重新初始化之前，先上傳尚未同步處理的變更**  
     僅限合併式複寫。 選取即可在使用快照集覆寫訂閱者端的資料之前，從訂閱資料庫上傳任何暫止變更。  
  
     如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
2.  訂閱會在下一次同步處理時重新初始化：(異動複寫的)「散發代理程式」或 (合併式複寫的)「合併代理程式」，為含有標示要重新初始化訂閱的每個「訂閱者」套用最新的快照集。 如需有關同步處理訂閱的資訊，請參閱＜ [Synchronize a Push Subscription](synchronize-a-push-subscription.md) ＞和＜ [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)資料夾中可用。  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-management-studio-at-the-publisher"></a>若要在 Management Studio (在發行者端) 中標示要重新初始化的單一發送訂閱或提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開含有您要重新初始化之訂閱的發行集。  
  
4.  以滑鼠右鍵按一下訂閱，然後按一下 **[重新初始化]**。  
  
5.  在 **[重新初始化訂閱]** 對話方塊中選取選項，然後按一下 **[標示為重新初始化]**。  
  
#### <a name="to-mark-a-single-pull-subscription-for-reinitialization-in-management-studio-at-the-subscriber"></a>若要在 Management Studio (在訂閱者端) 中標示要重新初始化的單一提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下訂閱，然後按一下 **[重新初始化]**。  
  
4.  在顯示的確認對話方塊中，按一下 **[是]**。  
  
#### <a name="to-mark-all-subscriptions-for-reinitialization-in-management-studio"></a>若要在 Management Studio 中標示要重新初始化的所有訂閱  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下包含您要重新初始化之訂閱的發行集，然後按一下 **[重新初始化所有訂閱]**。  
  
4.  在 **[重新初始化訂閱]** 對話方塊中選取選項，然後按一下 **[標示為重新初始化]**。  
  
#### <a name="to-mark-a-single-push-or-pull-subscription-for-reinitialization-in-replication-monitor"></a>若要在複寫監視器中標示要重新初始化的單一發送或提取訂閱  
  
1.  在複寫監視器中，展開左窗格裡的發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  在您要重新初始化的訂閱上按一下滑鼠右鍵，再按一下 **[重新初始化訂閱]**。  
  
4.  在 **[重新初始化訂閱]** 對話方塊中選取選項，然後按一下 **[標示為重新初始化]**。  
  
#### <a name="to-mark-all-subscriptions-for-reinitialization-in-replication-monitor"></a>若要在複寫監視器中標示要重新初始化的所有訂閱  
  
1.  在複寫監視器的左窗格中展開發行者群組，然後展開發行者。  
  
2.  以滑鼠右鍵按一下包含您要重新初始化之訂閱的發行集，然後按一下 **[重新初始化所有訂閱]**。  
  
3.  在 **[重新初始化訂閱]** 對話方塊中選取選項，然後按一下 **[標示為重新初始化]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用複寫預存程序來以程式設計的方式重新初始化訂閱。 使用的預存程序取決於訂閱的類型 (發送訂閱或提取訂閱) 以及訂閱所屬的發行集類型而定。  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>重新初始化交易式發行集的提取訂閱  
  
1.  在訂閱資料庫的訂閱者端，執行 [sp_reinitpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql)。 指定**@publisher**、 **@publisher_db**和**@publication**。 這樣會標示此訂閱，在下次執行散發代理程式時重新初始化。  
  
2.  (選擇性) 在訂閱者上啟動散發代理程式，以同步處理此訂閱。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)。  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>重新初始化交易式發行集的發送訂閱  
  
1.  在發行者端，執行 [sp_reinitsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql)。 指定**@publication**、 **@subscriber**和**@destination_db**。 這樣會標示此訂閱，在下次執行散發代理程式時重新初始化。  
  
2.  (選擇性) 在散發者上啟動散發代理程式，以同步處理此訂閱。 如需詳細資訊，請參閱 [同步處理發送訂閱](synchronize-a-push-subscription.md)。  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>重新初始化合併式發行集的提取訂閱  
  
1.  在訂閱資料庫的訂閱者端，執行 [sp_reinitmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql)。 指定**@publisher**、 **@publisher_db**和**@publication**。 若要在重新初始化發生之前從訂閱者上傳變更， `true`請**@upload_first**為指定的值。 這樣會標示此訂閱，在下次執行合併代理程式時重新初始化。  
  
    > [!IMPORTANT]  
    >  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
2.  (選擇性) 在訂閱者上啟動合併代理程式，以同步處理此訂閱。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)。  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>重新初始化合併式發行集的發送訂閱  
  
1.  在發行者端，執行 [sp_reinitmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql)。 指定**@publication**、 **@subscriber**和**@subscriber_db**。 若要在重新初始化發生之前從訂閱者上傳變更， `true`請**@upload_first**為指定的值。 這樣會標示此訂閱，在下次執行散發代理程式時重新初始化。  
  
    > [!IMPORTANT]  
    >  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
2.  (選擇性) 在散發者上啟動合併代理程式，以同步處理此訂閱。 如需詳細資訊，請參閱 [同步處理發送訂閱](synchronize-a-push-subscription.md)。  
  
#### <a name="to-set-the-reinitialization-policy-when-creating-a-new-merge-publication"></a>在建立新的合併式發行集時，設定重新初始化原則  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)，針對 **@automatic_reinitialization_policy**指定下列其中一個值：  
  
    -   **1** -在發行集的變更需要自動重新初始化訂閱之前，從訂閱者上傳變更。  
  
    -   **0** -當發行集的變更需要自動重新初始化訂閱時，會捨棄訂閱者端的變更。  
  
    > [!IMPORTANT]  
    >  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
     如需詳細資訊，請參閱[建立發行集](publish/create-a-publication.md)。  
  
#### <a name="to-change-the-reinitialization-policy-for-an-existing-merge-publication"></a>針對現有的合併式發行集變更重新初始化原則  
  
1.  在發行集資料庫的發行者上，執行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，針對 **@property** @upload_first **@property** ，並針對 **@value**指定下列其中一個值：  
  
    -   **1** -在發行集的變更需要自動重新初始化訂閱之前，從訂閱者上傳變更。  
  
    -   **0** -當發行集的變更需要自動重新初始化訂閱時，會捨棄訂閱者端的變更。  
  
    > [!IMPORTANT]  
    >  如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
     如需詳細資訊，請參閱 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 個別訂閱可標示為要重新初始化，好讓下一次同步處理期間會套用新的快照集。 您可以使用 Replication Management Objects (RMO) 以程式設計的方式重新初始化訂閱。 使用的類別取決於訂閱所屬的發行集類型及訂閱的類型 (發送訂閱或提取訂閱) 而定。  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-transactional-publication"></a>重新初始化交易式發行集的提取訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別的執行個體，並設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>及針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>設定步驟 1 中的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。  
  
    > [!NOTE]  
    >  如果此方法傳回 `false`，則表示步驟 2 中的訂閱屬性定義不正確，或者提取訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> 方法。 此方法會標示要重新初始化的訂閱。  
  
5.  同步處理提取訂閱。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)。  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-transactional-publication"></a>重新初始化交易式發行集的發送訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別的執行個體，並設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>及針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>設定步驟 1 中的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。  
  
    > [!NOTE]  
    >  如果此方法傳回 `false`，則表示步驟 2 中的訂閱屬性定義不正確，或者發送訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> 方法。 此方法會標示要重新初始化的訂閱。  
  
5.  同步處理發送訂閱。 如需詳細資訊，請參閱 [同步處理發送訂閱](synchronize-a-push-subscription.md)。  
  
#### <a name="to-reinitialize-a-pull-subscription-to-a-merge-publication"></a>重新初始化合併式發行集的提取訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別的執行個體，並設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>及針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>設定步驟 1 中的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。  
  
    > [!NOTE]  
    >  如果此方法傳回 `false`，則表示步驟 2 中的訂閱屬性定義不正確，或者提取訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> 方法。 傳遞 `true` 的值可在重新初始化之前上傳訂閱者上的變更，或者傳遞 `false` 的值可重新初始化及遺失訂閱者上的任何暫止變更。 此方法會標示要重新初始化的訂閱。  
  
    > [!NOTE]  
    >  如果此訂閱已過期，將無法上傳變更。 如需詳細資訊，請參閱 [Set the Expiration Period for Subscriptions](publish/set-the-expiration-period-for-subscriptions.md)。  
  
5.  同步處理提取訂閱。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)。  
  
#### <a name="to-reinitialize-a-push-subscription-to-a-merge-publication"></a>重新初始化合併式發行集的發送訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別的執行個體，並設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>及針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>設定步驟 1 中的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。  
  
    > [!NOTE]  
    >  如果此方法傳回 `false`，則表示步驟 2 中的訂閱屬性定義不正確，或者發送訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> 方法。 傳遞 `true` 的值可在重新初始化之前上傳訂閱者上的變更，或者傳遞 `false` 的值可重新初始化及遺失訂閱者上的任何暫止變更。 此方法會標示要重新初始化的訂閱。  
  
    > [!NOTE]  
    >  如果此訂閱已過期，將無法上傳變更。 如需詳細資訊，請參閱 [Set the Expiration Period for Subscriptions](publish/set-the-expiration-period-for-subscriptions.md)。  
  
5.  同步處理發送訂閱。 如需詳細資訊，請參閱 [同步處理發送訂閱](synchronize-a-push-subscription.md)。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會重新初始化交易式發行集的提取訂閱。  
  
 [!code-csharp[HowTo#rmo_ReinitTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 此範例會在初次上傳訂閱者上的暫止變更之後，重新初始化合併式發行集的提取訂閱。  
  
 [!code-csharp[HowTo#rmo_ReinitMergePullSub_WithUpload](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## <a name="see-also"></a>另請參閱  
 [重新初始化訂閱](reinitialize-subscriptions.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [複寫安全性最佳作法](security/replication-security-best-practices.md)  
  
  
