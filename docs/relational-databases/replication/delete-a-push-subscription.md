---
title: "刪除發送訂閱 | Microsoft Docs"
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
  - "移除訂閱"
  - "發送訂閱 [SQL Server 複寫], 刪除"
  - "刪除訂閱"
  - "訂閱 [SQL Server 複寫], 發送"
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 刪除發送訂閱
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO) 來刪除 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的發送訂閱。  
  
 **本主題內容**  
  
-   **若要刪除發送訂閱，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 刪除發送訂閱在發行者端 (從 **本機發行集** 資料夾中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 或 「 訂閱者 」 (從 **本機訂閱** 資料夾)。 刪除訂閱並無法從訂閱中移除物件或資料，這些必須手動移除。  
  
#### 若要在發行者端刪除發送訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開與您要刪除的訂閱相關聯的發行集。  
  
4.  在訂閱中，以滑鼠右鍵按一下，然後按一下 **刪除**。  
  
5.  在確認對話方塊中，選取是否要連接訂閱者以刪除訂閱資訊。 如果您清除 **[連接到訂閱者]** 核取方塊，則稍後應連接到「訂閱者」以刪除資訊。  
  
#### 若要在訂閱者端刪除發送訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要刪除，然後按一下 [的訂閱 **刪除**。  
  
4.  在確認對話方塊中，選取是否要連接發行者以刪除訂閱資訊。 若您清除 **[連接到發行者]** 核取方塊，應於稍後連接到發行者以便刪除資訊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式刪除發送訂閱。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### 刪除快照式或交易式發行集的發送訂閱  
  
1.  在發行集資料庫的發行者，執行 [sp_dropsubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)。 指定 **@publication** 和 **@subscriber**。 為 **@article** 指定 **all**的值。 （選擇性）如果無法存取散發者，指定其值為 **1** 的 **@ignore_distributor** 而不移除相關的物件，在散發者端刪除訂閱。  
  
2.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_subscription_cleanup & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) 若要移除訂閱資料庫中的複寫中繼資料。  
  
#### 刪除合併式發行集的發送訂閱  
  
1.  在 「 發行者 」 執行 [sp_dropmergesubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md), ，並指定 **@publication**, ，**@subscriber** 和 **@subscriber_db**。 （選擇性）如果無法存取散發者，指定其值為 **1** 的 **@ignore_distributor** 而不移除相關的物件，在散發者端刪除訂閱。  
  
2.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_mergesubscription_cleanup & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。 這樣會移除訂閱資料庫中的合併中繼資料。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會刪除交易式發行集的發送訂閱。  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 此範例會刪除合併式發行集的發送訂閱。  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 用於刪除發送訂閱的 RMO 類別取決於該發送訂閱所屬的發行集類型而定。  
  
#### 刪除快照式或交易式發行集的發送訂閱  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 屬性。  
  
4.  設定 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
5.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該訂閱存在。 如果這個屬性的值為 **false**，則表示步驟 2 中的訂閱屬性定義錯誤或是此訂閱不存在。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 方法。  
  
#### 刪除合併式發行集的發送訂閱  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 屬性。  
  
4.  設定 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
5.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該訂閱存在。 如果這個屬性的值為 **false**，則表示步驟 2 中的訂閱屬性定義錯誤或是此訂閱不存在。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 方法。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式刪除發送訂閱。  
  
 [!code-csharp[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## 另請參閱  
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  