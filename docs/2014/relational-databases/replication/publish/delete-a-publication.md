---
title: 刪除發行集 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing publications
- publications [SQL Server replication], deleting
- articles [SQL Server replication], deleting
- deleting publications
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa08a7f84cd413f1212cc73d4242b5da70fd33eb
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882283"
---
# <a name="delete-a-publication"></a>Delete a Publication
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO) 來刪除 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中的發行集。  
  
 **本主題內容**  
  
-   **若要刪除發行集，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 從 **的** [本機發行集] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]資料夾中刪除發行集。  
  
#### <a name="to-delete-a-publication"></a>若要刪除出版品  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想刪除的發行集，然後按一下 **[刪除]** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序以程式設計的方式刪除發行集。 使用哪些預存程序取決於所要刪除的發行集類型而定。  
  
> [!NOTE]  
>  刪除發行集不會從發行集資料庫中移除發行的物件，或是從訂閱資料庫中移除對應物件。 必要的話，請使用 `DROP <object>` 命令來手動移除這些物件。  
  
#### <a name="to-delete-a-snapshot-or-transactional-publication"></a>刪除快照式或交易式發行集  
  
1.  執行下列其中之一：  
  
    -   若要刪除單一發行集，請在發行集資料庫的發行者上執行 [sp_droppublication](/sql/relational-databases/system-stored-procedures/sp-droppublication-transact-sql) 。  
  
    -   若要從發行的資料庫中刪除所有發行集及移除所有複寫物件，請在發行者上執行 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 。 為 **\@類型**指定 `tran` 的值。 (選擇性) 如果無法存取散發者，或是資料庫的狀態為可疑或離線，請為force **指定 \@1** 值。 (選擇性) 如果未在發行集資料庫上執行 **sp_removedbreplication\@，請為** [dbname](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 指定資料庫的名稱。  
  
        > [!NOTE]  
        >  為force **指定 \@1** 值時，可能會將與複寫有關的發行物件留在資料庫中。  
  
2.  (選擇性) 如果此資料庫沒有任何其他發行集，請執行 [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)，以便使用快照式或異動複寫來停用目前資料庫的發行集。  
  
3.  (選擇性) 在訂閱資料庫的訂閱者上，執行 [sp_subscription_cleanup](/sql/relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql) 來移除訂閱資料庫中任何剩餘的複寫中繼資料。  
  
#### <a name="to-delete-a-merge-publication"></a>刪除合併式發行集  
  
1.  執行下列其中之一：  
  
    -   若要刪除單一發行集，請在發行集資料庫的發行者端執行 [sp_dropmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql)。  
  
    -   若要從發行的資料庫中刪除所有發行集及移除所有複寫物件，請在發行者上執行 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 。 為 **\@類型**指定 `merge` 的值。 (選擇性) 如果無法存取散發者，或是資料庫的狀態為可疑或離線，請為force **指定 \@1** 值。 (選擇性) 如果未在發行集資料庫上執行 **sp_removedbreplication\@，請為** [dbname](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 指定資料庫的名稱。  
  
        > [!NOTE]  
        >  為force **指定 \@1** 值時，可能會將與複寫有關的發行物件留在資料庫中。  
  
2.  (選擇性) 如果此資料庫沒有任何其他發行集，請執行 [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)，以便使用合併式複寫來停用目前資料庫的發行集。  
  
3.  (選擇性) 在訂閱資料庫的訂閱者端，執行 [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql) 來移除訂閱資料庫中任何剩餘的複寫中繼資料。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會示範如何移除交易式發行集，並針對資料庫停用交易式發行。 這個範例假設之前已移除所有的訂閱。 如需相關資訊，請參閱 [Delete a Pull Subscription](../delete-a-pull-subscription.md) 或 [Delete a Push Subscription](../delete-a-push-subscription.md)。  
  
 [!code-sql[HowTo#sp_droppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/droptranpub.sql#sp_droppublication)]  
  
 此範例會示範如何移除合併式發行集，並針對資料庫停用合併式發行。 這個範例假設之前已移除所有的訂閱。 如需相關資訊，請參閱 [Delete a Pull Subscription](../delete-a-pull-subscription.md) 或 [Delete a Push Subscription](../delete-a-push-subscription.md)。  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepub.sql#sp_dropmergepublication)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式刪除發行集。 用來移除發行集的 RMO 類別，將取決於所移除的發行集類型而定。  
  
#### <a name="to-remove-a-snapshot-or-transactional-publication"></a>移除快照式或交易式發行集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體。  
  
3.  設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
4.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該發行集存在。 如果這個屬性的值為 `false`，則表示步驟 3 中的發行集屬性定義錯誤或是此發行集不存在。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 方法。  
  
6.  (選擇性) 如果此資料庫沒有任何其他的交易式發行集存在，則可以針對交易式發行停用此資料庫，如下所示：  
  
    1.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別的執行個體。 將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為步驟 1 中 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 的執行個體。  
  
    2.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 `false`，請確認此資料庫存在。  
  
    3.  將 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 屬性設為 `false`。  
  
    4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  關閉連接。  
  
#### <a name="to-remove-a-merge-publication"></a>移除合併式發行集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。  
  
3.  設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
4.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認該發行集存在。 如果這個屬性的值為 `false`，則表示步驟 3 中的發行集屬性定義錯誤或是此發行集不存在。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 方法。  
  
6.  (選擇性) 如果此資料庫沒有任何其他的合併式發行集存在，則可以針對合併式發行停用此資料庫，如下所示：  
  
    1.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別的執行個體。 將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為步驟 1 中 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 的執行個體。  
  
    2.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 `false`，請確認此資料庫存在。  
  
    3.  將 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 屬性設為 `false`。  
  
    4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  關閉連接。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 下列範例會刪除交易式發行集。 如果此資料庫沒有任何其他的交易式發行集存在，則也會停用交易式發行。  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 下列範例會刪除合併式發行集。 如果此資料庫沒有任何其他的合併式發行集存在，則也會停用合併式發行。  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## <a name="see-also"></a>另請參閱  
 [複寫系統預存程序概念](../concepts/replication-system-stored-procedures-concepts.md)   
 [發行資料和資料庫物件](publish-data-and-database-objects.md)  
  
  
