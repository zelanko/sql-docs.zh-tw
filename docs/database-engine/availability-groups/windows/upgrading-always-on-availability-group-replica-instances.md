---
title: "升級 AlwaysOn 可用性群組複本執行個體 | Microsoft Docs"
ms.custom: 
ms.date: 01/10/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cd24872a05d4d8c210cc3b54e70b22cdb1ec799c
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="upgrading-always-on-availability-group-replica-instances"></a>升級 AlwaysOn 可用性群組複本執行個體
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

將裝載 AlwaysOn 可用性群組 (AG) 的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體升級為新的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 版本、新的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 或累積更新，或安裝至新的 Windows Service Pack 或累積更新時，您可透過執行輪流升級來將主要複本的停機時間減少至僅單一手動容錯移轉 (回復為原始主要複本時則為兩次手動容錯移轉)。 在升級過程中無法使用次要複本執行容錯移轉或唯讀作業，且在升級完成後，次要複本可能需要花費一些時間趕上主要複本節點，根據主要複本節點的活動量而定 (因此網路流量會偏高)。 另請注意，在初始容錯移轉到執行較新版 SQL Server 的次要複本之後，該可用性群組中的資料庫會執行整個升級程序，以將其升級為最新版本。 在這段期間內，這些資料庫都不會有可讀取的複本。 初始容錯移轉之後的停機時間長短，取決於可用性群組中的資料庫數量。 如果您打算容錯回復為原始的主要複本，此步驟在您進行容錯回復時不會重覆。
  
>[!NOTE]  
>本文僅限討論 SQL Server本身的升級。 其未涵蓋包含 Windows Server 容錯移轉叢集 (WSFC) 的作業系統升級。 Windows Server 2012 R2 之前的作業系統，不支援裝載容錯移轉叢集的 Windows 作業系統升級。 若要升級在 Windows Server 2012 R2 上執行的叢集結點，請參閱[叢集作業系統輪流升級](http://docs.microsoft.com/windows-server/failover-clustering/cluster-operating-system-rolling-upgrade) \(機器翻譯\)。  
  
## <a name="prerequisites"></a>Prerequisites  
在開始之前，請檢閱以下重要資訊：  
  
- [支援的版本與版本升級](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)︰確認您可從您的 Windows 作業系統版本與 SQL Server 版本升級至 SQL Server 2016。 例如，您無法直接從 SQL Server 2005 執行個體升級至 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
- [選擇資料庫引擎升級方法](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md)︰若要依正確順序升級，請根據您檢閱的支援版本與版本升級，選取適當的升級方法和步驟，此外亦根據作業環境中安裝的其他元件。  
  
- [計劃和測試資料庫引擎升級計畫](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)︰檢閱版本資訊與已知的升級問題、升級前檢查清單，並開發和測試升級計畫。  
  
- [安裝 SQL Server 的硬體和軟體需求](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)：檢閱安裝 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 的軟體需求。 如果需要其他軟體，請先將其安裝在每個節點上，然後開始升級程序，以將任何停機時間降到最低。  

- [檢查是否針對任何 AG 資料庫使用異動資料擷取或複寫](#special-steps-for-change-data-capture-or-replication)：如果啟用 AG 中的任何資料庫進行異動資料擷取 (CDC)，請完成這些[指示](#special-steps-for-change-data-capture-or-replication)。

>[!NOTE]  
>在就地升級複本的輪流升級之外，不支援在相同 AG 中混用 SQL Server 執行個體版本。 較高版本的 SQL Server 執行個體無法作為新複本新增至現有的 AG。 例如，SQL Server 2017 複本無法新增至現有的 SQL Server 2016 AG。 若要使用 AG 移轉至新版本的 SQL Server 執行個體，唯一支援的方法是 SQL Server 2016 Enterprise Edition 或更新版本中的分散式 AG。

## <a name="rolling-upgrade-basics-for-always-on-ags"></a>AlwaysOn AG 的輪流升級基本概念  
當您執行伺服器升級或更新時，請遵循下列指導方針，好讓停機時間及 AG 的資料遺失情況降至最低：  
  
- 在開始輪流升級之前，  
  
    - 至少在其中一個同步認可複本執行個體上，執行手動容錯移轉練習  
  
    - 在每一個可用性資料庫上執行完整資料庫備份來保護資料  
  
    - 在每一個可用性資料庫上執行 DBCC CHECKDB  
  
-   請務必先升級遠端次要複本執行個體，然後是本機次要複本執行個體，最後是主要複本執行個體。  
  
-   在進行升級的資料庫上，不會發生備份。  在升級次要複本之前，請設定自動備份喜好設定，只在主要複本上執行備份。  執行版本升級時，無法讀取任何複本或使用其執行備份。 執行非版本升級時，您可先設定要在次要複本上執行的自動備份，然後再升級主要複本。  
  
-   執行版本升級時，在升級可讀取次要複本之後，以及將主要複本容錯移轉至升級的次要複本或是升級主要複本之前，皆無法讀取可讀取的次要複本。  
  
-   為了避免 AG 在升級程序期間發生意外的容錯移轉，請從所有同步認可複本中移除可用性容錯移轉，再開始操作。  
  
-   將 AG 容錯移轉至包含次要複本的已升級執行個體之前，請勿升級主要複本執行個體。 否則，用戶端應用程式在主要複本執行個體的升級期間可能會受困於停機時間延長。  
  
-   一定要將 AG 容錯移轉至同步認可的次要複本執行個體。 若您容錯移轉到非同步認可的次要複本執行個體，資料庫將會很容易遺失資料，而且資料移動會自動暫停，直到您手動繼續資料移動為止。  
  
-   在您升級或更新其他任何次要複本執行個體之前，請勿升級主要複本執行個體。 已升級的主要複本將無法再傳送記錄到尚未升級 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 執行個體至相同版本的次要複本。 當移至次要複本的資料移動作業暫停時，該複本無法進行自動容錯移轉，而且您的可用性資料庫很容易發生資料遺失。  
  
-   在容錯移轉 AG 之前，請確認容錯移轉目標的同步處理狀態為 SYNCHRONIZED。  
  
## <a name="rolling-upgrade-process"></a>輪流升級處理程序  
 實際上，確切的程序將取決於一些因素，例如 AG 的部署拓撲和每個複本的認可模式。 但是在最簡單的案例中，輪流升級是多階段的程序，其最簡單的形式包含以下步驟：  
  
 ![HADR 案例中的 AG 升級](../../../database-engine/availability-groups/windows/media/alwaysonupgrade-ag-hadr.gif "HADR 案例中的 AG 升級")  
  
1.  在所有同步認可複本上移除自動容錯移轉  
  
2.  升級執行非同步認可次要複本的所有遠端伺服器複本執行個體  
  
3.  升級目前未執行主要複本的所有本機複本次要執行個體  
  
4.  手動將 AG 容錯移轉至本機同步認可的次要複本  
  
5.  升級或更新先前裝載主要複本的本機複本執行個體  
  
6.  視需要設定自動容錯移轉夥伴  
  
 必要時，您可以執行額外的手動容錯移轉，讓 AG 回到原始的設定。  
  
## <a name="ag-with-one-remote-secondary-replica"></a>具有一個遠端次要複本的 AG  
 如果您部署 AG 只是為了災害復原，您可能必須將 AG 容錯移轉至非同步認可的次要複本。 下圖說明這類組態：  
  
 ![DR 案例中的 AG 升級](../../../database-engine/availability-groups/windows/media/agupgrade-ag-dr.gif "DR 案例中的 AG 升級")  
  
 在此情況下，您必須在輪流升級期間將 AG 容錯移轉至非同步認可的次要複本。 為了防止資料遺失，請將認可模式變更為同步認可，並等候次要複本同步處理，再容錯移轉 AG。 因此，輪流升級程序可能如下所示：  
  
1.  升級位於遠端站台的次要複本執行個體  
  
2.  將認可模式變更為同步認可  
  
3.  等到同步處理狀態變成 SYNCHRONIZED  
  
4.  將 AG 容錯移轉至遠端站台上的次要複本  
  
5.  升級或更新本機 (主要站台) 複本執行個體  
  
6.  將 AG 容錯移轉至主要站台  
  
7.  將認可模式變更為非同步認可  
  
 因為與遠端站台的資料同步處理不建議使用同步認可模式的設定，所以用戶端應用程式可能會注意到，設定變更之後會立刻增加資料庫延遲。 此外，執行容錯移轉會導致所有未認可的記錄訊息遭到捨棄。 捨棄的記錄訊息數量可能很龐大，這是因為兩個站台之間的高度網路延遲，導致用戶端遭遇大量的交易失敗。 您可以執行下列動作，讓用戶端應用程式的影響降至最低：  
  
-   謹慎選擇維護期間，使其發生於用戶端流量較低的期間  
  
-   在主要站台上升級或更新 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 時，請將可用性模式變更回非同步認可，當您再次準備好要容錯移轉至主要站台時，再還原成同步認可模式。  
  
## <a name="ag-with-failover-cluster-instance-nodes"></a>包含容錯移轉叢集執行個體節點的 AG  
 若 AG 包含容錯移轉叢集執行個體 (FCI) 節點，您應該先升級非使用中節點，再升級使用中節點。 下圖說明具有 FCI 的常見 AG 案例 (為了擁有本機高可用性及 FCI 之間用於遠端災害復原的非同步認可) 以及升級順序。  
  
 ![包含 FCI 的AG 升級](../../../database-engine/availability-groups/windows/media/agupgrade-ag-fci-dr.gif "包含 FCI 的AG 升級")  
  
1.  升級或更新 REMOTE2  
  
2.  將 FCI2 容錯移轉到 REMOTE2  
  
3.  升級或更新 REMOTE1  
  
4.  升級或更新 PRIMARY2  
  
5.  將 FCI1 容錯移轉到 PRIMARY2  
  
6.  升級或更新 PRIMARY1  
  
## <a name="upgrade-update-sql-server-instances-with-multiple-ags"></a>升級/更新具有多個 AG 的 SQL Server 執行個體  
 若您正在執行多個 AG，而其中的主要複本位於不同的伺服器節點上 (主動/主動設定)，則升級路徑會牽涉到更多的容錯移轉步驟，以保留程序中的高可用性。 假設您在三個伺服器節點上執行三個 AG，且其所有複本都是在同步認可模式中，如下表所示：  
  
|AG|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1|Primary|||  
|AG2||Primary||  
|AG3|||Primary|  
  
 在您的案例中，可能適合依照以下順序執行負載平衡的輪流升級：  
  
1.  將 AG2 容錯移轉到 Node3 (以釋出 Node2)  
  
2.  升級或更新 Node2  
  
3.  將 AG1 容錯移轉到 Node2 (以釋出 Node1)  
  
4.  升級或更新 Node1  
  
5.  將 AG2 和 AG3 容錯移轉到 Node1 (以釋出 Node3)  
  
6.  升級或更新 Node3  
  
7.  將 AG3 容錯移轉到 Node3  
  
 此升級順序的平均停機時間少於每個 AG 的兩次容錯移轉。 產生的設定如下表所示。  
  
|AG|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1||Primary||  
|AG2|Primary|||  
|AG3|||Primary|  
  
 根據您的特定實作方式，您的升級路徑可能會有不同，用戶端應用程式遇到的停機時間也可能會有差異。  
  
> [!NOTE]  
>  在許多情況下，您在完成輪流升級後會容錯回復至原始主要複本。 

## <a name="special-steps-for-change-data-capture-or-replication"></a>異動資料擷取或複寫的特殊步驟

根據所套用的更新，可能需要額外的步驟才能啟用 AG 複本資料庫進行異動資料擷取或複寫。 請參閱更新的版本資訊，以判斷是否需要下列步驟：

1. 升級每個次要複本。

1. 升級所有次要複本之後，將 AG 容錯移轉至已升級的執行個體。 

1. 在裝載主要複本的執行個體上執行下列 Transact-SQL：

   ```sql
   EXECUTE [master].[sys].[sp_vupgrade_replication];
   ```

   >[!NOTE]
   >此命令可能需要幾分鐘才能完成執行。 

1. 升級原本為主要複本的執行個體。

如需背景資訊，請參閱 [CDC functionality may break after upgrading to the latest CU](http://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/) (CDC 功能可能會在升級至最新版 CU 之後中斷)。

  
## <a name="see-also"></a>另請參閱  
 [使用安裝精靈升級為 SQL Server 2016 &#40;安裝程式&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   

 [從命令提示字元安裝 SQL Server 2016](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
