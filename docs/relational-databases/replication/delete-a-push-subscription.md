---
title: 刪除發送訂閱 | Microsoft 文件
description: 了解如何使用 SQL Server Management Studio、Transact-SQL 或 Replication Management Objects，在 SQL Server 中刪除發送訂閱。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- push subscriptions [SQL Server replication], deleting
- deleting subscriptions
- subscriptions [SQL Server replication], push
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 6dcc7801a33f05c4f874731dbe0efd4e608f9a53
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918090"
---
# <a name="delete-a-push-subscription"></a>刪除發送訂閱
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO) 來刪除 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的發送訂閱。  
  
 **本主題內容**  
  
-   **若要刪除發送訂閱，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在發行者端 (從 **中的** [本機發行集] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料夾) 或訂閱者端 (從 **[本機訂閱]** 資料夾) 刪除發送訂閱。 刪除訂閱並無法從訂閱中移除物件或資料，這些必須手動移除。  
  
#### <a name="to-delete-a-push-subscription-at-the-publisher"></a>若要在發行者端刪除發送訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開與您要刪除的訂閱相關聯的發行集。  
  
4.  以滑鼠右鍵按一下訂閱，然後按一下 **[刪除]** 。  
  
5.  在確認對話方塊中，選取是否要連接訂閱者以刪除訂閱資訊。 如果您清除 **[連接到訂閱者]** 核取方塊，則稍後應連接到「訂閱者」以刪除資訊。  

#### <a name="to-delete-a-push-subscription-at-the-subscriber"></a>若要在訂閱者端刪除發送訂閱  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要刪除的訂閱，然後按一下 **[刪除]** 。  
  
4.  在確認對話方塊中，選取是否要連接發行者以刪除訂閱資訊。 若您清除 **[連接到發行者]** 核取方塊，應於稍後連接到發行者以便刪除資訊。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式刪除發送訂閱。 使用哪些預存程序要依訂閱所屬的發行集類型而定。  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>刪除快照式或交易式發行集的發送訂閱  
  
1.  在發行集資料庫的發行者端，執行 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)。 指定 **\@publication** 和 **\@subscriber**。 為 **\@article** 指定 **all** 值。 (選擇性) 如果無法存取散發者，請為 **\@ignore_distributor** 指定 **1** 值來刪除此訂閱，而不需要移除散發者端上的相關物件。  
  
2.  (選擇性) 在訂閱資料庫的訂閱者端，執行 [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) 來移除訂閱資料庫中的複寫中繼資料。  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>刪除合併式發行集的發送訂閱  
  
1.  在發行者端，執行 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)，並指定 **\@publication**、 **\@subscriber** 和 **\@subscriber_db**。 (選擇性) 如果無法存取散發者，請為 **\@ignore_distributor** 指定 **1** 值來刪除此訂閱，而不需要移除散發者端上的相關物件。  
  
2.  在訂閱資料庫的訂閱者端，執行 [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)。 指定 **\@publisher**、 **\@publisher_db** 和 **\@publication**。 這樣會移除訂閱資料庫中的合併中繼資料。  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會刪除交易式發行集的發送訂閱。  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 此範例會刪除合併式發行集的發送訂閱。  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 用於刪除發送訂閱的 RMO 類別取決於該發送訂閱所屬的發行集類型而定。  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>刪除快照式或交易式發行集的發送訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>和 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 屬性設定步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 。  
  
5.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該訂閱存在。 如果這個屬性的值為 **false**，則表示步驟 2 中的訂閱屬性定義錯誤或是此訂閱不存在。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 方法。  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>刪除合併式發行集的發送訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別的執行個體。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>和 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 屬性。  
  
4.  針對 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 屬性設定步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 。  
  
5.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該訂閱存在。 如果這個屬性的值為 **false**，則表示步驟 2 中的訂閱屬性定義錯誤或是此訂閱不存在。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 方法。  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> 範例 (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式刪除發送訂閱。  
  
 [!code-cs[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## <a name="see-also"></a>另請參閱  
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [複寫安全性最佳作法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
