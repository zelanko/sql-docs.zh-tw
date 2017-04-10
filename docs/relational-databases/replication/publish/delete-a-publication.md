---
title: "刪除發行集 | Microsoft Docs"
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
  - "移除發行集"
  - "發行集 [SQL Server 複寫], 刪除"
  - "發行項 [SQL Server 複寫], 刪除"
  - "刪除發行集"
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 刪除發行集
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO) 來刪除 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中的發行集。  
  
 **本主題內容**  
  
-   **若要刪除發行集，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 從 **的** [本機發行集] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]資料夾中刪除發行集。  
  
#### 若要刪除出版品  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要刪除，然後按一下 [發行的集 **刪除**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式刪除發行集。 使用哪些預存程序取決於所要刪除的發行集類型而定。  
  
> [!NOTE]  
>  刪除發行集不會從發行集資料庫中移除發行的物件，或是從訂閱資料庫中移除對應物件。 必要的話，請使用 `DROP <object>` 命令來手動移除這些物件。  
  
#### 刪除快照式或交易式發行集  
  
1.  執行下列其中之一：  
  
    -   若要刪除單一發行集，請執行 [sp_droppublication](../../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md) 於發行集資料庫的發行者端。  
  
    -   若要刪除的所有發行集，並移除所有複寫物件從已發行的資料庫，執行 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 在 「 發行者 」。 針對 **@type** 指定 **tran**的值。 （選擇性）如果無法存取散發者或資料庫的狀態有疑問或離線，指定值為 **1** 的 **@force**。 （選擇性）指定的資料庫名稱 **@dbname** 如果 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 不會在發行集資料庫上執行。  
  
        > [!NOTE]  
        >  指定的值為 **1** 的 **@force** 可能會留在資料庫的複寫相關發行的物件。  
  
2.  （選擇性）如果此資料庫其他發行集，請執行 [sp_replicationdboption & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 若要停用目前的資料庫使用快照式或交易式複寫的發行集。  
  
3.  （選擇性）在訂閱資料庫上的 「 訂閱者 」 執行 [sp_subscription_cleanup](../../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) 訂閱資料庫中移除任何剩餘的複寫中繼資料。  
  
#### 刪除合併式發行集  
  
1.  執行下列其中之一：  
  
    -   若要刪除單一發行集，請執行 [sp_dropmergepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md) 在發行集資料庫上的 「 發行者 」。  
  
    -   若要刪除的所有發行集，並移除所有複寫物件從已發行的資料庫，執行 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 在 「 發行者 」。 針對 **@type** 指定 **merge**的值。 （選擇性）如果無法存取散發者或資料庫的狀態有疑問或離線，指定值為 **1** 的 **@force**。 （選擇性）指定的資料庫名稱 **@dbname** 如果 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 不會在發行集資料庫上執行。  
  
        > [!NOTE]  
        >  指定的值為 **1** 的 **@force** 可能會留在資料庫的複寫相關發行的物件。  
  
2.  （選擇性）如果此資料庫其他發行集，請執行 [sp_replicationdboption & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 若要停用目前的資料庫使用合併式複寫的發行集。  
  
3.  （選擇性）在訂閱資料庫上的 「 訂閱者 」 執行 [sp_mergesubscription_cleanup & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md) 若要移除訂閱資料庫中的任何剩餘的複寫中繼資料。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會示範如何移除交易式發行集，並針對資料庫停用交易式發行。 這個範例假設之前已移除所有的訂閱。 如需相關資訊，請參閱 [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) 或 [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md)。  
  
 [!code-sql[HowTo#sp_droppublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_1.sql)]  
  
 此範例會示範如何移除合併式發行集，並針對資料庫停用合併式發行。 這個範例假設之前已移除所有的訂閱。 如需相關資訊，請參閱 [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) 或 [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md)。  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式刪除發行集。 用來移除發行集的 RMO 類別，將取決於所移除的發行集類型而定。  
  
#### 移除快照式或交易式發行集  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 發行集，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 在步驟 1 中建立的連接屬性。  
  
4.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認發行集存在。 如果這個屬性的值為 **false**，則表示步驟 3 中的發行集屬性定義錯誤或是此發行集不存在。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 方法。  
  
6.  (選擇性) 如果此資料庫沒有任何其他的交易式發行集存在，則可以針對交易式發行停用此資料庫，如下所示：  
  
    1.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別。 設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 的執行個體的內容 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中。  
  
    2.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 **false**，請確認此資料庫存在。  
  
    3.  設定 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 屬性 **false**。  
  
    4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  關閉連接。  
  
#### 移除合併式發行集  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 發行集，並設定屬性 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 在步驟 1 中建立的連接屬性。  
  
4.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認發行集存在。 如果這個屬性的值為 **false**，則表示步驟 3 中的發行集屬性定義錯誤或是此發行集不存在。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 方法。  
  
6.  (選擇性) 如果此資料庫沒有任何其他的合併式發行集存在，則可以針對合併式發行停用此資料庫，如下所示：  
  
    1.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別。 設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 的執行個體的內容 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 從步驟 1。  
  
    2.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 **false**，請確認此資料庫存在。  
  
    3.  設定 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 屬性 **false**。  
  
    4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  關閉連接。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 下列範例會刪除交易式發行集。 如果此資料庫沒有任何其他的交易式發行集存在，則也會停用交易式發行。  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 下列範例會刪除合併式發行集。 如果此資料庫沒有任何其他的合併式發行集存在，則也會停用合併式發行。  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## 另請參閱  
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  