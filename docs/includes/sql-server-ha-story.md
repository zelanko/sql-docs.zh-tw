---
ms.openlocfilehash: 1394414db170826fa96ca51a5d35ff8dea199310
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68212231"
---
本文提供 SQL Server 中有關業務持續性解決方案之高可用性和災害復原的概觀。 

大眾部署 SQL Server 時都必須考量的一項工作，是確定所有任務關鍵性 SQL Server 執行個體及其內部資料庫，在企業和使用者需要它們時都能夠使用，無論是上班時間或全天候。 目標是維持企業運轉不中斷或將影響降至最低。 這個概念就是所謂的企業持續營運。

SQL Server 2017 引進了許多新功能或現有項目的增強功能，有些就是針對可用性。 SQL Server 2017 最大的變化是新增 Linux 發行版本的 SQL Server 支援。 如需 SQL Server 2017 新功能的完整清單，請參閱 [SQL Server 2017 的新功能](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2017)主題。

本文著重於涵蓋 SQL Server 2017 的可用性案例，以及 SQL Server 2017 中新增和強化的可用性功能。 包括跨 Windows Server 和 Linux 的 SQL Server 部署混合式案例，以及能增加可讀取資料庫複本數目的案例。 雖然此文章不涵蓋 SQL Server 外部的可用性選項，例如虛擬化提供的可用性選項，但這裡討論的所有內容都適用於客體虛擬機器內的 SQL Server 安裝，無論在公用雲端或由內部部署 Hypervisor 伺服器所主控。

## <a name="sql-server-2017-scenarios-using-the-availability-features"></a>使用可用性功能的 SQL Server 2017 案例

可用性群組、FCI 和記錄傳送都有多種使用方式，並非只供可用性使用。 可用性功能有四個主要的使用方式：

* 高可用性
* 災害復原
* 移轉與升級
* 向外延展一或多個資料庫的可讀取複本

每節都會討論可用於該特定案例的相關功能。 未涵蓋的一項功能是 [SQL Server 複寫](https://docs.microsoft.com/sql/relational-databases/replication/sql-server-replication)。 雖未正式指定為 AlwaysOn 範圍內的可用性功能，但經常用於特定情況下的資料備援。 未來的 Linux SQL Server 版本會新增複寫。

> [!IMPORTANT] 
> SQL Server 可用性功能不會取代任何可用性方案對強固且經過備份和還原策略測試的最基本建置組塊的需求。

### <a name="high-availability"></a>高可用性

如果資料中心所在地或雲端區域的單一區域發生問題，則確保 SQL Server 執行個體或資料庫可以使用十分重要。 本節會討論 SQL Server 可用性功能如何協助該工作。 Windows Server 和 Linux 都提供文中所述的所有功能。 

#### <a name="always-on-availability-groups"></a>AlwaysOn 可用性群組

AlwaysOn 可用性群組 (可用性群組) 在 SQL Server 2012 中引進，將資料庫的每一筆交易傳送到另一個執行個體 (稱為複本) 以特殊狀態包含該資料庫的複本，提供資料庫層級的保護。 可用性群組可以部署在 Standard Edition 或 Enterprise Edition。  參與可用性群組的執行個體，可以是獨立執行個體或 AlwaysOn 容錯移轉叢集執行個體 (FCI，下節中予以說明)。 因為交易會在發生時傳送到複本；所以，對復原點和復原時間目標的需求較低時，建議使用可用性群組。 複本之間的資料移動可為同步或非同步，Enterprise Edition 最多允許三個複本 (包括主要) 同步。 可用性群組有一個主要複本資料庫的完全讀取/寫入複本，所有次要複本皆無法直接從使用者或應用程式接收交易。 

> [!NOTE] 
> AlwaysOn 是 SQL Server 可用性功能的概括性術語，涵蓋可用性群組和 FCI。 AlwaysOn 不是可用性群組功能的名稱。

因為可用性群組只提供資料庫層級，而非執行個體層級的保護，所以非自交易記錄檔中擷取或在資料庫中設定的任何項目，都需要以手動方式就每個次要複本進行同步處理。 有些必須以手動方式同步處理的物件範例，是在執行個體層級、連結的伺服器和 SQL Server Agent 作業的登入。

可用性群組還有稱為接聽程式的另一個元件，可讓應用程式和使用者在不需要知道哪個 SQL Server 執行個體裝載主要複本的情況下連線。 每個可用性群組都會有自己的接聽程式。 雖然接聽程式在 Windows 與 Linux 伺服器上的實作略有不同，但功能和使用方式相同。 下圖顯示使用 Windows Server 容錯移轉叢集 (WSFC) 的 Windows Server 可用性群組。 無論是在 Linux 或 Windows Server 上，可用性都需要作業系統層的基礎叢集。 此範例會示範 WSFC 為基礎叢集的雙伺服器或雙節點簡單組態。 

![簡單的可用性群組](media/sql-server-ha-story/image1.png)
 
Standard 和 Enterprise Edition 有不同的複本數上限。 Standard Edition 中的可用性群組又稱為基本可用性群組，只支援可用性群組中單一資料庫的兩個複本 (一個主要、一個次要)。 Enterprise Edition 不只允許在單一可用性群組中設定多個資料庫，最多還可以有總計 9 個複本 (一個主要、八個次要)。 Enterprise Edition 也提供其他選擇性的優點，例如可讀取的次要複本、製作次要複本備份的能力，及其他更多。

>[!NOTE]
> Linux 版 SQL Server 不再提供也不會新增 SQL Server 2012 已取代的資料庫鏡像。 仍在使用資料庫鏡像的客戶，應該開始規劃移轉至可用性群組，它們會取代資料庫鏡像。

涉及可用性時，可用性群組會提供自動或手動的容錯移轉。 如已設定同步資料移動，且主要與次要複本的資料庫為同步處理狀態，就會發生自動容錯移轉。 只要使用了接聽程式，且應用程式使用較新版的 .NET (具有更新的 3.5 或 4.0 和更新版本)，就應該能夠在使用接聽程式的情況下，控制容錯移轉對使用者不產生影響或影響甚微。 將次要複本容錯移轉成新的主要複本，可以設定成自動或手動，一般按秒計時。

下列清單會強調 Windows Server 和 Linux 可用性群組的一些差異：
* 因為基礎叢集在 Linux 和 Windows Server 上運作方式的差異，所以所有可用性群組的容錯移轉 (手動或自動) 都是透過 Linux 上的叢集完成。 在 Windows Server 可用性群組部署中，手動容錯移轉必須透過 SQL Server 完成。 自動容錯移轉是由 Windows Server 和 Linux 上的基礎叢集控制。 
* 在 SQL Server 2017 中，Linux 上的可用性群組建議組態至少是三個複本。 這是由於基礎叢集的運作方式。 兩個複本組態的改善解決方案會在發行後推出。
* 在 Linux 上，每個接聽程式使用的通用名稱是在 DNS 中定義，不像 Windows Server 是在叢集中。

SQL Server 2017 有一些可用性群組的新功能和增強功能：

* 叢集類型
* REQUIRED_SECONDARIES_TO_COMMIT
* Windows Server 組態的增強式 Microsoft 分散式交易協調器 (DTC) 支援
* 其他唯讀資料庫的相應放大案例 (本文稍後敘述)

##### <a name="always-on-availability-group-cluster-types"></a>AlwaysOn 可用性群組叢集類型

Windows Server 叢集的內建可用性形式是透過名為容錯移轉叢集功能啟用。 它可讓您建置 WSFC，與可用性群組或 FCI 搭配使用。 隨附於 SQL Server 的叢集感知資源 Dll 會提供可用性群組和 FCI 的整合。 

每個受支援的 Linux 發行版本都附帶自己的 Pacemaker 叢集解決方案版本。 Linux SQL Server 2017 支援使用 Pacemaker。 Pacemaker 是開啟式堆疊解決方案，每個發行版本都可與其堆疊整合。 雖然發行版本附帶 Pacemaker，但並非像 Windows Server 中的容錯移轉叢集功能一樣整合。

WSFC 和 Pacemaker 同大於異。 它們都提供一種方式，採用個別伺服器並將它們結合在一個組態以提供可用性，而且有資源、條件約束 (即使實作方式不同)、容錯移轉等等項目的概念。 為支援可用性群組和 FCI 組態的 Pacemaker，包括自動容錯移轉等項目，Microsoft 為 Pacemaker 提供 mssql-server-ha 套件，類似 WSFC 中的資源 Dll，但不完全相同。 WSFC 和 Pacemaker 的其中一項差異，是 Pacemaker 沒有網路名稱資源，這是協助在 WSFC 上摘要接聽程式名稱 (或 FCI 名稱) 的元件。 DNS 在 Linux 上提供該名稱解析。

因為叢集堆疊的差異，所以可用性群組需要進行某些變更，因為 SQL Server 必須處理一些經過 WSFC 原生處理的中繼資料。 最 [!IMPORTANT] 的變更是引進可用性群組的叢集類型。 這儲存在 cluster_type 和 cluster_type_desc 資料行中的 sys.availability_groups。 有三種叢集類型：

* WSFC 
* External
* None

所有需要可用性的可用性群組都必須使用基礎叢集，這在 SQL Server 2017 即為 WSFC 或 Pacemaker。 使用基礎 WSFC 的 Windows Server 可用性群組，其預設叢集類型是 WSFC，而且不需要設定。 至於 Linux 可用性群組，在建立可用性群組時，叢集類型必須設定為外部。 整合 Pacemaker 是在建立可用性群組之後設定，而在 WSFC 是於建立階段完成。

None 叢集類型可以搭配 Windows Server 和 Linux 可用性群組。 將叢集類型設定為 None，表示可用性群組不需要有基礎叢集。 這表示 SQL Server 2017 是第一個支援沒有叢集之可用性群組的 SQL Server 版本，但代價是此組態不能當作高可用性解決方案支援。 

> [!IMPORTANT] 
> SQL Server 2017 不允許在建立可用性群組後變更其叢集類型。 這表示可用性群組不能從 None 切換成外部或 WSFC，反之亦然。 

對只想新增更多資料庫唯讀複本，或希望可用性群組提供移轉/升級但不受基礎叢集或甚至複寫的額外複雜性所約束的使用者來說，叢集類型為 None 的可用性群組是理想的解決方案。 如需詳細資訊，請參閱[移轉與升級](#Migrations)及[讀取級別](#ReadScaleOut)等章節。 

下列螢幕擷取畫面會顯示對 SSMS 中不同種類的叢集類型的支援。 您必須執行版本 17.1 或更新版本。 下列螢幕擷取畫面取自 17.2 版本。

![SSMS AG 選項](media/sql-server-ha-story/image2.png)
 
##### <a name="requiredsynchronizedsecondariestocommit"></a>REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT

SQL Server 2016 對 Enterprise Edition 的同步複本數目支援，從二個增加到三個。 不過，如果一個次要複本已同步處理，但另一個卻發生問題，沒有辦法控制行為以通知主要複本去等候行為異常的複本或允許它繼續。 這表示在某些時候，主要複本會繼續接收寫入流量，即使次要複本不在同步處理的狀態，這表示次要複本上有資料遺失。
SQL Server 2017 現在有選項能夠控制當名為 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT 的同步複本出現時的行為。 選項的運作方式如下：
* 有三個可能的值：0、1 與 2
* 值是必須同步的次要複本數目，對資料遺失、可用性群組的可用性和容錯移轉都有影響。
* WSFC 和 None 叢集類型的預設值為 0，可以手動設定為 1 或 2。
* 根據預設，外部叢集類型的叢集機制會設定它，且可手動覆寫。 三個同步複本的預設值都會是 1。
在 Linux 上，REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT 的值是在叢集的可用性群組資源中設定。 在 Windows 中，它是透過 Transact SQL 設定。

因為如果無法使用所需的次要複本數目，在解決之前即無法使用主要複本，所以高於 0 的值可確保較高的資料保護。 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT 也會影響容錯移轉行為，因為如果正確的次要複本數目不是處於適當的狀態，即無法進行自動容錯移轉。 在 Linux，值為 0 將不允許自動容錯移轉，所以在 Linux 上，使用同步加上自動容錯移轉時，此值必須設定大於 0，才能達到自動容錯移轉。 在 Windows Server 上設為 0 是 SQL Server 2016 及舊版的行為。

##### <a name="enhanced-microsoft-distributed-transaction-coordinator-support"></a>增強式 Microsoft 分散式交易協調器支援

在 SQL Server 2016 之前，為要求使用基礎 DTC 分散式交易的應用程式取得 SQL Server 可用性的唯一方式，是部署 FCI。 下列兩種方式可以完成分散式交易：
* 在相同的 SQL Server 執行個體中跨越多個資料庫的交易
* 跨越多個 SQL Server 執行個體或可能牽涉到非 SQL Server 資料來源的交易

SQL Server 2016 引進的 DTC 部分支援與可用性群組，涵蓋後面的案例。 SQL Server 2017 支援使用 DTC 的兩種案例完成該劇本。

可用性群組的其他 DTC 支援增強功能，是在 SQL Server 2016 中，可用性群組的 DTC 支援只能在建立可用性群組時完成，無法於稍後新增。 在 SQL Server 2017，DTC 支援也可以在建立可用性群組之後新增。

>[!NOTE]
> DTC 支援只能設定供以 Windows Server 為基礎 SQL Server 執行個體的資料庫使用。 如果您的應用程式需要 DTC，您就必須使用 Windows Server 作為 SQL Server 部署的作業系統，而不能使用 Linux。 

#### <a name="always-on-failover-cluster-instances"></a>AlwaysOn 容錯移轉叢集執行個體
叢集安裝自 6.5 版起即為 SQL Server 功能。 FCI 是可為稱之為執行個體的整個 SQL Server 安裝，提供可用性的經證實方法。 這表示，要是基礎伺服器遇到問題，執行個體內的所有項目，包括資料庫、SQL Server Agent 作業、連結的伺服器等等，都會移至另一部伺服器。 所有 FCI 都需要某種類型的共用儲存體，即使是透過網路提供的。 無論任何時候，FCI 的資源都只能由一個節點執行及擁有。 下圖中，第一個叢集節點擁有 FCI 中，這也表示它擁有以實線表示其與儲存體建立關聯的共用儲存體資源。

![容錯移轉叢集執行個體](media/sql-server-ha-story/image3.png)
 
容錯移轉之後，擁有權變更如下圖所示。

![容錯移轉後](media/sql-server-ha-story/image4.png)
 
FCI 未遺失任何資料，但基礎的共用儲存體是單一失敗點，因為有資料複本。 FCI 通常會結合其他可用性方法，例如可用性群組或記錄傳送，以擁有多餘的資料庫複本。 額外部署的方法應該使用和 FCI 實體分隔的儲存體。 當 FCI 容錯移轉到另一個節點時，它會停在一個節點，然後在另一個節點開始，不像關閉再開啟伺服器。 FCI 通過一般復原程序，表示會回復需要向前復原的任何交易，以及不完整的任何交易。 因此，資料庫和失敗或手動容錯移轉時間點的資料是一致的，因此不會遺失資料。 資料庫要在復原完成後才可以使用，因此復原時間取決於許多因素，且通常會超過容錯移轉可用性群組的時間。 代價是，當您容錯移轉可用性群組時，可能需要其他工作才能使用資料庫，例如：啟用 SQL Server Agent 作業的工作。

如同可用性群組，FCI 會摘要哪個基礎叢集節點裝載它。 FCI 一律保留相同的名稱。 應用程式和使用者永遠不會連線到節點。使用指派給 FCI 的唯一名稱。 FCI 可以參與可用性群組，作為裝載主要或次要複本的其中一個執行個體。

下列清單會強調 Windows Server 和 Linux 上 FCI的一些差異：

* 在 Windows Server 上，FCI 是安裝程序的一部分。 在 Linux 上，則是安裝 SQL Server 後才設定 FCI。
* Linux 每部主機僅支援單一 SQL Server 安裝，因此所有的 FCI 都是預設執行個體。 Windows Server 最多每個 WSFC 支援 25 個 FCI。
* FCI 在 Linux 中使用的通用名稱是在 DNS 中定義，應該與為 FCI 建立的資源同名。

#### <a name="log-shipping"></a>記錄傳送
如果復原點和復原時間目標更具彈性，或者資料庫不被視為高任務關鍵性，則記錄傳送是 SQL Server 中另一個經過驗證的可用性功能。 根據 SQL Server 原生備份，記錄傳送程序會自動產生交易記錄備份，將其複製到一或多個稱為暖待命的執行個體，並自動將交易記錄備份套用至該待命。 記錄傳送使用 SQL Server Agent 作業，自動化備份、複製和套用交易記錄備份的程序。

![記錄傳送](media/sql-server-ha-story/image5.png)
 
在某些容量中使用記錄傳送的最大優點，可以說是考量人為錯誤。 套用交易記錄檔可予延遲。 因此，如果有人發出類似不含 WHERE 子句的 UPDATE 這樣的內容，待命可能不會變更，而您無法在修復主要系統時切換至該待命。 雖然記錄傳送很容易設定，但從主要切換到暖待命，也稱為角色變更，一律為手動。 角色變更是透過 TRANSACT-SQL 起始，就像可用性群組，交易記錄檔中未擷取的所有物件都必須以手動方式同步處理。 記錄傳送也需要依資料庫一一設定，而單一可用性群組可以包含多個資料庫。 不同於可用性群組或 FCI，記錄傳送沒有任何角色變更的抽象概念。 應用程式必須能夠處理這個事件。 無法使用 DNS 別名 (CNAME) 這類技術，但優劣各半，例如切換之後 DNS 重新整理所耗費的時間。

## <a name="disaster-recovery"></a>災害復原

當主要可用性位置發生重大事件，例如水災或地震時，企業必須準備讓系統在其他地方上線。 本節會討論 SQL Server 可用性功能如何協助企業持續營運。

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性群組

可用性群組的優點之一，是能夠使用單一功能設定高可用性和災害復原。 不要求確保共用儲存體也高度可用，更容易在當地的資料中心擁有許多用於高可用性的複本，在其他資料中心擁有用於災害復原的遠端複本，每個複本有不同的儲存體。 擁有資料庫的其他複本，是確保備援性應付的代價。 以下為跨多個資料中心的可用性群組範例。 一個主要複本負責保存所有同步處理的次要複本。

![可用性群組](media/sql-server-ha-story/image6.png)
 
在叢集類型為 None 的可用性群組之外，可用性群組要求所有複本都屬於相同的基礎叢集，無論是 WSFC 或 Pacemaker。 這表示在上圖中，WSFC 會延伸到兩個不同的資料中心工作，這會增加複雜度。 無論平台 (Windows Server 或 Linux)。 跨距離延展叢集會增加複雜性。 SQL Server 2016 引進的分散式可用性群組，能讓可用性群組跨越在不同叢集上設定的可用性群組。 如此即可減少所有節點參與相同叢集的需求，使設定災害復原更為容易。 如需分散式可用性群組的詳細資訊，請參閱[分散式可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/distributed-availability-groups)。

![分散式可用性群組](media/sql-server-ha-story/image11.png)
 
### <a name="always-on-failover-cluster-instances"></a>AlwaysOn 容錯移轉叢集執行個體

FCI 可用於災害復原。 與一般可用性群組一樣，基礎叢集機制也必須擴展到所有位置，這會增加複雜度。 FCI 有其他考量：共用儲存體。 主要和次要站台需要使用相同的磁碟；因此，需要使用儲存體廠商在硬體層提供的功能，或在 Windows Server 使用儲存體複本等外部方法，才能確保其他地方也有 FCI 使用的磁碟。 

![AlwaysOn FCI](media/sql-server-ha-story/image8.png)
 
### <a name="log-shipping"></a>記錄傳送
記錄傳送是提供 SQL Server 資料庫災害復原最古老的方法之一。 記錄傳送通常給合可用性群組和 FCI 使用，提供符合成本效益且更簡單的災害復原，其他選項可能因為環境、系統管理技術或預算而發生困難。 類似記錄傳送的高可用性案例，許多環境會延遲載入交易記錄備份以考量人為錯誤。

## <a name = "Migrations"></a> 移轉與升級

部署新執行個體或升級舊執行個體時，企業無法容許長時間中斷。 本節將討論如何使用 SQL Server 可用性功能，將計劃的架構變更、伺服器切換、平台變更 (例如 Windows Server 換成 Linux，或反之) 或修補期間的停機時間降到最低。

> [!NOTE]
> 其他方法，例如使用備份和還原至其他地方，也可以用於移轉與升級。 本文不討論它們。 

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性群組

包含一或多個可用性群組的現有執行個體可以就地升級為 SQL Server 2017。 雖然這項作業需要一定程度的停機時間，但只要有正確的時間規劃，就可降至最低。 

如果目標是要移轉到新的伺服器且不變更組態 (包括作業系統或 SQL Server 版本)，這些伺服器就可以新增為現有基礎叢集的節點，並新增至可用性群組。 只要複本處於正確的狀態，即可手動容錯移轉至新的伺服器，從可用性群組中移除舊的伺服器，最終解除委任。 

分散式 AG 也是移轉至新組態或升級 SQL Server 的另一種方法。 因為分散式 AG 支援不同架構上的不同基礎 AG；例如，您可以從在 Windows Server 2012 R2 上執行的 SQL Server 2016 變更成在 Windows Server 2016 上執行的 SQL Server 2017。 

![分散式 AG](media/sql-server-ha-story/image10.png)

最後，叢集類型為 None 的可用性群組也可以用於移轉或升級。 您不能混用及比對一般可用性群組組態中的叢集類型，因此所有複本的類型都必須是 None。 分散式可用性群組可以用來跨越以不同叢集類型設定的可用性群組。 這個方法在各種不同的作業系統平台上也受到支援。

移轉與升級可用性群組的所有變數都允許工作中最耗時的部分完成，即資料同步處理。 要起始切換至新的組態時，相對於需要完成包括資料同步處理在內所有工作的長時間停機，完全移轉中斷服務的時間較短。 

可用性群組會在修補作業完成時將主要複本手動容錯移轉至次要複本，讓修補基礎作業系統期間的停機時間降至最低。 從作業系統的觀點而言，在 Windows 伺服器上這樣做更常見，因為提供服務給基礎作業系統，通常 (但非一律) 需要重新開機。 修補 Linux 有時候需要重新開機，但不常見。 

[修補參與可用性群組的 SQL Server 執行個體](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances)也能將停機時間降至最低，視可用性群組架構的複雜程度而定。 若要修補參與可用性群組的伺服器，必須先修補次要複本。 修補完成正確的複本數目後，主要複本即可手動容錯移轉至另一個要升級的節點。 任何剩餘的次要複本也可以在此時升級。 

### <a name="always-on-failover-cluster-instances"></a>AlwaysOn 容錯移轉叢集執行個體

自力更生的 FCI 無法協助傳統的移轉或升級。FCI 的資料庫和計算在內的所有其他物件都必須設定可用性群組或記錄傳送。 不過，基礎的 Windows Server 需要修補時，Windows Server 下的 FCI 仍是大受歡迎的選項。 可起始手動容錯移轉，這表示短暫中斷，而不是在整個修補 Windows Server 的期間完全無法使用執行個體。
FCI 可以就地升級為 SQL Server 2017。 如需相關資訊，請參閱[升級 SQL Server 容錯移轉叢集執行個體](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance)。

### <a name="log-shipping"></a>記錄傳送

記錄傳送仍然是移轉和升級資料庫的熱門選項。 類似可用性群組，但這次將交易記錄用作同步處理方法，可以在切換伺服器前先妥善啟動資料傳播。 在切換的同時，一旦所有流量都停在來源，就需要採用、複製最後一個交易記錄，並將它套用至新的組態。 此時，資料庫就可以上線了。 記錄傳送通常能忍受速度較慢的網路，而切換完成時間可能比使用可用性群組或分散式可用性群組略長，通常以分鐘計 (非以小時、天或週計)。

類似可用性群組，記錄傳送可以提供修補時切換到另一部伺服器的方式。

### <a name="other-sql-server-deployment-methods-and-availability"></a>其他 SQL Server 部署方法和可用性

Linux 的 SQL Server 另有兩種部署方法：容器和使用 Azure (或其他公用雲端提供者)。 如本文所述的一般可用性需求，無論 SQL Server 部署方式為何都存在。 當要讓 SQL Server 具有高可用性時，這兩個方法有一些特殊考量。

[使用 Docker 的容器](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)，對 Windows Server 或 Linux 而言，都是部署 SQL Server 的新方法。 容器是準備好要執行的 SQL Server 完整影像。 不過，目前沒有叢集化高可用性或災害復原的原生支援。 目前，使用容器提供 SQL Server 資料庫的選項是記錄傳送以及備份和還原。 雖然如前文所述可以設定 None 叢集類型的可用性群組，但它不會視為真正的可用性組態。 Microsoft 正在尋找使用容器啟用可用性群組或 FCI 的方式。 

如果您目前使用的是容器，且容器遺失，它可以再次部署並附加至所用的共用儲存體，視容器平台而定。 此機制有部分由容器協調者提供。 雖然這提供某種程度的靈活度，但仍有一些與資料庫復原有關的停機時間，如果使用可用性群組或 FCI，並非真的如預期般高度可用。 

Linux IaaS 虛擬機器的部署可以使用 Azure 安裝 SQL Server。 與內部部署安裝一樣，受支援的安裝需要 Pacemaker 本身以外使用 STONITH (將另一個節點爆頭)。 STONITH 是透過隔離可用性代理程式提供。 某些發行版本會將它們隨平台出貨，有些則依賴外部的硬體和軟體供應商。 請查看您慣用的 Linux 發行版本，了解所提供的 STONITH 格式為何，以便在公用雲端中部署支援的解決方案。

## <a name="cross-platform-and-linux-distribution-interoperability"></a>跨平台和 Linux 發行版本互通性

現在 Windows Server 和 Linux 都支援 SQL Server，本節討論它們在其他用途之外如何針對可用性搭配工作的案例，以及會併入多個 Linux 發行版本的解決方案劇本。

討論跨平台和互通性案例之前，必須先說明兩個事實：

* 沒有以 WSFC 為基礎的 FCI 或可用性群組會直接使用以 Linux 為基礎的 FCI 或可用性群組的案例。 Pacemaker 節點無法擴充 WSFC，反之亦然。 
* 混合式 Linux 發行版本不支援外部叢集類型的 FCI 或可用性群組。 該案例中所有的可用性群組複本不僅必須設定相同的 Linux 發行版本，還要設定相同的版本。 SQL Server 可以跨兩個平台或多個 Linux 發行版本操作的兩個支援方式，是可用性群組和記錄傳送。

## <a name="distributed-availability-groups"></a>分散式可用性群組 

分散式可用性群組的設計是用來跨越可用性群組組態，無論可用性群組下的這兩個基礎叢集是兩個不同的 WSFC、Linux 發行版本，或一個在 WSFC、一個在 Linux。 分散式可用性群組會是具有跨平台解決方案的主要方法。 分散式可用性群組也是移轉的主要解決方案，例如從 Windows Server 的 SQL Server 基礎結構轉換成 Linux 的，如果這是貴公司想要做的事。 如前所述，可用性群組，特別是分散式可用性群組，會將無法使用應用程式的時間降至最低。 跨 WSFC 和 Pacemaker 的分散式可用性群組範例如下所示。

![分散式可用性群組](media/sql-server-ha-story/image9.png)
 
如果使用 None 叢集類型設定可用性群組，它可以跨 Windows Server 和 Linux，以及多個 Linux 發行版本。 因為這不是真正的高可用性組態，所以不應用於任務關鍵部署，但可用於讀取級別或移轉/升級案例。

## <a name="log-shipping"></a>記錄傳送

因為記錄傳送只以備份與還原為基礎，所以 Windows Server 的 SQL Server 和 Linux 的 SQL Server 的資料庫、檔案結構等等沒有任何差異。 這表示 Windows Server 的 SQL Server 安裝和 Linux 的 SQL Server 安裝之間，以及 Linux 發行版本之間，可以設定記錄傳送。 其他一切保持不變。 唯一需要注意的是，記錄傳送就和可用性群組一樣，當來源位在較高的 SQL Server 主要版本，而目標位於較低的 SQL Server 版本時，無法運作。 

## <a name = "ReadScaleOut"></a> 讀取級別

自 SQL Server 2012 引進次要複本後，其就已經能夠用於唯讀查詢。 以可用性群組可以達到的兩種方式：允許直接存取次要複本以及[設定唯讀路由](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server) (必須使用接聽程式)。  SQL Server 2016 引進了透過接聽程式使用循環配置資源演算法的負載平衡唯讀狀態連線能力，允許唯讀要求散佈到所有的可讀取複本。 

> [!NOTE]
> 可讀取的次要複本是 Enterprise Edition 的獨有功能，每個裝載可讀取複本的執行個體都需要 SQL Server 授權。

透過可用性群組調整可讀取的資料庫複本，首次引進是在 SQL Server 2016 的分散式可用性群組中。 這可讓公司不僅在當地有資料庫的唯讀複本，還可以最少量的組態在地區及全球擁有資料庫的唯讀複本，且因為在本地執行查詢，而減少網路流量和延遲。 每個可用性群組的主要複本皆可植入兩個其他可用性群組，即使它不是完整的讀取/寫入複本，因此每個分散式可用性群組最多可以支援 27 份可讀取的資料。 

![分散式可用性群組](media/sql-server-ha-story/image11.png)

從 SQL Server 2017 開始，便可建立近乎即時的唯讀解決方案，設定叢集類型為 None 的可用性群組。 如果目標是使用可用性群組取得可讀取的次要複本而不是可用性，這樣做會移除使用 WSFC 或 Pacemaker 的複雜性，並以簡單的部署方法提供可用性群組的可讀取優點。 

最需要注意的是，由於沒有叢集類型為 None 的基礎叢集，設定唯讀路由略有不同。 就 SQL Server 的觀點而言，即使沒有叢集，仍需要接聽程式以路由要求。 使用 IP 位址或主要複本的名稱，而非設定傳統的接聽程式。 接著使用主要複本路由唯讀要求。

您可以還原資料庫 WITH STANDBY，針對可讀取使用方式技術性設定記錄傳送暖待命。 不過，由於交易記錄需要獨佔資料庫進行還原，這表示在此情況下，使用者無法存取資料庫。 這會使記錄傳送略遜於理想的解決方案，特別是當需要近乎即時的資料時。 

所有使用可用性群組的讀取級別案例，都應該注意一件事，不像使用所有資料都是即時的異動複寫，每個次要複本都不是唯一索引可以套用的狀態，複本是完全相符的主要複本。 這表示，如果報告需要任何索引，或資料需要操作，都必須在主要複本的資料庫上完成。 如果您需要這樣的彈性，複寫會是取得可讀取資料的較佳解決方案。

## <a name="summary"></a>摘要

在 Windows Server 和 Linux 上使用相同的功能，可令 SQL Server 2017 的執行個體與資料庫成為高可用性。 除了本機高可用性和災害復原的標準可用性案例外，SQL Server 的可用性功能可以將因升級和移轉所致的停機時間降到最低。 可用性群組也可以提供資料庫的其他複本，當作相同架構的一部分，以相應放大可讀取的複本。 無論是使用 SQL Server 2017 部署新的解決方案或考慮升級，SQL Server 2017 都有您需要的可用性與可靠性。
 
[SimpleAG]:media\sql-server-ha-story\image1.png
[SSMSAGOptions]:media\sql-server-ha-story\image2.png
[BasicFCI]:media\sql-server-ha-story\image3.png
[PostFailoverFCI]:media\sql-server-ha-story\image4.png
[LogShipping]:media\sql-server-ha-story\image5.png
[AG]:media\sql-server-ha-story\image6.png
[DAG]:media\sql-server-ha-story\image7.png
[AlwaysOnFCI]:media\sql-server-ha-story\image8.png
[BasicDAG]:media\sql-server-ha-story\image9.png
[image10]:media\sql-server-ha-story\image10.png
[DAG]:media\sql-server-ha-story\image11.png
