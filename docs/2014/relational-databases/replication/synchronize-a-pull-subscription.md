---
title: 同步處理提取訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41374e742c31574f3504c20104f0a7a3775d77cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48213018"
---
# <a name="synchronize-a-pull-subscription"></a>同步處理提取訂閱
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]複寫代理程式 [或 Replication Management Objects (RMO) 來同步處理](agents/replication-agents-overview.md)中的提取訂閱。  
  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 訂閱是由散發代理程式 (適用於快照式與異動複寫) 或合併代理程式 (適用於合併式複寫) 同步處理。 代理程式可以繼續執行、視需要執行，或是依照排程執行。 如需指定同步處理排程的詳細資訊，請參閱[指定同步處理排程](specify-synchronization-schedules.md)。  
  
 從 **中的** [本機訂閱] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料夾視需要同步處理訂閱。  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>若要在 Management Studio 中視需要同步處理提取訂閱  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要同步處理的訂閱，然後按一下 **[檢視同步處理的狀態]**。  
  
4.  在 [檢視同步處理的狀態 - \<訂閱者>:\<訂閱資料庫>] 對話方塊中，按一下 [啟動]。 同步處理完成後，會顯示 **[同步處理已完成]** 的訊息。  
  
5.  按一下 [ **關閉**]。  
  
##  <a name="ReplProg"></a> Replication Agents  
 提取訂閱可透過程式設計方式加以同步處理，以及視需要從命令提示字元叫用適當的複寫代理程式可執行檔加以同步處理。 叫用的複寫代理程式可執行檔取決於提取訂閱所屬的發行集類型。 如需詳細資訊，請參閱 [Replication Agents](agents/replication-agents.md)。  
  
> [!NOTE]  
>  複寫代理程式會使用從命令提示字元啟動此代理程式之使用者的 Windows 驗證認證，連接到本機伺服器。 當使用「Windows 整合式驗證」連接到遠端伺服器時，也會使用這些 Windows 認證。  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>從命令提示字元或批次檔執行散發代理程式  
  
1.  從命令提示字元或批次檔中，執行 [distrib.exe](agents/replication-distribution-agent.md) 來啟動 **複寫散發代理程式**，並指定下列命令列引數：  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     如果您正在使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」，您也必須指定下列引數：  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### <a name="to-start-the-merge-agent-from-the-command-prompt-or-from-a-batch-file"></a>從命令提示字元或批次檔執行合併代理程式  
  
1.  從命令提示字元或批次檔中，執行 [replmerg.exe](agents/replication-merge-agent.md) 來啟動 **複寫合併代理程式**，並指定下列命令列引數：  
  
    -   **-Publisher**  
  
    -   **-PublisherDB**  
  
    -   **-PublisherSecurityMode** = **1**  
  
    -   **-Publication**  
  
    -   **-Distributor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Subscriber**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     如果您正在使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」，您也必須指定下列引數：  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> 範例 (複寫代理程式)  
 下列範例會啟動散發代理程式，以同步處理提取訂閱。 所有的連接都是使用「Windows 驗證」所建立。  
  
 [!code-sql[HowTo#bat_synctranpullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/synctranpullsub_10.bat)]  
  
 下列範例會啟動合併代理程式，以同步處理提取訂閱。 所有的連接都是使用「Windows 驗證」所建立。  
  
 [!code-sql[HowTo#bat_syncmergepullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/syncmergepullsub_10.bat)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 和對複寫代理程式功能的 Managed 程式碼存取，以程式設計的方式同步處理提取訂閱。 用於同步處理提取訂閱的類別依該訂閱所屬的發行集類型而定。  
  
> [!NOTE]  
>  如果您要啟動自發執行的同步處理而不影響應用程式，請非同步啟動代理程式。 不過，如果要監視同步處理的結果並在同步處理期間從代理程式接收回撥 (例如，顯示進度列)，您就應該同步啟動代理程式。 您必須為「 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 訂閱者」同步啟動代理程式。  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>若要同步處理快照式或交易式發行集的提取訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別的執行個體，並設定下列屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>設為訂閱資料庫名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>設為訂閱所屬發行集的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>設定為發行集資料庫名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>設為「發行者」的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>設為步驟 1 中建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得剩餘的訂閱屬性。 如果此方法傳回`false`，確認該訂閱存在。  
  
4.  以下列其中一種方式啟動「訂閱者」上的「散發代理程式」：  
  
    -   從步驟 2 的 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> 執行個體上呼叫 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 方法。 此方法會以非同步方式啟動散發代理程式，並且控制項會在代理程式作業執行時立即傳回至應用程式。 您不可以針對「[!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 訂閱者」呼叫此方法，或者如果訂閱是以 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 的 `false` 值 (預設值) 建立的，也不可以。  
  
    -   從 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 屬性取得 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> 類別的執行個體，並呼叫 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> 方法。 此方法會同步啟動代理程式，而控制項仍會停留於正在執行的代理程式作業。 在同步執行期間，您可以在代理程式執行時處理 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> 事件。  
  
        > [!NOTE]  
        >  如果您指定的值`false`for <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> （預設值） 當您在建立提取訂閱，您也需要指定<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>， <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>，並選擇性地<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A>和<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A>因為代理程式作業相關訂用帳戶的中繼資料中沒有[MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)。  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>若要同步處理合併式發行集的提取訂閱  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別的執行個體，並設定下列屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>設為訂閱資料庫名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>設為訂閱所屬發行集的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>設為發行的資料庫名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>設為「發行者」的名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>設為步驟 1 中建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得剩餘的訂閱屬性。 如果此方法傳回`false`，確認該訂閱存在。  
  
4.  以下列其中一種方式啟動「訂閱者」上的「合併代理程式」：  
  
    -   從步驟 2 的 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> 執行個體上呼叫 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 方法。 此方法會以非同步方式啟動合併代理程式，並且控制項會在代理程式作業執行時立即傳回至應用程式。 您不可以針對「[!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 訂閱者」呼叫此方法，或者如果訂閱是以 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 的 `false` 值 (預設值) 建立的，也不可以。  
  
    -   從 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 屬性取得 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> 類別的執行個體，並呼叫 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> 方法。 此方法會同步啟動「合併代理程式」，而控制項仍會停留於正在執行的代理程式作業。 在同步執行期間，您可以在代理程式執行時處理 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> 事件。  
  
        > [!NOTE]  
        >  如果您指定的值`false`for <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> （預設值） 當您在建立提取訂閱，您也需要指定<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A>， <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>， <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>， <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>， <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>， <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>，及選擇性地<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A>， <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A>， <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A>，以及<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A>因為代理程式作業相關中繼資料的訂用帳戶不適用於[MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例同步處理交易式發行集的提取訂閱，其中代理程式會使用代理程式作業非同步啟動。  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub_withjob)]  
  
 此範例同步處理交易式發行集的提取訂閱，其中代理程式會同步啟動。  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub)]  
  
 此範例同步處理合併式發行集的提取訂閱，其中代理程式會使用代理程式作業非同步啟動。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_withjob)]  
  
 此範例同步處理合併式發行集的提取訂閱，其中代理程式會同步啟動。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub)]  
  
 此範例使用 Web 同步處理來同步處理合併式發行集的提取訂閱。 該訂閱是在沒有代理程式作業和相關訂閱中繼資料的情況下建立的，因此必須同步啟動代理程式並提供其他訂閱資訊。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_NoJobWebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_nojobwebsync)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_NoJobWebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_nojobwebsync)]  
  
## <a name="see-also"></a>另請參閱  
 [同步處理資料](synchronize-data.md)   
 [建立提取訂閱](create-a-pull-subscription.md)   
 [複寫安全性最佳作法](security/replication-security-best-practices.md)  
  
  
