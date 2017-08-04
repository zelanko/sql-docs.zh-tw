---
title: "高可用性和災害復原 Master Data services |Microsoft 文件"
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
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2afbf59101a0605dba2e79f09777160cb4de5cab
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>高可用性和災害復原 Master Data services

**摘要︰** 這篇文章說明 AlwaysOn 可用性群組設定上所裝載 Master Data Service (MDS) 的解決方案。 這篇文章說明如何在 SQL 2016 AlwaysOn 可用性群組 (AG) 上安裝及設定 SQL 2016 Master Data Services。 此解決方案的主要目的為提升 SQL Server 資料庫所裝載 MDS 後端資料的高可用性及災害復原。

## <a name="introduction"></a>簡介


本文說明解決方案的主要資料服務 (MDS) 位於 AlwaysOn 可用性群組組態。 本文描述如何安裝和設定上的 SQL 2016 AlwaysOn 可用性群組 (AG) 的 SQL 2016 MDS。 此解決方案的主要目的為提升 SQL Server 資料庫所裝載 MDS 後端資料的高可用性及災害復原。

若要實作解決方案，您必須完成本文章涵蓋下列工作。

1.  [安裝和設定註冊 Windows Server 容錯移轉叢集 (WSFC)](#windows-server-failover-cluster-wsfc)。

2.  [設定 AlwaysOn AG](#sql-server-alwayson-availability-group)。

3.  [設定 WSFC 節點上執行的 MDS](#configure-mds-to-run-on-an-wsfc-node)。

以上各節將簡短介紹的技術，後面接著的指示。 如需技術的詳細資訊，請檢閱連結至每個區段中的文件。

本文說明此解決方案是建立在 SQL Server AlwaysOn AG，其中每個資料庫都有多個同步或非同步複本之上。 只有一個複本接受的交易 （接受使用者要求）。 這是主要複本。

每個複本都有自己的儲存體，因此這個方案中沒有任何集中式的共用存放裝置。 發生時軟體失敗或硬體失敗影響主要複本，可以自動或手動方式根據組態和情況下為同步或非同步複本容錯移轉的主要複本。 這會確保使用者最小中斷資料庫的高可用性。

非同步複本通常會在主要複本的資料中心的遠端資料中心裝載。 如果損毀的情況下，主要複本可以容錯移轉至另一個資料中心。 這可確保資料庫的災害復原。

基於示範目的，本文章中所述的解決方案會使用下列版本的軟體。 較舊版本的運作方式應該與潛在微小差異之處。

-   與伺服器容錯移轉叢集的 Windows Server 2012R2

-   SQL Server 2016 Master Data Services 功能

此外，解決方案會使用兩個 Vm， **MDS HA1**和**MDS HA2**、 要裝載兩個複本。 只要它支援 SQL Server AlwaysOn AG，MDS 將不會限制您可以使用幾個複本。

本文假設您有 Windows Server、 Windows Server 容錯移轉叢集、 SQL Server AlwaysOn、 和 SQL Server MDS 相關的基本知識。

## <a name="what-is-not-covered"></a>未涵蓋

本文件未涵蓋下列：

-   如何讓 IIS web 伺服器裝載主要資料服務的 UI，高度可用且可在損毀之後復原。 MDS 不會造成任何特定的需求，在 IIS 上，以便讓 IIS 成為高可用性和負載平衡的標準技術可以在這裡以及。

-   如何使用 SQL Server AlwaysOn 容錯移轉 (FCI) 叢集以支援高可用性 (HA) 在 MDS 後端。 SQL Server 容錯移轉叢集不同的 HA 解決方案，而正式支援 SQL server，它與 MDS 運作。

-   如何使用混合式解決方案的 SQL Server 容錯移轉叢集 (FCI) 與 AlwaysOn AG 支援 HA MDS 後端上。 使用 MDS 運作混合式解決方案。

## <a name="design-consideration"></a>設計考量

圖 1 顯示的大部分用於 AlwaysOn AG 的一般組態。 在主要資料中心，有兩個複本的同步認可的關聯性，而且兩個複本投票權限。 這主要用來改善主要複本失敗時的高可用性。

在災害復原資料中心，沒有次要複本與主要與一個非同步認可的關聯。 此資料中心通常是不同於主要資料中心地區。 次要複本沒有投票權限。

此組態用來達成復原，萬一主要資料中心發生災害，例如引發地震、 等等。組態會達到這兩個高可用性和災害復原與相對較低的成本。

![AlwaysOn 可用性群組的一般設定](media/Fig1_TypicalConfig.png)

圖 1。 典型的 AlwaysOn 可用性群組組態

如果您不需要考慮災害復原，您不需要具有第二個資料中心內的複本。 如果您需要增進高可用性，您可以使用相同的主要資料中心有更多的同步複本。

因此，請考量您的案例和需求，並選擇幾個非同步和同步複本中，您需要以及哪個資料中心，您應該將它們放在重要。

## <a name="windows-server-failover-cluster-wsfc"></a>Windows Server 容錯移轉叢集 (WSFC)

本章節涵蓋下列工作。

1.  [安裝 Windows 容錯移轉叢集功能](#install-failover-cluster-feature)。

2.  [建立 Windows Server 容錯移轉叢集](#create-a-windows-server-failover-cluster)。

上一節中的圖 1 所示，在本文中所描述的方案包含 Windows Server 容錯移轉叢集 (WSFC)。 我們需要設定 WSFC，因為 SQL AlwaysOn 取決於 WFSC 失敗偵測和容錯移轉。

WSFC 是以改善應用程式和服務的高可用性的功能。 它使用這些執行個體上執行 Microsoft 容錯移轉叢集服務組成的獨立 windows 伺服器執行個體群組。 Windows 伺服器執行個體 (或節點為有時稱為)，而它們可以彼此通訊，失敗偵測可能連線。 WSFC 提供失敗偵測和容錯移轉功能。 如果節點或服務失敗叢集中，然後偵測到失敗，並且另一個節點自動或手動開始提供失敗的節點上裝載的服務。 因此，使用者只發生在服務中，最少中斷的情況，進而改善服務可用性。  

### <a name="prerequisites"></a>필수 구성 요소

Windows Server 作業系統上已安裝所有的執行個體，且所有更新已完成都修補。

>[!NOTE] 
>它是**強烈建議**安裝相同的 Windows 版本以及所有執行個體上設定，以避免任何潛在的不相容問題的相同功能。

### <a name="install-failover-cluster-feature"></a>安裝容錯移轉叢集功能

完成下列步驟安裝 WSFC 功能，每個執行個體上每個 Windows 伺服器執行個體。 您需要系統管理員權限。

1.  開啟**伺服器管理員**中 Windows Server 中，按一下**新增角色及功能**右窗格中。 這樣就會啟動**新增角色及功能精靈**。

2.  按一下**下一步**直到到達**功能**頁面。

3.  選取**容錯移轉叢集**核取方塊，然後按一下 **下一步**完成安裝。 請參閱圖 2。

    如果詢問您確認是否要**新增所需的容錯移轉叢集功能**，按一下 **新增功能**。 請參閱圖 3。

    ![新增角色及功能精靈，容錯移轉叢集](media/Fig2_SelectFeatures.png)

    圖 2

    ![新增角色及功能精靈，所需的容錯移轉叢集](media/Fig3_RequiredFeaturesFailover.png)

    圖 3

4.  在**確認**頁面上，按一下**安裝**安裝容錯移轉叢集功能。

5.  在**結果**頁面上，確定所有項目已成功安裝不含錯誤和警告。

### <a name="create-a-windows-server-failover-cluster"></a>建立 Windows Server 容錯移轉叢集節點

WSFC 功能安裝於所有的執行個體之後，您可以設定 WSFC。 此外，您應該只需要一個節點上執行這項操作。

1.  開啟**伺服器管理員**中 Windows Server 中，按一下**容錯移轉叢集管理員**上**工具**右邊角落以啟動管理員 功能表。

2.  在**容錯移轉叢集管理員**，按一下 **驗證設定**右窗格中。 請參閱圖 4。

    ![容錯移轉叢集管理員 中，驗證組態](media/Fig4_ValidateConfig.png)

    圖 4

3.  在**驗證設定****精靈**，按一下 **下一步**。

4.  在**選取伺服器或叢集**對話方塊方塊中，將伺服器名稱，將裝載 SQL Server，然後按一下 新增**下一步**。 請參閱圖 5。

    在此範例中，我們會加入兩個執行個體，MDS HA1 和 MDS HA2。

    ![驗證設定精靈中，選取伺服器或叢集 頁面](media/Fig5_AddServer.png)

    圖 5

5.  在**測試選項**頁面上，按一下**執行所有測試**，然後按一下 **下一步**。

6.  按一下**下一步**完成驗證。

    **Validating**頁面會顯示進度，而**摘要**頁面會顯示驗證摘要。 請參閱圖 6 和 7。

7.  在**摘要**頁面上，檢查是否有任何警告或錯誤訊息。

    必須修復的錯誤。 不過，警告可能不會產生問題。 警告訊息表示 「 測試項目可能會符合需求，但您應該檢查有"。 例如，圖 7 顯示 「 驗證磁碟存取延遲 」 警告，可能是因為磁碟正在忙碌於其他工作，和您可能會忽略它。 您應該檢查線上文件中的每個警告和錯誤訊息，如需詳細資訊。 請參閱圖 7。
 
    ![驗證設定精靈，驗證中 頁面](media/Fig6_ValidationTests.png)

    圖 6

    ![驗證設定精靈 摘要頁面](media/Fig7_ValidationSummary.png)

    圖 7

8.  在**摘要**頁面上，確認**立即使用經過驗證的節點來建立叢集**核取方塊已選取，然後按一下**完成**啟動**建立叢集****精靈**。

9.  在**建立叢集****精靈**，按一下 **下一步**。

10. 在**用於管理叢集的存取點**頁面上，輸入 WSFC 叢集名稱，然後按一下**下一步**。 在此範例中，我們使用 「 MDS-HA"做為叢集的名稱。 請參閱圖 8。

    ![輸入叢集名稱](media/Fig8_EnterClusterName.png)

    圖 8

11. 繼續按**下一步**完成建立叢集。 **摘要的叢集 MDS-HA**區段會顯示叢集資訊。 請參閱圖 9。

    ![檢視叢集的摘要資訊](media/Fig9_ClusterSummary.png)

    圖 9

    如果您要將節點加入之後，請按一下**加入節點**在右窗格中的動作**容錯移轉叢集管理員**。

注意：

-   WSFC 功能可能無法使用所有 Windows Server 版本上。 請確定您的版本有這項功能。

-   請確定您有 active directory 中設定 WSFC 適當的權限。 如果有任何問題，請參閱[容錯移轉叢集逐步指南： 設定 Active Directory 中帳戶](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx)。

如需詳細 WSFC 相關資訊，請參閱[容錯移轉叢集](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx)。

## <a name="sql-server-alwayson-availability-group"></a>SQL Server AlwaysOn 可用性群組

本章節涵蓋下列工作。

1.  [啟用 SQL Server AlwaysOn 可用性群組](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance)。

2.  [建立可用性群組](#create-an-availability-group)。

3.  [驗證並測試可用性群組](#validation-and-test-the-availability-group)。

Sql Server AlwaysOn 解決方案提供高可用性和災害復原的 sql Server 資料庫。 AlwaysOn 有兩個可能的解決方案。
兩者的 WSFC 上建立。

-   AlwaysOn 可用性群組 (AG)

-   AlwaysOn 容錯移轉叢集執行個體 (FCI)。

AG 增強資料庫層級高可用性。 AG （一組使用者資料庫） 和其虛擬網路名稱會註冊為 WSFC 中的資源。

FCI 增強的執行個體層級高可用性。 SQL Server 服務和相關的服務會註冊為 WSFC 中的資源。 此外，FCI 方案需要對稱共用的磁碟存放裝置，例如 SAN 或 SMB 檔案共用必須是 WFC 叢集中的所有節點都可使用。


### <a name="prerequisites"></a>필수 구성 요소

-   所有節點上安裝 SQL Server。 如需詳細資訊，請參閱[安裝 SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server)。

-   （建議選項）每個節點上安裝的完全相同的 SQL Server 功能集和版本。 特別是，您必須安裝 MDS。

-   （建議選項）每個 SQL Server 執行個體上使用相同的設定。 特別是，所有 SQL Server 執行個體上必須設定相同的伺服器定序。

-   （建議選項）您可以使用相同的服務帳戶執行每個 SQL Server 執行個體。 否則，您必須授與每個 SQL Server 執行個體的權限，並確定 SQL Server 執行個體可以與對方進行通訊。

-   確認 Windows 防火牆設定可讓 SQL Server 執行個體，來與對方進行通訊。

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>啟用 SQL Server AlwaysOn 可用性群組每個 SQL Server 執行個體

1.  在**SQL Server 組態管理員**按一下**SQL Server 服務**在左窗格中，以滑鼠右鍵按一下**SQL Server**在右窗格中，然後按一下**屬性**。 請參閱圖 10。

    ![SQL Server 屬性 視窗](media/Fig10_SQLServerProperties.png)

    圖 10

2.  在**SQL Server (MSSQLSERVER)** **屬性**對話方塊中，按一下  **AlwaysOn 高可用性**索引標籤，然後選取**啟用 AlwaysOn 可用性群組**核取方塊。 當值會顯示在**Windows 容錯移轉叢集名稱** 文字方塊中，按一下**確定**才能繼續。 圖 11，請參閱。

    ![啟用 AlwaysOn 可用性群組選項](media/Fig11_EnableAlwaysOn.png)

    圖 11

3.  當顯示警告頁面上時，按一下**確定**才能繼續。 請參閱圖 12。

    ![確認停止並重新啟動服務](media/Fig12_WarningServiceStopStart.png)

    圖 12

4.  按一下**重新啟動**、 重新啟動**SQL Server**服務，並讓此變更生效。 請參閱圖 10。

>[!NOTE] 
>您可以變更執行 SQL Server 服務使用的服務帳戶**SQL Server 組態管理員**。 按一下**登入**索引標籤中**SQL Server (MSSQLSERVER)** **屬性** 對話方塊。 圖 11，請參閱。

### <a name="create-an-availability-group"></a>建立可用性群組

在所有 SQL Server 執行個體啟用 AlwaysOn 功能後，您會建立包含其中一個節點上的 MDS 資料庫的新 AG。

AG 才可以建立現有的資料庫。 因此可能是 MDS 資料庫建立一個節點上，或建立暫時的資料庫，再卸除暫存資料庫。 在此範例中，我們建立 emptyMDS 資料庫以及建立 AG 這個 MDS 資料庫。

1.  啟動**SQL Server Management Studio** (**SSMS**) 節點上，並連接到具有適當認證的本機 SQL Server 執行個體。

2.  在 SSMS 中，開啟**新查詢**視窗並執行下列指令碼來建立空的資料庫。 取代 c:\\暫存位置與您想要使用執行完整備份。

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >完整資料庫備份是必要的這個資料庫上建立 AG。

3.  在**物件總管 中**，依序展開**AlwaysOn 高可用性**資料夾，然後按一下**新增可用性群組精靈**啟動**新增可用性群組精靈**。 請參閱圖 13。

    ![啟動新增可用性群組精靈](media/Fig13_AvailabilityGroupsFolder.png)

    圖 13

4.  在**新增可用性群組**精靈 中，按一下**下一步**顯示**指定名稱**頁面。 輸入 AG 的名稱，然後按一下**下一步**。 請參閱圖 14。

    ![請輸入可用性群組的名稱](media/Fig14_AvailabilityGroupName.png)

    圖 14

5.  按一下您剛建立的資料庫**選取資料庫**頁面，然後再按一下**下一步**。 請參閱圖 15。

    ![選取的資料庫](media/Fig15_AvailabilityGroupSelectDatabase.png)

    圖 15

6.  在**指定複本**頁面上，按一下以加入另一個複本**將複本加入**。 此頁面已列出目前的本機 SQL Server 執行個體，為複本。 請參閱圖 16。

7.  在**連接到伺服器**對話方塊，加入適當的認證，然後按一下**連接**。

    ![連接到 SQL Server 執行個體](media/Fig16_AddReplicaConnectServer.png)

    圖 16

    現在您應該會看到兩個清單中的複本。 重複此步驟，新增其他節點，做為複本。 請參閱圖 17。

    ![檢視的複本清單](media/Fig17_AvailabilityGroupSQLReplicas.png)

    圖 17

    針對每個複本，設定下列各項**同步認可**，**自動容錯移轉**，和**可讀取次要複本**設定。 請參閱圖
17.

    **同步認可**： 這可以確保，如果資料庫的主要複本上認可交易，然後認可交易是也在其他所有同步複本上。 非同步認可並不保證，並可能會落後主要複本。

    只有當兩個節點位於相同的資料中心，您通常應該啟用同步認可。 如果它們是在不同資料中心，同步認可可能會降低資料庫效能。

    如果未選取此核取方塊，則會使用非同步認可。

    **自動容錯移轉：**時的主要複本已關閉，AG 會自動容錯移轉至其的次要複本選取自動容錯移轉時。 這只使用同步認可複本上啟用。

    **可讀取的次要複本：**根據預設，使用者就無法連接到任何次要複本。 這會讓使用者連線至具有唯讀存取的次要複本。

8.  在**指定複本**頁面上，按一下**接聽程式**索引標籤，然後執行下列動作。 請參閱圖 18。

    a.  按一下**建立可用性群組接聽程式**設定 MDS 資料庫連接的可用性群組接聽程式。

    b.  輸入**接聽程式 DNS 名稱**，例如 MDSSQLServer。

    c.  在中輸入預設 SQL 通訊埠 1433，**連接埠**文字方塊。

    d.  輸入中的 DHCP**網路模式**文字方塊，然後再按一下**下一步**才能繼續。

    >[!NOTE] 
    >（選擇性） 您可以選擇 [靜態 IP] 作為**網路模式**並輸入靜態 ip 位址。 您也可以輸入 1433年以外的連接埠。 

    ![設定接聽程式](media/Fig18_AvailabilityGroupCreateListener.png)

    圖 18

9.  在**選取資料同步處理**頁面上，按一下**完整**，並指定每個節點都可以存取網路共用。 按 **[下一步]** ，繼續進行。 請參閱圖 19。

    此網路共用將用來儲存資料庫備份來建立次要複本。 如果這不是適用於您的組織，請選擇另一個資料同步處理喜好設定。 請參閱[SQL Server 2016 AlwaysOn 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)如何使用其他選項來建立次要複本。 圖 17 也會列出其他選項。

    ![設定資料同步處理](media/Fig19_AvailabilityGroupDataSync.png)

    圖 19 

10. 在**驗證**頁面上，確定所有驗證傳遞成功，並更正任何錯誤。 按 **[下一步]** ，繼續進行。

11. 在**摘要**頁面上，檢閱所有組態設定，然後按一下**完成**。 這會建立可用性群組，並加以設定。

12. 在**結果**頁面上，確認已完成所有必要的步驟。

### <a name="validation-and-test-the-availability-group"></a>驗證和測試可用性群組

1.  開啟 SSMS 並連接到您在建立接聽程式 DNS 名稱[建立可用性群組](#create-an-availability-group)> 一節。 在此範例中，它可以是 MDSSQLServer。

2.  在**物件總管 中**，依序展開**AlwaysOn 高可用性**資料夾中，以滑鼠右鍵按一下您剛的 AG 中建立[建立可用性群組](#create-an-availability-group)區段，然後再按一下**顯示儀表板**。 圖 20，請參閱。 新增 AG 和其複本的狀態會顯示。

    ![檢視儀表板](media/Fig20_ShowDashboard.png)

    圖 20 

3.  按一下**容錯移轉**進行容錯移轉至同步複本而在非同步複本。 這是要確認容錯移轉正確，不需要發生問題。

 AlwaysOn 安裝程式已完成。

如需有關 AlwaysOn 可用性群組的詳細資訊，請參閱[SQL Server 2016 AlwaysOn 可用性群組](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)。

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>設定 MDS WSFC 節點上執行

本文章中呈現此解決方案只需要執行 WSFC 上的 MDS 後端資料庫。 MDS 的其他部分，例如 web 應用程式與 MDS 組態管理員中，可以執行在節點 WSFC 之內或之外 WSFC 中，只要 MDS 也可以連接到 AG。

1.  開啟**Master Data Service 組態管理員**一個節點上，按一下 **資料庫組態**，然後按一下  **Create Database**啟動**建立資料庫精靈**。

2.  上**資料庫伺服器**頁面上，輸入中的 AG 接聽程式 DNS 名稱**SQL Server 執行個體** 文字方塊中，按一下 **測試連接**，然後按一下 **下一步**。 請參閱圖 21。

    ![AG 接聽程式與設定資料庫伺服器](media/Fig21_MDSDatabaseServerListener.png)

    圖 21

3.  在**資料庫**頁面上，輸入您在建立資料庫的名稱[建立可用性群組](#create-an-availability-group)區段，然後再按一下**下一步**。 請參閱圖 22。

    ![建立和設定資料庫](media/Fig22_MDSCreateDatabase.png)

    圖 22

4.  完成**建立資料庫****精靈**。 如需詳細資訊，請參閱[Master Data Services 安裝和設定](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)。

5.  按一下**Web 應用程式**中**Master Data Service 組態管理員**來設定 Web 應用程式，然後按一下**套用**將設定套用至 MDS。 請參閱圖 23。 如需詳細資訊，請參閱[Master Data Services 安裝和設定](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration)。

    ![設定 Web 應用程式](media/Fig23_MDSWebApplication.png)

    圖 23

    MDS 安裝已完成。 您可以重複前面的步驟，設定 MDS 的所有節點上執行。 在同一個 AG 相同後端資料庫。

6.  如果您先前建立的暫存資料庫 (請參閱[建立可用性群組](#create-an-availability-group)> 一節) 若要建立 AlwaysOn AG，然後您應該要卸除暫存資料庫

    如需 Master Data Service 的詳細資訊，請參閱[Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds)。

## <a name="conclusion"></a>結論

在這份技術白皮書，我們已經看到如何安裝及設定 Master Data Services 的後端資料庫在 SQL Server AlwaysOn 可用性群組。 此設定 Master Data Services 的後端資料庫提供高可用性和災害復原。 若要實作這項設定，您需要安裝及設定 Windows Server 容錯移轉叢集，SQL Server AlwaysOn 可用性群組和 Master Data Services。

## <a name="feedback"></a>意見反應

這份技術白皮書對您是否有幫助？ 請提供您的意見反應，即可**註解**頂端的發行項。 

您的意見反應將協助我們改善我們發行的技術白皮書品質。 


