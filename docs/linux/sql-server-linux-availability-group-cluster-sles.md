---
title: 設定 SQL Server 可用性群組的 SLES 叢集 |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: 288348e1b18e5a20ec2b9890bfc54f613230436e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655209"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>設定 SQL Server 可用性群組的 SLES 叢集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本指南提供指示來建立適用於 SQL Server 在 SUSE Linux Enterprise Server (SLES) 12 SP2 的三個節點叢集。 如需高可用性，Linux 上的可用性群組需要三個節點-請參閱[可用性群組組態的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。 叢集層根據 SUSE[高可用性延伸模組 (HAE)](https://www.suse.com/products/highavailability)之上建置[Pacemaker](http://clusterlabs.org/)。 

如需有關叢集設定、 資源代理程式選項、 管理、 最佳做法和建議的詳細資訊，請參閱 < [SUSE Linux Enterprise 高可用性延伸模組 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)。

>[!NOTE]
>到目前為止，不是與使用 Windows 上為 WSFC，結合與 Linux 上的 Pacemaker 的 SQL Server 的整合。 在 Linux 上的 SQL Server 服務不是感知叢集。 Pacemaker 會控制所有叢集資源，包括可用性群組資源的協調流程。 在 Linux 上，您不應依賴一律在可用性群組動態管理檢視 (Dmv) 可提供叢集的資訊，例如 sys.dm_hadr_cluster。 此外，虛擬網路名稱是特有 WSFC 的相同的 Pacemaker 沒有對等。 您仍然可以建立要用於容錯移轉之後，透明的重新連線的接聽程式，但您必須手動在 DNS 伺服器中註冊的接聽程式名稱以用來建立虛擬 IP 資源 （如下列各節所述） 的 IP。


## <a name="roadmap"></a>藍圖

建立高可用性的可用性群組的程序不同於 Linux 伺服器和 Windows Server 容錯移轉叢集。 下列清單說明的概要步驟： 

1. [設定叢集節點上的 SQL Server](sql-server-linux-setup.md)。

2. [建立可用性群組](sql-server-linux-availability-group-failover-ha.md)。 

3. 設定叢集資源管理員，例如 Pacemaker。 這些指示是本文件中。
   
   若要設定叢集資源管理員的方式取決於特定的 Linux 散發套件。 

   >[!IMPORTANT]
   >生產環境需要隔離代理程式，例如高可用性的 STONITH。 這篇文章中的範例不會使用隔離代理程式。 也就是進行測試和僅驗證。 
   
   >Pacemaker 叢集會使用隔離，讓叢集回到已知狀態。 若要設定隔離的方式取決於發佈和環境。 在此階段中，隔離不適用於某些雲端環境。 請參閱[SUSE Linux Enterprise 高可用性延伸模組](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)。

5. [新增可用性群組為叢集中資源](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)。 

## <a name="prerequisites"></a>先決條件

若要完成下列的端對端案例中，您需要三部機器來部署三個節點叢集。 下列步驟概述如何設定這些伺服器。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>安裝和設定每個叢集節點上的作業系統 

第一個步驟是設定叢集節點上的作業系統。 此逐步解說中，使用 SLES 12 SP2 與有效的訂用帳戶的 HA 附加元件。

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>安裝和設定每個叢集節點上的 SQL Server 服務

1. 安裝和設定所有節點上的 SQL Server 服務。 如需詳細指示，請參閱 < [Linux 上安裝 SQL Server](sql-server-linux-setup.md)。

1. 將一個節點指定作為次要資料庫的主要和其他節點。 使用本指南的這些詞彙。

1. 請確定將會屬於叢集的節點可以互相通訊。

   下列範例所示`/etc/hosts`具名 SLES1、 SLES2，以及 SLES3 的三個節點的新增項目。

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   所有叢集節點必須都能夠透過 SSH 互相存取。 之類的工具`hb_report`或`crm_report`（適用於疑難排解） 和 Hawk 的 History Explorer 都需要在節點之間的無密碼 SSH 存取權，否則它們只能收集資料從目前的節點。 如果您使用非標準 SSH 連接埠，請使用-X 選項 (請參閱`man`頁面)。 例如，如果您的 SSH 連接埠是 3479，叫用`crm_report`使用：

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   如需詳細資訊，請參閱 < [SLES 系統管理指南-其他區段](http://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)。


## <a name="create-a-sql-server-login-for-pacemaker"></a>為 Pacemaker 建立 SQL Server 登入

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>設定 Alwayson 可用性群組

在 Linux 伺服器上設定可用性群組，並再設定叢集資源。 若要設定可用性群組時，請參閱[設定 Always On 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>安裝並在每個叢集節點上設定 Pacemaker

1. 安裝高可用性延伸模組

   如需參考，請參閱[安裝 SUSE Linux Enterprise Server 和高可用性延伸模組](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. 這兩個節點上安裝 SQL Server 資源代理程式套件。

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>設定第一個節點

   請參閱[SLES 安裝指示](http://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. 身分登入`root`在實體或虛擬機器，您想要為叢集節點。
2. 藉由執行啟動啟動程序的指令碼：
   ```bash
   sudo ha-cluster-init
   ```

   如果 NTP 尚未設定為在開機時啟動，則會出現一則訊息。 

   如果您決定要繼續，指令碼自動產生金鑰進行 SSH 存取和 Csync2 同步作業工具，並啟動兩個所需的服務。 

3. 若要設定叢集通訊層 (Corosync): 

   A. 輸入繫結至的網路位址。 根據預設，指令碼所提出 eth0 的網路的位址。 或者，輸入不同的網路位址，例如 bond0 的位址。 

   B. 輸入多點傳送的位址。 指令碼建議為預設值，您可以使用隨機位址。 

   c. 輸入多點傳送連接埠。 指令碼建議 5405 為預設值。 

   d. 若要設定`SBD ()`，輸入您想要使用 SBD 的區塊裝置的分割區的持續性的路徑。 在叢集中的所有節點之間必須一致的路徑。 
   最後，指令碼會啟動 Pacemaker 服務，若要讓單一節點叢集上線，並啟用 Web 管理介面 Hawk2。 要用於 Hawk2 URL 會顯示在螢幕上。 

4. 取得安裝程序的詳細資訊，請檢查`/var/log/sleha-bootstrap.log`。 現在，您會有執行單節點叢集。 檢查叢集狀態與 crm 狀態：

   ```bash
   sudo crm status
   ```

   您也可以查看與叢集組態`crm configure show xml`或`crm configure show`。

5. 啟動程序的程序會建立名為 hacluster 密碼 linux 使用的 Linux 使用者。 用來取代預設的密碼安全儘速： 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>將節點新增至現有的叢集

如果您有一個或多個節點執行的叢集，新增更多叢集節點的 ha 叢集-加入啟動程序的指令碼。 指令碼只需要存取現有的叢集節點，並會自動完成目前的電腦上的基本安裝。 使用下列步驟：

如果您已設定使用現有的叢集節點`YaST`叢集模組時，請確定您執行之前，先滿足下列必要條件`ha-cluster-join`:
- 現有的節點上的根使用者有 SSH 金鑰為無密碼登入。 
- `Csync2` 現有的節點上設定。 如需詳細資訊，請參閱 < 使用 YaST 設定的 Csync2。 

1. 在實體或虛擬機器應該要加入叢集的根身分登入。 
2. 藉由執行啟動啟動程序的指令碼： 

   ```bash
   sudo ha-cluster-join
   ```

   如果 NTP 尚未設定為在開機時啟動，則會出現一則訊息。 

3. 如果您決定要繼續，將會提示您的現有節點的 IP 位址。 輸入 IP 位址。 

4. 如果您未設定這兩部電腦之間的無密碼 SSH 存取，您還必須輸入的現有節點的根密碼。 

   登入指定的節點之後，指令碼複製 Corosync 組態、 設定 SSH 和`Csync2`，並將目前的機器上線為新的叢集節點。 除了，它會啟動 Hawk 所需的服務。 如果您已設定使用的共用儲存體`OCFS2`，它也會自動建立的掛接點目錄`OCFS2`檔案系統。 

5. 重複上述步驟，針對您想要新增到叢集的所有機器。 

6. 此程序的詳細資訊，請檢查`/var/log/ha-cluster-bootstrap.log`。 

1. 檢查叢集狀態與`sudo crm status`。 如果您已成功加入第二個節點，則輸出將如下所示︰

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` 是在初始單節點叢集安裝期間設定的虛擬 IP 叢集資源。

加入之後的所有節點，請檢查是否需要調整沒有仲裁原則中的全域叢集選項。 這是對雙節點叢集來說尤其重要。 如需詳細資訊，請參閱節 4.1.2，選項沒有仲裁原則。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>設定叢集屬性叢集重新檢查間隔

`cluster-recheck-interval` 指示輪詢間隔的叢集檢查有變更的資源參數、 條件約束或其他叢集的選項。 如果複本停止運作時，叢集會嘗試重新啟動的時間間隔繫結的複本`failure-timeout`值和`cluster-recheck-interval`值。 例如，如果`failure-timeout`設定為 60 秒和`cluster-recheck-interval`設為 120 秒，超過 60 秒，但不超過 120 秒的間隔嘗試重新啟動。 我們建議您將失敗逾時設定為 60 秒和叢集重新檢查-間隔大於 60 秒的值。 建議您不要將叢集重新檢查間隔設定為較小的值。

若要將屬性值更新為`2 minutes`執行：

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 如果您已經有由 Pacemaker 叢集管理可用性群組資源，請注意，使用最新可用 Pacemaker 封裝 1.1.18-11.el7 的所有發行版本導入開始失敗-時-嚴重的叢集設定時的行為變更其值為 false。 這項變更會影響容錯移轉工作流程。 如果主要複本發生中斷，叢集應該容錯移轉至其中一個可用的次要複本。 相反地，使用者會發現叢集會嘗試啟動失敗的主要複本。 如果該主要永遠不會上線 （因為永久中斷），叢集絕不會容錯移轉至另一個可用的次要複本。 由於這項變更，先前建議的設定，來設定開始失敗-時-嚴重不再有效，且必須還原回其預設值是設定`true`。 此外，必須更新以包含 AG 資源`failover-timeout`屬性。 
>
>若要將屬性值更新為`true`執行：
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>更新您現有的 AG 資源屬性`failure-timeout`要`60s`執行 (取代`ag1`您可用性群組資源的名稱): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

如需有關 Pacemaker 叢集內容的詳細資訊，請參閱[設定叢集資源](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html)。

## <a name="configure-fencing-stonith"></a>設定隔離 (STONITH)
Pacemaker 叢集廠商需要啟用 STONITH 和隔離裝置設定為支援的叢集安裝程式。 當叢集資源管理員無法判斷狀態的節點或節點上的資源時，隔離會用於再一次將叢集設為已知狀態。

資源層級隔離主要是確保所設定的資源是在中斷期間的任何資料損毀。 您可以使用資源層級的隔離，比方說，使用 DRBD （分散式複寫區塊裝置） 將標示為已過期時的節點上的磁碟通訊連結中斷。

節點層級隔離可確保節點不會執行任何資源。 這是藉由重設節點和它的 Pacemaker 實作稱為 STONITH （這代表 「 限定標頭中的另一個節點 」）。 Pacemaker 支援很棒的各種不同的隔離裝置，例如伺服器不斷電供應器或管理的介面卡。

如需詳細資訊，請參閱 < [Pacemaker 叢集從頭](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)，[隔離和 Stonith](http://clusterlabs.org/doc/crm_fencing.html)並[SUSE HA 文件： 隔離和 STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html)。

在叢集的初始設定時，如果偵測不到任何設定時，會停用 STONITH。 它可稍後再執行下列命令：

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>停用 STONITH 是只基於測試目的。 如果您打算在生產環境中使用 Pacemaker 時，您應該規劃 STONITH 實作，根據您的環境，並將它保持啟用。 SUSE 不提供任何雲端環境 （包括 Azure） 或 HYPER-V 隔離代理程式。 因此，叢集供應商不提供支援在這些環境中執行生產叢集。 我們正努力將會在未來版本中提供此鴻溝的解決方案。


## <a name="configure-the-cluster-resources-for-sql-server"></a>設定 SQL Server 叢集資源

請參閱[SLES 管理 Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

## <a name="enable-pacemaker"></a>啟用 Pacemaker

啟用 Pacemaker，讓它自動啟動。

在叢集中的每個節點上執行下列命令。

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>建立可用性群組資源

下列命令會建立，並設定可用性群組 [ag1] 的三個複本的可用性群組資源。 監視作業和逾時必須明確地指定 sles 基礎是以逾時高工作負載和相關，而且需要仔細調整每個部署。
其中一個叢集中節點上執行命令：

1. 執行`crm configure`開啟 crm 提示字元：

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

如果您未建立虛擬 IP 資源執行時`ha-cluster-init`您現在可以建立此資源。 下列命令來建立虛擬 IP 資源。 取代`<**0.0.0.0**>`與您的網路中可用的位址和`<**24**>`與 CIDR 子網路遮罩的位元數。 在一個節點上執行。

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>加入共置條件約束
在 Pacemaker 叢集中，例如選擇應在何處資源執行，幾乎每個決策是藉由比較分數。 分數會計算每個資源，和 「 叢集資源管理員會選擇具有最高分數的特定資源的節點。 （如果節點的資源負分數，該節點上即無法執行資源）。我們可以操作的條件約束的叢集所做的決策。 條件約束有分數。 如果條件約束的分數低於無限大，則僅供建議。 無限大的分數表示它是不可。 我們想要確保主要可用性群組和虛擬 ip 資源執行在相同主機上，因此我們定義分數為無限大的共置條件約束。 

若要設定共置在相同的主要節點上執行的虛擬 IP 的條件約束，請在一個節點上執行下列命令：

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>加入排序條件約束
共置條件約束有隱含的排序條件約束。 將可用性群組資源之前，它會移動虛擬 IP 資源。 根據預設事件的順序為： 

1. 使用者問題的資源將移轉到主要可用性群組中，從 node1 到 node2。
2. 在節點 1 上，停止虛擬 IP 資源。
3. 啟動節點 2 上的虛擬 IP 資源。 此時，IP 位址暫時節點 2 點而節點 2 仍是在容錯移轉之前次要。 
4. 在節點 1 上的可用性群組主要降級為從屬。
5. 可用性群組從屬節點 2 升級至 master。 

若要避免暫時指向與容錯移轉前次要節點的 IP 位址，請加入排序條件約束。 若要加入排序條件約束，請在一個節點上執行下列命令： 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>在設定叢集，並新增為叢集資源的可用性群組之後，您無法使用 TRANSACT-SQL 來容錯移轉可用性群組資源。 在 Linux 上的 SQL Server 叢集資源未結合緊密與作業系統和它們在 Windows Server 容錯移轉叢集 (WSFC)。 SQL Server 服務並不知道叢集的目前狀態。 所有的協調流程是透過叢集管理工具。 在 SLES 使用`crm`。 

手動容錯移轉之可用性群組的`crm`。 不會起始與 TRANSACT-SQL 的容錯移轉。 如需詳細資訊，請參閱 <<c0> [ 容錯移轉](sql-server-linux-availability-group-failover-ha.md#failover)。


如需詳細資訊，請參閱：
- [管理叢集資源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm)。   
- [HA 概念](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Pacemaker 快速參考](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>後續步驟

[操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)
