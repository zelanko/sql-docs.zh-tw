---
title: 設定可用性群組的 Ubuntu 叢集
titleSuffix: SQL Server on Linux
description: 了解如何在 Ubuntu 上建立三節點叢集，並將先前建立的可用性群組資源新增至叢集。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 52511077d0f4f0da4db0f32dc057b614830587ec
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784858"
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>設定 Ubuntu 叢集和可用性群組資源

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本文件說明如何在 Ubuntu 上建立三個節點的叢集，並將先前建立的可用性群組新增為叢集中資源。 為了提供高可用性，Linux 上的可用性群組需要三個節點，請參閱[可用性群組設定的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。

> [!NOTE] 
> 目前，SQL Server 與 Linux 上的 Pacemaker 之間的整合程度，尚不如 Windows 上的 WSFC。 SQL 不會知道叢集是否存在，所有協調流程都是從外而入，且 Pacemaker 會以獨立執行個體形式來控制服務。 此外，虛擬網路名稱為 WSFC 特定，Pacemaker 中沒有相同的對應項。 查詢叢集資訊的 Always On 動態管理檢視會傳回空的資料列。 您仍然可以建立接聽程式，在容錯移轉之後用它來進行透明重新連線，但您必須在 DNS 伺服器中使用建立虛擬 IP 資源所用的 IP 來手動註冊接聽程式名稱 (如下列各節所述)。

下列各節將逐步解說設定容錯移轉叢集解決方案的步驟。 

## <a name="roadmap"></a>藍圖

在 Linux 伺服器上建立可用性群組以提供高可用性的步驟，與 Windows Server 容錯移轉叢集上的步驟不同。 下列清單描述高階步驟： 

1. [在叢集節點上設定 SQL Server](sql-server-linux-setup.md)。

2. [建立可用性群組](sql-server-linux-availability-group-configure-ha.md)。 

3. 設定叢集資源管理員，例如 Pacemaker。 此文件包含這些指示。
   
   設定叢集資源管理員的方式取決於特定 Linux 發行版本。 

   >[!IMPORTANT]
   >生產環境需要 STONITH 這類隔離代理程式來取得高可用性。 此文件的示範不會使用隔離代理程式。 這些示範僅適用於測試和驗證。 
   >
   >Linux 叢集會使用隔離功能將叢集回復為已知的狀態。 設定隔離的方式取決於發行版本和環境。 目前，有些雲端環境中無法使用隔離。 如需詳細資訊，請參閱 [RHEL 高可用性叢集的支援原則 - 虛擬化平台](https://access.redhat.com/articles/29440)。
   >
   >隔離通常是在作業系統上實作且相依於環境。 在作業系統散發者文件中尋找隔離的指示。

5.  [將可用性群組新增為叢集中的資源](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每個叢集節點上安裝和設定 Pacemaker

1. 在所有節點上，開啟防火牆連接埠。 開啟 Pacemaker 高可用性服務、SQL Server 執行個體和可用性群組端點的連接埠。 執行 SQL Server 的伺服器預設 TCP 通訊埠為 1433。  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   或者，您可以直接停用防火牆：
        
   ```bash
   sudo ufw disable
   ```

1. 安裝 Pacemaker 套件。 在所有節點上，執行下列命令：

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. 設定安裝 Pacemaker 和 Corosync 封裝時建立的預設使用者密碼。 在所有節點上使用相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>啟用並啟動 pcsd 服務和 Pacemaker

下列命令會啟用並啟動 pcsd 服務和 Pacemaker。 在所有節點上執行。 這可讓節點在重新啟動後重新加入叢集。 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Enable pacemaker 命令可能會完成並出現錯誤 'pacemaker Default-Start contains no runlevels, aborting' (pacemaker Default-Start 不含任何執行層級，即將中止)。 這不會有影響，叢集設定仍可繼續進行。 

## <a name="create-the-cluster"></a>建立叢集

1. 從所有節點移除任何現有的叢集設定。 

   執行 'sudo apt-get install pcs' 會同時安裝 pacemaker、corosync 和 pcs 並開始執行所有 3 項服務。  啟動 corosync 會產生範本 '/etc/cluster/corosync.conf' 檔案。  若要讓後續步驟成功，這個檔案不應該存在；因此，解決辦法是停止 pacemaker/corosync 並刪除 '/etc/cluster/corosync.conf'，即可順利完成後續步驟。 'pcs cluster destroy' 會進行相同的作業，因此您可以將它作為一次性的初始叢集設定步驟。
   
   下列命令會移除任何現有的叢集設定檔，並停止所有叢集服務。 這麼做會永久終結叢集。 在生產階段前環境中，請將它作為第一個步驟來執行。 請注意，'pcs cluster destroy' 已停用 Pacemaker 服務，必須重新啟用。 在所有節點上執行下列命令。
   
   >[!WARNING]
   >此命令會終結任何現有的叢集資源。

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. 建立叢集。 

   >[!WARNING]
   >由於叢集廠商正在調查的已知問題，啟動叢集 ('pcs cluster start') 會失敗並出現下列錯誤。 這是因為 /etc/corosync/corosync.conf 中所設的記錄檔 (在執行叢集設定命令時建立) 有誤所致。 若要解決此問題，請將記錄檔變更為 /var/log/corosync/corosync.log。 或者，您可以建立 /var/log/cluster/corosync.log 檔案。
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
下列命令會建立三個節點的叢集。 執行指令碼之前，請取代 `< ... >` 之間的值。 在主要節點上執行下列命令。 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2...> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >如果您先前已在相同節點上設定叢集，執行 'pcs cluster setup' 時需要使用 '--force' 選項。 請注意，這相當於執行 'pcs cluster destroy'，而且需要使用 'sudo systemctl enable pacemaker' 來重新啟用 Pacemaker 服務。


## <a name="configure-fencing-stonith"></a>設定隔離 (STONITH)

Pacemaker 叢集廠商必須啟用 STONITH，並針對支援的叢集設定設好隔離裝置。 當叢集資源管理員無法判斷節點或節點上的資源狀態時，即會使用隔離來讓叢集再次進入已知狀態。 資源層級隔離主要可透過設定資源，確保在發生中斷時不會有資料損毀。 舉例來說，您可以搭配使用資源層級隔離與 DRBD (分散式複寫區塊裝置)，將節點上的磁碟標示為在通訊連結中斷時過期。 節點層級隔離可確保節點不會執行任何資源。 這是藉由重設節點來完成，且其 Pacemaker 的實作名稱為 STONITH ("shoot the other node in the head" 的簡稱)。 Pacemaker 支援各種隔離裝置，例如不斷電系統或伺服器的管理介面卡。 如需詳細資訊，請參閱 [Pacemaker Clusters from Scratch](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/) (從頭開始使用 Pacemaker 叢集) 和 [Fencing and Stonith](https://clusterlabs.org/doc/crm_fencing.html) (隔離與 Stonith) 

由於節點層級隔離設定主要取決於您的環境，所以我們會在本教學課程中將其停用 (可在稍後設定)。 在主要節點上執行下列指令碼： 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>停用 STONITH 僅基於測試目的。 如果您打算在生產環境中使用 Pacemaker，則應該根據您的環境規劃 STONITH 實作，並讓它保持啟用狀態。 如需任何特定散發的隔離代理程式相關資訊，請連絡作業系統廠商。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>設定 cluster-recheck-interval 叢集屬性

`cluster-recheck-interval` 表示輪詢間隔，叢集會依此間隔檢查資源參數、限制式或其他叢集選項中的變更。 如果複本中斷，叢集會嘗試以 `failure-timeout` 值和 `cluster-recheck-interval` 值所繫結的間隔重新啟動複本。 例如，如果 `failure-timeout` 設為 60 秒，而 `cluster-recheck-interval` 設為 120 秒，則會以大於 60 秒但小於 120 秒的間隔嘗試重新啟動。 建議您將 failure-timeout 設為 60 秒，並將 cluster-recheck-interval 設為大於 60 秒的值。 不建議將 cluster-recheck-interval 設為較小的值。

若要將屬性值更新為 `2 minutes`，請執行：

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 如果您已具備由 Pacemaker 叢集管理的可用性群組資源，請注意，所有使用最新可用 Pacemaker 套件 1.1.18-11.el7 的發行版本，都會在 start-failure-is-fatal 叢集設定值為 false 時，採用其行為變更。 此變更會影響容錯移轉工作流程。 如果主要複本發生中斷，則叢集應該要容錯移轉至其中一個可用的次要複本。 但是，使用者卻發現叢集繼續嘗試啟動失敗的主要複本。 如果該主要複本永遠無法上線 (因為永久中斷)，則叢集永遠不會容錯移轉至其他可用的次要複本。 此變更導致先前建議作為 start-failure-is-fatal 的設定不再有效，且必須將此設定還原回其預設值 `true`。 此外，您必須更新 AG 資源以包含 `failover-timeout` 屬性。 
>
>若要將屬性值更新為 `true`，請執行：
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>將您現有的 AG 資源屬性 `failure-timeout` 更新為 `60s` 執行 (將 `ag1` 取代為您的可用性群組資源名稱)：
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>安裝 SQL Server 資源代理程式以與 Pacemaker 整合

在所有節點上執行下列命令。 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>為 Pacemaker 建立 SQL Server 登入

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>建立可用性群組資源

若要建立可用性群組資源，請使用 `pcs resource create` 命令，並設定資源屬性。 下列命令會針對名為 `ag1` 的可用性群組建立 `ocf:mssql:ag` 主要/從屬類型資源。 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>建立虛擬 IP 資源

若要建立虛擬 IP 位址資源，請在一個節點上執行下列命令。 使用網路中可用的靜態 IP 位址。 執行指令碼之前，請以有效 IP 位址取代 `< ... >` 之間的值。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker 中沒有對等的虛擬伺服器名稱。 若要使用指向字串伺服器名稱的連接字串，而不使用 IP 位址，請在 DNS 中註冊 IP 資源位址和所需的虛擬伺服器名稱。 針對 DR 設定，請在主要和 DR 網站上，向 DNS 伺服器註冊所需的虛擬伺服器名稱和 IP 位址。

## <a name="add-colocation-constraint"></a>新增共置限制式

在 Pacemaker 叢集中，幾乎每個決策都是藉由比較分數來完成，例如，選擇應執行資源的位置。 分數是針對每個資源計算得來的，而叢集資源管理員會選擇對特定資源具有最高分數的節點 (如果節點對於某資源的分數為負值，此資源就無法在該節點上執行)。使用限制式來設定叢集的決策。 限制式具有分數。 如果限制式的分數低於 INFINITY，則系統僅會將其視為建議。 INFINITY 分數表示它是必要項目。 若要確保該主要複本和虛擬 IP 資源都位於相同主機，請使用 INFINITY 分數定義共置限制式。 若要新增共置限制式，請在一個節點上執行下列命令。 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>新增排序限制式

共置限制式具有隱含的排序限制式。 它會先移動虛擬 IP 資源，再移動可用性群組資源。 根據預設，事件的順序如下：

1. 使用者會從 node1 到 node2 對可用性群組主要複本發出 `pcs resource move`。
1. 虛擬 IP 資源會在 node1 上停止。
1. 虛擬 IP 資源會在 node2 上啟動。

   >[!NOTE]
   >此時，IP 位址會暫時指向 node2，而 node2 仍是容錯移轉前的次要複本。 
   
1. node1 上的可用性群組主要複本會降級為次要複本。
1. node2 上的可用性群組次要複本會升級為主要複本。 

為了防止 IP 位址暫時指向含容錯移轉前之次要複本的節點，請新增排序限制式。 

若要新增排序限制式，請在一個節點上執行下列命令：

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>當您設定叢集並將可用性群組新增為叢集資源之後，就無法使用 Transact-SQL 來容錯移轉可用性群組資源。 Linux 上的 SQL Server 叢集資源不會與作業系統緊密結合，因為其位於 Windows Server 容錯移轉叢集 (WSFC) 上。 SQL Server 服務不知道叢集是否存在。 所有協調流程都會透過叢集管理工具來完成。 在 RHEL 或 Ubuntu 中，請使用 `pcs`。 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>後續步驟

[操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)

