---
title: 刪除提取訂閱 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- deleting subscriptions
- pull subscriptions [SQL Server replication], deleting
- subscriptions [SQL Server replication], pull
ms.assetid: 997c0b8e-d8d9-4eed-85b1-6baa1f8594ce
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac5d4f7d199e3ee3de6ffb43e2c43e232681b0d3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721465"
---
# <a name="delete-a-pull-subscription"></a>刪除提取訂閱
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO) 來刪除 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的提取訂閱。  
  
 **本主題內容**  
  
-   **若要刪除提取訂閱，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在發行者端 (從 **的** [本機發行集] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料夾) 或訂閱者端 (從 **[本機訂閱]** 資料夾) 刪除提取訂閱。 刪除訂閱並無法從訂閱中移除物件或資料，這些必須手動移除。  
  
#### <a name="to-delete-a-pull-subscription-at-the-publisher"></a>若要在發行者端刪除提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開與您要刪除的訂閱相關聯的發行集。  
  
4.  以滑鼠右鍵按一下訂閱，然後按一下 **[刪除]**。  
  
5.  在確認對話方塊中，選取是否要連接訂閱者以刪除訂閱資訊。 如果清除 **[連接到訂閱者]** 核取方塊，則應在稍後連接到「訂閱者」以刪除資訊。  
  
#### <a name="to-delete-a-pull-subscription-at-the-subscriber"></a>若要在訂閱者端刪除提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要刪除的訂閱，然後按一下 **[刪除]**。  
  
4.  在確認對話方塊中，選取是否要連接發行者以刪除訂閱資訊。 若您清除 **[連接到發行者]** 核取方塊，應於稍後連接到發行者以便刪除資訊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式刪除提取訂閱。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### <a name="to-delete-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>刪除快照式或交易式發行集的提取訂閱  
  
1.  在訂閱資料庫的訂閱者端，執行 [sp_droppullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql)。 指定 **@publication**或 Replication Management Objects (RMO) 來重新初始化 **@publisher**和 **@publisher_db**資料夾中可用。  
  
2.  在發行集資料庫的發行者端，執行 [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql)。 指定 **@publication** 和 **@subscriber**。 為 **@article** 指定 **@article**。 (選擇性) 如果無法存取散發者，請為 **@ignore_distributor** 指定 **@ignore_distributor** 的值來刪除此訂閱，而不需要移除散發者端上的相關物件。  
  
#### <a name="to-delete-a-pull-subscription-to-a-merge-publication"></a>刪除合併式發行集的提取訂閱  
  
1.  在訂閱資料庫的訂閱者端，執行 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql)。 指定 **@publication**或 Replication Management Objects (RMO) 來刪除 **@publisher**和 **@publisher_db**。  
  
2.  在發行集資料庫的發行者端，執行 [sp_dropmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql)。 指定 **@publication**或 Replication Management Objects (RMO) 來重新初始化 **@subscriber**和 **@subscriber_db**資料夾中可用。 為 **@subscription_type** 指定 **@subscription_type**。 (選擇性) 如果無法存取散發者，請為 **@ignore_distributor** 指定 **@ignore_distributor** 的值來刪除此訂閱，而不需要移除散發者端上的相關物件。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會刪除交易式發行集的提取訂閱。 第一批次是在「訂閱者」上執行，而第二批次是在「發行者」上執行。  
  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/droptranpullsub.sql#sp_droptranpullsubscription)]  
  
 [!code-sql[HowTo#sp_droptransubscription](../../snippets/tsql/SQL15/replication/howto/tsql/droptranpullsub.sql#sp_droptransubscription)]  
  
 下列範例會刪除合併式發行集的提取訂閱。 第一批次是在「訂閱者」上執行，而第二批次是在「發行者」上執行。  
  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepullsub.sql#sp_dropmergepullsubscription)]  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepullsub.sql#sp_dropmergesubscription)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式刪除提取訂閱。 用於刪除提取訂閱的 RMO 類別依該提取訂閱所屬的發行集類型而定。  
  
#### <a name="to-delete-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>刪除快照式或交易式發行集的提取訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與訂閱者和發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別的執行個體，並設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性。 使用步驟 1 中的訂閱者連接，以設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
3.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該訂閱存在。 如果這個屬性的值為 `false`，則表示步驟 2 中的訂閱屬性定義錯誤或是此訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> 方法。  
  
5.  使用步驟 1 中的發行者連接建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 `false`，則表示步驟 5 中指定的屬性不正確，或伺服器上沒有該發行集存在。  
  
7.  呼叫 <xref:Microsoft.SqlServer.Replication.TransPublication.RemovePullSubscription%2A> 方法。 為 *subscriber* 和 *subscriberDB* 參數指定訂閱者和訂閱資料庫的名稱。  
  
#### <a name="to-delete-a-pull-subscription-to-a-merge-publication"></a>刪除合併式發行集的提取訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與訂閱者和發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別的執行個體，並設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性。 使用步驟 1 中的連接，以設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
3.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該訂閱存在。 如果這個屬性的值為 `false`，則表示步驟 2 中的訂閱屬性定義錯誤或是此訂閱不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> 方法。  
  
5.  使用步驟 1 中的發行者連接建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 `false`，則表示步驟 5 中指定的屬性不正確，或伺服器上沒有該發行集存在。  
  
7.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.RemovePullSubscription%2A> 方法。 為 *subscriber* 和 *subscriberDB* 參數指定訂閱者和訂閱資料庫的名稱。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會刪除交易式發行集的提取訂閱，並在發行者上移除訂閱註冊。  
  
 [!code-csharp[HowTo#rmo_DropTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpullsub)]  
  
 此範例會刪除合併式發行集的提取訂閱，並在發行者上移除訂閱註冊。  
  
 [!code-csharp[HowTo#rmo_DropMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropmergepullsub)]  
  
## <a name="see-also"></a>另請參閱  
 [訂閱發行集](subscribe-to-publications.md)   
 [複寫安全性最佳作法](security/replication-security-best-practices.md)  
  
  
