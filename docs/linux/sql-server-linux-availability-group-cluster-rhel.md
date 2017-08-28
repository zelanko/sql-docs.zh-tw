---
title: "設定 SQL Server 可用性群組的 RHEL 叢集 |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7930fd8cee6f6fabe00a711f9109573e42550563
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>設定 SQL Server 可用性群組的 RHEL 叢集

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本文件說明如何建立三個節點的可用性群組叢集 Red Hat Enterprise Linux 上的 SQL Server。 高可用性，Linux 上的可用性群組需要三個節點-請參閱[的可用性群組組態的高可用性與資料保護](sql-server-linux-availability-group-ha.md)。 叢集的圖層以基礎上 Red Hat Enterprise Linux (RHEL) [HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)之上[Pacemaker](http://clusterlabs.org/)。 

> [!NOTE] 
> Red Hat 的完整文件存取需要有效的訂用帳戶。 

如需叢集設定、 資源代理程式選項，以及管理的詳細資訊，請瀏覽[RHEL 參考文件](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)。

> [!NOTE] 
> SQL Server 並未會緊密整合到 Pacemaker on Linux 和 Windows Server 容錯移轉叢集。 無法感知叢集的 SQL Server 執行個體。 Pacemaker 提供叢集資源的協調流程。 此外，虛擬網路名稱是 Windows Server 容錯移轉叢集的特定-Pacemaker 中沒有任何對等項目。 可用性群組動態管理檢視 (Dmv 查詢叢集資訊) Pacemaker 叢集傳回空的資料列。 若要建立透明容錯移轉後的重新連線的接聽程式，手動與 IP 用來建立虛擬 IP 資源的 DNS 中註冊的接聽程式名稱。 

下列各節逐步解說設定 Pacemaker 叢集和高可用性的叢集中資源新增可用性群組的步驟。

## <a name="roadmap"></a>藍圖

在高可用性的 Linux 伺服器上建立可用性群組的步驟會與不同的 Windows Server 容錯移轉叢集的步驟。 下列清單描述的概要步驟： 

1. [設定 SQL Server 叢集節點上](sql-server-linux-setup.md)。

2. [建立可用性群組](sql-server-linux-availability-group-configure-ha.md)。 

3. 設定叢集資源管理員，例如 Pacemaker。 這些指示是本文件中。
   
   設定叢集資源管理員的方式取決於特定 Linux 發佈。 

   >[!IMPORTANT]
   >實際執行環境中需要隔離代理程式，例如 STONITH 高可用性。 在本文件示範請勿圍欄代理程式。 此示範的使用者是用於測試和驗證。 
   
   >Linux 叢集使用圍欄叢集回到已知狀態。 設定範圍的方式取決於分佈和環境。 目前，範圍不適用於某些雲端環境中。 如需詳細資訊，請參閱[RHEL 的高可用性叢集-而虛擬化平台的支援政策](https://access.redhat.com/articles/29440)。

5. [新增可用性群組為叢集中資源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。  

## <a name="configure-high-availability-for-rhel"></a>Rhel 設定高可用性

若要設定 RHEL 高可用性，請啟用高可用性的訂用帳戶，然後再設定 Pacemaker。

### <a name="enable-the-high-availability-subscription-for-rhel"></a>啟用 RHEL 的高可用性訂用帳戶

每個叢集中的節點必須具有適當的訂用帳戶 RHEL 和高可用性新增上。 檢閱需求，在[如何安裝高可用性叢集封裝在 Red Hat Enterprise Linux](http://access.redhat.com/solutions/45930)。 請遵循下列步驟來設定訂用帳戶和儲存機制：

1. 註冊系統。

   ```bash
   sudo subscription-manager register
   ```

   提供您的使用者名稱和密碼。   

1. 列出可用的集區註冊。

   ```bash
   sudo subscription-manager list --available
   ```

   從可用的集區的清單，請注意高可用性的訂用帳戶的集區識別碼。

1. 更新下列指令碼。 取代`<pool id>`與高可用性，從上一個步驟的集區識別碼。 執行指令碼以連結的訂用帳戶。

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. 啟用儲存機制。

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

如需詳細資訊，請參閱[Pacemaker-開啟來源，高可用性叢集](http://www.opensourcerers.org/pacemaker-the-open-source-high-availability-cluster/)。 

設定訂用帳戶之後，完成下列步驟來設定 Pacemaker:

### <a name="configure-pacemaker"></a>設定 Pacemaker

註冊訂用帳戶之後，完成下列步驟來設定 Pacemaker:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Pacemaker 設定之後，使用`pcs`叢集與互動。 從叢集的其中一個節點上執行所有的命令。 

## <a name="configure-fencing-stonith"></a>設定範圍 (STONITH)

Pacemaker 叢集廠商需要啟用 STONITH 和圍欄裝置設定為支援的叢集安裝。 STONITH 代表 「 豬羊另一個節點標頭中。 」 當叢集資源管理員無法判斷節點或節點上資源的狀態時，圍欄會再次叢集至已知的狀態。

資源層級範圍可確保所設定的資源會發生中斷時沒有資料損毀。 例如，您可以使用資源層級的範圍若要將磁碟標示為過期時的節點上的通訊連結中斷。 

節點層級圍欄可確保節點不會執行任何資源。 這是重設節點。 Pacemaker 支援絕佳各種柵欄裝置。 範例包括伺服器不斷電供應系統或管理的介面卡。

如 STONITH 和範圍的相關資訊，請參閱下列文章：

* [從頭 pacemaker 叢集](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)
* [範圍和 STONITH](http://clusterlabs.org/doc/crm_fencing.html)
* [Red Hat 高可用性的附加元件與 Pacemaker： 柵欄](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

因為節點層級範圍組態高度取決於您的環境，請將它停用此教學課程中 （它可以設定更新版本）。 下列指令碼會停用節點層級範圍：

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>停用 STONITH 只適用於測試目的。 如果您打算使用 Pacemaker 實際執行環境中，您應該規劃 STONITH 實作，根據您的環境，並保持啟用。 RHEL 不提供任何雲端環境 （包括 Azure） 或 HYPER-V 圍欄代理程式。 因此，叢集供應商不提供支援在這些環境中執行生產叢集。 我們正在將會在未來版本中提供此間隔的解決方案。

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>開始失敗-是-嚴重叢集屬性設定為 false

`start-failure-is-fatal`指出是否在節點上啟動資源失敗可防止進一步該節點上的啟動嘗試。 當設定為`false`，叢集會決定是否要嘗試再次根據資源的目前失敗計數和移轉臨界值的相同節點上啟動。 發生容錯移轉之後，Pacemaker 重試啟動可用性群組上先前的主要資源，可使用的 SQL 執行個體後。 Pacemaker 會降級至次要複本，並自動重新加入可用性群組。 

若要更新的屬性值`false`執行：

```bash
sudo pcs property set start-failure-is-fatal=false
```

>[!WARNING]
>自動容錯移轉之後，當`start-failure-is-fatal = true`資源管理員會嘗試啟動資源。 如果第一次嘗試失敗，手動執行`pcs resource cleanup <resourceName>`清除資源失敗計數和重設的設定。

如需 Pacemaker 叢集內容資訊，請參閱[Pacemaker 叢集屬性](http://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html)。

## <a name="create-a-sql-server-login-for-pacemaker"></a>Pacemaker 建立的 SQL Server 登入

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>建立可用性群組資源

若要建立可用性群組資源，請使用`pcs resource create`命令，並設定資源屬性。 El comando siguiente crea`ocf:mssql:ag`主/從可用性群組名稱的型別資源`ag1`。

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 --master meta notify=true
```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>建立虛擬 IP 資源

若要建立虛擬 IP 位址資源，請在一個節點上執行下列命令。 使用 從網路可用的靜態 IP 位址。 取代 IP 位址之間`**<10.128.16.240>**`具有有效的 IP 位址。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=**<10.128.16.240>**
```

沒有 Pacemaker 中相等的虛擬伺服器名稱。 若要使用的連接字串指向字串伺服器名稱，而不是 IP 位址，請在 DNS 中登錄的虛擬 IP 資源的位址和所需的虛擬伺服器名稱。 DR 組態註冊所需的虛擬伺服器名稱和 IP 位址與主要和 DR 網站上的 DNS 伺服器。

## <a name="add-colocation-constraint"></a>加入共置條件約束

藉由比較分數是在 Pacemaker 叢集中，例如選擇應在何處資源執行，幾乎每個決策。 分數會計算每個資源。 叢集資源管理員會選擇特定資源的分數最高的節點。 如果節點的負分數的資源，資源無法執行該節點上。

在 pacemaker 叢集上，您可以管理叢集條件約束的決策。 分數是條件約束。 如果條件約束的分數低於`INFINITY`，Pacemaker 做建議將儲存它。 分數為`INFINITY`是強制性。

若要確保主要複本和虛擬 ip 資源執行相同的主機上，定義分數為無限大的共置條件約束。 若要加入的共置條件約束，請在一個節點上執行下列命令。

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>加入排序條件約束

共置條件約束具有隱含的排序條件約束。 它會移動虛擬 IP 資源之前它會將可用性群組資源移動。 依預設事件的順序為：

1. 使用者發出`pcs resource move`至可用性群組主要複本從 node1 到 node2。
1. 虛擬 IP 資源會在節點 1 上停止。
1. 啟動節點 2 上的虛擬 IP 資源。
  
   >[!NOTE]
   >這個時候的 IP 位址暫時至節點 2 點時仍前容錯移轉節點 2。 第二個。 
   
1. 主要節點 1 上的可用性群組已降級為次要。
1. 次要節點 2 上的可用性群組會提升為主要。 

若要防止暫時指向與前容錯移轉的次要節點的 IP 位址，請加入排序條件約束。 

若要加入排序條件約束，請在一個節點上執行下列命令：

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>您設定叢集，並新增為叢集資源的可用性群組之後，您無法使用 TRANSACT-SQL 來容錯移轉可用性群組資源。 在 Linux 上的 SQL Server 叢集資源不搭配嚴格作業系統和它們在 Windows Server 容錯移轉叢集 (WSFC)。 SQL Server 服務並不知道叢集的存在。 所有的協調流程會透過叢集管理工具。 在 RHEL 或 Ubuntu 使用`pcs`和 SLES 使用中的`crm`工具。 

手動容錯移轉之可用性群組的`pcs`。 不會起始與 TRANSACT-SQL 的容錯移轉。 如需指示，請參閱[容錯移轉](sql-server-linux-availability-group-failover-ha.md#failover)。

## <a name="next-steps"></a>後續的步驟

[操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)

