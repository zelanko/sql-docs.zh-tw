---
title: 設定 SQL Server 可用性群組的 RHEL 叢集
titleSuffix: SQL Server
description: 了解可用性群組叢集時執行 Red Hat Enterprise Linux (RHEL)
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/12/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: ac544f145ae5d571f8e4dac979738585b0c13c60
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581331"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>設定 SQL Server 可用性群組的 RHEL 叢集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文件說明如何建立 Red Hat Enterprise Linux 上的 SQL Server 的三個節點的可用性群組叢集。 如需高可用性，Linux 上的可用性群組需要三個節點-請參閱[可用性群組組態的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。 叢集層以在 Red Hat Enterprise Linux (RHEL) 為基礎[HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)之上建置[Pacemaker](https://clusterlabs.org/)。 

> [!NOTE] 
> Red Hat 的完整文件的存取需要有效的訂用帳戶。 

如需有關叢集設定、 資源代理程式選項，以及管理的詳細資訊，請瀏覽[RHEL 參考文件](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)。

> [!NOTE] 
> SQL Server 並未緊密整合到 Linux 上的 Pacemaker，與 Windows Server 容錯移轉叢集。 無法感知叢集的 SQL Server 執行個體。 Pacemaker 會提供叢集資源的協調流程。 此外，虛擬網路名稱是 Windows Server 容錯移轉叢集的特定-Pacemaker 中沒有任何對等項目。 可用性群組動態管理檢視 (Dmv) 查詢叢集資訊會傳回空的資料列，Pacemaker 叢集上。 若要建立透明容錯移轉之後的重新連線的接聽程式，以用來建立虛擬 IP 資源的 IP 的 DNS 中手動註冊接聽程式名稱。 

下列各節會逐步設定 Pacemaker 叢集，並將可用性群組新增為高可用性叢集中的資源。

## <a name="roadmap"></a>藍圖

在高可用性的 Linux 伺服器上建立可用性群組的步驟是從 Windows Server 容錯移轉叢集上的步驟不同。 下列清單說明的概要步驟： 

1. [設定叢集節點上的 SQL Server](sql-server-linux-setup.md)。

2. [建立可用性群組](sql-server-linux-availability-group-configure-ha.md)。 

3. 設定叢集資源管理員，例如 Pacemaker。 這些指示是本文件中。
   
   若要設定叢集資源管理員的方式取決於特定的 Linux 散發套件。 

   >[!IMPORTANT]
   >生產環境需要隔離代理程式，例如高可用性的 STONITH。 在本文件示範，請勿使用隔離代理程式。 示範適用於測試、 僅驗證。 
   
   >Linux 叢集會使用隔離，讓叢集回到已知狀態。 若要設定隔離的方式取決於發佈和環境。 目前，隔離不適用於某些雲端環境。 如需詳細資訊，請參閱 < [RHEL 的高可用性叢集-而虛擬化平台的支援原則](https://access.redhat.com/articles/29440)。

5. [新增可用性群組為叢集中資源](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)。  

## <a name="configure-high-availability-for-rhel"></a>適用於 RHEL 設定高可用性

若要設定高可用性，適用於 RHEL，啟用高可用性的訂用帳戶及設定 Pacemaker。

### <a name="enable-the-high-availability-subscription-for-rhel"></a>啟用適用於 RHEL 的高可用性訂用帳戶

叢集中的每個節點必須有適用於 RHEL 和高可用性新增適當的訂用帳戶。 檢閱的需求[如何在 Red Hat Enterprise Linux 中安裝高可用性叢集封裝](https://access.redhat.com/solutions/45930)。 請遵循下列步驟來設定訂用帳戶和儲存機制：

1. 註冊系統。

   ```bash
   sudo subscription-manager register
   ```

   提供您的使用者名稱和密碼。   

1. 列出可用的集區進行註冊。

   ```bash
   sudo subscription-manager list --available
   ```

   從可用的集區的清單，請注意高可用性的訂用帳戶的集區識別碼。

1. 更新下列指令碼。 取代`<pool id>`使用從先前步驟中的高可用性的集區識別碼。 執行指令碼，以連結的訂用帳戶。

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. 啟用儲存機制。

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

如需詳細資訊，請參閱 < [Pacemaker 的開放原始碼、 高可用性叢集](https://clusterlabs.org/pacemaker/)。 

設定訂用帳戶之後，請完成下列步驟來設定 Pacemaker:

### <a name="configure-pacemaker"></a>設定 Pacemaker

註冊訂用帳戶之後，請完成下列步驟來設定 Pacemaker:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

設定 Pacemaker 之後，使用`pcs`與叢集互動。 從叢集的其中一個節點上執行所有命令。 

## <a name="configure-fencing-stonith"></a>設定隔離 (STONITH)

Pacemaker 叢集廠商需要啟用 STONITH 和隔離裝置設定為支援的叢集安裝程式。 STONITH 代表 「 豬羊另一個節點在標頭中。 」 時，叢集資源管理員無法判斷狀態的節點或節點上的資源，隔離會再次將設為已知狀態的叢集。

資源層級隔離可確保所設定的資源會發生中斷時的任何資料損毀。 比方說，您可以使用資源層級的隔離，若要將該磁碟標示為已過期時在節點上的通訊連結中斷。 

節點層級隔離可確保節點不會執行任何資源。 這是重設節點。 Pacemaker 支援很棒的各種不同的隔離裝置。 範例包括伺服器不斷電供應器或管理的介面卡。

STONITH 和隔離的相關資訊，請參閱下列文章：

* [從零開始的 pacemaker 叢集](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/index.html)
* [隔離和 STONITH](https://clusterlabs.org/doc/crm_fencing.html)
* [Red Hat pacemaker 的高可用性附加元件：隔離](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

因為節點層級的隔離設定大量取決於您的環境，請將它停用此教學課程中 （它可以設定更新版本）。 下列指令碼會停用節點層級隔離：

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>停用 STONITH 是只基於測試目的。 如果您打算在生產環境中使用 Pacemaker 時，您應該規劃 STONITH 實作，根據您的環境，並將它保持啟用。 RHEL 不提供任何雲端環境 （包括 Azure） 或 HYPER-V 隔離代理程式。 因此，叢集供應商不提供支援在這些環境中執行生產叢集。 我們正努力將會在未來版本中提供此鴻溝的解決方案。

## <a name="set-cluster-property-cluster-recheck-interval"></a>設定叢集屬性叢集重新檢查間隔

`cluster-recheck-interval` 指示輪詢間隔的叢集檢查有變更的資源參數、 條件約束或其他叢集的選項。 如果複本停止運作時，叢集會嘗試重新啟動的時間間隔繫結的複本`failure-timeout`值和`cluster-recheck-interval`值。 例如，如果`failure-timeout`設定為 60 秒和`cluster-recheck-interval`設為 120 秒，超過 60 秒，但不超過 120 秒的間隔嘗試重新啟動。 我們建議您將失敗逾時設定為 60 秒和叢集重新檢查-間隔大於 60 秒的值。 建議您不要將叢集重新檢查間隔設定為較小的值。

若要將屬性值更新為`2 minutes`執行：

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> 其值為 false 時，所有發行版本 （包括 RHEL 7.3 和 7.4） 使用最新可用 Pacemaker 封裝 1.1.18-11.el7 導入開始失敗-時-嚴重的叢集設定的行為變更。 這項變更會影響容錯移轉工作流程。 如果主要複本發生中斷，叢集應該容錯移轉至其中一個可用的次要複本。 相反地，使用者會發現叢集會嘗試啟動失敗的主要複本。 如果該主要永遠不會上線 （因為永久中斷），叢集絕不會容錯移轉至另一個可用的次要複本。 由於這項變更，先前建議的設定，來設定開始失敗-時-嚴重不再有效，且必須還原回其預設值是設定`true`。 此外，必須更新以包含 AG 資源`failover-timeout`屬性。 

若要將屬性值更新為`true`執行：

```bash
sudo pcs property set start-failure-is-fatal=true
```

若要更新`ag_cluster`資源屬性`failure-timeout`至`60s`執行：

```bash
pcs resource update ag_cluster meta failure-timeout=60s
```


如需 Pacemaker 叢集內容資訊，請參閱[Pacemaker 叢集屬性](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html)。

## <a name="create-a-sql-server-login-for-pacemaker"></a>為 Pacemaker 建立 SQL Server 登入

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>建立可用性群組資源

若要建立可用性群組資源，請使用`pcs resource create`命令，並設定資源屬性。 下列命令會建立`ocf:mssql:ag`主要/附屬類型名稱的可用性群組的資源`ag1`。

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s master notify=true
``` 

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>建立虛擬 IP 資源

若要建立的虛擬 IP 位址資源，請在一個節點上執行下列命令。 使用網路中可用的靜態 IP 位址。 取代 IP 位址之間`<10.128.16.240>`具備有效的 IP 位址。

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

沒有 Pacemaker 中的對等的虛擬伺服器名稱。 若要使用的連接字串指向字串伺服器名稱，而非 IP 位址，請在 DNS 中登錄的虛擬 IP 資源的位址和所需的虛擬伺服器名稱。 DR 組態中，註冊所需的虛擬伺服器名稱和 IP 位址與主要和 DR 站台上的 DNS 伺服器。

## <a name="add-colocation-constraint"></a>加入共置條件約束

在 Pacemaker 叢集中，例如選擇應在何處資源執行，幾乎每個決策是藉由比較分數。 分數會計算每個資源。 「 叢集資源管理員會選擇具有最高分數的特定資源的節點。 如果節點的負分數的資源，資源無法執行該節點上。

在 pacemaker 叢集上，您可以處理的條件約束的叢集所做的決策。 條件約束有分數。 如果條件約束有分數低於`INFINITY`，Pacemaker 將它與建議。 分數的`INFINITY`是必要的。

若要確保主要複本和虛擬 ip 資源執行相同的主機上，請定義分數為無限大的共置條件約束。 若要新增的共置條件約束，請在一個節點上執行下列命令。

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>加入排序條件約束

共置條件約束有隱含的排序條件約束。 將可用性群組資源之前，它會移動虛擬 IP 資源。 根據預設事件的順序為：

1. 使用者問題`pcs resource move`至可用性群組主要複本從 node1 到 node2。
1. 在節點 1 上，停止虛擬 IP 資源。
1. 啟動節點 2 上的虛擬 IP 資源。
  
   >[!NOTE]
   >此時，IP 位址暫時節點 2 點而節點 2 仍是在容錯移轉之前次要。 
   
1. 主要節點 1 上的可用性群組會降級為次要。
1. 次要節點 2 上的可用性群組會提升為主要。 

若要避免暫時指向與容錯移轉前次要節點的 IP 位址，請加入排序條件約束。 

若要加入排序條件約束，請在一個節點上執行下列命令：

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>在設定叢集，並新增為叢集資源的可用性群組之後，您無法使用 TRANSACT-SQL 來容錯移轉可用性群組資源。 在 Linux 上的 SQL Server 叢集資源未結合緊密與作業系統和它們在 Windows Server 容錯移轉叢集 (WSFC)。 SQL Server 服務並不知道叢集的目前狀態。 所有的協調流程是透過叢集管理工具。 在 RHEL 或 Ubuntu 會使用`pcs`並且在 SLES 使用`crm`工具。 

手動容錯移轉之可用性群組的`pcs`。 不會起始與 TRANSACT-SQL 的容錯移轉。 如需相關指示，請參閱 <<c0> [ 容錯移轉](sql-server-linux-availability-group-failover-ha.md#failover)。

## <a name="next-steps"></a>後續步驟

[操作 HA 可用性群組](sql-server-linux-availability-group-failover-ha.md)
