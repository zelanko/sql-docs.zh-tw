---
title: 分散式可用性群組 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/12/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], distributed
ms.assetid: ''
caps.latest.revision: ''
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c035428e526b64dd4b0245719b139f6567108b6
ms.sourcegitcommit: d3432a37b23b61c37092daf7519b30fc42fc0538
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/20/2018
ms.locfileid: "36270949"
---
# <a name="distributed-availability-groups"></a>分散式可用性群組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
分散式可用性群組是 SQL Server 2016 中引進的新功能，為現有 AlwaysOn 可用性群組功能的變異。 本文釐清分散式可用性群組的某些層面，並補充現有 [SQL Server 文件](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation)。

> [!NOTE]
> "DAG" 不是「分散式可用性群組」的官方縮寫，因為這個縮寫已用於「Exchange 資料庫可用性群組」功能。 此 Exchange 功能與 SQL Server 可用性群組或分散式可用性群組無關。

若要設定分散式可用性群組，請參閱[設定分散式可用性群組](configure-distributed-availability-groups.md)。

## <a name="understand-distributed-availability-groups"></a>了解分散式可用性群組

分散式可用性群組是跨兩個不同可用性群組之特殊類型的可用性群組。 基礎可用性群組設定於兩個不同的 Windows Server 容錯移轉叢集 (WSFC) 叢集上。 參與分散式可用性群組的可用性群組不需要位於相同的位置中。 在公用雲端或支援可用性群組部署的任何位置中，它們可以是實體、虛擬、內部部署。 只要兩個可用性群組可以通訊，您就可以設定包含它們的分散式可用性群組。

傳統可用性群組具有 WSFC 叢集中所設定的資源。 分散式可用性群組不會在 WSFC 叢集中設定任何項目。 在 SQL Server 內維護它的所有相關項目。 若要了解如何檢視分散式可用性群組的資訊，請參閱[檢視分散式可用性群組資訊](#viewing-distributed-availability-group-information)。 

分散式可用性群組需要基礎可用性群組具有接聽程式。 當您建立分散式可用性群組時，可以使用 ENDPOINT_URL 參數指定它的已設定接聽程式，而不是像使用傳統可用性群組一樣地提供獨立執行個體的基礎伺服器名稱 (或者，如果是 SQL Server 容錯移轉叢集執行個體 [FCI]，則是與網路名稱資源建立關聯的值)。 雖然分散式可用性群組的每個基礎可用性群組都具有接聽程式，但是分散式可用性群組沒有接聽程式。

下圖顯示跨兩個可用性群組 (AG 1 和 AG 2) 之分散式可用性群組的高階檢視，而這兩個可用性群組都設定於其專屬 WSFC 叢集上。 分散式可用性群組共有四個複本，而每個可用性群組各有兩個複本。 每個可用性群組皆可支援最大複本數，因此分散式可用性最多可以有總共 18 個複本。

<a name="fig1"></a>
![分散式可用性群組的高階檢視][1]

您可以將分散式可用性群組中的資料移動設定為同步或非同步。 不過，相較於傳統可用性群組，資料移動在分散式可用性群組內略有不同。 雖然每個可用性群組都有主要複本，但是參與可接受插入、更新和刪除之分散式可用性群組的資料庫只能有一個複本。 如下圖所示，AG 1 是主要可用性群組。 其主要複本會將交易傳送至次要複本 AG 1 和主要複本 AG 2。 AG 2 的主要複本也稱為「轉寄站」。 轉寄站是分散式可用性群組的次要可用性群組中的主要複本。 轉寄站會接收來自主要可用性群組中主要複本的交易，並將它們轉寄至其專屬可用性群組中的次要複本。  轉寄站接著會持續更新 AG 2 的次要複本。 

![分散式可用性群組和其資料移動][2]

將 AG 2 的主要複本設為接受插入、更新和刪除的唯一方式，是從 AG 1 手動容錯移轉分散式可用性群組。 在上圖中，因為 AG 1 包含資料庫的可寫入複本，所以發出容錯移轉時會將 AG 2 設為可處理插入、更新和刪除的可用性群組。 如需如何將某個分散式可用性群組容錯移轉至另一個可用性群組的資訊，請參閱[容錯移轉至次要可用性群組]( https://docs.microsoft.com/sql/database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups)。

> [!NOTE]
> SQL Server 2016 中的分散式可用性群組只支援使用 FORCE_FAILOVER_ALLOW_DATA_LOSS 選項從某個可用性群組容錯移轉至另一個可用性群組。

> [!NOTE]
> 搭配使用異動複寫與分散式可用性群組時，無法將轉寄站複本設定為發行者。

## <a name="sql-server-version-and-edition-requirements-for-distributed-availability-groups"></a>分散式可用性群組的 SQL Server 版本需求

分散式可用性群組目前只能與使用相同主要 SQL Server 版本所建立的可用性群組搭配運作。 例如，目前必須使用 SQL Server 2016 建立所有參與分散式可用性群組的可用性群組。 因為 SQL Server 2012 或 2014 中沒有分散式可用性群組功能，所以使用這些版本所建立的可用性群組不能參與分散式可用性群組。 

> [!NOTE]
> 無法使用 Standard 版本或混用 Standard 與 Enterprise 版本來設定分散式可用性群組。

因為有兩個不同的可用性群組，所以在參與分散式可用性群組的複本上安裝 Service Pack 或累積更新的程序會與傳統可用性群組的程序略有不同：

1. 請從更新分散式可用性群組中第二個可用性群組的複本開始。

2. 修補分散式可用性群組中主要可用性群組的複本。

3. 與標準可用性群組相同，將主要可用性群組容錯移轉至它自己的其中一個複本 (而不是容錯移轉至第二個可用性群組的主要複本)，並進行修補。 如果沒有主要複本以外的複本，則需要手動容錯移轉至第二個可用性群組。

> [!NOTE]
> 未宣告有關未來的 SQL Server 版本是否允許舊版本參與相同的分散式可用性群組。 如果已啟用該案例，將允許分散式可用性群組成為 SQL Server 版本升級計畫的一部分。

### <a name="windows-server-versions-and-distributed-availability-groups"></a>Windows Server 版本和分散式可用性群組

分散式可用性群組跨多個可用性群組，且各在其專屬基礎 WSFC 叢集上，而且分散式可用性群組是僅限 SQL Server 建構。  這表示裝載個別可用性群組的 WSFC 叢集可以有不同的 Windows Server 主要版本。 SQL Server 的主要版本必須相同，如上節所討論。 與[初始圖](#fig1)類似，下圖顯示參與分散式可用性群組的 AG 1 和 AG 2，但每個 WSFC 叢集都是不同版本的 Windows Server。


![具有不同 Windows Server 版本之 WSFC 叢集的分散式可用性群組][3]

個別 WSFC 叢集和其對應可用性群組都遵循傳統規則。 也就是說，它們可以加入網域或不加入網域 (Windows Server 2016 或更新版本)。 在單一分散式可用性群組中合併兩個不同的可用性群組時，有四個案例：

* 這兩個 WSFC 叢集都已加入相同的網域。
* 每個 WSFC 叢集都會加入不同的網域。
* 一個 WSFC 叢集會加入網域，而一個 WSFC 叢集未加入網域。
* 兩個 WSFC 叢集都未加入網域。

如果將這兩個 WSFC 叢集加入相同的網域 (非叢集網路)，則在您建立分散式可用性群組時不需要執行特殊作業。 針對未加入相同網域的可用性群組和 WSFC 叢集，使用憑證讓分散式可用性群組運作，這種方式與建立可用性群組作為網域獨立的可用性群組的方式極為相同。 若要查看如何設定分散式可用性群組的憑證，請遵循[建立網域獨立的可用性群組](domain-independent-availability-groups.md#create-a-domain-independent-availability-group)下的步驟 3-13。

使用分散式可用性群組時，每個基礎可用性群組中的主要複本都必須要有對方的憑證。 如果您已經有未使用憑證的端點，請使用 [ALTER ENDPOINT](https://docs.microsoft.com/sql/t-sql/statements/alter-endpoint-transact-sql) 重新設定這些端點，以反映憑證的使用。

## <a name="distributed-availability-group-usage-scenarios"></a>分散式可用性群組使用案例

以下是分散式可用性群組的三個主要使用案例： 

* [災害復原和更輕鬆的多網站組態](#disaster-recovery-and-multi-site-scenarios)
* [移轉至新硬體或組態，可能包括使用新硬體或變更基礎作業系統](#migration-using-a-distributed-availability-group)
* [跨多個可用性群組以在單一可用性群組中增加八個以上的可讀取複本數目](#scaling-out-readable-replicas-with-distributed-accessibility-groups)

### <a name="disaster-recovery-and-multi-site-scenarios"></a>災害復原和多網站案例

傳統可用性群組需要所有伺服器都屬於相同的 WSFC 叢集，這樣可讓跨多個資料中心更具挑戰。 下圖顯示傳統多網站可用性群組架構的樣子，包含資料流程。 有一個主要複本會將交易傳送至所有次要複本。 此組態在某些方向較分散式可用性群組不具彈性。 例如，您必須在 WSFC 叢集中實作 Active Directory (如果適用) 和仲裁見證這類事物。 您也可能需要考量 WSFC 叢集的其他方面，例如改變節點投票。

![傳統多網站可用性群組][4]

分散式可用性群組針對跨多個資料中心的可用性群組，提供更具彈性的部署案例。 您甚至可以使用過去使用[記錄傳送]( https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server)這類功能的分散式可用性群組。 不過，與傳統可用性群組不同，分散式可用性群組不能延遲套用交易。 這表示可用性群組或分散式可用性群組對於錯誤地更新或刪除資料的人為錯誤沒有任何幫助。

分散式可用性群組是鬆散偶合的，在此情況下，表示它們不需要單一 WSFC 叢集，而且它們是由 SQL Server 進行維護。 因為 WSFC 叢集是個別進行維護，而且兩個可用性群組之間的同步處理主要不同步，所以可以更輕鬆地在另一個網站上設定災害復原。 每個可用性群組中的主要複本都會同步處理其專屬次要複本。

* 只有分散式可用性群組支援手動容錯移轉。 在切換資料中心的災害復原狀況中，您不應該設定自動容錯移轉 (極少數的例外狀況)。 
* 您很可能不需要為多網站或子網路 WSFC 叢集設定一些傳統項目或參數 (例如 CrossSubnetThreshold)，但仍然需要了解資料傳輸之不同層的網路延遲。 差異在於每個 WSFC 叢集都會維持其本身的可用性；叢集不是四個節點的一個巨型實體。 如上圖所示，您有兩個不同的兩節點 WSFC 叢集。  
* 建議非同步資料移動，因為這個方法是用於災害復原。
* 如果您在主要複本與第二個可用性群組之至少一個次要複本間設定同步資料移動，並且在分散式可用性群組上設定同步移動，則分散式可用性群組會等待，直到所有同步複本都認可它們具有資料。

### <a name="migrate-by-using-a-distributed-availability-group"></a>使用分散式可用性群組移轉

因為分散式可用性群組支援兩個完全不同的可用性群組組態，所以它們不僅可啟用較輕鬆的災害復原和多網站案例，也可以啟用移轉案例。 不論移轉至新硬體還是虛擬機器 (公用雲端中的內部部署或 IaaS)，設定分散式可用性群組都允許進行移轉，而在過去，您可能會使用備份、複製和還原，或記錄傳送。 

在您要變更或升級基礎 OS 但同時保留相同 SQL Server 版本的情況下，移轉能力特別有用。 雖然 Windows Server 2016 確實允許在相同的硬體上從 Windows Server 2012 R2 進行輪流升級，但是大部分使用者都會選擇部署新的硬體或虛擬機器。 

若要完成移轉至新的組態，請在程序結束時停止原始可用性群組的所有資料流量，並將分散式可用性群組變更為同步資料移動。 此動作確保完全同步處理第二個可用性群組的主要複本，因此不會遺失任何資料。 確認同步處理之後，請將分散式可用性群組容錯移轉至次要可用性群組。 如需詳細資訊，請參閱[容錯移轉至次要可用性群組](configure-distributed-availability-groups.md#failover)。

移轉後，其中，第二個可用性群組現在是新的主要可用性群組，您可能需要執行下列任一項：

* 重新命名次要可用性群組上的接聽程式 (而且可能會刪除或重新命名原始主要可用性群組上的舊接聽程式)，或使用原始主要可用性群組中的接聽程式來重新建立它，讓應用程式和使用者可以存取新的組態。
* 如果無法重新命名或重新建立，請將應用程式和使用者指向第二個可用性群組上的接聽程式。

### <a name="scale-out-readable-replicas-with-distributed-availability-groups"></a>使用分散式可用性群組相應放大可讀取複本

單一分散式可用性群組視需要最多可以有 16 個次要複本。 因此，它最多可以有 18 個複本可供讀取，包括不同可用性群組的兩個主要複本。 這個方法表示多個網站可以有各種應用程式報告的接近即時存取權。

分散式可用性群組協助您相應放大唯讀伺服器陣列的程度，高於只使用單一可用性群組。 分散式可用性群組可以使用兩種方式相應放大可讀取複本：

* 您可以在分散式可用性群組中使用第二個可用性群組的主要複本來建立另一個分散式可用性群組，即使資料庫未處於復原狀態也是一樣。
* 您也可以使用第一個可用性群組的主要複本來建立另一個分散式可用性群組。

也就是說，主要複本可以參與兩個不同的分散式可用性群組。 下圖顯示 AG 1 和 AG 2 參與分散式 AG 1，而 AG 2 和 AG 3 參與分散式 AG 2。 AG 2 的主要複本 (或轉寄站) 是分散式 AG 1 的次要複本，也是分散式 AG 2 的主要複本。

![使用分散式可用性群組相應放大讀取][5]

下圖顯示 AG 1 作為兩個不同分散式可用性群組的主要複本：分散式 AG 1 (包含 AG 1 和 AG2) 和分散式 AG 2 (包含 AG 1 和 AG 3)。


![使用分散式可用性群組相應放大讀取的另一個範例][6]


在這兩個上述範例中，這三個可用性群組最多可能共會有 27 個複本，而且全部都可以用於唯讀查詢。 

[唯讀路由]( https://docs.microsoft.com/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server)無法完全與分散式可用性群組搭配運作。 具體來說：

1. 唯讀路由可加以設定，並用於分散式可用性群組的主要可用性群組。 
2. 唯讀路由可加以設定，但無法用於分散式可用性群組的次要可用性群組。 查詢若使用接聽程式連線到次要可用性群組，則會全部移至次要可用性群組的主要複本。 否則，您必須設定每個複本都允許次要複本的所有連接，並直接存取它們。 不過，如果次要可用性群組在容錯移轉之後成為主要，則可以使用唯讀路由。 在 SQL Server 2016 更新或 SQL Server 的未來版本中，可能會變更此行為。


## <a name="initialize-secondary-availability-groups-in-a-distributed-availability-group"></a>初始化分散式可用性群組中的次要可用性群組

分散式可用性群組過去是使用[自動植入]( https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group)所設計，而自動植入是用來初始化第二個可用性群組上主要複本的主要方法。 如果您執行下列作業，才能對第二個可用性群組的主要複本進行完整資料庫還原：

1. 使用 WITH NORECOVERY 還原資料庫備份。
2. 若有必要，請使用 WITH NORECOVERY 還原正確的交易記錄備份。
3. 在未指定資料庫名稱並將 SEEDING_MODE 設定為 AUTOMATIC 的情況下，建立第二個可用性群組。
4. 使用自動植入來建立分散式可用性群組。

當您將第二個可用性群組的主要複本新增至分散式可用性群組時，會對第一個可用性群組的主要資料庫檢查該複本，而且植入會將資料庫快取到來源。 有一些警示：

* 第二個可用性群組之主要複本上的 `sys.dm_hadr_automatic_seeding` 中所顯示的輸出，會將 `current_state` 顯示為 FAILED，且原因為「植入檢查訊息逾時」。

* 第二個可用性群組之主要複本上的目前 SQL Server 記錄會顯示植入已運作，並且已同步處理 [LSN]( https://docs.microsoft.com/sql/relational-databases/sql-server-transaction-log-architecture-and-management-guide)。

* 第一個可用性群組之主要複本上的 `sys.dm_hadr_automatic_seeding` 中所顯示的輸出，會將 current_state 顯示為 COMPLETED。 

* 分散式可用性群組的植入也會有不同的行為。 若要在第二個複本上開始植入，您必須在複本上發出 `ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE` 命令。 雖然這個條件仍然適用於參與基礎可用性群組的任何次要複本，但是第二個可用性群組的主要複本在將新增至分散式可用性群組之後已有允許開始植入的正確權限。 

### <a name="view-distributed-availability-group-information"></a>檢視分散式可用性群組資訊 
    
如前所述，分散式可用性群組是僅限 SQL Server 建構，而且在基礎 WSFC 叢集中看不到它。 下圖顯示兩個不同的 WSFC 叢集 (CLUSTER_A 和 CLUSTER_B)，且各有其專屬可用性群組。 這裡只討論 CLUSTER_A 中的 AG1 以及 CLUSTER_B 中的 AG2。 

<!-- ![Two WSFC clusters with multiple availability groups through PowerShell Get-ClusterGroup command][7]  -->
<a name="fig7"></a>

```
PS C:\> Get-ClusterGroup -Cluster CLUSTER_A

Name                            OwnerNode             State
----                            ---------             -----
AG1                             DENNIS                Online
Available Storage               GLEN                  Offline
Cluster Group                   JY                    Online
New_RoR                         DENNIS                Online
Old_RoR                         DENNIS                Online
SeedingAG                       DENNIS                Online


PS C:\> Get-ClusterGroup -Cluster CLUSTER_B

Name                            OwnerNode             State
----                            ---------             -----
AG2                             TOMMY                 Online
Available Storage               JC                    Offline
Cluster Group                   JC                    Online
```

分散式可用性群組的所有詳細資訊皆位在 SQL Server 檢視中，特別是在可用性群組動態管理檢視中。 目前，SQL Server Management Studio 中顯示的唯一分散式可用性群組資訊，是可用性群組的主要複本相關資訊。 如下圖所示，在 [可用性群組] 資料夾底下，SQL Server Management Studio 顯示有分散式的可用性群組。 此圖顯示 AG1 是本機執行個體之個別可用性群組的主要複本，不是分散式可用性群組的主要複本。

![在 SQL Server Management Studio 中檢視分散式可用性群組的第一個 WSFC 叢集的主要複本][8]


不過，如果您以滑鼠右鍵按一下分散式的可用性群組，沒有選項可用 (請參閱下圖)，展開 [可用性資料庫]，[可用性群組接聽程式]，以及 [可用性複本] 資料夾也都是空的。 SQL Server Management Studio 16 會顯示此結果，但未來的 SQL Server Management Studio 版本可能會變更。

![動作沒有可用的選項][9]

如下圖所示，次要複本在 SQL Server Management Studio 中不顯示與分散式可用性群組相關的任何資訊。 這些可用性群組名稱對應至上一個 [CLUSTER_A WSFC 叢集](#fig7)映像中所示的角色。

![在 SQL Server Management Studio 中檢視次要複本][10]

使用動態管理檢視時，適用相同的概念。 使用下列查詢，您可以看到所有可用性群組 (一般和分散式) 和加入它們的節點。 只有當您在其中一個加入分散式可用性群組的 WSFC 叢集中查詢主要複本時，才會顯示此結果。 在動態管理檢視 `sys.availability_groups` 中有個名為 `is_distributed` 的新資料行，當可用性群組是分散式可用性群組時，它會是 1。 查看此資料行：

```sql
SELECT ag.[name] as 'AG Name', 
    ag.Is_Distributed, 
    ar.replica_server_name as 'Replica Name'
FROM    sys.availability_groups ag, 
    sys.availability_replicas ar       
WHERE   ag.group_id = ar.group_id
```

下圖顯示加入分散式可用性群組之第二個 WSFC 叢集的輸出範例。 SPAG1 是由兩個複本組成：DENNIS 和 JY。 不過，名為 SPDistAG 的分散式可用性群組，和傳統的可用性群組一樣，有兩個加入的可用性群組名稱 (SPAG1 和 SPAG2)，而不是執行個體的名稱。 

![前項查詢的範例輸出][11]

在 SQL Server Management Studio 中，儀表板和其他區域顯示的任何狀態都只供該可用性群組內本機同步處理之用。 若要顯示分散式可用性群組的健康狀態，請查詢動態管理檢視。 下列範例查詢會延伸並縮小上一個查詢：

```sql
SELECT ag.[name] as 'AG Name', ag.is_distributed, ar.replica_server_name as 'Underlying AG', ars.role_desc as 'Role', ars.synchronization_health_desc as 'Sync Status'
FROM    sys.availability_groups ag, 
sys.availability_replicas ar,       
sys.dm_hadr_availability_replica_states ars       
WHERE   ar.replica_id = ars.replica_id
and     ag.group_id = ar.group_id 
and ag.is_distributed = 1
```
       
       
![分散式可用性群組狀態][12]


若要進一步延伸前一個查詢，您也可新增 `sys.dm_hadr_database_replicas_states`，透過動態管理檢視查看基礎效能。 動態管理檢視目前只儲存有關第二個可用性群組的資訊。 下列範例查詢，針對主要可用性群組執行，會產生如下所示的範例輸出：

```
SELECT ag.[name] as 'Distributed AG Name', ar.replica_server_name as 'Underlying AG', dbs.[name] as 'DB', ars.role_desc as 'Role', drs.synchronization_health_desc as 'Sync Status', drs.log_send_queue_size, drs.log_send_rate, drs.redo_queue_size, drs.redo_rate
FROM    sys.databases dbs,
    sys.availability_groups ag,
    sys.availability_replicas ar,
    sys.dm_hadr_availability_replica_states ars,
    sys.dm_hadr_database_replica_states drs
WHERE   drs.group_id = ag.group_id
and ar.replica_id = ars.replica_id
and ars.replica_id = drs.replica_id
and dbs.database_id = drs.database_id
and ag.is_distributed = 1
```

![分散式可用性群組的效能資訊][13]


### <a name="next-steps"></a>後續步驟 

* [使用可用性群組精靈 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

* [使用新增可用性群組對話方塊 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
* [使用 Transact-SQL 建立可用性群組](create-an-availability-group-transact-sql.md)

<!--Image references-->
[1]: ./media/dag-01-high-level-view-distributed-ag.png
[2]: ./media/dag-02-distributed-ag-data-movement.png
[3]: ./media/dag-03-distributed-ags-wsfcs-different-versions-windows-server.png
[4]: ./media/dag-04-traditional-multi-site-ag.png
[5]: ./media/dag-05-scaling-out-reads-with-distributed-ags.png
[6]: ./media/dag-06-another-scaling-out-reads-using-distributed-ags-example.png
[7]: ./media/dag-07-two-wsfcs-multiple-ags-through-get-clustergroup-command.png
[8]: ./media/dag-08-view-smss-primary-replica-first-wsfc-distributed-ag.png
[9]: ./media/dag-09-no-options-available-action.png
[10]: ./media/dag-10-view-ssms-secondary-replica.png
[11]: ./media/dag-11-example-output-of-query-above.png
[12]: ./media/dag-12-distributed-ag-status.png
[13]: ./media/dag-13-performance-information-distributed-ag.png

 
