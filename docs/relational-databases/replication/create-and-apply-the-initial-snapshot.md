---
title: 建立和套用初始快照集 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 11628e5b490c30ef64329f6b9d06aee1b6c10fa9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908286"
---
# <a name="create-and-apply-the-initial-snapshot"></a>建立和套用初始快照集
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立及套用初始快照集。 使用參數化篩選的合併式發行集需要一個兩段式快照集。 如需詳細資訊，請參閱 [使用參數化篩選建立合併式發行集的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  快照集在發行集建立之後由「快照代理程式」產生。 它們可以：  
  
-   立即產生。 依預設，在「新增發行集精靈」中建立發行集後會立即產生合併式發行集的快照集。    
-   在排程時間產生。 在「新增發行集精靈」的 **[快照集代理程式]** 頁面上指定排程，或在使用預存程序或 Replication Management Objects (RMO) 時指定排程。    
-   手動。 在命令提示下或從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行「快照集代理程式」。 如需執行代理程式的詳細資訊，請參閱[複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)和[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
針對合併式複寫，每次執行快照集代理程式都會產生快照集。 針對異動複寫，是否產生快照集是依照發行集屬性 **immediate_sync**的設定而定。 若屬性設定為 TRUE (使用新增發行集精靈的預設)，每次執行快照集代理程式都會產生快照集，同時隨時可套用至訂閱者。 若屬性設定為 FALSE (使用 **sp_addpublication**時的預設)，則只有在上次執行快照集代理程式後有加入新訂閱的情況下，才會產生快照集。訂閱者必須等待快照集代理程式完成，才能同步處理。  
  
依預設，快照集產生後會儲存在「散發者」上的預設快照集資料夾中。 您也可以將快照集檔案儲存於抽取式媒體，例如卸除式磁碟機、CD-ROM 或預設快照集資料夾之外的位置。 此外，您可以壓縮檔案，使它們更易儲存和傳送，還可以在快照集套用至「訂閱者」端前後執行指令碼。 如需這些選項的詳細資訊，請參閱 [Snapshot Options](../../relational-databases/replication/snapshot-options.md)。  
  
若快照集是專為使用參數化篩選的合併式發行集而產生，該快照集會使用兩部份處理建立而成。 首先建立結構描述快照集，其中包含複寫指令碼和已發行物件的結構描述，但不包含資料。 接下來每個訂閱皆以快照集初始化，該快照集中包含從結構描述快照集複製而來的指令碼和結構描述，以及屬於訂閱分割的資料。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
快照集在「發行者」端建立，並儲存於預設或替代的快照集位置之後，可以傳送「訂閱者」並進行套用。 初始同步處理期間，「散發代理程式」 (用於快照式或異動複寫) 或「合併代理程式」 (用於合併式複寫) 會傳送快照集，並將結構描述和資料檔套用至「訂閱者」端的訂閱資料庫。 依預設，如果您使用「新增訂閱精靈」，初始同步處理便會在建立訂閱之後立即進行。 此行為由精靈 **[初始化訂閱]** 頁面上的 **[初始化時機]** 選項控制。 快照集在訂閱初始化之後產生時，不會套用至「訂閱者」，除非訂閱已標示為要重新初始化。 如需詳細資訊，請參閱 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
「散發代理程式」或「合併代理程式」套用初始化快照集後，代理程式會傳播後續的更新以及其他資料修改。 快照集散發並套用至「訂閱者」後，只有等待初始快照集或新快照集的「訂閱者」會受影響。 該發行集的其他「訂閱者」(收到對已發行資料之插入、更新、刪除或其他修改的「訂閱者」) 均不受影響。  

若要檢視或修改預設的快照資料夾位置，請參閱  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:[修改快照集選項](../../relational-databases/replication/snapshot-options.md)  
  
-   複寫程式設計和 RMO 程式設計：[設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)  

## <a name="default-snapshot-location"></a>預設快照集位置

 在「設定散發精靈」的 **[快照集資料夾]** 頁面中指定預設快照集位置。 如需使用此精靈的詳細資訊，請參閱[設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)。 如果您在未設定為「散發者」的伺服器上建立發行集，則請在「新增發行集精靈」的 **[快照集資料夾]** 頁面中指定預設快照集位置。 如需使用此精靈的詳細資訊，請參閱[建立發行集](../../relational-databases/replication/publish/create-a-publication.md)。  
  
 在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，修改預設快照集位置。 如需詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。 在 [發行集屬性 - \<發行集>]  對話方塊中為每個發行集設定快照集資料夾。 如需詳細資訊，請參閱 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### <a name="modify-the-default-snapshot-location"></a>修改預設快照集位置  
  
1.  在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，按一下您要變更其預設快照集位置之發行者的屬性按鈕 ( **...** )。  
  
2.  在 [發行者屬性 - \<發行者>]  對話方塊中，輸入 [預設快照集資料夾]  屬性的值。  
  
    > [!NOTE]  
    >  快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定一個共用目錄作為通用命名慣例 (UNC) 路徑，例如 \\\computername\snapshot。 如需詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="create-snapshot"></a>建立快照集
根據預設，如果 SQL Server Agent 正在執行，則在使用「新增發行集精靈」建立發行集之後，「快照集代理程式」會立即產生快照集。 隨後，「散發代理程式」(針對快照式複寫和異動複寫) 或「合併代理程式」(針對合併訂閱) 預設會為所有訂閱套用該快照集。 也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和複寫監視器來產生快照集。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  

### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio

1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。    
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。    
3.  以滑鼠右鍵按一下您要為其建立快照集的發行集，然後按一下 **[檢視快照集代理程式的狀態]** 。    
4.  在 [檢視快照集代理程式的狀態 - \<發行集>]  對話方塊中，按一下 [啟動]  。    
 快照集代理程式產生完快照集後，就會顯示一個訊息，例如「[100%] 已產生 17 個發行項的快照集」。  
  
### <a name="in-replication-monitor"></a>在複寫監視器中  
  
1.  在複寫監視器的左窗格中展開發行者群組，然後展開發行者。    
2.  以滑鼠右鍵按一下要產生快照集的發行集，然後按一下 **[產生快照集]** 。    
3.  若要檢視快照集代理程式的狀態，請按一下 **[代理程式]** 索引標籤。如需詳細資訊，請以滑鼠右鍵按一下方格中的「快照集代理程式」，然後按一下 **[檢視詳細資料]** 。  

## <a name="using-transact-sql"></a>使用 Transact-SQL
可以透過程式設計方式建立初始快照集，其方式是建立及執行快照集代理程式作業，或是從批次檔執行快照集代理程式的可執行檔。 在產生初始快照集之後，此快照集會在第一次同步處理訂閱時，傳送及套用到訂閱者。 如果您從命令提示字元或批次檔執行快照集代理程式，每當現有的快照集無效時，您將需要重新執行此代理程式。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  

1.  建立快照式、交易式或合併式發行集。 如需詳細資訊，請參閱[建立發行集](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定 **\@publication** 及下列參數：  
  
    -   **\@job_login**，其會指定散發者上快照集代理程式執行時所用的 Windows 驗證認證。  
  
    -   **\@job_password**，其為所提供 Windows 認證的密碼。  
  
    -   (選擇性) 如果代理程式會在連接到發行者時使用 SQL Server 驗證，請為 **\@publisher_security_mode** 設定為 **0** 值。 在此情況下，您也必須為 **\@publisher_login** 和 **\@publisher_password** 指定 SQL Server 驗證的登入資訊。  
  
    -   (選擇性) 快照集代理程式作業的同步排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
3.  將發行項加入至發行集。 如需詳細資訊，請參閱 [定義發行項](../../relational-databases/replication/publish/define-an-article.md)。  
  
4.  在發行集資料庫的發行者端，執行 [sp_startpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)，並指定步驟 1 中的 **\@publication** 值。  
  
## <a name="apply-a-snapshot"></a>套用快照集  

### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio
  
1.  產生快照集後，將透過「散發代理程式」或「合併代理程式」對訂閱進行同步處理來套用該快照集：   
    -   如果將代理程式設定為連續執行 (異動複寫的預設值)，快照集會在產生後自動套用。   
    -   如果將代理程式設定為按排程執行，則快照集將在該代理程式排程的下次執行時套用。    
    -   如果將代理程式設定為視需要執行，則快照集將您在下次執行該代理程式時套用。  
  
     如需有關同步處理訂閱的資訊，請參閱＜ [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) ＞和＜ [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)資料夾中可用。  
  
###   <a name="use-transact-sql"></a>使用 Transact-SQL  
 
1.  建立快照式、交易式或合併式發行集。 如需詳細資訊，請參閱[建立發行集](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  將發行項加入至發行集。 如需詳細資訊，請參閱 [定義發行項](../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  從命令提示字元或批次檔中，執行 [snapshot.exe](../../relational-databases/replication/agents/replication-snapshot-agent.md) 來啟動 **複寫合併代理程式**，並指定下列命令列引數：  
  
    -   **-Publication**  
    -   **-Publisher**  
    -   **-Distributor**   
    -   **-PublisherDB**   
    -   **-ReplicationType**  
  
     無果您正在使用「SQL Server 驗證」，您也必須指定下列引數：  
  
    -   **-DistributorLogin**    
    -   **-DistributorPassword**   
    -   **-DistributorSecurityMode** =  **\@publisher_security_mode**    
    -   **-PublisherLogin**    
    -   **-PublisherPassword**    
    -   **-PublisherSecurityMode** =  **@publisher_security_mode**  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會示範如何建立交易式發行集，並針對新的發行集加入快照集代理程式作業 (使用 **sqlcmd** 指令碼變數)。 此範例也會啟動此作業。  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_1.sql)]  
  
 此範例會建立合併式發行集，並針對此發行集加入快照集代理程式作業 (使用 **sqlcmd** 變數)。 此範例也會啟動此作業。  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_2.sql)]  
  
 下列命令列引數會啟動快照集代理程式，以針對合併式發行集產生快照集。  
  
> [!NOTE]  
>  加入了分行符號，以提升可讀性。 在批次檔中，必須在單一行中撰寫命令。  
  
```  
  
REM -- Declare variables  
SET Publisher=%InstanceName%  
SET PublicationDB=AdventureWorks2012   
SET Publication=AdvWorksSalesOrdersMerge   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 快照集代理程式會在發行集建立之後產生快照集。 您可以使用 Replication Management Objects (RMO) 和對複寫代理程式功能的直接 Managed 程式碼存取，以程式設計的方式產生這些快照集。 您使用的物件取決於複寫的類型而定。 您可以使用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 物件同步啟動快照集代理程式，或是使用代理程式作業以非同步方式啟動它。 在產生初始快照集之後，此快照集會在第一次同步處理訂閱時，傳送及套用到訂閱者。 每當現有的快照集不再包含有效且最新的資料時，您就需要重新執行此代理程式。 如需詳細資訊，請參閱[維護發行集](../../relational-databases/replication/publish/maintain-publications.md)。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>啟動快照集代理程式作業 (非同步) 來針對快照式或交易式發行集產生初始快照集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性，並將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以載入物件的剩餘屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  如果 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 的值是 **false**，請呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 來針對這個發行集建立快照集代理程式作業。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法來啟動代理程式作業，以針對這個發行集產生快照集。  
  
6.  (選擇性) 當 <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> 的值是 **true**時，表示快照集可供訂閱者使用。  
  
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
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以載入物件的剩餘屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  如果 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 的值是 **false**，請呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 來針對這個發行集建立快照集代理程式作業。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法來啟動代理程式作業，以針對這個發行集產生快照集。  
  
6.  (選擇性) 當 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 的值是 **true**時，表示快照集可供訂閱者使用。  
  
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
  
 [!code-cs[HowTo#rmo_GenerateSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 這個範例會以非同步方式啟動代理程式作業，以針對交易式發行集產生初始快照集。  
  
 [!code-cs[HowTo#rmo_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)   
 [使用快照集初始化訂閱](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [以指令碼變數使用 sqlcmd](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
