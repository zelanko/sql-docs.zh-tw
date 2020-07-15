---
title: SUSE：在 Linux 上設定 SQL Server 的可用性群組
titleSuffix: SQL Server
description: 了解如何在 SUSE Linux Enterprise Server (SLES) 上設定 SQL Server 可用性群組叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: c6c5ecf91349a94acb2b18156f28056ce04da3a1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892336"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>設定 SQL Server 可用性群組的 SLES 叢集

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本指南提供在 SUSE Linux Enterprise Server (SLES) 12 SP2 上，為 SQL Server 建立三個節點之叢集的指示。 為了提供高可用性，Linux 上的可用性群組需要三個節點，請參閱[可用性群組設定的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。 叢集層會以建置於 [Pacemaker](https://clusterlabs.org/) \(英文\) 之上的 SUSE [高可用性擴充功能 (HAE)](https://www.suse.com/products/highavailability) \(英文\) 為基礎。 

如需叢集設定、資源代理程式選項、管理、最佳做法和建議的詳細資訊，請參閱 [SUSE Linux Enterprise 高可用性擴充功能 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html) \(英文\)。

>[!NOTE]
>目前，SQL Server 與 Linux 上的 Pacemaker 之間的整合程度，尚不如 Windows 上的 WSFC。 Linux 上的 SQL Server 服務不是叢集感知的。 Pacemaker 會控制叢集資源的所有協調流程，包括可用性群組資源。 在 Linux 上，您不應該依賴 Always On 可用性群組動態管理檢視 (DMV)，其會提供 sys.dm_hadr_cluster 之類的叢集資訊。 此外，虛擬網路名稱為 WSFC 特定，Pacemaker 中沒有相同的對應項。 您仍然可以建立接聽程式，在容錯移轉之後用它來進行透明重新連線，但您將必須在 DNS 伺服器中，使用建立虛擬 IP 資源所用的 IP，手動註冊接聽程式名稱 (如下列各節所述)。

[!INCLUDE [bias-sensitive-term-t](../includes/bias-sensitive-term-t.md)]

## <a name="roadmap"></a>藍圖

建立可用性群組以取得高可用性的程序，在 Linux 伺服器和 Windows Server 容錯移轉叢集之間有所差異。 下列清單描述高階步驟： 

1. [在叢集節點上設定 SQL Server](sql-server-linux-setup.md)。

2. [建立可用性群組](sql-server-linux-availability-group-failover-ha.md)。 

3. 設定叢集資源管理員，例如 Pacemaker。 此文件包含這些指示。
   
   設定叢集資源管理員的方式取決於特定 Linux 發行版本。 

   >[!IMPORTANT]
   >生產環境需要 STONITH 這類隔離代理程式來取得高可用性。 此文章的範例不會使用隔離代理程式。 它們僅供測試和驗證使用。 
   
   >Pacemaker 叢集會使用隔離來將叢集回復為已知狀態。 設定隔離的方式取決於發行版本和環境。 目前，有些雲端環境中無法使用隔離。 請參閱 [SUSE Linux Enterprise 高可用性延伸模組](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing) \(英文\)。

5. [將可用性群組新增為叢集中的資源](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)。 

## <a name="prerequisites"></a>必要條件

若要完成下列端對端案例，您需要三部電腦來部署三個節點的叢集。 下列步驟概述如何設定這些伺服器。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>在每個叢集節點上安裝和設定作業系統 

第一個步驟是在叢集節點上設定作業系統。 在此逐步解說中，針對 HA 附加元件搭配有效的訂用帳戶來使用 SLES 12 SP2。

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>在每個叢集節點上安裝和設定 SQL Server 服務

1. 在所有節點上，安裝和設定 SQL Server 服務。 如需詳細指示，請參閱[安裝 Linux 上的 SQL Server](sql-server-linux-setup.md)。

1. 將一個節點指定為主要，並將其他節點指定為次要。 請在這整份指南中使用這些字詞。

1. 確定即將成為叢集一部分的節點可以彼此通訊。

   下列範例顯示 `/etc/hosts`，以及適用於三個節點 (名稱為 SLES1、SLES2 和 SLES3) 的新增項目。

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   所有叢集節點都必須能夠透過 SSH 互相存取。 `hb_report` 或 `crm_report` 之類的工具 (用於疑難排解) 和 Hawk 的 History Explorer 都要求節點之間的無密碼 SSH 存取，否則它們只能從目前的節點收集資料。 如果您使用非標準的 SSH 連接埠，請使用 -X 選項 (請參閱 `man` 頁面)。 例如，如果您的 SSH 連接埠是 3479，則以下列方式叫用 `crm_report`：

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   如需詳細資訊，請參閱 [SLES 管理指南 - 其他](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc) \(英文\) 一節。


## <a name="create-a-sql-server-login-for-pacemaker"></a>為 Pacemaker 建立 SQL Server 登入

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>設定 Always On 可用性群組

在 Linux 伺服器上，設定可用性群組，接著設定叢集資源。 若要設定可用性群組，請參閱[在 Linux 上設定 SQL Server 的 Always On 可用性群組](sql-server-linux-availability-group-configure-ha.md)。

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每個叢集節點上安裝和設定 Pacemaker

1. 安裝高可用性延伸模組

   如需參考，請參閱[安裝 SUSE Linux Enterprise Server 和高可用性延伸模組](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation) \(英文\)。

1. 在這兩個節點上安裝 SQL Server 資源代理程式套件。

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>設定第一個節點

   請參閱 [SLES 安裝指示](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node) \(英文\)

1. 以 `root` 登入您想要用來作為叢集節點的實體或虛擬機器。
2. 執行下列程式碼來啟動啟動程序指令碼：
   ```bash
   sudo ha-cluster-init
   ```

   如果 NTP 尚未設定為在開機時啟動，則會出現一則訊息。 

   如果您決定無論如何都要繼續，指令碼就會自動產生金鑰來進行 SSH 存取以及用於 Csync2 同步處理工具，並啟動這兩者所需的服務。 

3. 設定叢集通訊層 (Corosync)： 

   a. 輸入要繫結的網路位址。 根據預設，指令碼會建議使用 eth0 的網路位址。 或者，輸入不同的網路位址，例如 bond0 的位址。 

   b. 輸入多點傳送位址。 指令碼會建議一個隨機位址，讓您可用來作為預設值。 

   c. 輸入多點傳送連接埠。 指令碼會建議 5405 作為預設值。 

   d. 若要設定 `SBD ()`，請輸入您想要針對 SBD 使用的區塊裝置分割區的持續路徑。 路徑在叢集中的所有節點之間必須一致。 
   最後，指令碼將啟動 Pacemaker 服務，讓單一節點的叢集上線，並啟用 Web 管理介面 Hawk2。 用於 Hawk2 的 URL 會顯示於畫面上。 

4. 如需安裝程序的任何詳細資料，請查看 `/var/log/sleha-bootstrap.log`。 您現在有一個執行中的單一節點叢集。 使用 crm status 來檢查叢集狀態：

   ```bash
   sudo crm status
   ```

   您也可以使用 `crm configure show xml` 或 `crm configure show` 來查看叢集設定。

5. 啟動程序會使用密碼 linux 來建立名為 hacluster 的 Linux 使用者。 儘快以安全的密碼取代預設密碼： 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>將節點新增至現有叢集

如果您的叢集會搭配一或多個節點來執行，請使用 ha-cluster-join 啟動程序指令碼來新增更多叢集節點。 指令碼只需存取現有的叢集節點，並且將在目前的電腦上自動完成基本設定。 使用下列步驟：

如果您已經使用 `YaST` 叢集模組來設定現有的叢集節點，請先確定會完成下列先決條件，然後再執行 `ha-cluster-join`：
- 現有節點上的根使用者已備妥 SSH 金鑰以用於無密碼登入。 
- `Csync2` 設定於現有的節點上。 如需詳細資訊，請參閱「使用 YaST 設定 Csync2」。 

1. 以 root 身分登入應加入叢集的實體或虛擬機器。 
2. 執行下列程式碼來啟動啟動程序指令碼： 

   ```bash
   sudo ha-cluster-join
   ```

   如果 NTP 尚未設定為在開機時啟動，則會出現一則訊息。 

3. 如果您決定無論如何都要繼續，系統將提示您輸入現有節點的 IP 位址。 輸入 IP 位址。 

4. 如果您尚未在這兩部機器之間設定無密碼 SSH 存取，則系統也將提示您輸入現有節點的根密碼。 

   登入指定的節點之後，指令碼會複製 Corosync 設定、設定 SSH 和 `Csync2`，並將目前的電腦上線以成為新的叢集節點。 除此之外，它也會啟動 Hawk 所需的服務。 如果您已使用 `OCFS2` 設定共用儲存體，它也會自動建立適用於 `OCFS2` 檔案系統的掛接點目錄。 

5. 針對您要新增至叢集的所有機器重複上述步驟。 

6. 如需此程序的詳細資訊，請檢查 `/var/log/ha-cluster-bootstrap.log`。 

1. 使用 `sudo crm status` 來檢查叢集狀態。 如果您已成功加入第二個節點，則輸出將如下所示︰

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` 是虛擬 IP 叢集資源，它是在初始單節點叢集設定期間所設定的。

新增所有節點之後，檢查您是否需要調整全域叢集選項中的 no-quorum-policy。 這對於雙節點的叢集而言特別重要。 如需詳細資訊，請參閱「第 4.1.2 節，no-quorum-policy 選項」。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>設定 cluster-recheck-interval 叢集屬性

`cluster-recheck-interval` 表示輪詢間隔，叢集會依此間隔檢查資源參數、限制式或其他叢集選項中的變更。 如果複本中斷，叢集會嘗試以 `failure-timeout` 值和 `cluster-recheck-interval` 值所繫結的間隔重新啟動複本。 例如，如果 `failure-timeout` 設為 60 秒，而 `cluster-recheck-interval` 設為 120 秒，則會以大於 60 秒但小於 120 秒的間隔嘗試重新啟動。 建議您將 failure-timeout 設為 60 秒，並將 cluster-recheck-interval 設為大於 60 秒的值。 不建議將 cluster-recheck-interval 設為較小的值。

若要將屬性值更新為 `2 minutes`，請執行：

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 如果您已具備由 Pacemaker 叢集管理的可用性群組資源，請注意，所有使用最新可用 Pacemaker 套件 1.1.18-11.el7 的發行版本，都會在 start-failure-is-fatal 叢集設定值為 false 時，採用其行為變更。 此變更會影響容錯移轉工作流程。 如果主要複本發生中斷，則叢集應該要容錯移轉至其中一個可用的次要複本。 但是，使用者卻發現叢集繼續嘗試啟動失敗的主要複本。 如果該主要複本永遠無法上線 (因為永久中斷)，則叢集永遠不會容錯移轉至其他可用的次要複本。 此變更導致先前建議作為 start-failure-is-fatal 的設定不再有效，且必須將此設定還原回其預設值 `true`。 此外，您必須更新 AG 資源以包含 `failover-timeout` 屬性。 
>
>若要將屬性值更新為 `true`，請執行：
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>將您現有的 AG 資源屬性 `failure-timeout` 更新為 `60s` 執行 (將 `ag1` 取代為您的可用性群組資源名稱)： 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

如需 Pacemaker 叢集屬性的詳細資訊，請參閱[設定叢集資源](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html) \(英文\)。

## <a name="configure-fencing-stonith"></a>設定隔離 (STONITH)
Pacemaker 叢集廠商必須啟用 STONITH，並針對支援的叢集設定設好隔離裝置。 當叢集資源管理員無法判斷節點或節點上的資源狀態時，即會使用隔離來讓叢集再次進入已知狀態。

資源層級隔離主要可透過設定資源，確保在發生中斷時不會有資料損毀。 舉例來說，您可以搭配使用資源層級隔離與 DRBD (分散式複寫區塊裝置)，將節點上的磁碟標示為在通訊連結中斷時過期。

節點層級隔離可確保節點不會執行任何資源。 這是藉由重設節點來完成，且其 Pacemaker 的實作名稱為 STONITH ("shoot the other node in the head" 的簡稱)。 Pacemaker 支援各種隔離裝置，例如不斷電系統或伺服器的管理介面卡。

如需詳細資訊，請參閱

- [從頭開始 Pacemaker 叢集](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/) \(英文\)
- [Fencing and Stonith](https://clusterlabs.org/doc/crm_fencing.html) (隔離和 STONITH)
- [SUSE HA documentation:Fencing and STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html) (SUSE HA 文件：隔離和 STONITH)

在叢集初始化期間，如果未偵測到任何設定，即會停用 STONITH。 您稍後可執行下列命令來啟用它：

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>停用 STONITH 僅基於測試目的。 如果您打算在生產環境中使用 Pacemaker，則應該根據您的環境規劃 STONITH 實作，並讓它保持啟用狀態。 SUSE 並未針對任何雲端環境 (包括 Azure) 或 Hyper-V 提供隔離代理程式。 因此，叢集廠商不支援在這些環境中執行生產叢集。 我們正在為此差距尋找解決方案，以便在未來的版本中提供。

## <a name="configure-the-cluster-resources-for-sql-server"></a>設定 SQL Server 的叢集資源

請參閱 [SLES 管理指南](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config) \(英文\)

## <a name="enable-pacemaker"></a>啟用 Pacemaker

啟用 Pacemaker，讓它能夠自動啟動。

在叢集中的每個節點上執行下列命令。

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>建立可用性群組資源

下列命令會為可用性群組 [ag1] 的三個複本建立和設定可用性群組資源。 您必須在 SLES 中明確指定監視作業和逾時，這是因為逾時與工作負載高度相關，而且需要針對每個部署仔細調整。
在叢集的其中一個節點上執行命令：

1. 執行 `crm configure` 以開啟 crm 提示字元：

   ```bash
   sudo crm configure 
   ```

1. 在 crm 提示字元中，執行下列命令來設定資源屬性。

   ```bash
   primitive ag_cluster \
      ocf:mssql:ag \
      params ag_name="ag1" \
      meta failure-timeout=60s \
      op start timeout=60s \
      op stop timeout=60s \
      op promote timeout=60s \
      op demote timeout=10s \
      op monitor timeout=60s interval=10s \
      op monitor timeout=60s interval=11s role="Master" \
      op monitor timeout=60s interval=12s role="Slave" \
      op notify timeout=60s
   ms ms-ag_cluster ag_cluster \
      meta master-max="1" master-node-max="1" clone-max="3" \
     clone-node-max="1" notify="true" \
   commit
      ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>建立虛擬 IP 資源

如果您未在執行 `ha-cluster-init` 時建立虛擬 IP 資源，可立即建立此資源。 下列命令會建立虛擬 IP 資源。 以您網路中可用的位址取代 `<**0.0.0.0**>`，並以 CIDR 子網路遮罩中的位元數取代 `<**24**>`。 在一個節點上執行。

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>新增共置限制式
在 Pacemaker 叢集中，幾乎每個決策都是藉由比較分數來完成，例如，選擇應執行資源的位置。 分數是針對每個資源計算得來的，而叢集資源管理員會選擇對特定資源具有最高分數的節點 (如果節點對於某資源的分數為負值，此資源就無法在該節點上執行)。我們可以使用限制式來操控叢集的決策。 限制式具有分數。 如果限制式的分數低於 INFINITY，則系統僅會將其視為建議。 INFINITY 分數表示它是必要項目。 我們想要確保可用性群組的主要複本和虛擬 IP 資源都會在相同主機上執行，因此，會使用 INFINITY 分數來定義共置限制式。 

若要將虛擬 IP 的共置限制式設定為在與主要複本相同的節點上執行，請在一個節點上執行下列命令：

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>新增排序限制式
共置限制式具有隱含的排序限制式。 它會先移動虛擬 IP 資源，再移動可用性群組資源。 根據預設，事件的順序如下： 

1. 使用者會從節點 1 到節點 2，將資源移轉至可用性群組主要複本。
2. 虛擬 IP 資源會在節點 1 上停止。
3. 虛擬 IP 資源會在節點 2 上啟動。 此時，IP 位址會暫時指向節點 2，而節點 2 仍是容錯移轉前的次要複本。 
4. 節點 1 上的可用性群組主要複本已降級。
5. 節點 2 上的可用性群組已升級為主要複本。 

為了防止 IP 位址暫時指向含容錯移轉前之次要複本的節點，請新增排序限制式。 若要新增排序限制式，請在一個節點上執行下列命令： 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>當您設定叢集並將可用性群組新增為叢集資源之後，就無法使用 Transact-SQL 來容錯移轉可用性群組資源。 Linux 上的 SQL Server 叢集資源不會與作業系統緊密結合，因為其位於 Windows Server 容錯移轉叢集 (WSFC) 上。 SQL Server 服務不知道叢集是否存在。 所有協調流程都會透過叢集管理工具來完成。 在 SLES 中，請使用 `crm`。 

使用 `crm` 手動容錯移轉可用性群組。 請勿使用 Transact-SQL 來起始容錯移轉。 如需詳細資訊，請參閱[容錯移轉](sql-server-linux-availability-group-failover-ha.md#failover)。


如需詳細資訊，請參閱
- [管理叢集資源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm) \(英文\)   
- [HA 概念](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts) \(英文\)
- [Pacemaker 快速參考](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) \(英文\) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>後續步驟

[操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)
