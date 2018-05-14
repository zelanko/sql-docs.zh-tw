---
title: 停用發行和散發 | Microsoft Docs
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
- disabling publishing
- publishing [SQL Server replication], disabling
- distribution disabling [SQL Server replication]
- removing replication
- replication [SQL Server], removing
- disabling replication
- disabling distribution
ms.assetid: 6d4a1474-4d13-4826-8be2-80050fafa8a5
caps.latest.revision: 41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1ba752dbcf4131864b3ce8e3891723bc1ac6096f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="disable-publishing-and-distribution"></a>停用發行和散發
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中停用發行和散發。  
  
 您可以執行下列工作：  
  
-   刪除「散發者」上的散發資料庫。  
  
-   停用所有使用「散發者」的「發行者」，以及刪除這些「發行者」上的所有發行集。  
  
-   刪除所有的發行集訂閱。 發行集和訂閱資料庫中的資料不會刪除，不過它會遺失與任何發行資料庫的同步處理關聯性。 若要刪除「訂閱者」中的資料，您必須手動刪除。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
-   **若要停用發行和散發，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   若要停用發行和散發，所有散發和發行集資料庫都必須在線上。 如果存在散發或發行集資料庫的任何 *「資料庫快照集」* ，則必須先卸除這些快照集，然後才能停用發行和散發。 資料庫快照集是資料庫的唯讀離線副本，與複寫快照集無關聯。 如需詳細資訊，請參閱[資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「停用發行與散發精靈」停用發行和散發。  
  
#### <a name="to-disable-publishing-and-distribution"></a>停用發行和散發  
  
1.  連接到您要在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中停用的「發行者」或「散發者」，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **[複寫]** 資料夾，然後按一下 **[停用發行與散發]**。  
  
3.  完成「停用散發暨發行精靈」中的步驟。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式停用發行和散發。  
  
#### <a name="to-disable-publishing-and-distribution"></a>停用發行和散發  
  
1.  停止所有複寫相關的作業。 如需作業名稱清單，請參閱＜ [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)＞一節中的「SQL Server Agent 下的代理程式安全性」。  
  
2.  在訂閱資料庫的每一個訂閱者上，執行 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 從資料庫中移除複寫物件。 這個預存程序將不會移除散發者上的複寫作業。  
  
3.  在發行集資料庫的發行者上，執行 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 從資料庫中移除複寫物件。  
  
4.  如果發行者使用遠端散發者，請執行 [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)。  
  
5.  在散發者上執行 [sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)。 應該針對散發者上註冊的每一個發行者執行此預存程序一次。  
  
6.  在散發者上，執行 [sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md) 來刪除散發資料庫。 應該針對散發者上的每一個散發資料庫執行此預存程序一次。 這樣也會移除與散發資料庫有關的任何佇列讀取器代理程式作業。  
  
7.  在散發者上，執行 [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) 從伺服器移除散發者的指定。  
  
    > [!NOTE]  
    >  如果在您執行 [sp_dropdistpublisher](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md) 和 [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)之前，尚未卸除所有複寫發行和散發物件，這些程序將會傳回錯誤。 若要在卸除了發行者或散發者時，一併卸除所有複寫相關的物件， **@no_checks** 參數必須設定為 **1**。 如果發行者或散發者已離線或是無法連上， **@ignore_distributor** 參數可以設定為 **1** ，好讓它們可以卸除；但是，必須手動移除任何留下來的發行和散發物件。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例指令碼會從訂閱資料庫中移除複寫物件。  
  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/disable-publishing-and-d_1.sql)]  
  
 此範例指令碼會停用當做發行者和散發者之伺服器上的發行和散發，並卸除散發資料庫。  
  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/disable-publishing-and-d_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
#### <a name="to-disable-publishing-and-distribution"></a>停用發行和散發  
  
1.  移除使用散發者之發行集的所有訂閱。 如需相關資訊，請參閱 [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md) 以及 [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md)。  
  
2.  移除使用散發者的所有訂閱，以及停用所有資料庫的發行 (如果發行者和散發者在相同的伺服器上)。 如需詳細資訊，請參閱 [Delete a Publication](../../relational-databases/replication/publish/delete-a-publication.md)。  
  
3.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連接。  
  
4.  建立 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> 屬性，並傳遞步驟 3 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
5.  (選擇性) 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法，以取得物件的屬性及確認發行者確實存在。 如果此方法傳回 **false**，則表示步驟 4 中設定的發行者名稱不正確，或是此散發者並未使用此發行者。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Remove%2A> 方法。 如果發行者和散發者位於不同的伺服器上，以及應該在散發者上解除安裝發行者，而不需要先確認發行集是否已經不在發行者上時，請針對 **force** 傳遞 *true* 的值。  
  
7.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別的執行個體。 傳遞步驟 3 的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.UninstallDistributor%2A> 方法。 針對 **force** 傳遞 *true* 的值，可在散發者上移除所有複寫物件，而不需要先確認是否已經停用所有本機發行集資料庫及解除安裝散發資料庫。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會移除散發者上的發行者註冊、捨棄散發資料庫，以及解除安裝散發者。  
  
 [!code-cs[HowTo#rmo_DropDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropdistpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropdistpub)]  
  
 此範例會解除安裝散發者，而不先停用本機發行集資料庫或捨棄散發資料庫。  
  
 [!code-cs[HowTo#rmo_DropDistPubForce](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropdistpubforce)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPubForce](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropdistpubforce)]  
  
## <a name="see-also"></a>另請參閱  
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [複寫系統預存程序概念](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
