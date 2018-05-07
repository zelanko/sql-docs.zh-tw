---
title: 設定 SQL Server 可用性群組的 SLES 叢集 |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: 4ac7fc7c865599ccf5fb8a10782fe786c7e81255
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>設定 SQL Server 可用性群組的 SLES 叢集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本指南提供指示來建立適用於 SQL Server 上 SUSE Linux Enterprise Server (SLES) 12 SP2 的三個節點叢集。 高可用性，Linux 上的可用性群組需要三個節點-請參閱[的可用性群組組態的高可用性與資料保護](sql-server-linux-availability-group-ha.md)。 叢集的圖層根據 SUSE[高可用性延伸模組 (HAE)](https://www.suse.com/products/highavailability)之上[Pacemaker](http://clusterlabs.org/)。 

如需有關叢集設定、 資源代理程式的選項、 管理、 最佳做法和建議的詳細資訊，請參閱[SUSE Linux Enterprise 高可用性延伸 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)。

>[!NOTE]
>此時，不是與使用 Windows 上的 WSFC 為結合與 Pacemaker Linux 上的 SQL Server 的整合。 在 Linux 上的 SQL Server 服務不會感知叢集。 Pacemaker 控制所有的叢集資源，包括可用性群組資源的協調流程。 On Linux，您不應依賴一律在可用性群組動態管理檢視 (Dmv)，提供類似 sys.dm_hadr_cluster 叢集資訊。 此外，虛擬網路名稱是屬於 WSFC、 沒有對等的 Pacemaker 中相同。 您仍然可以建立來做為透明的重新連線到容錯移轉之後，接聽程式，但您必須手動在 DNS 伺服器註冊接聽程式名稱與 IP 用來建立虛擬 IP 資源 （如下列各節所述）。


## <a name="roadmap"></a>藍圖

建立高可用性的可用性群組的程序各有不同 Linux 伺服器和 Windows Server 容錯移轉叢集。 下列清單描述的概要步驟： 

1. [設定 SQL Server 叢集節點上](sql-server-linux-setup.md)。

2. [建立可用性群組](sql-server-linux-availability-group-failover-ha.md)。 

3. 設定叢集資源管理員，例如 Pacemaker。 這些指示是本文件中。
   
   設定叢集資源管理員的方式取決於特定 Linux 發佈。 

   >[!IMPORTANT]
   >實際執行環境中需要隔離代理程式，例如 STONITH 高可用性。 這篇文章中的範例不會使用隔離代理程式。 它們是用於測試和驗證。 
   
   >Pacemaker 叢集使用圍欄叢集回到已知狀態。 設定範圍的方式取決於分佈和環境。 此時，圍欄不適用於某些雲端環境中。 請參閱[SUSE Linux Enterprise 高可用性延伸](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing)。

5. [新增可用性群組為叢集中資源](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)。 

## <a name="prerequisites"></a>필수 구성 요소

若要完成下列端對端案例中，您需要將三個節點叢集部署的三部機器。 下列步驟概述如何設定這些伺服器。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>安裝和設定每個叢集節點上的作業系統 

第一個步驟是設定叢集節點上的作業系統。 這個逐步解說，使用 SLES 12 SP2 與有效的訂用帳戶的 HA 附加元件。

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>安裝和設定每個叢集節點上的 SQL Server 服務

1. 安裝及設定 SQL Server 服務的所有節點上。 如需詳細指示，請參閱[安裝 SQL Server on Linux](sql-server-linux-setup.md)。

1. 將一個節點指定為主要和次要節點。 使用本指南這些詞彙。

1. 確定要將屬於叢集的節點可以彼此通訊。

   下列範例所示`/etc/hosts`與名為 SLES1、 SLES2 和 SLES3 的三個節點的新增項目。

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   所有叢集節點都必須能夠彼此透過 SSH 存取。 工具喜歡`hb_report`或`crm_report`（以便疑難排解） 和鷹的歷程記錄 Explorer 需要在節點之間的 passwordless SSH 存取，否則它們就可以只收集資料從目前的節點。 如果您使用非標準 SSH 連接埠，請使用-X 選項 (請參閱`man`頁面)。 例如，如果您的 SSH 連接埠是 3479，叫用`crm_report`使用：

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   如需詳細資訊，請參閱[SLES 系統管理指南-其他區段](http://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)。


## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker 建立的 SQL Server 登入

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>設定 Alwayson 可用性群組

在 Linux 伺服器上設定可用性群組，然後設定叢集資源。 若要設定可用性群組，請參閱[設定 Alwayson 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>安裝和設定每個叢集節點上 Pacemaker

1. 安裝高可用性的擴充功能

   如需參考，請參閱[安裝 SUSE Linux Enterprise Server 和高可用性的擴充功能](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. 這兩個節點上安裝 SQL Server 資源代理程式套件。

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>設定第一個節點

   請參閱[SLES 安裝指示](http://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. 以登入`root`實體或虛擬機器，您想要為叢集節點使用。
2. 藉由執行啟動啟動程序的指令碼：
   ```bash
   sudo ha-cluster-init
   ```

   如果 NTP 尚未設定要在開機時啟動，就會出現一則訊息。 

   如果您決定要繼續，指令碼自動產生金鑰，讓 SSH 存取並讓 Csync2 同步作業工具，並啟動兩個所需的服務。 

3. 若要設定叢集通訊層 (Corosync): 

   a. 輸入繫結至網路位址。 根據預設，指令碼所提出 eth0 的網路位址。 或者，請輸入不同的網路位址，例如 bond0 的位址。 

   b. 輸入多點傳送的位址。 指令碼所提出的隨機位址時，您可以使用做為預設值。 

   c. 輸入多點傳送連接埠。 指令碼建議 5405 做為預設值。 

   d. 若要設定`SBD ()`，輸入您想要用於架 SBD 您封鎖裝置的磁碟分割的持續性路徑。 叢集中所有節點之間必須一致的路徑。 
   最後，指令碼會啟動來讓單一節點叢集上線，並啟用 Web 管理介面 Hawk2 Pacemaker 服務。 要用於 Hawk2 URL 會顯示在螢幕上。 

4. 取得安裝程序的詳細資訊，請檢查`/var/log/sleha-bootstrap.log`。 您現在可以執行的單一節點叢集。 檢查 crm 狀態的叢集狀態：

   ```bash
   sudo crm status
   ```

   您也可以查看叢集組態`crm configure show xml`或`crm configure show`。

5. 啟動程序的程序會建立名為 hacluster 密碼 linux 的 Linux 使用者。 用來取代預設密碼安全儘速： 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>將節點加入至現有的叢集

如果您有一或多個節點執行的叢集，新增多個叢集節點的高可用性-叢集-結合啟動程序指令碼。 指令碼只需要存取現有的叢集節點，並會自動完成目前的電腦上的基本安裝。 使用下列步驟：

如果您已設定使用現有的叢集節點`YaST`叢集模組時，請確定符合下列必要條件再執行`ha-cluster-join`:
- 現有的節點上的根使用者有 SSH 金鑰以便於 passwordless 登入。 
- `Csync2` 現有的節點上設定。 如需詳細資訊，請參閱 < 設定 Csync2 YaST 與。 

1. 在實體或虛擬機器應該要加入叢集的根身分登入。 
2. 藉由執行啟動啟動程序的指令碼： 

   ```bash
   sudo ha-cluster-join
   ```

   如果 NTP 尚未設定要在開機時啟動，就會出現一則訊息。 

3. 如果您決定要繼續，系統會提示您為現有節點的 IP 位址。 輸入 IP 位址。 

4. 如果您未設定這兩部電腦之間的 passwordless SSH 存取，您還必須輸入的現有節點的根密碼。 

   登入指定的節點之後，指令碼複製 Corosync 組態、 設定 SSH 和`Csync2`，並使目前的電腦上線為新的叢集節點。 除了以外，它會啟動鷹所需的服務。 如果您已設定共用存放裝置，且`OCFS2`，它也會自動建立的掛接點目錄`OCFS2`檔案系統。 

5. 您想要新增到叢集的所有電腦重複上述步驟。 

6. 如需程序的詳細資訊，請查看`/var/log/ha-cluster-bootstrap.log`。 

1. 檢查叢集狀態，以及`sudo crm status`。 如果您已成功加入第二個節點，則輸出將如下所示︰

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` 是在初始的單一節點叢集安裝期間設定的虛擬 IP 叢集資源。

加入所有節點之後, 檢查是否您需要調整沒有仲裁原則中的全域叢集選項。 這是特別重要的雙節點叢集。 如需詳細資訊，請參閱節 4.1.2，選項沒有仲裁原則。 

## <a name="set-cluster-property-cluster-recheck-interval"></a>設定叢集屬性叢集重新檢查間隔

`cluster-recheck-interval` 指出的輪詢間隔的叢集檢查有變更的資源參數、 條件約束或其他叢集的選項。 如果複本關閉，叢集會嘗試重新啟動的時間間隔是由繫結的複本`failure-timeout`值和`cluster-recheck-interval`值。 例如，如果`failure-timeout`設為 60 秒及`cluster-recheck-interval`設定為 120 秒，超過 60 秒，但小於 120 秒的間隔嘗試重新啟動。 我們建議您將失敗逾時設定為 60 秒及叢集重新檢查的間隔為大於 60 秒的值。 建議您不要將叢集重新檢查間隔設定為較小的值。

若要更新的屬性值`2 minutes`執行：

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 如果您已經有由 Pacemaker 叢集管理可用性群組資源，請注意使用最新可用 Pacemaker 封裝 1.1.18-11.el7 的所有分佈都造成啟動失敗-是-嚴重的叢集設定時的行為變更其值為 false。 這項變更會影響容錯移轉工作流程。 如果主要複本發生中斷，叢集必須容錯移轉至其中一個可用的次要複本。 相反地，使用者會發現，叢集會嘗試啟動失敗的主要複本。 如果該主永遠不會上線時 （因為在永久中斷），叢集絕不會容錯移轉至另一個可用的次要複本。 由於此項變更，先前建議的設定，來設定開始失敗-是-嚴重已不再有效，此設定需要還原為其預設值`true`。 此外，必須更新，以包含 AG 資源`failover-timeout`屬性。 
>
>若要更新的屬性值`true`執行：
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>更新您現有的 AG 資源屬性`failure-timeout`至`60s`執行 (取代`ag1`具有可用性群組資源的名稱): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

如需有關 Pacemaker 叢集內容的詳細資訊，請參閱[設定叢集資源](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html)。

# <a name="configure-fencing-stonith"></a>設定範圍 (STONITH)
Pacemaker 叢集廠商需要啟用 STONITH 和圍欄裝置設定為支援的叢集安裝。 當叢集資源管理員無法判斷狀態的節點或節點上的資源時，隔離會用於叢集讓已知狀態重新。

資源層級範圍主要是確保所設定的資源設定是中斷期間發生資料損毀。 您可以使用資源層級的範圍，比方說，DRBD （分散式複寫區塊裝置） 來標示為過期時的節點上的磁碟使用的通訊連結中斷。

節點層級圍欄可確保節點不會執行任何資源。 這是藉由重設節點和它的 Pacemaker 實作稱為 STONITH （它代表"羊標頭中的另一個節點 」）。 Pacemaker 支援絕佳各種柵欄裝置，例如伺服器不斷電供應系統或管理的介面卡。

如需詳細資訊，請參閱[從頭 Pacemaker 叢集](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)，[圍欄和 Stonith](http://clusterlabs.org/doc/crm_fencing.html)和[SUSE HA 文件： 圍欄和 STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html)。

在叢集初始化階段，如果偵測不到任何設定時，會停用 STONITH。 它可啟用稍後由執行下列命令：

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>停用 STONITH 只適用於測試目的。 如果您打算使用 Pacemaker 實際執行環境中，您應該規劃 STONITH 實作，根據您的環境，並保持啟用。 SUSE 不提供任何雲端環境 （包括 Azure） 或 HYPER-V 圍欄代理程式。 因此，叢集供應商不提供支援在這些環境中執行生產叢集。 我們正在將會在未來版本中提供此間隔的解決方案。


## <a name="configure-the-cluster-resources-for-sql-server"></a>設定 SQL Server 的叢集資源

請參閱[SLES 管理 Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

### <a name="create-availability-group-resource"></a>建立可用性群組資源

下列命令會建立，並設定可用性群組資源的三個複本的可用性群組 [ag1]。 監視作業和逾時值必須是在中明確指定 SLES 基礎的高工作負載相依性和需要仔細調整每個部署逾時。
其中一個叢集節點上執行命令：

1. 執行`crm configure`開啟 crm 提示字元：

   ```bash
   sudo crm configure 
   ```

1. 在 crm 提示字元中，執行下列命令來設定資源內容。

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

如果您未建立虛擬 IP 資源當您執行`ha-cluster-init`您現在可以建立此資源。 下列命令來建立虛擬 IP 資源。 取代`<**0.0.0.0**>`與可用的位址，從您的網路和`<**24**>`具有 CIDR 子網路遮罩的位元數。 在一個節點上執行。

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>加入共置條件約束
藉由比較分數是在 Pacemaker 叢集中，例如選擇應在何處資源執行，幾乎每個決策。 分數計算每個資源，並叢集資源管理員選擇特定資源的分數最高的節點。 （如果節點具有負數資源的分數，該節點上即無法執行資源）。我們可以管理具有條件約束叢集的決策。 分數是條件約束。 如果條件約束的分數低於無限大，則僅供建議。 分數為無限大表示它是必備。 我們想要確保主要可用性群組和虛擬 ip 資源都執行相同主機上，因此我們定義分數為無限大的共置條件約束。 

若要設定共置在相同的主要節點上執行的虛擬 IP 的條件約束，請在一個節點上執行下列命令：

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>加入排序條件約束
共置條件約束具有隱含的排序條件約束。 它會移動虛擬 IP 資源之前它會將可用性群組資源移動。 依預設事件的順序為： 

1. 使用者問題的資源將從 node1 到 node2 移轉到主要可用性群組。
2. 虛擬 IP 資源會在節點 1 上停止。
3. 啟動節點 2 上的虛擬 IP 資源。 這個時候的 IP 位址暫時至節點 2 點時仍前容錯移轉節點 2。 第二個。 
4. 在節點 1 上的主要可用性群組已降級為從屬。
5. 可用性群組從屬節點 2 升級到主機。 

若要防止暫時指向與前容錯移轉的次要節點的 IP 位址，請加入排序條件約束。 若要加入排序條件約束，請在一個節點上執行下列命令： 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>您設定叢集，並新增為叢集資源的可用性群組之後，您無法使用 TRANSACT-SQL 來容錯移轉可用性群組資源。 在 Linux 上的 SQL Server 叢集資源不搭配嚴格作業系統和它們在 Windows Server 容錯移轉叢集 (WSFC)。 SQL Server 服務並不知道叢集的存在。 所有的協調流程會透過叢集管理工具。 在 SLES 使用`crm`。 

手動容錯移轉之可用性群組的`crm`。 不會起始與 TRANSACT-SQL 的容錯移轉。 如需詳細資訊，請參閱[容錯移轉](sql-server-linux-availability-group-failover-ha.md#failover)。


如需詳細資訊，請參閱：
- [管理叢集資源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm)。   
- [HA 概念](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Pacemaker 快速參考](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>後續的步驟

[操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)
