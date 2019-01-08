---
title: 建立和套用初始快照集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a69d4805a21cfbd83bd9a8d79b5150460d4977be
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358190"
---
# <a name="create-and-apply-the-initial-snapshot"></a>建立和套用初始快照集
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立及套用初始快照集。 使用參數化篩選的合併式發行集需要一個兩段式快照集。 如需詳細資訊，請參閱 [使用參數化篩選建立合併式發行集的快照集](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
 **本主題內容**  
  
-   **若要建立和套用初始快照集，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 依預設，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 正在執行中，則在使用「新增發行集精靈」建立發行集之後，快照集代理程式便會立即產生快照集。 隨後，「散發代理程式」(針對快照式複寫和異動複寫) 或「合併代理程式」(針對合併訂閱) 預設會為所有訂閱套用該快照集。 也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和複寫監視器來產生快照集。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](monitor/start-the-replication-monitor.md)。  
  
#### <a name="to-create-a-snapshot-in-management-studio"></a>若要在 Management Studio 中建立快照集  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要為其建立快照集的發行集，然後按一下 **[檢視快照集代理程式的狀態]**。  
  
4.  在 [檢視快照集代理程式的狀態 - \<發行集>] 對話方塊中，按一下 [啟動]。  
  
 快照集代理程式產生完快照集後，就會顯示一個訊息，例如「[100%] 已產生 17 個發行項的快照集」。  
  
#### <a name="to-create-a-snapshot-in-replication-monitor"></a>若要在複寫監視器中建立快照集  
  
1.  在複寫監視器的左窗格中展開發行者群組，然後展開發行者。  
  
2.  以滑鼠右鍵按一下要產生快照集的發行集，然後按一下 **[產生快照集]**。  
  
3.  若要檢視快照集代理程式的狀態，請按一下 **[代理程式]** 索引標籤。如需詳細資訊，請以滑鼠右鍵按一下方格中的「快照集代理程式」，然後按一下 **[檢視詳細資料]**。  
  
#### <a name="to-apply-a-snapshot"></a>若要套用快照集  
  
1.  產生快照集後，將透過「散發代理程式」或「合併代理程式」對訂閱進行同步處理來套用該快照集：  
  
    -   如果將代理程式設定為連續執行 (異動複寫的預設值)，快照集會在產生後自動套用。  
  
    -   如果將代理程式設定為按排程執行，則快照集將在該代理程式排程的下次執行時套用。  
  
    -   如果將代理程式設定為視需要執行，則快照集將您在下次執行該代理程式時套用。  
  
     如需有關同步處理訂閱的資訊，請參閱＜ [Synchronize a Push Subscription](synchronize-a-push-subscription.md) ＞和＜ [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)資料夾中可用。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以透過程式設計方式建立初始快照集，其方式是建立及執行快照集代理程式作業，或是從批次檔執行快照集代理程式的可執行檔。 在產生初始快照集之後，此快照集會在第一次同步處理訂閱時，傳送及套用到訂閱者。 如果您從命令提示字元或批次檔執行快照集代理程式，每當現有的快照集無效時，您將需要重新執行此代理程式。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
#### <a name="to-create-and-run-a-snapshot-agent-job-to-generate-the-initial-snapshot"></a>建立及執行快照集代理程式作業以產生初始快照集  
  
1.  建立快照式、交易式或合併式發行集。 如需詳細資訊，請參閱 [Create a Publication](publish/create-a-publication.md)。  
  
2.  執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 指定 **@publication** 及下列參數：  
  
    -   **@job_login，它會指定**散發者上的快照集代理程式執行時所用的 Windows 驗證認證。  
  
    -   **@job_password**，它是提供之 Windows 認證的密碼。  
  
    -   (選擇性) 如果代理程式在連接到發行者時將使用「SQL Server 驗證」，會將 **@publisher_security_mode** 設定為 **@publisher_security_mode** 的值。 在此情況下，您也必須針對 **@publisher_login** ＞和＜ **@publisher_password**。  
  
    -   (選擇性) 快照集代理程式作業的同步排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](specify-synchronization-schedules.md)。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
3.  將發行項加入至發行集。 如需詳細資訊，請參閱 [定義發行項](publish/define-an-article.md)。  
  
4.  在發行集資料庫的發行者端，執行 [sp_startpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql)，並指定步驟 1 中的 **@publication** 值。  
  
#### <a name="to-run-the-snapshot-agent-to-generate-the-initial-snapshot"></a>執行快照集代理程式來產生初始快照集  
  
1.  建立快照式、交易式或合併式發行集。 如需詳細資訊，請參閱 [Create a Publication](publish/create-a-publication.md)。  
  
2.  將發行項加入至發行集。 如需詳細資訊，請參閱 [定義發行項](publish/define-an-article.md)。  
  
3.  從命令提示字元或批次檔中，執行 [snapshot.exe](agents/replication-snapshot-agent.md) 來啟動 **複寫合併代理程式**，並指定下列命令列引數：  
  
    -   **-Publication**  
  
    -   **-Publisher**  
  
    -   **-Distributor**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     無果您正在使用「SQL Server 驗證」，您也必須指定下列引數：  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **@publisher_security_mode**  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會示範如何建立交易式發行集，並針對新的發行集加入快照集代理程式作業 (使用 **sqlcmd** 指令碼變數)。 此範例也會啟動此作業。  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpubinitialsnapshot.sql#sp_trangenerate_snapshot)]  
  
 此範例會建立合併式發行集，並針對此發行集加入快照集代理程式作業 (使用 **sqlcmd** 變數)。 此範例也會啟動此作業。  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubinitialsnapshot.sql#sp_mergegenerate_snapshot)]  
  
 下列命令列引數會啟動快照集代理程式，以針對合併式發行集產生快照集。  
  
> [!NOTE]  
>  加入了分行符號，以提升可讀性。 在批次檔中，必須在單一行中撰寫命令。  
  
 [!code-sql[HowTo#startmergesnapshot_10](../../snippets/tsql/SQL15/replication/howto/tsql/createmergesnapshot_10.bat)]  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 快照集代理程式會在發行集建立之後產生快照集。 您可以使用 Replication Management Objects (RMO) 和對複寫代理程式功能的直接 Managed 程式碼存取，以程式設計的方式產生這些快照集。 您使用的物件取決於複寫的類型而定。 您可以使用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 物件同步啟動快照集代理程式，或是使用代理程式作業以非同步方式啟動它。 在產生初始快照集之後，此快照集會在第一次同步處理訂閱時，傳送及套用到訂閱者。 每當現有的快照集不再包含有效且最新的資料時，您就需要重新執行此代理程式。 如需詳細資訊，請參閱[維護發行集](publish/maintain-publications.md)。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>啟動快照集代理程式作業 (非同步) 來針對快照式或交易式發行集產生初始快照集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以載入物件的剩餘屬性。 如果此方法傳回 `false`，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  如果 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 的值是 `false`，請呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 來針對這個發行集建立快照集代理程式作業。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法來啟動代理程式作業，以針對這個發行集產生快照集。  
  
6.  (選擇性) 當 <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> 的值是 `true` 時，表示快照集可供訂閱者使用。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-running-the-snapshot-agent-synchronous"></a>執行快照集代理程式 (同步) 來針對快照式或交易式發行集產生初始快照集  
  
1.  建立 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 類別的執行個體，並設定下列必要的屬性：  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 發行者的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 發行集資料庫的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 發行集的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 散發者的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 表示連接到發行者時會使用 Windows 驗證的 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 值或是 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 的值； <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 的值表示連接到發行者時會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 建議使用 Windows 驗證。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 表示連接到散發者時會使用 Windows 驗證的 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 值或是 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 的值； <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 的值表示連接到散發者時會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 建議使用 Windows 驗證。  
  
2.  針對 <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> 設定 <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> 或 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>的值。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 方法。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>啟動快照集代理程式作業 (非同步) 來針對合併式發行集產生初始快照集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以載入物件的剩餘屬性。 如果此方法傳回 `false`，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  如果 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 的值是 `false`，請呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 來針對這個發行集建立快照集代理程式作業。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法來啟動代理程式作業，以針對這個發行集產生快照集。  
  
6.  (選擇性) 當 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 的值是 `true` 時，表示快照集可供訂閱者使用。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-running-the-snapshot-agent-synchronous"></a>執行快照集代理程式 (同步) 來針對合併式發行集產生初始快照集  
  
1.  建立 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 類別的執行個體，並設定下列必要的屬性：  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 發行者的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 發行集資料庫的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 發行集的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 散發者的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 表示連接到發行者時會使用 Windows 驗證的 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 值或是 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 的值； <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 的值表示連接到發行者時會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 建議使用 Windows 驗證。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 表示連接到散發者時會使用 Windows 驗證的 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 值或是 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 的值； <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 的值表示連接到散發者時會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 建議使用 Windows 驗證。  
  
2.  為 <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> 設定 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>的值。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 方法。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 這個範例會同步執行快照集代理程式，以針對交易式發行集產生初始快照集。  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 這個範例會以非同步方式啟動代理程式作業，以針對交易式發行集產生初始快照集。  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](publish/create-a-publication.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Specify Synchronization Schedules](specify-synchronization-schedules.md)   
 [建立並套用快照集](create-and-apply-the-snapshot.md)   
 [使用快照集初始化訂閱](initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [以指令碼變數使用 sqlcmd](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
