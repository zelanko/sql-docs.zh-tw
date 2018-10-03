---
title: Always On 可用性群組，在 Linux 上的 SQL server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: 6bc375492034f4e9b05eda85805cd452fe6d3557
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723186"
---
# <a name="always-on-availability-groups-on-linux"></a>Always On Linux 上的可用性群組

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明 Alwayson 可用性群組 (Ag) 在以 Linux 為基礎的特性[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]安裝。 它也包含 Linux 和 Windows Server 容錯移轉叢集 (WSFC) 之間的差異-基礎 Ag。 請參閱[以 Windows 為基礎的文件](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)的基本概念的 Ag，因為它們在 Windows 和 Linux 除了 WSFC 上運作方式相同。

從高階觀點而言，可用性群組底下[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Linux 上是相同的 WSFC 為基礎的實作。 這表示，所有的限制和功能都相同，但有些例外狀況。 主要差異包括：

-   Microsoft Distributed Transaction Coordinator (DTC) 不支援在 Linux 中[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如果您的應用程式需要使用分散式交易，而且需要 AG，部署[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]在 Windows 上。
-   以 Linux 為基礎的部署使用 Pacemaker，而不是 WSFC。
-   不同於大部分的 Workgroup 叢集案例除外的 Ag 在 Windows 上設定，Pacemaker 永遠不需要 Active Directory 網域服務 (AD DS)。
-   如何容錯到另一個節點從 AG 是 Linux 和 Windows 之間不同。
-   某些設定，例如`required_synchronized_secondaries_to_commit`只可以透過在 Linux 上的 Pacemaker 而以 WSFC 為基礎的安裝是使用 TRANSACT-SQL。

## <a name="number-of-replicas-and-cluster-nodes"></a>複本數和叢集節點

中的 AG[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]可以有兩個總計的複本： 一個主要及一個僅適用於可用性進行的次要複本。 它不能用於其他用途，例如可讀取的查詢。 中的 AG[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]可以有總計最多 9 個複本： 一個主要和最多八個次要資料庫，其中多達三 （包括主要） 可以是同步。 如果使用基礎叢集，可以有 16 個節點總計最多涉及 Corosync 時。 可用性群組可以跨越最多 9 個具有 16 個節點[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]，而另兩個[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]。

必須能夠自動容錯移轉至另一個複本的兩個複本組態需要僅設定的複本，使用，如中所述[僅設定的複本和仲裁](#configuration-only-replica-and-quorum)。 僅設定的複本中導入[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]Cumulative Update 1 (CU1)，因此，應該是部署此組態的最小版本。

如果使用 Pacemaker，則它必須正確設定讓它保持啟動並執行。 這表示，仲裁和 STONITH 必須正確地實作才 Pacemaker 的觀點而言，除了任何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]需求，例如僅設定的複本。

可讀取次要複本，只支援[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]。

## <a name="cluster-type-and-failover-mode"></a>叢集類型和容錯移轉模式

剛接觸[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]是引進的叢集類型的 Ag。 針對 Linux，有兩個有效的值： External 和 None。 叢集類型的外部表示 Pacemaker 用以 AG 底下。 使用外部叢集類型需要容錯移轉模式設定為 外部也 (新功能[!INCLUDE[sssql17-md](../includes/sssql17-md.md)])。 支援自動容錯移轉，但不同於 WSFC 容錯移轉模式設定為外部，不是自動的當 Pacemaker 會使用。 不同於 WSFC AG 設定後，會建立 AG 的 Pacemaker 部分。

叢集類型為 None 表示不需要，也將 AG 使用，Pacemaker。 即使在伺服器上已設定的 Pacemaker，AG 是否設有叢集類型為 None、 Pacemaker 將會看見或管理該 AG。 None 叢集類型只支援手動的容錯移轉從主要到次要複本。 建立具有無 AG 主要被針對讀取向外延展案例，以及升級。 雖然它可在災害復原或其中任何自動容錯移轉是必要的本機可用性等的情況下，不建議。 接聽程式的案例也是更複雜，而不需要 Pacemaker。

叢集類型會儲存在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]動態管理檢視 (DMV) `sys.availability_groups`，資料行中`cluster_type`和`cluster_type_desc`。

## <a name="requiredsynchronizedsecondariestocommit"></a>必要\_同步處理\_次要\_到\_認可

剛接觸[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]設定，可由呼叫的 Ag `required_synchronized_secondaries_to_commit`。 這會告訴 AG 必須與主要的密集的次要複本的數目。 這可讓自動容錯移轉 （只與 Pacemaker 叢集類型的外部整合） 時，等項目，並控制的主要可用性等的行為，如果正確的次要複本的數目是線上或離線。 若要深入了解其運作方式，請參閱[可用性群組組態的高可用性和資料保護](sql-server-linux-availability-group-ha.md)。 `required_synchronized_secondaries_to_commit`值是預設設定和維護的 Pacemaker /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 您可以手動覆寫此值。

組合`required_synchronized_secondaries_to_commit`和新的序號 (其會儲存於`sys.availability_groups`) 會通知 Pacemaker 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，比方說，自動容錯移轉可能會發生。 在此情況下，次要複本會有相同的順序編號為主要，也就是說，它最新狀態的最新的組態資訊。

有三個值可以設給`required_synchronized_secondaries_to_commit`: 0、 1 或 2。 控制行為的複本變成無法使用時，會發生什麼事。 數字對應必須與主要同步的次要複本的數目。 行為會低於 Linux，如下所示：

-   0 – 不自動容錯移轉是可能這是因為沒有次要複本需要同步處理。 隨時都可在主要資料庫。
-   1 – 一個次要複本必須位於與主要; 已同步處理狀態可以自動容錯移轉。 主要資料庫是無法使用，直到次要同步複本為止。
-   2 – 中的三個或多個節點 AG 組態兩個次要複本必須與主要; 同步處理可以自動容錯移轉。

`required_synchronized_secondaries_to_commit` 控制不只具有同步複本，但資料遺失的容錯移轉行為。 值為 1 或 2，次要複本時一律需要同步處理，因此資料備援。 這表示不會遺失資料。

若要變更的值`required_synchronized_secondaries_to_commit`，使用下列語法：

>[!NOTE]
>變更值，會導致資源以重新啟動，這表示短暫中斷。 若要避免這個問題的唯一方法是設定為不受叢集暫時資源。

**Red Hat Enterprise Linux (RHEL) 和 Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

何處*AGResourceName* ag，設定資源的名稱並*值*是 0、 1 或 2。 您可以將它設回 Pacemaker 管理參數的預設值，請執行相同的陳述式，而且沒有值。

符合下列條件時，就可能自動容錯移轉 AG 的：

-   主要和次要複本設定為同步資料移動。
-   次要資料庫都有狀態的同步處理 （未進行同步處理），這表示兩個位於相同的資料點。
-   叢集類型設定為外部。 自動容錯移轉不可能的叢集類型為 None。
-   `sequence_number`次要複本變成主要資料庫會有最高的順序號碼 – 亦即，次要複本的`sequence_number`符合從原始的主要複本。

如果符合這些條件，而裝載主要複本的伺服器失敗，AG 會變成同步複本的擁有權。 同步複本的行為 (這可以有三個的總計： 一個主要複本和兩個次要複本) 可以進一步控制`required_synchronized_secondaries_to_commit`。 這適用於 Windows 與 Linux Ag，但設定的設定完全不同。 在 Linux 上，此值會自動由本身的 AG 資源上的叢集設定。

## <a name="configuration-only-replica-and-quorum"></a>僅設定的複本和仲裁

新功能[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]CU1 是僅設定的複本。 Pacemaker 是 WSFC 的不同，因為仲裁，並需要 STONITH，尤其擁有只是兩個節點組態不能說到 AG。 針對 FCI，Pacemaker 所提供的仲裁機制可能沒問題，因為所有的 FCI 容錯移轉仲裁會在叢集層。 在 Linux 的仲裁會在 ag 中， [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]、 儲存的所有中繼資料。 這是僅設定的複本會發揮作用。

沒有任何其他項目，第三個節點和至少一個同步處理的複本會是必要。 這不可行的[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]，因為它只能有兩個參與 AG 的複本。 僅設定的複本會儲存在 master 資料庫中，相同的 AG 組態中的其他複本 AG 組態。 僅設定的複本並沒有在 AG 中參與的使用者資料庫。 設定資料會從主要以同步方式傳送。 這項組態資料則會使用在容錯移轉期間，無論是自動或手動。

為了維持仲裁，並啟用自動容錯移轉的外部叢集類型 AG，它是必須：

-   有三個同步複本 ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]只); 或
-   有兩個複本 （主要和次要），以及僅限設定的複本。

是否使用外部，就會發生手動容錯移轉或 None 叢集類型 AG 組態。 僅設定的複本可以設定 none 叢集類型 AG，而不建議您使用，因為它變得非常複雜的部署。 如需這些組態中，以手動方式修改`required_synchronized_secondaries_to_commit`具有至少 1 的值，使其沒有至少一個同步處理的複本。

僅設定的複本可以任何版本上裝載[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，包括[!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]。 這會減少授權成本，並確保它使用中的 Ag [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]。 這表示第三個必要的伺服器只需要符合的最小規格[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，因為它不會接收使用者交易流量 ag。

使用僅設定的複本時，它會有下列行為：

-   根據預設，`required_synchronized_secondaries_to_commit`設為 0。 這可以手動修改為 1 如有需要。
-   如果主要複本失敗和`required_synchronized_secondaries_to_commit`為 0，次要複本會變成新主要資料庫，並可供讀取和寫入。 如果值為 1，自動容錯移轉，就會發生，但另一個複本上線之前，則不會接受新的交易。
-   如果次要複本失敗和`required_synchronized_secondaries_to_commit`為 0，主要複本仍可接受的交易，但如果主要複本失敗，此時，沒有任何保護資料，也不可能的容錯移轉 （手動或自動），因為沒有次要複本。
-   如果僅設定的複本失敗，AG 會正常運作，但是沒有自動容錯移轉。
-   如果僅設定的複本和同步的次要複本失敗，主要無法接受的交易，以及這裡沒有地方要容錯到主要。

在 CU1 的已知的 bug 中沒有產生透過 corosync.log 檔案中的記錄`mssql-server-ha`。 如果次要複本無法成為主要，因為需要可用的複本數目，目前的訊息指出 「 預期收到 1 的序號，但只收到 2。 沒有足夠的複本都在線上安全地將升級的本機複本。 」 要反轉的數字，而且應該是 「 預期會收到 2 的序號，但只收到 1。 沒有足夠的複本都在線上安全地將升級的本機複本。 」 

## <a name="multiple-availability-groups"></a>多個可用性群組 

每個 Pacemaker 叢集或一組伺服器，您可以建立多個 AG。 唯一的限制是系統資源。 顯示主要 AG 的擁有權。 不同的 Ag 只能為不同的節點;並非全都必須有相同的節點上執行它們。

## <a name="drive-and-folder-location-for-databases"></a>資料庫的磁碟機和資料夾位置

在以 Windows 為基礎的 Ag 上, 參與 AG 中的使用者資料庫的磁碟機和資料夾結構應該相同。 例如，如果使用者資料庫都在`/var/opt/mssql/userdata`應該在伺服器 A 上，伺服器 b 上存在同一個資料夾唯一的例外一節中所述[互通性，以 Windows 為基礎的可用性群組和複本](#interoperability-with-windows-based-availability-groups-and-replicas)。

## <a name="the-listener-under-linux"></a>在 Linux 接聽程式

接聽程式是 ag 的選用功能。 使應用程式和終端使用者不需要知道哪一部伺服器裝載資料，它可以提供所有連線 （讀取/寫入的主要複本和/或唯讀次要複本） 的單一進入點。 在 WSFC 中，這會是一個網路名稱資源與 IP 資源，然後註冊於 AD DS （如果需要） 的組合以及 DNS。 AG 資源本身結合，它會提供該抽象概念。 如需有關接聽程式的詳細資訊，請參閱[接聽程式、 用戶端連接性及應用程式容錯移轉](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)。

在 Linux 的接聽程式的設定不同，但其功能都相同。 沒有在 Pacemaker 中的網路名稱資源的概念，也不建立在 AD DS; 中的物件沒有只是 IP 位址資源建立 pacemaker 可以在任一個節點上執行。 必須建立相關聯的 「 易記名稱 」 在 DNS 中的接聽程式 IP 資源的項目。 接聽程式 IP 資源，才會在裝載該可用性群組之主要複本的伺服器上作用。

如果 Pacemaker 會使用和建立與接聽程式相關聯的 IP 位址資源，會有短暫中斷，IP 位址在一部伺服器會停止，並在另一個，開始是否自動或手動容錯移轉。 雖然這可透過單一的名稱和 IP 位址的組合的抽象概念，它不會加上遮罩中斷。 應用程式必須能夠處理由某一種能夠偵測到此資料並重新連線的中斷連線。

不過，DNS 名稱和 IP 位址的組合是仍然不足，無法提供的 WSFC 上的接聽程式提供，例如唯讀路由的次要複本的所有功能。 在設定時設定 AG，仍然需要 「 接聽程式 」 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 這可以看到 「 精靈 」，以及 TRANSACT-SQL 語法。 有兩種方式，這可以設定為 Windows 上的相同函式：

-   為外部叢集類型 ag，IP 位址相關聯 「 接聽程式 」 中建立[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]應該在 Pacemaker 中建立之資源的 IP 位址。
-   建立使用 None 叢集類型 ag，使用與主要複本相關聯的 IP 位址。

然後提供的 IP 位址與相關聯的執行個體變成唯讀路由要求，從應用程式等協調器。

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>以 Windows 為基礎的可用性群組和複本的互通性 

叢集類型 External 或另一個則是 WSFC AG 不能跨平台及其複本。 這是 true AG 是否[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]或[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]。 這表示在傳統的 AG 組態與基礎的叢集，一個複本不可位於 WSFC，而另一個在 Linux 上使用 Pacemaker。

None 叢集類型 AG 可以跨 OS 界限，因此在相同 AG 中可能有兩個 Linux 和 Windows 為基礎的複本及其複本。 以下是範例的主要複本所在 Windows 為基礎，而次要資料庫位於其中一個 Linux 散發套件。

![混合式無](./media/sql-server-linux-availability-group-overview/image1.png)

分散式的 AG 也可以跨 OS 界限。 基礎 Ag 會繫結規則的設定方式，例如使用外部要設定 Linux 專用，但無法使用 WSFC 設定已加入至 AG。 請設想下列範例：

![混合式 Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>後續步驟
[設定 Linux 上的 SQL Server 可用性群組](sql-server-linux-availability-group-configure-ha.md)

[Linux 上的 SQL Server 設定讀取級別可用性群組](sql-server-linux-availability-group-configure-rs.md)

[在 RHEL 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-rhel.md)

[在 SLES 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-sles.md)

[在 Ubuntu 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-ubuntu.md)

[設定跨平台可用性群組](sql-server-linux-availability-group-cross-platform.md)

