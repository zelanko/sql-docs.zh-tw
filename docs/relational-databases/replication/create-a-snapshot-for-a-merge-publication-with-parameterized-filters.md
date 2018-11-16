---
title: 使用參數化篩選建立合併式發行集的快照集 | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- parameterized filters [SQL Server replication], snapshots
- snapshots [SQL Server replication], parameterized filters and
- filters [SQL Server replication], parameterized
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 71d7e79a0e941b5f080b033469700e19eaa3241e
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666089"
---
# <a name="create-a-snapshot-for-a-merge-publication-with-parameterized-filters"></a>使用參數化篩選建立合併式發行集的快照集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中使用參數化篩選建立合併式發行集的快照集。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要使用參數化篩選建立合併式發行集的快照集，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   在使用參數化篩選產生合併式發行集的快照集時，您必須先產生一個標準 (結構描述) 快照集，其中包含所有發行的資料以及訂閱的訂閱者中繼資料。 如需詳細資訊，請參閱 [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。 在您建立結構描述快照集之後，您可以產生包含發行資料之訂閱者特有資料分割的快照集。  
  
-   如果發行集內的一或多個發行項的篩選產生對每個訂閱而言是唯一的非重疊資料分割，則只要合併代理程式一執行，就會清除中繼資料。 這表示分割快照集會更快過期。 使用這個選項時，您應該考慮允許訂閱者初始化快照集的產生與傳遞。 如需篩選選項的詳細資訊，請參閱[含參數化篩選之合併式發行集的快照集](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)的＜設定資料分割選項＞一節。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以在 [發行集屬性 - \<發行集>] 對話方塊的 [資料分割] 頁面上，產生資料分割的快照集。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。 您可以讓訂閱者初始化快照集產生和傳遞，並且/或者產生快照集。  
  
 產生一個或多個資料分割的快照集之前，必須：  
  
1.  使用「新增發行集精靈」建立合併發行集，並在精靈的 **[加入篩選]** 頁面上，指定一個或多個參數化資料列篩選器。 如需詳細資訊，請參閱 [針對合併發行項定義及修改參數化資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
2.  產生發行集的結構描述快照集。 依預設，當您完成「新增發行集精靈」時，便會產生結構描述快照集；您也可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]產生結構描述快照集。  
  
#### <a name="to-generate-a-schema-snapshot"></a>若要產生結構描述快照集  
  
1.  連接到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要為其建立快照集的發行集，然後按一下 **[檢視快照集代理程式的狀態]**。  
  
4.  在 [檢視快照集代理程式的狀態 - \<發行集>] 對話方塊中，按一下 [啟動]。  
  
     快照集代理程式產生完快照集後，就會顯示一個訊息，例如「[100%] 已產生 17 個發行項的快照集」。  
  
#### <a name="to-allow-subscribers-to-initiate-snapshot-generation-and-delivery"></a>若要允許訂閱者初始化快照集的產生與傳遞  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [資料分割] 頁面上，選取 [新的訂閱者嘗試進行同步處理時，自動定義資料分割並依需要產生快照]。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-generate-and-refresh-snapshots"></a>若要產生和重新整理快照集  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [資料分割] 頁面上，按一下 [新增]。  
  
2.  輸入與您要建立快照集的資料分割關聯之 **HOST_NAME()** 和 (或) **SUSER_SNAME()** 的值。  
  
3.  選擇性地指定重新整理快照集的排程：  
  
    1.  選取 **[排程這個資料分割的快照集代理程式在下列時間執行]**  
  
    2.  接受重新重理快照集的預設排程，或按一下 **[變更]** 以指定其他排程。  
  
4.  按一下 [確定] 回到 [發行集屬性 - \<發行集>] 對話方塊。  
  
5.  在屬性方格中選取資料分割，然後按一下 **[立即產生選取的快照集]**。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用預存程序和快照集代理程式進行以下作業：  
  
-   允許訂閱者在首次執行同步處理時，要求快照集產生和應用程式。  
  
-   為每個資料分割預先產生快照集。  
  
-   以手動方式為每一個訂閱者產生快照集。  
  
    > [!IMPORTANT]  
    >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
#### <a name="to-create-a-publication-that-allows-subscribers-to-initiate-snapshot-generation-and-delivery"></a>建立可讓訂閱者初始化快照集產生和傳遞的發行集  
  
1.  在發行集資料庫的發行者端，執行 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定下列參數：  
  
    -   將 **@publication**。  
  
    -   將 **@allow_subscriber_initiated_snapshot** @allow_subscriber_initiated_snapshot **@allow_subscriber_initiated_snapshot**的值，這樣可讓訂閱者起始快照集處理。  
  
    -   (選擇性) 將 **@max_concurrent_dynamic_snapshots**。 如果正在執行最大的處理序數目，而且訂閱者嘗試產生快照集，則會將此處理序置於佇列中。 根據預設，並行處理序的數目沒有任何限制。  
  
2.  在發行者端，執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 針對 **@publication** 指定步驟 1 中所用的發行集名稱，並針對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] @job_login [@password](../../relational-databases/replication/agents/replication-snapshot-agent.md) 和 **@job_login** 指定執行 **@password**。 如果代理程式會在與「發行者」時連接時使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」，則也必須指定 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 指定步驟 1 中所用的發行集名稱，並針對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@publisher_login** 指定執行 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
3.  若要將發行項新增至發行集中，請執行 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 必須針對發行集中的每一個發行項執行一次此預存程序。 在使用參數化篩選時，您必須使用 **@subset_filterclause** 參數來指定一個或多個發行項的參數化資料列篩選器。 如需詳細資訊，請參閱 [針對合併發行項定義及修改參數化資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果將根據參數化資料列篩選器來篩選其他發行項，請執行 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 來定義兩個發行項之間的聯結或邏輯記錄關聯性。 必須針對每一個定義的關聯性執行一次此預存程序。 如需詳細資訊，請參閱 [定義和修改合併發行項之間的聯結篩選](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  當合併代理程式要求此快照集初始化訂閱者時，會自動產生要求之訂閱資料分割的快照集。  
  
#### <a name="to-create-a-publication-and-pre-generate-or-automatically-refresh-snapshots"></a>建立發行集及預先產生或自動重新整理快照集  
  
1.  若要建立發行集，請執行 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  在發行者端，執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 針對 **@publication** 指定步驟 1 中所使用的發行集名稱，以及針對 **@job_login** 指定執行 **@password**。 如果代理程式會在與「發行者」時連接時使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」，則也必須指定 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 指定步驟 1 中所用的發行集名稱，並針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@publisher_login** 指定執行 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
3.  若要將發行項新增至發行集中，請執行 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 必須針對發行集中的每一個發行項執行一次此預存程序。 在使用參數化篩選時，您必須使用 **@subset_filterclause** 參數來指定一個或多個發行項的參數化資料列篩選器。 如需詳細資訊，請參閱 [針對合併發行項定義及修改參數化資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果將根據參數化資料列篩選器來篩選其他發行項，請執行 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 來定義兩個發行項之間的聯結或邏輯記錄關聯性。 必須針對每一個定義的關聯性執行一次此預存程序。 如需詳細資訊，請參閱 [定義和修改合併發行項之間的聯結篩選](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  在發行集資料庫的發行者端，執行 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)，並指定步驟 1 中的 **@publication** 值。 請注意結果集中 **snapshot_jobid** 的值。  
  
6.  將步驟 5 取得之 **snapshot_jobid** 的值轉換成 **uniqueidentifier**。  
  
7.  在 **msdb** 資料庫的發行者端，執行 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)，並針對 **@job_id** 指定步驟 6 中所取得的轉換值。  
  
8.  在發行集資料庫的發行者端，執行 [sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)。 針對 **@publication** 指定步驟 1 中的發行集名稱，並針對 **@suser_sname** (如果 [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) 用於篩選子句) 或是針對 **@host_name** (如果 [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) 用於篩選子句) 指定用於定義資料分割的值。  
  
9. 在發行集資料庫的發行者端，執行 [sp_adddynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)。 針對 **@publication**指定步驟 1 中的發行集名稱、步驟 8 中的 **@suser_sname** 或 **@host_name** 的值，以及此作業的排程。 這樣會建立針對指定的資料分割產生參數化快照集的作業。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
    > [!NOTE]  
    >  這個作業會使用與步驟 2 中定義的初始快照集作業相同的 Windows 帳戶來執行。 若要移除參數化快照集作業及其相關的資料分割，請執行 [sp_dropdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)。  
  
10. 在發行集資料庫的發行者端，執行 [sp_helpmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)，並指定步驟 1 中的 **@publication** 值，以及步驟 8 中的 **@suser_sname** 或 **@host_name** 值。 請注意結果集中 **dynamic_snapshot_jobid** 的值。  
  
11. 在 **msdb** 資料庫的散發者端，執行 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)，並針對 **@job_id** 指定步驟 9 中所取得的值。 這樣會啟動資料分割的參數化快照集作業。  
  
12. 針對每一個訂閱重複步驟 8-11 來產生分割快照集。  
  
#### <a name="to-create-a-publication-and-manually-create-snapshots-for-each-partition"></a>針對每一個資料分割建立發行集及手動建立快照集  
  
1.  若要建立發行集，請執行 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  在發行者端，執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 針對 **@publication** 指定步驟 1 中所使用的發行集名稱，以及針對 **@job_login** 指定執行 **@password**。 如果代理程式會在與「發行者」時連接時使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」，則也必須指定 **@publisher_security_mode** @allow_subscriber_initiated_snapshot **@publisher_security_mode** 指定步驟 1 中所用的發行集名稱，並針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@publisher_login** 指定執行 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
3.  若要將發行項新增至發行集中，請執行 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 必須針對發行集中的每一個發行項執行一次此預存程序。 在使用參數化篩選時，您必須使用 **@subset_filterclause** 參數來指定一個或多個發行項的參數化資料列篩選器。 如需詳細資訊，請參閱 [針對合併發行項定義及修改參數化資料列篩選](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)。  
  
4.  如果將根據參數化資料列篩選器來篩選其他發行項，請執行 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 來定義兩個發行項之間的聯結或邏輯記錄關聯性。 必須針對每一個定義的關聯性執行一次此預存程序。 如需詳細資訊，請參閱 [定義和修改合併發行項之間的聯結篩選](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
5.  從命令提示字元啟動快照集作業或是執行複寫快照集代理程式，以產生標準快照集結構描述和其他檔案。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
6.  再次從命令提示字元執行複寫快照集代理程式，以產生大量複製 (.bcp) 檔案，為 **-DynamicSnapshotLocation** 指定分割快照集的位置，以及指定可定義此資料分割的下列其中一個或兩個屬性：  
  
    -   **-DynamicFilterHostName** - 使用 [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) 時的值。  
  
    -   **-DynamicFilterLogin** - 使用 [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) 時的值。  
  
7.  針對每一個訂閱重複步驟 6 來產生分割快照集。  
  
8.  針對每一個訂閱執行合併代理程式，以便在訂閱者上套用初始分割快照集，並指定下列屬性：  
  
    -   **-Hostname** - 如果正在覆寫 HOST_NAME 的實際值，則表示用於定義資料分割的值。  
  
    -   **-DynamicSnapshotLocation** - 此資料分割的動態快照集位置。  
  
> [!NOTE]  
>  如需複寫代理程式之程式設計的詳細資訊，請參閱[複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會使用參數化篩選來建立合併式發行集，其中的訂閱者會起始快照集的產生程序。 **@job_login** 和 **@job_password** 的值會使用指令碼變數來傳遞。  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_1.sql)]  
  
 這個範例會使用參數化篩選建立發行集，其中的每一個訂閱者會藉由執行 [sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) 來定義其資料分割，並藉由執行 [sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) 來建立篩選的快照集作業，傳遞資料分割資訊。 **@job_login** 和 **@job_password** 的值會使用指令碼變數來傳遞。  
  
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
>  當篩選發行項產生了對每個訂閱而言是唯一的非重疊資料分割時 (在建立合併發行項時，針對 P:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption 指定 F:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription 的值)，則只要合併代理程式一執行，就會清除中繼資料。 這表示分割快照集會更快過期。 當使用這個選項時，您應該考慮允許訂閱者要求產生快照集。 如需詳細資訊，請參閱＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞主題中的「使用適當的篩選選項」一節。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
#### <a name="to-create-a-publication-that-allows-subscribers-to-initiate-snapshot-generation-and-delivery"></a>建立可讓訂閱者初始化快照集產生和傳遞的發行集  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  為發行集資料庫建立 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別的執行個體、將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為步驟 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 執行個體，並呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 If <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 傳回 **false**，請確認此資料庫確實存在。  
  
3.  If <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 屬性為 **false**，請將它設定為 **@allow_subscriber_initiated_snapshot** 然後呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>。  
  
4.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體，並為此物件設定下列屬性：  
  
    -   將 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 設定為步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>設為發行的資料庫名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>設定為發行集名稱。  
  
    -   將 <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>設定為動態快照集作業的最大數目。 由於訂閱者起始的快照集要求可在任何時間發生，所以當多個訂閱者同時要求其分割快照集時，這個屬性會限制可以同時執行的快照集代理程式作業數目。 當正在執行最大的作業數目時，其他分割快照集要求會排入佇列中，直到其中一個執行中的作業完成為止。  
  
    -   使用位元邏輯 OR (Visual C# 中為**|** 且 Visual Basic 中為 **Or** ) 運算子，將 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> 值加入 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 欄位，可提供執行快照集代理程式作業所使用之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的認證。  
  
        > [!NOTE]  
        >  當發行集是由 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 固定伺服器角色的成員所建立時，建議您設定 **P:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity** 。 如需詳細資訊，請參閱 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法來建立發行集。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有屬性的值 (包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連線，然後再呼叫 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
6.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 屬性將發行項加入發行集中。 至少針對定義參數化篩選的一個發行項指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 屬性。 (選擇性) 建立可在發行項之間定義聯結篩選的 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 物件。 如需詳細資訊，請參閱 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
7.  如果 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 的值是 **false**，請呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 來針對這個發行集建立初始快照集代理程式作業。  
  
8.  呼叫步驟 4 中建立之 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 物件的 <xref:Microsoft.SqlServer.Replication.MergePublication> 方法。 這樣會啟動可產生初始快照集的代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
9. (選擇性) 檢查是否有為 **@allow_subscriber_initiated_snapshot** 屬性設定 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 的值，以判斷初始快照集何時可準備好供人使用。  
  
10. 當訂閱者的合併代理程式第一次連接時，會自動產生分割快照集。  
  
#### <a name="to-create-a-publication-and-pregenerate-or-automatically-refresh-snapshots"></a>建立發行集及預先產生或自動重新整理快照集  
  
1.  使用 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體來定義合併式發行集。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 屬性將發行項加入發行集中。 至少針對定義參數化篩選的一個發行項指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 屬性，並建立可在兩個發行項之間定義聯結篩選的任何 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 物件。 如需詳細資訊，請參閱 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  如果 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 的值是 **false**，請呼叫 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 來針對這個發行集建立快照集代理程式作業。  
  
4.  呼叫步驟 1 中建立之 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 物件的 <xref:Microsoft.SqlServer.Replication.MergePublication> 方法。 這個方法會啟動可產生初始快照集的代理程式作業。 如需有關產生初始快照集以及為快照集代理程式定義自訂排程的詳細資訊，請參閱＜ [建立和套用初始快照集](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)＞。  
  
5.  檢查是否有為 **@allow_subscriber_initiated_snapshot** 屬性設定 <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 的值，以判斷初始快照集何時可準備好供人使用。  
  
6.  建立 <xref:Microsoft.SqlServer.Replication.MergePartition> 類別的執行個體，並使用以下其中一個或兩個屬性來為訂閱者設定參數化篩選準則：  
  
    -   如果訂閱者的資料分割是由 [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) 的結果所定義，請使用 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>。  
  
    -   如果訂閱者的資料分割是由 [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) 的結果或這個函式的多載所定義，請使用 <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>。  
  
7.  建立 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 類別的執行個體，並設定與步驟 6 中相同的屬性。  
  
8.  使用 <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> 類別來定義排程，以針對訂閱者資料分割產生篩選的快照集。  
  
9. 使用步驟 1 中的 <xref:Microsoft.SqlServer.Replication.MergePublication> 執行個體，呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>。 傳遞步驟 6 的 <xref:Microsoft.SqlServer.Replication.MergePartition> 物件。  
  
10. 使用步驟 1 中的 <xref:Microsoft.SqlServer.Replication.MergePublication> 執行個體，呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> 方法。 傳遞步驟 7 中的 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 物件及步驟 8 中的 <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> 物件。  
  
11. 呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>並在 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> 物件中找出傳回的陣列中新加入的分割快照集作業。  
  
12. 取得此作業的 <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> 屬性。  
  
13. 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與散發者的連接。  
  
14. 建立 SQL Server 管理物件 (SMO) <xref:Microsoft.SqlServer.Management.Smo.Server> 類別的執行個體，傳遞步驟 13 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
15. 建立 <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> 類別的執行個體，傳遞步驟 14 中 <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> 的 <xref:Microsoft.SqlServer.Management.Smo.Server> 屬性及步驟 12 中的作業名稱。  
  
16. 呼叫 <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> 方法來啟動分割快照集作業。  
  
17. 對每一個訂閱者重複步驟 6-16。  
  
#### <a name="to-create-a-publication-and-manually-create-snapshots-for-each-partition"></a>針對每一個資料分割建立發行集及手動建立快照集  
  
1.  使用 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體來定義合併式發行集。 如需詳細資訊，請參閱 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
2.  使用 <xref:Microsoft.SqlServer.Replication.MergeArticle> 屬性將發行項加入發行集中。至少針對定義參數化篩選的一個發行項指定 <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> 屬性，並建立可在兩個發行項之間定義聯結篩選的任何 <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> 物件。 如需詳細資訊，請參閱 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
3.  產生初始快照集。 如需詳細資訊，請參閱 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
4.  建立 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 類別的執行個體，並設定下列必要的屬性：  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 發行者的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 發行集資料庫的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 發行集的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 散發者的名稱  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 代表使用「Windows 整合式驗證」的 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 值，或使用「SQL Server 驗證」的 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 值。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 代表使用「Windows 整合式驗證」的 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 值，或使用「SQL Server 驗證」的 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 值。  
  
5.  為 <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> 設定 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>的值。  
  
6.  設定以下其中一個或多個屬性來定義資料分割參數：  
  
    -   如果訂閱者的資料分割是由 [SUSER_SNAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md) 的結果所定義，請使用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A>。  
  
    -   如果訂閱者的資料分割是由 [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md) 的結果或這個函式的多載所定義，請使用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A>。  
  
7.  呼叫 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 方法。  
  
8.  對每一個訂閱者重複步驟 4-7。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 此範例會建立允許訂閱者要求產生快照集的合併式發行集。  
  
 [!code-cs[HowTo#rmo_CreateMergePub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 這個範例會使用參數化資料列篩選器，針對合併式發行集手動建立訂閱者資料分割及篩選的快照集。  
  
 [!code-cs[HowTo#rmo_CreateMergePartition](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 這個範例會使用參數化資料列篩選器，針對合併式發行集的訂閱者啟動快照集代理程式來產生篩選的資料快照集。  
  
 [!code-cs[HowTo#rmo_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## <a name="see-also"></a>另請參閱  
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [含參數化篩選之合併式發行集的快照集](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)   
 [複寫安全性最佳作法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
