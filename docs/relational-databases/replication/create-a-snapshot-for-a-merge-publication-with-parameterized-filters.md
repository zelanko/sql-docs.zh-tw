---
title: "使用參數化篩選建立合併式發行集的快照集 | Microsoft Docs"
ms.custom: ""
ms.date: "05/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "參數化篩選 [SQL Server 複寫], 快照集"
  - "快照集 [SQL Server 複寫], 參數化篩選和"
  - "篩選 [SQL Server 複寫], 參數化"
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 使用參數化篩選建立合併式發行集的快照集
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用參數化篩選建立合併式發行集的快照集。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要使用參數化篩選建立合併式發行集的快照集，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   在使用參數化篩選產生合併式發行集的快照集時，您必須先產生一個標準 (結構描述) 快照集，其中包含所有發行的資料以及訂閱的訂閱者中繼資料。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。 在您建立結構描述快照集之後，您可以產生包含發行資料之訂閱者特有資料分割的快照集。  
  
-   如果發行集內的一或多個發行項的篩選產生對每個訂閱而言是唯一的非重疊資料分割，則只要合併代理程式一執行，就會清除中繼資料。 這表示分割快照集會更快過期。 使用這個選項時，您應該考慮允許訂閱者初始化快照集的產生與傳遞。 如需篩選選項的詳細資訊，請參閱 \< 設定 '資料分割選項 > 一節 [使用參數化篩選的合併式發行集的快照集](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 產生資料分割的快照集上 **資料分割** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。 您可以讓訂閱者初始化快照集產生和傳遞，並且/或者產生快照集。  
  
 產生一個或多個資料分割的快照集之前，必須：  
  
1.  使用「新增發行集精靈」建立合併發行集，並在精靈的 **[加入篩選]** 頁面上，指定一個或多個參數化資料列篩選器。 如需詳細資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
2.  產生發行集的結構描述快照集。 依預設，當您完成「新增發行集精靈」時，便會產生結構描述快照集；您也可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]產生結構描述快照集。  
  
#### 若要產生結構描述快照集  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要建立快照集，並按一下 [發行的集 **檢視快照集代理程式狀態**。  
  
4.  在 **檢視快照集代理程式狀態-\< 發行集>** 對話方塊中，按一下 [ **啟動**。  
  
     快照集代理程式產生完快照集後，就會顯示一個訊息，例如「[100%] 已產生 17 個發行項的快照集」。  
  
#### 若要允許訂閱者初始化快照集的產生與傳遞  
  
1.  在 **資料分割** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取 **自動定義資料分割並依需要新的訂閱者嘗試進行同步處理時產生快照集**。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### 若要產生和重新整理快照集  
  
1.  在 **資料分割** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **新增**。  
  
2.  輸入一個值 **host_name （)** 及/或 **suser_sname （)** 與您要建立快照集的資料分割相關聯的值。  
  
3.  選擇性地指定重新整理快照集的排程：  
  
    1.  選取 **排程在下列時間執行的這個資料分割快照集代理程式**  
  
    2.  接受重新重理快照集的預設排程，或按一下 **[變更]** 以指定其他排程。  
  
4.  按一下 [ **確定**, ，它會傳回您 **發行集屬性-\< 發行集>** 對話方塊。  
  
5.  在屬性方格中選取資料分割，然後按一下 **[立即產生選取的快照集]**。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用預存程序和快照集代理程式進行以下作業：  
  
-   允許訂閱者在首次執行同步處理時，要求快照集產生和應用程式。  
  
-   為每個資料分割預先產生快照集。  
  
-   以手動方式為每一個訂閱者產生快照集。  
  
    > [!IMPORTANT]  
    >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
#### 建立可讓訂閱者初始化快照集產生和傳遞的發行集  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定下列參數：  
  
    -   將 **@publication**設定為發行集的名稱。  
  
    -   值為 **true** 的 **@allow_subscriber_initiated_snapshot**, ，可讓訂閱者初始化快照集處理序。  
  
    -   （選擇性）可以同時執行的動態快照集處理序數目 **@max_concurrent_dynamic_snapshots**。 如果正在執行最大的處理序數目，而且訂閱者嘗試產生快照集，則會將此處理序置於佇列中。 根據預設，並行處理序的數目沒有任何限制。  
  
2.  在 「 發行者 」 執行 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定為步驟 1 中所使用的發行集名稱 **@publication** 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 所在的 Windows 認證 [複寫快照集代理程式](../../relational-databases/replication/agents/replication-snapshot-agent.md) 執行 **@job_login** 和 **@password**。 如果代理程式會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到發行者時，您必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有參數的值來設定發行者時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
3.  執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 您可以將發行項加入發行集。 必須針對發行集中的每一個發行項執行一次此預存程序。 使用參數化的篩選時，您必須指定一個或多個發行項使用的參數化資料列篩選 **@subset_filterclause** 參數。 如需詳細資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果將根據參數化資料列篩選器來篩選其他文件，執行 [sp_addmergefilter & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 若要定義聯結或發行項之間的邏輯記錄關聯性。 必須針對每一個定義的關聯性執行一次此預存程序。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  當合併代理程式要求此快照集初始化訂閱者時，會自動產生要求之訂閱資料分割的快照集。  
  
#### 建立發行集及預先產生或自動重新整理快照集  
  
1.  執行 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 若要建立發行集。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  在 「 發行者 」 執行 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定為步驟 1 中所使用的發行集名稱 **@publication** 和 Windows 認證的快照集代理程式執行 **@job_login** 和 **@password**。 如果代理程式會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到發行者時，您必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有參數的值來設定發行者時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
3.  執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 您可以將發行項加入發行集。 必須針對發行集中的每一個發行項執行一次此預存程序。 使用參數化的篩選時，您必須指定一個發行項使用的參數化資料列篩選 **@subset_filterclause** 參數。 如需詳細資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果將根據參數化資料列篩選器來篩選其他文件，執行 [sp_addmergefilter & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 若要定義聯結或發行項之間的邏輯記錄關聯性。 必須針對每一個定義的關聯性執行一次此預存程序。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  在發行集資料庫的發行者，執行 [sp_helpmergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，指定的值 **@publication** 步驟 1 中。 記下的值 **snapshot_jobid** 結果集中。  
  
6.  值轉換成 **snapshot_jobid** 在步驟 5 中取得 **uniqueidentifier**。  
  
7.  在發行者上 **msdb** 資料庫，請執行 [sp_start_job & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), ，指定步驟 6 中所取得的已轉換的值 **@job_id**。  
  
8.  在發行集資料庫的發行者，執行 [sp_addmergepartition & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)。 指定步驟 1 中的發行集名稱 **@publication** 以及用來定義的資料分割的值 **@suser_sname** 如果 [SUSER_SNAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md) 可用於篩選子句中或 **@host_name** 如果 [HOST_NAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) 用於篩選子句。  
  
9. 在發行集資料庫的發行者，執行 [sp_adddynamicsnapshot_job & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)。 指定步驟 1 中的發行集名稱 **@publication**, ，值 **@suser_sname** 或 **@host_name** 從步驟 8 和工作的排程。 這樣會建立針對指定的資料分割產生參數化快照集的作業。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
    > [!NOTE]  
    >  這個作業會使用與步驟 2 中定義的初始快照集作業相同的 Windows 帳戶來執行。 若要移除的參數化快照集作業和其相關的資料分割，請執行 [sp_dropdynamicsnapshot_job & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)。  
  
10. 在發行集資料庫的發行者，執行 [sp_helpmergepartition & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md), ，指定的值 **@publication** 從步驟 1 和的值 **@suser_sname** 或 **@host_name** 步驟 8 中。 記下的值 **dynamic_snapshot_jobid** 結果集中。  
  
11. 在散發者上 **msdb** 資料庫，請執行 [sp_start_job & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), ，指定步驟 9 中所取得的值 **@job_id**。 這樣會啟動資料分割的參數化快照集作業。  
  
12. 針對每一個訂閱重複步驟 8-11 來產生分割快照集。  
  
#### 針對每一個資料分割建立發行集及手動建立快照集  
  
1.  執行 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 若要建立發行集。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  在 「 發行者 」 執行 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定為步驟 1 中所使用的發行集名稱 **@publication** 和 Windows 認證的快照集代理程式執行 **@job_login** 和 **@password**。 如果代理程式會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接到發行者時，您必須指定值為 **0** 的 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入資訊 **@publisher_login** 和 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有參數的值來設定發行者時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
3.  執行 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 您可以將發行項加入發行集。 必須針對發行集中的每一個發行項執行一次此預存程序。 使用參數化的篩選時，您必須指定至少一個發行項使用的參數化資料列篩選 **@subset_filterclause** 參數。 如需詳細資訊，請參閱 [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果將根據參數化資料列篩選器來篩選其他文件，執行 [sp_addmergefilter & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 若要定義聯結或發行項之間的邏輯記錄關聯性。 必須針對每一個定義的關聯性執行一次此預存程序。 如需詳細資訊，請參閱 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  從命令提示字元啟動快照集作業或是執行複寫快照集代理程式，以產生標準快照集結構描述和其他檔案。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
6.  再次執行複寫快照集代理程式，從命令提示字元中產生大量複製 (.bcp) 檔案，指定資料分割快照集位置 **-DynamicSnapshotLocation** 和一或兩個資料分割會定義下列屬性︰  
  
    -   **-DynamicFilterHostName** -值如果 [HOST_NAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) 會使用。  
  
    -   **-DynamicFilterLogin** -值如果 [SUSER_SNAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md) 會使用。  
  
7.  針對每一個訂閱重複步驟 6 來產生分割快照集。  
  
8.  針對每一個訂閱執行合併代理程式，以便在訂閱者上套用初始分割快照集，並指定下列屬性：  
  
    -   **-Hostname** -用來定義資料分割，如果要覆寫 HOST_NAME 的實際值的值。  
  
    -   **-DynamicSnapshotLocation** -此磁碟分割的動態快照集的位置。  
  
> [!NOTE]  
>  如需程式設計複寫代理程式的詳細資訊，請參閱 [複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會使用參數化篩選來建立合併式發行集，其中的訂閱者會起始快照集的產生程序。 值 **@job_login** 和 **@job_password** 傳入使用指令碼變數。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_1.sql)]  
  
 這個範例會建立發行集使用參數化的篩選，其中每個訂閱者有定義執行其資料分割 [sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) 和執行所建立的已篩選的快照集作業 [sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) 傳遞的資料分割資訊。 值 **@job_login** 和 **@job_password** 傳入使用指令碼變數。  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_2.sql)]  
  
 這個範例會使用參數化篩選建立發行集，其中的每一個訂閱者必須藉由提供資料分割資訊，以建立其資料分割和篩選的快照集作業。 訂閱者在手動執行複寫代理程式時，會使用命令列參數提供資料分割資訊。 此範例假設也已經建立發行集的訂閱。  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPartitionManual](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_3.sql)]  
  
```  
  
REM Line breaks are added to improve readability.   
REM In a batch file, commands must be made in a single line.  
REM Run the Snapshot agent from the command line to generate the standard snapshot   
REM schema and other files.   
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub% -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  
  
PAUSE  
  
```  
  
```  
  
REM Run the Snapshot agent from the command line, this time to generate   
REM the bulk copy (.bcp) data for each Subscriber partition.    
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
MD %SnapshotDir%  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub%  -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  -DynamicFilterHostName "adventure-works\Fernando"    
-DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
```  
  
REM Run the Merge Agent for each subscription to apply the partitioned   
REM snapshot for each Subscriber.    
SET Publisher = %computername%  
SET Subscriber = %computername%  
SET PubDB = AdventureWorks2012   
SET SubDB = AdventureWorks2012Replica   
SET PubName = AdvWorksSalesPersonMerge   
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publisher  %Publisher%    
-Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB %PubDB%    
-SubscriberDB %SubDB% -Publication %PubName%  -PublisherSecurityMode 1  -OutputVerboseLevel 3    
-Output -SubscriberSecurityMode 1  -SubscriptionType 3 -DistributorSecurityMode 1    
-Hostname "adventure-works\Fernando"  -DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以透過以下方式，以程式設計的方式使用 Replication Management Objects (RMO) 來產生分割快照集。  
  
-   允許訂閱者在首次執行同步處理時，要求快照集產生和應用程式。  
  
-   為每個資料分割預先產生快照集。  
  
-   執行「快照集代理程式」為每個訂閱者手動產生快照集。  
  
> [!NOTE]  
>  篩選的發行項會產生非重疊的資料分割 （藉由建立合併發行項時，指定如 P:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption F:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription 值） 都是唯一的每個訂閱時, 清除中繼資料只要合併代理程式執行。 這表示分割快照集會更快過期。 當使用這個選項時，您應該考慮允許訂閱者要求產生快照集。 如需詳細資訊，請參閱＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md)＞主題中的「使用適當的篩選選項」一節。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
#### 建立可讓訂閱者初始化快照集產生和傳遞的發行集  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別發行集資料庫中，設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 的執行個體的內容 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 從步驟 1，並呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 傳回 **false**, ，確認資料庫是否存在。  
  
3.  如果 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 屬性是 **false**, ，將它設定為 **true** 呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>。  
  
4.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別，並設定此物件的下列屬性︰  
  
    -    <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   針對已發行的資料庫名稱 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>。  
  
    -   發行集的名稱 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>。  
  
    -   若要執行的動態快照集作業的數目上限 <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>。 由於訂閱者起始的快照集要求可在任何時間發生，所以當多個訂閱者同時要求其分割快照集時，這個屬性會限制可以同時執行的快照集代理程式作業數目。 當正在執行最大的作業數目時，其他分割快照集要求會排入佇列中，直到其中一個執行中的作業完成為止。  
  
    -   使用位元邏輯 OR (**|** Visual C# 和 **或者** 在 Visual Basic 中) 運算子，以將值 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> 至 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>。  
  
    -    <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 提供的認證 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶下執行 「 快照集代理程式作業。  
  
        > [!NOTE]  
        >  設定 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 的成員建立發行集時，建議您使用 **sysadmin** 固定的伺服器角色。 如需相關資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法來建立發行集。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有屬性的值來設定發行者時包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, ，傳送到 「 散發者 」，以純文字。 您應該先加密 「 發行者 」 之前，先呼叫其遠端散發者之間連接 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
6.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 將發行項加入發行集的屬性。 指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 至少一個定義參數化的篩選的發行項的屬性。 （選擇性）建立 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 物件，以定義聯結發行項之間的篩選。 如需詳細資訊，請參閱 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
7.  如果值 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 是 **false**, ，呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 來建立此發行集的初始快照集代理程式作業。  
  
8.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法 <xref:Microsoft.SqlServer.Replication.MergePublication> 步驟 4 中建立的物件。 這樣會啟動可產生初始快照集的代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
9. （選擇性）檢查是否有值的 **true** 的 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 屬性，以判斷初始快照集可供使用時。  
  
10. 當訂閱者的合併代理程式第一次連接時，會自動產生分割快照集。  
  
#### 建立發行集及預先產生或自動重新整理快照集  
  
1.  使用的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別來定義合併式發行集。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 將發行項加入發行集的屬性。 指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 至少一個發行項定義參數化的篩選，並建立任何屬性 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 物件，以定義聯結發行項之間的篩選。 如需詳細資訊，請參閱 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  如果值 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 是 **false**, ，呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 來建立此發行集的快照集代理程式作業。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法 <xref:Microsoft.SqlServer.Replication.MergePublication> 步驟 1 中建立的物件。 這個方法會啟動可產生初始快照集的代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
5.  檢查是否有值的 **true** 的 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 屬性，以判斷初始快照集可供使用時。  
  
6.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePartition> 類別，並設定 「 訂閱者 」 的參數化篩選準則，使用其中一個或多個下列屬性︰  
  
    -   如果訂閱者資料分割會定義由結果 [SUSER_SNAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md), ，使用 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>。  
  
    -   如果訂閱者資料分割會定義由結果 [HOST_NAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) 多載的函式中，使用或 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>。  
  
7.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 類別，並設定相同的屬性，如步驟 6 所示。  
  
8.  使用 <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> 類別定義的排程產生訂閱者資料分割的篩選快照集。  
  
9. 使用的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 從步驟 1 中，呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>。 傳遞 <xref:Microsoft.SqlServer.Replication.MergePartition> 步驟 6 中的物件。  
  
10. 使用的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 從步驟 1 中，呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> 方法。 傳遞 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 步驟 7 中的物件和 <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> 步驟 8 中的物件。  
  
11. 呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>, ，並找出 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 新加入的資料分割快照集作業傳回的陣列中的物件。  
  
12. 取得 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> 工作的屬性。  
  
13. 建立連接到散發者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
14. 建立執行個體的 SQL Server 管理物件 (SMO) <xref:Microsoft.SqlServer.Management.Smo.Server> 類別，並傳遞 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 13 中的物件。  
  
15. 建立的執行個體 <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> 類別，並傳遞 <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> 屬性 <xref:Microsoft.SqlServer.Management.Smo.Server> 步驟 14 與步驟 12 中的作業名稱的物件。  
  
16. 呼叫 <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> 方法來啟動資料分割快照集作業。  
  
17. 對每一個訂閱者重複步驟 6-16。  
  
#### 針對每一個資料分割建立發行集及手動建立快照集  
  
1.  使用的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別來定義合併式發行集。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 屬性將發行項加入發行集指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 至少一個發行項定義參數化的篩選，並建立任何屬性 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 物件，以定義聯結發行項之間的篩選。 如需詳細資訊，請參閱 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  產生初始快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
4.  建立 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 類別的執行個體，並設定下列必要的屬性：  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> -發行者的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> -發行集資料庫的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> -發行集的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> -散發者的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -值 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 使用的 Windows 整合式驗證或值 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 使用 SQL Server 驗證。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -值 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 使用的 Windows 整合式驗證或值 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 使用 SQL Server 驗證。  
  
5.  設定值為 <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> 的 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>。  
  
6.  設定以下其中一個或多個屬性來定義資料分割參數：  
  
    -   如果訂閱者資料分割會定義由結果 [SUSER_SNAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md), ，使用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A>。  
  
    -   如果訂閱者資料分割會定義由結果 [HOST_NAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) 多載的函式中，使用或 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A>。  
  
7.  呼叫 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 方法。  
  
8.  對每一個訂閱者重複步驟 4-7。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會建立允許訂閱者要求產生快照集的合併式發行集。  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 這個範例會使用參數化資料列篩選器，針對合併式發行集手動建立訂閱者資料分割及篩選的快照集。  
  
 [!code-csharp[HowTo#rmo_CreateMergePartition](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 這個範例會使用參數化資料列篩選器，針對合併式發行集的訂閱者啟動快照集代理程式來產生篩選的資料快照集。  
  
 [!code-csharp[HowTo#rmo_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## 另請參閱  
 [參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [複寫系統預存程序概念](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [含參數化篩選之合併式發行集的快照集](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  