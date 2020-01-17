---
title: RHEL：在 Linux 中設定 SQL Server 的可用性群組
description: 了解如何在執行 Red Hat Enterprise Linux (RHEL) 時，為 SQL Server 設定可用性群組叢集。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: 6976d81994dbc8db154b285da03bed2397e9fee1
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558491"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>設定 SQL Server 可用性群組的 RHEL 叢集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文件說明如何在 Red Hat Enterprise Linux 上，針對 SQL Server 建立三個節點的可用性群組叢集。 為了提供高可用性，Linux 上的可用性群組需要三個節點，請參閱[可用性群組設定的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。 叢集層是以建置於 [Pacemaker](https://clusterlabs.org/) 之上的 Red Hat Enterprise Linux (RHEL) [HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)為基礎。 

> [!NOTE] 
> 存取 Red Hat 完整文件需要有效的訂用帳戶。 

如需叢集設定、資源代理程式選項和管理的詳細資訊，請造訪 [RHEL 參考文件](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html) \(英文\)。

> [!NOTE] 
> SQL Server 並未與 Linux 上的 Pacemaker 緊密整合，因為它會使用 Windows Server 容錯移轉叢集。 SQL Server 執行個體不知道該叢集。 Pacemaker 提供叢集資源協調流程。 此外，虛擬網路名稱是 Windows Server 容錯移轉叢集特有的，Pacemaker 中沒有對等項目。 查詢叢集資訊的可用性群組動態管理檢視 (DMV) 會在 Pacemaker 叢集上傳回空的資料列。 若要在容錯移轉之後建立適用於透明重新連線的接聽程式，請在 DNS 中以用來建立虛擬 IP 資源的 IP 手動註冊接聽程式名稱。 

下列各節將逐步解說設定 Pacemaker 叢集的步驟，並將可用性群組新增為叢集中的資源以提供高可用性。

## <a name="roadmap"></a>藍圖

在 Linux 伺服器上建立可用性群組以提供高可用性的步驟，與 Windows Server 容錯移轉叢集上的步驟不同。 下列清單描述高階步驟： 

1. [在叢集節點上設定 SQL Server](sql-server-linux-setup.md)。

2. [建立可用性群組](sql-server-linux-availability-group-configure-ha.md)。 

3. 設定叢集資源管理員，例如 Pacemaker。 此文件包含這些指示。
   
   設定叢集資源管理員的方式取決於特定 Linux 發行版本。 

   >[!IMPORTANT]
   >生產環境需要 STONITH 這類隔離代理程式來取得高可用性。 此文件的示範不會使用隔離代理程式。 這些示範僅適用於測試和驗證。
   
   >Linux 叢集會使用隔離功能將叢集回復為已知的狀態。 設定隔離的方式取決於發行版本和環境。 目前，有些雲端環境無法使用隔離。 如需詳細資訊，請參閱 [Support Policies for RHEL High Availability Clusters - Virtualization Platforms](https://access.redhat.com/articles/29440) (RHEL 高可用性叢集的支援原則 - 虛擬化平台)。

5. [將可用性群組新增為叢集中的資源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。  

## <a name="configure-high-availability-for-rhel"></a>為 RHEL 設定高可用性

若要為 RHEL 設定高可用性，請啟用高可用性訂用帳戶，然後設定 Pacemaker。

### <a name="enable-the-high-availability-subscription-for-rhel"></a>為 RHEL 啟用高可用性訂用帳戶

叢集中的每個節點都必須有適用於 RHEL 的適當訂用帳戶及高可用性附加元件。 檢閱[如何在 Red Hat Enterprise Linux 中安裝高可用性叢集套件](https://access.redhat.com/solutions/45930) \(英文\) 的需求。 請遵循以下步驟來設定訂用帳戶和存放庫：

1. 註冊系統。

   ```bash
   sudo subscription-manager register
   ```

   提供您的使用者名稱與密碼。   

1. 列出可用的集區以進行註冊。

   ```bash
   sudo subscription-manager list --available
   ```

   從可用集區的清單中，記下高可用性訂用帳戶的集區識別碼。

1. 更新下列指令碼。 以上一個步驟中高可用性的集區識別碼取代 `<pool id>`。 執行指令碼以附加訂用帳戶。

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. 啟用存放庫。

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

如需詳細資訊，請參閱 [Pacemake - 開放原始碼、高可用性叢集](https://clusterlabs.org/pacemaker/) \(英文\)。 

當您設定訂用帳戶之後，需完成下列設定 Pacemaker 的步驟：

### <a name="configure-pacemaker"></a>設定 Pacemaker

當您註冊訂用帳戶之後，需完成下列設定 Pacemaker 的步驟：
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

設定 Pacemaker 之後，使用 `pcs` 來與叢集互動。 在叢集的一個節點上執行所有命令。 

## <a name="configure-fencing-stonith"></a>設定隔離 (STONITH)

Pacemaker 叢集廠商必須啟用 STONITH，並針對支援的叢集設定設好隔離裝置。 STONITH 代表 "Shoot the Other Node in the Head" (直譯：將另一節點爆頭)。 當叢集資源管理員無法判斷節點或節點上之資源的狀態時，隔離會讓叢集再次進入已知狀態。

STONITH 裝置提供隔離代理程式。 [在 Azure 的 Red Hat Enterprise Linux 中設定 Pacemaker](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker/#1-create-the-stonith-devices) 提供範例，說明如何在 Azure 中為此叢集建立 STONITH 裝置。 修改環境的指示。

資源層級隔離可透過設定資源，確保在發生中斷時不會有資料損毀。 例如，您可以使用資源層級隔離，將節點上的磁碟標示為在通訊連結中斷時過期。 

節點層級隔離可確保節點不會執行任何資源。 這會透過重設節點來完成。 Pacemaker 支援各式各樣的隔離裝置。 範例包括適用於伺服器的不斷電供應系統或管理介面卡。

如需有關 STONITH 和隔離的詳細資訊，請參閱下列文章：

* [從頭開始 Pacemaker 叢集](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/index.html) \(英文\)
* [隔離和 STONITH](https://clusterlabs.org/doc/crm_fencing.html) \(英文\)
* [Red Hat 高可用性附加元件與 Pacemaker：隔離](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

>[!NOTE]
>由於節點層級隔離設定主要取決於您的環境，因此，請在本教學課程中將其停用 (可於稍後設定)。 下列指令碼會停用節點層級隔離：
>
>```bash
>sudo pcs property set stonith-enabled=false
>``` 
>
>停用 STONITH 僅基於測試目的。 如果您打算在生產環境中使用 Pacemaker，則應該根據您的環境規劃 STONITH 實作，並讓它保持啟用狀態。

## <a name="set-cluster-property-cluster-recheck-interval"></a>設定 cluster-recheck-interval 叢集屬性

`cluster-recheck-interval` 表示輪詢間隔，叢集會依此間隔檢查資源參數、限制式或其他叢集選項中的變更。 如果複本中斷，叢集會嘗試以 `failure-timeout` 值和 `cluster-recheck-interval` 值所繫結的間隔重新啟動複本。 例如，如果 `failure-timeout` 設為 60 秒，而 `cluster-recheck-interval` 設為 120 秒，則會以大於 60 秒但小於 120 秒的間隔嘗試重新啟動。 建議您將 failure-timeout 設為 60 秒，並將 cluster-recheck-interval 設為大於 60 秒的值。 不建議將 cluster-recheck-interval 設為較小的值。

若要將屬性值更新為 `2 minutes`，請執行：

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 所有使用最新可用 Pacemaker 套件 1.1.18-11.el7 的發行版本 (包括 RHEL 7.3 和 7.4)，都會在 start-failure-is-fatal 叢集設定值為 false 時，採用其行為變更。 此變更會影響容錯移轉工作流程。 如果主要複本發生中斷，則叢集應該要容錯移轉至其中一個可用的次要複本。 但是，使用者卻發現叢集繼續嘗試啟動失敗的主要複本。 如果該主要複本永遠無法上線 (因為永久中斷)，則叢集永遠不會容錯移轉至其他可用的次要複本。 此變更導致先前建議作為 start-failure-is-fatal 的設定不再有效，且必須將此設定還原回其預設值 `true`。 此外，您必須更新 AG 資源以包含 `failover-timeout` 屬性。 

若要將屬性值更新為 `true`，請執行：

```bash
sudo pcs property set start-failure-is-fatal=true
```

若要將 `ag_cluster` 資源屬性 `failure-timeout` 更新為 `60s`，請執行：

```bash
pcs resource update ag_cluster meta failure-timeout=60s
```


如需 Pacemaker 叢集屬性的相關資訊，請參閱 [Pacemaker 叢集屬性](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html) \(英文\)。

## <a name="create-a-sql-server-login-for-pacemaker"></a>為 Pacemaker 建立 SQL Server 登入

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>建立可用性群組資源

若要建立可用性群組資源，請使用 `pcs resource create` 命令，並設定資源屬性。 下列命令會針對名稱為 `ocf:mssql:ag` 的可用性群組建立 `ag1` 主要/從屬類型資源。

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s master notify=true
``` 

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>建立虛擬 IP 資源

若要建立虛擬 IP 位址資源，請在一個節點上執行下列命令。 使用網路中可用的靜態 IP 位址。 以有效的 IP 位址取代 `<10.128.16.240>` 之間的 IP 位址。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Pacemaker 中沒有對等的虛擬伺服器名稱。 若要使用指向字串伺服器名稱而非 IP 位址的連接字串，請在 DNS 中註冊虛擬 IP 資源位址和所需的虛擬伺服器名稱。 針對 DR 設定，請在主要和 DR 網站上，向 DNS 伺服器註冊所需的虛擬伺服器名稱和 IP 位址。

## <a name="add-colocation-constraint"></a>新增共置限制式

在 Pacemaker 叢集中，幾乎每個決策都是藉由比較分數來完成，例如，選擇應執行資源的位置。 分數是針對每個資源計算得來的。 叢集資源管理員會選擇對特定資源具有最高分數的節點。 如果節點對於某資源的分數為負值，則該資源就無法在該節點上執行。

在 Pacemaker 叢集上，您可以使用限制式來操控叢集的決策。 限制式具有分數。 如果限制式的分數低於 `INFINITY`，則 Pacemaker 會將其視為建議。 `INFINITY` 的分數是強制性的。

若要確保該主要複本和虛擬 IP 資源都在相同主機上執行，定義分數為 INFINITY 的共置限制式。 若要新增共置限制式，請在一個節點上執行下列命令。

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>新增排序限制式

共置限制式具有隱含的排序限制式。 它會先移動虛擬 IP 資源，再移動可用性群組資源。 根據預設，事件的順序如下：

1. 使用者會從 node1 到 node2 對可用性群組主要複本發出 `pcs resource move`。
1. 虛擬 IP 資源會在節點 1 上停止。
1. 虛擬 IP 資源會在節點 2 上啟動。
  
   >[!NOTE]
   >此時，IP 位址會暫時指向節點 2，而節點 2 仍是容錯移轉前的次要複本。 
   
1. 節點 1 上的可用性群組主要複本會降級為次要複本。
1. 節點 2 上的可用性群組次要複本會升級為主要複本。 

為了防止 IP 位址暫時指向含容錯移轉前之次要複本的節點，請新增排序限制式。 

若要新增排序限制式，請在一個節點上執行下列命令：

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>當您設定叢集並將可用性群組新增為叢集資源之後，就無法使用 Transact-SQL 來容錯移轉可用性群組資源。 Linux 上的 SQL Server 叢集資源不會與作業系統緊密結合，因為其位於 Windows Server 容錯移轉叢集 (WSFC) 上。 SQL Server 服務不知道叢集是否存在。 所有協調流程都會透過叢集管理工具來完成。 在 RHEL 或 Ubuntu 中使用 `pcs`，在 SLES 中使用 `crm` 工具。 

使用 `pcs` 手動容錯移轉可用性群組。 請勿使用 Transact-SQL 來起始容錯移轉。 如需指示，請參閱[容錯移轉](sql-server-linux-availability-group-failover-ha.md#failover)。

## <a name="next-steps"></a>後續步驟

[操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)
