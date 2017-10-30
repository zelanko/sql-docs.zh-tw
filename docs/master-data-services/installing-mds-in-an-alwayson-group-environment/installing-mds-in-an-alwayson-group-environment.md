---
title: "Master Data Services 的高可用性和災害復原 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f5cebe2ba32765cc5f4bddc974ee62b3ed3b8915
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Master Data Services 的高可用性和災害復原

**摘要︰** 這篇文章說明 AlwaysOn 可用性群組設定上所裝載 Master Data Service (MDS) 的解決方案。 這篇文章說明如何在 SQL 2016 AlwaysOn 可用性群組 (AG) 上安裝及設定 SQL 2016 Master Data Services。 此解決方案的主要目的為提升 SQL Server 資料庫所裝載 MDS 後端資料的高可用性及災害復原。

## <a name="introduction"></a>簡介


本文描述 AlwaysOn 可用性群組組態上所裝載 Master Data Service (MDS) 的解決方案。 本文描述如何在 SQL 2016 AlwaysOn 可用性群組 (AG) 上安裝及設定 SQL 2016 MDS。 此解決方案的主要目的為提升 SQL Server 資料庫所裝載 MDS 後端資料的高可用性及災害復原。

若要實作解決方案，您需要完成本文所涵蓋的下列工作。

1.  [安裝和設定 Windows Server 容錯移轉叢集 (WSFC)](#windows-server-failover-cluster-wsfc)。

2.  [設定 AlwaysOn AG](#sql-server-alwayson-availability-group)。

3.  [設定在 WSFC 節點上執行 MDS](#configure-mds-to-run-on-an-wsfc-node)。

上述各節將簡短介紹技術，並且後面接著指示。 如需技術的詳細資訊，請檢閱連結至每個章節的文件。

本文所述的這個解決方案是以 SQL Server AlwaysOn AG 為建置基礎，其中每個資料庫都有多個同步或非同步複本。 只有一個複本可接受交易 (接受使用者要求)。 這是主要複本。

每個複本都有自己的儲存體；因此，這個解決方案中沒有任何集中式共用儲存體。 發生影響主要複本的軟體失敗或硬體故障時，可以自動或根據組態和情況手動將主要複本容錯移轉至同步或非同步複本。 這確保資料庫的高可用性，且使用者中斷最小。

非同步複本通常裝載於主要複本資料中心的遠端資料中心。 如果損毀，可以將主要複本容錯移轉至另一個資料中心。 這確保資料庫的災害復原。

基於示範目的，本文所述的解決方案會使用下列版本的軟體。 除了潛在的微小差異之外，舊版本的運作方式應該都相同。

-   含伺服器容錯移轉叢集的 Windows Server 2012R2

-   含 Master Data Service 功能的 SQL Server 2016

此外，解決方案會使用 **MDS-HA1** 和 **MDS-HA2** 這兩個 VM 來裝載兩個複本。 只要 SQL Server AlwaysOn AG 支援，MDS 就不會限制您可使用的複本數。

本文假設您對 Windows Server、Windows Server 容錯移轉叢集、SQL Server AlwaysOn 和 SQL Server MDS 有基本了解。

## <a name="what-is-not-covered"></a>未涵蓋內容

本文件未涵蓋下列內容：

-   如何讓 IIS (即裝載 Master Data Service UI 的網頁伺服器) 高度可用且可在災害之後復原。 MDS 不會造成 IIS 的任何特定需求；因此，讓 IIS 高度可用且負載平衡的標準技術在這裡也可以運作良好。

-   如何使用 SQL Server AlwaysOn 容錯移轉 (FCI) 叢集，以支援 MDS 後端上的高可用性 (HA)。 SQL Server 容錯移轉叢集是不同的 HA 解決方案並由 SQL Server 正式支援，而且可以與 MDS 搭配運作。

-   如何使用 SQL Server 容錯移轉叢集 (FCI) 和 AlwaysOn AG 的混合式解決方案，以支援 MDS 後端上的 HA。 混合式解決方案確實可以與 MDS 搭配運作。

## <a name="design-consideration"></a>設計考量

圖 1 顯示大部分用於 AlwaysOn AG 的一般組態。 在主要資料中心內，有兩個含同步認可關聯性的複本，而且兩個複本都有 VOTE 權限。 這主要用來改善主要複本失敗時的 HA。

在災害復原資料中心內，具有的次要複本包含與主要複本的非同步認可關聯性。 此資料中心通常位在與主要資料中心不同的地區。 次要複本沒有 VOTE 權限。

如果主要資料中心發生災害 (例如火災、地震等等)，會使用此組態來達成復原。此組態可使用相當低的成本來達成 HA 和災害復原。

![一般 AlwaysOn 可用性群組組態](media/Fig1_TypicalConfig.png)

圖 1。 一般 AlwaysOn 可用性群組組態

如果您不需要考慮災害復原，則第二個資料中心內不需要有複本。 如果您需要改善 HA，則相同的主要資料中心內可以有更多的同步複本。

因此，請務必考量您的案例和需求，並選擇所需數目的非同步和同步複本，以及要放置它們的資料中心。

## <a name="windows-server-failover-cluster-wsfc"></a>Windows Server 容錯移轉叢集 (WSFC)

本節涵蓋下列工作。

1.  [安裝 Windows 容錯移轉叢集功能](#install-failover-cluster-feature)。

2.  [建立 Windows Server 容錯移轉叢集](#create-a-windows-server-failover-cluster)。

如上節中的圖 1 所示，本文所述的解決方案包含 Windows Server 容錯移轉叢集 (WSFC)。 我們需要設定 WSFC，因為 SQL AlwaysOn 依靠 WFSC 來進行失敗偵測和容錯移轉。

WSFC 是一種功能，可改善應用程式和服務的高可用性。 它包含一組獨立的 Windows Server 執行個體，而且這些執行個體上執行 Microsoft 容錯移轉叢集服務。 Windows Server 執行個體 (或偶而呼叫的節點) 會連接以彼此通訊，而且可以進行失敗偵測。 WSFC 提供失敗偵測和容錯移轉功能。 如果叢集中的節點或服務失敗，則會偵測到失敗，而且另一個節點自動或手動開始提供失敗節點上所裝載的服務。 因此，使用者只會發生最少的服務中斷，進而改善服務可用性。  

### <a name="prerequisites"></a>必要條件

Windows Server 作業系統安裝於所有執行個體上，並修補所有更新。

>[!NOTE] 
>**強烈建議**在所有執行個體上安裝相同的 Windows 版本和相同的功能集，避免任何潛在的不相容問題。

### <a name="install-failover-cluster-feature"></a>安裝容錯移轉叢集功能

針對每個 Windows Server 執行個體，完成下列步驟，以在每個執行個體上安裝 WSFC 功能。 您需要系統管理員權限。

1.  在 Windows Server 中開啟 [伺服器管理員]，然後按一下右窗格中的 [新增角色及功能]。 這將會啟動 [新增角色及功能精靈]。

2.  按一下 [下一步]，直到到達 [功能] 頁面。

3.  選取 [容錯移轉叢集] 核取方塊，然後按一下 [下一步] 完成安裝。 請參閱圖 2。

    如果系統要求您確認 [Add features that are required for Failover clustering]\(新增容錯移轉叢集所需的功能)，請按一下 [新增功能]。 請參閱圖 3。

    ![新增角色及功能精靈、容錯移轉叢集](media/Fig2_SelectFeatures.png)

    圖 2

    ![新增角色及功能精靈、容錯移轉叢集所需](media/Fig3_RequiredFeaturesFailover.png)

    圖 3

4.  在 [確認] 頁面上，按一下 [安裝] 以安裝容錯移轉叢集功能。

5.  在 [結果] 頁面上，確定已成功安裝所有項目，而未發生錯誤和警告。

### <a name="create-a-windows-server-failover-cluster"></a>建立 Windows Server 容錯移轉叢集節點

在所有執行個體上安裝 WSFC 功能之後，您可以設定 WSFC。 您應該只需要在一個節點上執行這項作業。

1.  在 Windows Server 中開啟 [伺服器管理員]，然後按一下右上角之 [工具] 功能表上的 [容錯移轉叢集管理員] 以啟動管理員。

2.  在 [容錯移轉叢集管理員] 中，按一下右窗格中的 [驗證組態]。 請參閱圖 4。

    ![容錯移轉叢集管理員、驗證組態](media/Fig4_ValidateConfig.png)

    圖 4

3.  在 [驗證組態精靈] 中，按一下 [下一步]。

4.  在 [選取伺服器或叢集] 對話方塊中，新增將裝載 SQL Server 的伺服器名稱，然後按一下 [下一步]。 請參閱圖 5。

    在此範例中，我們已新增兩個執行個體：MDS-HA1 和 MDS-HA2。

    ![驗證組態精靈、選取伺服器或叢集頁面](media/Fig5_AddServer.png)

    圖 5

5.  在 [測試選項] 頁面上，按一下 [執行所有測試]，然後按一下 [下一步]。

6.  按一下 [下一步] 完成驗證。

    [正在驗證] 頁面顯示進度，而 [摘要] 頁面顯示驗證摘要。 請參閱圖 6 和 7。

7.  在 [摘要] 頁面上，檢查是否有任何警告或錯誤訊息。

    錯誤必須予以修正。 不過，警告可能不會產生問題。 警告訊息表示「測試的項目可能符合需求，但您應該檢查一些事項」。 例如，圖 7 顯示「驗證磁碟存取延遲」警告，可能是因為磁碟暫時正在忙著處理其他工作，因此您可以忽略它。 您應該檢查線上文件中的每個警告和錯誤訊息，以取得詳細資料。 請參閱圖 7。
 
    ![驗證組態精靈、正在驗證頁面](media/Fig6_ValidationTests.png)

    圖 6

    ![驗證組態精靈、摘要頁面](media/Fig7_ValidationSummary.png)

    圖 7

8.  在 [摘要] 頁面上，確認已選取 [立即使用經過驗證的節點來建立叢集] 核取方塊，然後按一下 [完成] 啟動 [建立叢集精靈]。

9.  在 [建立叢集精靈] 中，按一下 [下一步]。

10. 在 [用於管理叢集的存取點] 頁面上，輸入 WSFC 叢集名稱，然後按一下 [下一步]。 在此範例中，我們使用 "MDS-HA" 作為叢集名稱。 請參閱圖 8。

    ![輸入叢集名稱](media/Fig8_EnterClusterName.png)

    圖 8

11. 繼續按一下 [下一步] 完成建立叢集。 [叢集 MDS-HA 的摘要] 區段會顯示叢集資訊。 請參閱圖 9。

    ![檢視叢集的摘要資訊](media/Fig9_ClusterSummary.png)

    圖 9

    如果您稍後需要新增節點，請按一下 [容錯移轉叢集管理員] 之右窗格中的 [新增節點] 動作。

注意：

-   並非所有 Windows Server 版本都會提供 WSFC 功能。 請確定您的版本有這項功能。

-   請確定您有適當的權限可在 Active Directory 中設定 WSFC。 如果有任何問題，請參閱 [Failover Cluster Step-by-Step Guide: Configure Accounts in Active Directory](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx) (容錯移轉叢集逐步指南：在 Active Directory 中設定帳戶)。

如需 WSFC 的詳細資訊，請參閱 [Failover Clusters](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx) (容錯移轉叢集)。

## <a name="sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn 可用性群組

本節涵蓋下列工作。

1.  [啟用 SQL Server AlwaysOn 可用性群組](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance)。

2.  [建立可用性群組](#create-an-availability-group)。

3.  [驗證和測試可用性群組](#validation-and-test-the-availability-group)。

SQL Server AlwaysOn 解決方案提供 SQL Server 資料庫的高可用性和災害復原。 AlwaysOn 有兩種可能的解決方案。
兩者都是以 WSFC 為建置基礎。

-   AlwaysOn 可用性群組 (AG)

-   AlwaysOn 容錯移轉叢集執行個體 (FCI)。

AG 可增強資料庫層級高可用性。 AG (一組使用者資料庫) 和其虛擬網路名稱會註冊為 WSFC 中的資源。

FCI 可增強執行個體層級高可用性。 SQL Server 服務和相關服務會註冊為 WSFC 中的資源。 此外，FCI 解決方案需要對稱共用磁碟儲存體 (例如 SAN 或 SMB 檔案共用)，而且 WFC 叢集中的所有節點都必須使用這些磁碟儲存體。


### <a name="prerequisites"></a>必要條件

-   在所有節點上安裝 SQL Server。 如需詳細資訊，請參閱[安裝 SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server)。

-   (建議) 在每個節點上安裝完全相同的 SQL Server 功能集和版本。 特別的是，您必須安裝 MDS。

-   (建議) 在每個 SQL Server 執行個體上使用相同的組態。 特別的是，必須在所有 SQL Server 執行個體上設定相同的伺服器定序。

-   (建議) 使用相同的服務帳戶執行每個 SQL Server 執行個體。 否則，您必須授與每個 SQL Server 執行個體的權限，確定 SQL Server 執行個體可以彼此通訊。

-   確認 Windows 防火牆設定可讓 SQL Server 執行個體彼此通訊。

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>在每個 SQL Server 執行個體上啟用 SQL Server AlwaysOn 可用性群組

1.  在 [SQL Server 組態管理員] 中，按一下左窗格中的 [SQL Server 服務]，並以滑鼠右鍵按一下右窗格中的 [SQL Server]，然後按一下 [屬性]。 請參閱圖 10。

    ![SQL Server 屬性視窗](media/Fig10_SQLServerProperties.png)

    圖 10

2.  在 [SQL Server (MSSQLSERVER) 屬性] 對話方塊中，按一下 [AlwaysOn 高可用性] 索引標籤，然後選取 [啟用 AlwaysOn 可用性群組] 核取方塊。 在 [Windows 容錯移轉叢集名稱] 文字方塊中顯示值時，請按一下 [確定] 繼續。 請參閱圖 11。

    ![啟用 AlwaysOn 可用性群組選項](media/Fig11_EnableAlwaysOn.png)

    圖 11

3.  顯示警告頁面時，請按一下 [確定] 繼續。 請參閱圖 12。

    ![確認停止並重新啟動服務](media/Fig12_WarningServiceStopStart.png)

    圖 12

4.  按一下 [重新啟動] 重新啟動 [SQL Server] 服務，並讓此變更生效。 請參閱圖 10。

>[!NOTE] 
>您可以使用 [SQL Server 組態管理員]，變更執行 SQL Server 服務的服務帳戶。 在 [SQL Server (MSSQLSERVER) 屬性] 對話方塊中，按一下 [登入] 索引標籤。 請參閱圖 11。

### <a name="create-an-availability-group"></a>建立可用性群組

在所有 SQL Server 執行個體上啟用 AlwaysOn 功能之後，即會建立包含一個節點上之 MDS 資料庫的新 AG。

AG 只能建立於現有資料庫上。 因此，您可以在一個節點上建立 MDS 資料庫，或建立暫存資料庫，再卸除暫存資料庫。 在此範例中，我們建立 emptyMDS 資料庫，並在此 MDS 資料庫上建立 AG。

1.  在節點上啟動 **SQL Server Management Studio** (**SSMS**)，並使用適當的認證連接至本機 SQL Server 執行個體。

2.  在 SSMS 中，開啟 [新增查詢] 視窗，並執行下列指令碼來建立空的資料庫。 將 C:\\temp 取代為您要用來執行完整備份的位置。

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >需要有完整資料庫備份，才能在這個資料庫上建立 AG。

3.  在物件總管中，展開 [AlwaysOn 高可用性] 資料夾，然後按一下 [新增可用性群組精靈] 啟動 [新增可用性群組精靈]。 請參閱圖 13。

    ![啟動新增可用性群組精靈](media/Fig13_AvailabilityGroupsFolder.png)

    圖 13

4.  在 [新增可用性群組精靈] 中，按一下 [下一步] 顯示 [指定名稱] 頁面。 鍵入 AG 的名稱，然後按一下 [下一步]。 請參閱圖 14。

    ![輸入可用性群組的名稱](media/Fig14_AvailabilityGroupName.png)

    圖 14

5.  在 [選取資料庫] 頁面上按一下您剛剛建立的資料庫，然後按一下 [下一步]。 請參閱圖 15。

    ![選取資料庫](media/Fig15_AvailabilityGroupSelectDatabase.png)

    圖 15

6.  在 [指定複本] 頁面上，按一下 [新增複本] 新增另一個複本。 此頁面已將目前的本機 SQL Server 執行個體列為複本。 請參閱圖 16。

7.  在 [連接到伺服器] 對話方塊中，新增適當的認證，然後按一下 [連接]。

    ![連接到 SQL Server 執行個體](media/Fig16_AddReplicaConnectServer.png)

    圖 16

    您現在應該會在清單中看到兩個複本。 重複此步驟，將其他節點新增為複本。 請參閱圖 17。

    ![檢視複本清單](media/Fig17_AvailabilityGroupSQLReplicas.png)

    圖 17

    針對每個複本，設定下列 [同步認可]、[自動容錯移轉] 和 [可讀取次要] 設定。 請參閱圖
17.

    **同步認可**：這確保如果在資料庫的主要複本上認可交易，則也會在所有其他同步複本上認可交易。 非同步認可不保證這點，而且可能會落後於主要複本。

    只有在兩個節點都位於相同的資料中心時，您通常才應該啟用同步認可。 如果它們位於不同的資料中心，則同步認可可能會降低資料庫效能。

    如果未選取此核取方塊，則會使用非同步認可。

    **自動容錯移轉**：如果選取自動容錯移轉，則在主要複本關閉時，AG 會自動容錯移轉至其次要複本。 這只能在具有同步認可的複本上啟用。

    **可讀取次要**：使用者預設無法連接到任何次要複本。 這可讓使用者連接到具有唯讀存取權的次要複本。

8.  在 [指定複本] 頁面上，按一下 [接聽程式] 索引標籤，然後執行下列動作。 請參閱圖 18。

    a.  按一下 [建立可用性群組接聽程式]，設定 MDS 資料庫連接的可用性群組接聽程式。

    b.  輸入 [接聽程式 DNS 名稱]，例如 MDSSQLServer。

    c.  在 [連接埠] 文字方塊中，輸入預設 SQL 連接埠 1433。

    d.  在 [網路模式] 文字方塊中輸入 DHCP，然後按一下 [下一步] 繼續。

    >[!NOTE] 
    >您可以選擇性選擇 [靜態 IP] 作為 [網路模式]，然後輸入靜態 IP。 您也可以輸入 1433 以外的連接埠。 

    ![設定接聽程式](media/Fig18_AvailabilityGroupCreateListener.png)

    圖 18

9.  在 [選取資料同步處理] 頁面上，按一下 [完整]，然後指定每個節點可存取的網路共用。 按 **[下一步]** ，繼續進行。 請參閱圖 19。

    此網路共用將用來儲存資料庫備份，以建立次要複本。 如果這不適用於您的組織，請選擇另一個資料同步處理喜好設定。 如需如何使用其他選項來建立次要複本，請參閱 [SQL Server 2016 AlwaysOn 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)。 圖 17 也會列出其他選項。

    ![設定資料同步處理](media/Fig19_AvailabilityGroupDataSync.png)

    圖 19 

10. 在 [驗證] 頁面上，確定所有驗證都成功通過，並更正任何錯誤。 按 **[下一步]** ，繼續進行。

11. 在 [摘要] 頁面上，檢閱所有組態設定，然後按一下 [完成]。 這將建立並設定可用性群組。

12. 在 [結果] 頁面上，確認已完成所有必要步驟。

### <a name="validation-and-test-the-availability-group"></a>驗證和測試可用性群組

1.  開啟 SSMS，並連接到您剛剛在[建立可用性群組](#create-an-availability-group)一節中建立的接聽程式 DNS 名稱。 在此範例中，它是 MDSSQLServer。

2.  在物件總管中，展開 [AlwaysOn 高可用性] 資料夾，並以滑鼠右鍵按一下您剛剛在[建立可用性群組](#create-an-availability-group)一節中建立的 AG，然後按一下 [顯示儀表板]。 請參閱圖 20。 新 AG 和其複本的狀態即會顯示。

    ![檢視儀表板](media/Fig20_ShowDashboard.png)

    圖 20 

3.  按一下 [容錯移轉]，以容錯移轉至同步複本和非同步複本。 這是要確認容錯移轉正確，未發生任何問題。

 AlwaysOn 安裝程式已完成。

如需 AlwaysOn 可用性群組的詳細資訊，請參閱 [SQL Server 2016 AlwaysOn 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)。

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>設定在 WSFC 節點上執行 MDS

本文所述的這個解決方案只需要在 WSFC 上執行的 MDS 後端資料庫。 只要 MDS 可以連接到 AG，就可以在 WSFC 或 WSFC 外部的節點上執行 MDS 的其他部分 (例如 Web 應用程式和 MDS 組態管理員)。

1.  開啟某個節點上的 [Master Data Service 組態管理員]，並按一下 [資料庫組態]，然後按一下 [建立資料庫] 啟動 [建立資料庫精靈]。

2.  在 [資料庫伺服器] 頁面的 [SQL Server 執行個體] 文字方塊中，鍵入 AG 接聽程式 DNS 名稱，並按一下 [測試連接]，然後按一下 [下一步]。 請參閱圖 21。

    ![使用 AG 接聽程式設定資料庫伺服器](media/Fig21_MDSDatabaseServerListener.png)

    圖 21

3.  在 [資料庫] 頁面上，鍵入您已在[建立可用性群組](#create-an-availability-group)一節中建立的資料庫名稱，然後按一下 [下一步]。 請參閱圖 22。

    ![建立和設定資料庫](media/Fig22_MDSCreateDatabase.png)

    圖 22

4.  完成 [建立資料庫精靈]。 如需詳細資訊，請參閱 [Master Data Services 安裝和組態](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)。

5.  按一下 [Master Data Service 組態管理員] 中的 [Web 應用程式] 設定 Web 應用程式，然後按一下 [套用] 以將設定套用至 MDS。 請參閱圖 23。 如需詳細資訊，請參閱 [Master Data Services 安裝和組態](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)。

    ![設定 Web 應用程式](media/Fig23_MDSWebApplication.png)

    圖 23

    MDS 安裝程式已完成。 您可以重複上述步驟，設定在所有節點上執行 MDS。 相同 AG 上的後端資料庫會相同。

6.  如果您先前建立暫存資料庫 (請參閱[建立可用性群組](#create-an-availability-group)一節) 來建立 AlwaysOn AG，則應該卸除暫存資料庫。

    如需 Master Data Service 的詳細資訊，請參閱 [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds)。

## <a name="conclusion"></a>結論

在這份技術白皮書，我們已經看到如何在 SQL Server AlwaysOn 可用性群組上安裝和設定 Master Data Services 後端資料庫。 此組態提供 Master Data Services 後端資料庫的高可用性和災害復原。 若要實作這項組態，您需要安裝和設定 Windows Server 容錯移轉叢集、SQL Server AlwaysOn 可用性群組和 Master Data Services。

## <a name="feedback"></a>意見反應

這份技術白皮書對您是否有幫助？ 請按一下文章頂端的 [意見] 提供您的意見反應。 

您的意見反應將協助我們改善未來發行的技術白皮書品質。 


