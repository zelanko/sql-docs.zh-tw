---
title: Alwayson 可用性群組的 SQL Server on Linux |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.workload: On Demand
ms.openlocfilehash: 9d442c41adaec7148b3eb0259f851fee3fd2b683
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="always-on-availability-groups-on-linux"></a>Always On Linux 上的可用性群組

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明 Alwayson 可用性群組 (Ag) 的特性下以 Linux 為基礎[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]安裝。 其中也涵蓋 Linux 和 Windows Server 容錯移轉叢集 (WSFC) 之間的差異-基礎 Ag。 請參閱[Windows 為基礎的文件](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)的基本概念的 Ag，為他們在 Windows 和 Linux 除了 WSFC 上的運作方式相同。

從高階觀點來看，可用性群組底下[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]on Linux 是否相同它們是在 WSFC 為基礎的實作。 這表示所有限制和功能都相同，但有些例外狀況。 主要的差異包括：

-   Microsoft Distributed Transaction Coordinator (DTC) 不支援在 Linux 中[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]。 如果您的應用程式都需要使用分散式交易，而且需要 AG，部署[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Windows 上。
-   以 Linux 為基礎的部署使用 Pacemaker 而不是在 WSFC。
-   不同於大部分的工作群組的叢集案例除外 Ag Windows 上的設定，Pacemaker 永遠不需要 Active Directory 網域服務 (AD DS)。
-   如何失敗到另一個節點從 AG 是 Linux 和 Windows 之間不同。
-   某些設定，例如`required_synchronized_secondaries_to_commit`只能變更透過 Pacemaker on Linux，而 WSFC 為基礎的安裝使用 Transact SQL。

## <a name="number-of-replicas-and-cluster-nodes"></a>複本與叢集節點數目

中的 AG[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]可以有兩個的總計複本： 一個主要和一個次要資料庫僅為了提供可用性而使用。 它不能用於其他用途，例如可讀取的查詢。 中的 AG[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]可以有最多 9 個的總計複本： 一個主要和最多八個次要資料庫，其中多達三 （包括主要） 可以是同步。 如果使用基礎叢集，可以有最多 16 個節點的總當 Corosync 涉及。 可用性群組可以跨越九個最多 16 個節點與[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]，和與兩個[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]。

中所述，需要能夠自動容錯移轉至另一個複本的兩個複本設定需要設定專用的複本，使用[設定唯讀複本和仲裁](#configuration-only-replica-and-quorum)。 設定複本中導入了[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]累計更新 1 (CU1)，因此，應該是部署此組態的最小版本。

如果使用 Pacemaker 時，它必須正確設定讓它保持啟動且正在執行。 這表示，仲裁及 STONITH 必須正確地實作 Pacemaker 的觀點而言，除了任何[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]需求，例如設定唯讀複本。

可讀取次要複本，只支援[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]。

## <a name="cluster-type-and-failover-mode"></a>叢集類型和容錯移轉模式

若要新[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]是 Ag 叢集類型的簡介。 適用於 Linux，有兩個有效的值： 外部和 None。 叢集類型的外部表示 Pacemaker 做 AG 下方。 為叢集類型需要容錯移轉模式設定為外部也使用外部 (還有一個新功能[!INCLUDE[sssql17-md](../includes/sssql17-md.md)])。 支援自動容錯移轉，但不同於在 WSFC 中，容錯移轉模式設定為外部、 不自動，使用 Pacemaker 時。 不同於在 WSFC 中，AG 設定後，會建立 AG 的 Pacemaker 部分。

叢集類型為 None 表示不需要也將 AG 使用，Pacemaker。 即使在伺服器上有設定 Pacemaker，AG 是否設定叢集類型為 None、 Pacemaker 無法看到或管理該 AG。 無叢集類型只支援從主手動容錯移轉至次要複本。 建立具有無 AG 主要被針對讀取向外延展案例，以及升級。 雖然它可以在其中沒有自動容錯移轉是必要的本機可用性嚴重損壞修復等的情況下運作，但不建議。 接聽程式劇本也是沒有 Pacemaker 更複雜的。

叢集類型會儲存在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]動態管理檢視 (DMV) `sys.availability_groups`，資料行中`cluster_type`和`cluster_type_desc`。

## <a name="requiredsynchronizedsecondariestocommit"></a>需要\_同步\_次要\_至\_認可

新手[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]是設定，可由呼叫 Ag `required_synchronized_secondaries_to_commit`。 這會告訴 AG 必須與主要 lockstep 的次要複本的數目。 這可讓之類的自動容錯移轉 （只有在與叢集類型為外部 Pacemaker 整合），並控制的主要可用性之類的行為，如果正確的次要複本的數目是線上或離線。 若要了解有關其運作方式的詳細資訊，請參閱[的可用性群組組態的高可用性與資料保護](sql-server-linux-availability-group-ha.md)。 `required_synchronized_secondaries_to_commit`值是預設設定和維護的 Pacemaker /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 您可以手動覆寫此值。

組合`required_synchronized_secondaries_to_commit`和新的序號 (其會儲存於`sys.availability_groups`) 會通知 Pacemaker 和[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，例如，自動容錯移轉可能會發生。 在此情況下，次要複本會有相同的順序編號為主要，也就是說，它最新狀態的最新的組態資訊。

有三個值可以設給`required_synchronized_secondaries_to_commit`: 0、 1 或 2。 這些控制行為的複本變成無法使用時，會發生什麼事。 數字對應必須與主要同步處理的次要複本的數目。 行為會低於 Linux，如下所示：

-   0 – 不自動容錯移轉會因為沒有次要複本需要同步處理。 隨時都可在主要資料庫。
-   1-一個次要複本必須位於與主要; 已同步處理狀態可能會自動容錯移轉。 同步次要複本可以使用之前，主要資料庫是無法使用。
-   2 – 在三個或多個節點 AG 組態兩個次要複本必須與主要; 同步處理可能會自動容錯移轉。

`required_synchronized_secondaries_to_commit` 控制不只具有同步複本，但資料遺失容錯移轉行為。 值為 1 或 2，次要複本永遠需要。 同步處理，因此資料備援性 這表示不會遺失資料。

若要變更的值`required_synchronized_secondaries_to_commit`，使用下列語法：

>[!NOTE]
>變更值，會導致重新啟動，資源表示短暫中斷。 若要避免此狀況的唯一方式是將設定不受叢集暫時資源。

**Red Hat Enterprise Linux (RHEL) 和 Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

其中*AGResourceName* ag，設定資源的名稱和*值*是 0、 1 或 2。 您可以將它設回 Pacemaker 管理參數的預設值，請執行相同的陳述式沒有值。

符合下列條件時，就可能的 AG 的自動容錯移轉：

-   主要和次要複本設定為同步的資料移動。
-   次要資料庫都有同步處理 （未進行同步處理），表示兩個在相同的資料點的狀態。
-   叢集類型設定為外部。 自動容錯移轉不可能叢集類型為 None。
-   `sequence_number`變成次要複本的主要具有最高的序號-亦即，次要複本的`sequence_number`符合從原始的主要複本。

如果符合這些條件，而裝載主要複本的伺服器失敗，AG 會變成同步複本的擁有權。 同步複本的行為 (其中可以有三個的總計： 一個主要和兩個次要複本) 可以進一步控制`required_synchronized_secondaries_to_commit`。 這適用於 Windows 和 Linux 上 Ag，但設定完全不同。 On Linux，值會自動根據本身的 AG 資源上的叢集設定。

## <a name="configuration-only-replica-and-quorum"></a>設定唯讀複本和仲裁

還有一個新功能[!INCLUDE[sssql17-md](../includes/sssql17-md.md)]CU1 為準，是只設定複本。 因為 Pacemaker 不同 WSFC，尤其是當談到仲裁和需要 STONITH，只要雙節點設定設定無法運作時 AG。 使用 fci，Pacemaker 所提供的仲裁機制可能沒問題，因為所有的 FCI 容錯移轉仲裁會發生在叢集的圖層。 中發生的 AG，仲裁下 Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]、 儲存的所有中繼資料。 這是設定唯讀複本會發揮作用。

沒有任何其他項目，第三個節點和至少一個同步處理的複本將會是必要。 這不適用於[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]，因為它只能有兩個複本 AG 中的參與。 設定唯讀複本會儲存在 master 資料庫中，AG 組態中的其他複本相同 AG 組態。 設定唯讀複本沒有參與 AG 中的使用者資料庫。 設定資料是從主要以同步方式傳送。 此設定資料則會使用容錯移轉期間，無論是自動或手動。

若要維持仲裁，並啟用自動容錯移轉叢集類型為外部 ag，它是必須：

-   有三個同步複本 ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]只); 或
-   有兩個複本 （主要和次要），以及設定唯一的複本。

不論使用的外部，可能會發生手動容錯移轉，或沒有任何叢集 AG 組態的類型。 雖然可以設定只設定複本與 AG 無叢集類型，不建議您使用，因為它變得非常複雜的部署。 這些設定，以手動方式修改`required_synchronized_secondaries_to_commit`具有至少 1 的值，使其沒有至少一個已同步處理的複本。

設定唯讀複本可裝載於任何版本的[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，包括[!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]。 這會減少授權成本並確保 Ag 中將它用於[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]。 這表示第三個必要的伺服器只需要以符合最小規格[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]，因為它不 AG 接收使用者交易流量。

使用僅限設定的複本時，它有下列行為：

-   根據預設，`required_synchronized_secondaries_to_commit`設為 0。 這可以手動修改，以 1 視。
-   如果主要失敗和`required_synchronized_secondaries_to_commit`為 0，次要複本會變成新的主要複本，並可供讀取和寫入。 如果值為 1，自動容錯移轉，就會發生，但另一個複本上線之前，則不會接受新的交易。
-   如果次要複本失敗和`required_synchronized_secondaries_to_commit`為 0，主要複本仍可接受的交易，但如果主要此時失敗，沒有任何保護的資料也不是可能的容錯移轉 （手動或自動），因為沒有次要複本。
-   如果僅設定複本失敗，AG 會正常運作，但是沒有自動容錯移轉。
-   如果同步次要複本，而且只設定複本失敗，主要無法接受的交易，而有無處可去主要失敗。

在 CU1 沒有已知的錯誤會產生透過 corosync.log 檔中記錄`mssql-server-ha`。 如果次要複本無法成為主要由於需要可用的複本數目，目前訊息指出 「 預期會收到 1 的序號，但只收到 2。 沒有足夠的複本都在線上安全地將升級的本機複本。 」 數字是應該相反的因此它應該會顯示 「 預期會收到 2 序號，但只接收 1。 沒有足夠的複本都在線上安全地將升級的本機複本。 」 

## <a name="multiple-availability-groups"></a>多個可用性群組 

每個 Pacemaker 叢集或一組伺服器，您可以建立一個以上的 AG。 唯一的限制是系統資源。 主要顯示 AG 擁有權。 可擁有不同的 Ag 的不同節點。並非所有需要的相同節點上執行它們。

## <a name="drive-and-folder-location-for-databases"></a>資料庫的磁碟機和資料夾位置

在 Windows 架構的 Ag，參與 AG 中的使用者資料庫的磁碟機和資料夾結構應該相同。 例如，如果使用者資料庫會處於`/var/opt/mssql/userdata`應該在伺服器 A 上，伺服器 b 上存在同一個資料夾唯一的例外一節中所述[與 Windows 架構的可用性群組和複本的互通性](#interoperability-with-windows-based-availability-groups-and-replicas)。

## <a name="the-listener-under-linux"></a>在 Linux 接聽程式

接聽程式是 AG 的選用功能。 如此應用程式和使用者不需要知道哪個伺服器主控資料，它提供所有連接 （讀取/寫入主要複本和/或唯讀次要複本） 的單一進入點。 在 WSFC 中，這可以是網路名稱資源和 IP 資源，然後登錄於 AD DS （如果需要） 的組合以及 DNS。 AG 資源本身的結合，它會提供該抽象概念。 如需有關接聽程式的詳細資訊，請參閱[接聽程式、 用戶端連接性及應用程式容錯移轉](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)。

在 Linux 接聽程式的設定不同，但其功能都相同。 沒有 Pacemaker，網路名稱資源的概念，也建立在 AD DS; 中的物件沒有剛 IP 位址資源可以在任一節點執行的 Pacemaker 中建立。 您必須建立相關聯的 「 易記名稱 」 在 DNS 中的接聽程式 IP 資源的項目。 接聽程式 IP 資源只能是裝載該可用性群組的主要複本的伺服器上使用中。

如果，Pacemaker 建立 IP 位址資源所關聯的接聽程式，會有短暫中斷如下的 IP 位址在一部伺服器上停止，並在另一個，開始其是否可以自動或手動容錯移轉。 這可透過單一的名稱和 IP 位址的組合的抽象概念，而它不會加上遮罩中斷。 應用程式必須能夠處理中斷連線，讓特定類型的偵測，並重新連接的功能。

不過，DNS 名稱和 IP 位址的組合是仍然不足，無法提供 WSFC 上的接聽程式提供，例如唯讀路由的次要複本的所有功能。 設定 AG 時, 「 接聽程式 」 仍必須設定在[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]。 這可以看到在此精靈，以及 TRANSACT-SQL 語法。 有兩種方式，這可以設定的運作與在 Windows 上相同：

-   叢集類型為外部 ag，IP 位址相關聯 「 接聽程式 」 中建立[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]應該 Pacemaker 中建立的資源的 IP 位址。
-   建立叢集類型為 None AG、 使用與主要複本相關聯的 IP 位址。

然後與提供的 IP 位址相關聯的執行個體成為唯讀路由要求，從應用程式之類的事情協調器。

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>與 Windows 架構的可用性群組和複本的互通性 

有叢集類型的外部或正在 WSFC AG 不能跨平台及其複本。 這是 true AG 是否[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]或[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]。 這表示具有基礎叢集的傳統 AG 組態中，一個複本不可以是 WSFC 和其他與 Pacemaker Linux 上。

叢集類型為 NONE AG 可以跨 OS 界限，因此相同的 AG 中可能有兩個 Linux 和 Windows 架構的複本及其複本。 以下是範例其中的主要複本時，Windows 為基礎，次要資料庫是 Linux 散發套件的其中一個。

![混合式無](./media/sql-server-linux-availability-group-overview/image1.png)

分散式的 AG 也可以跨 OS 界限。 基礎 Ag 由繫結規則的設定方式，例如一個設定為外部正在 Linux 僅限，但無法使用 WSFC 來設定它聯結至 AG。 請設想下列範例：

![混合式 Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>後續的步驟
[設定可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

[設定向外延展讀取可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-rs.md)

[RHEL 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-rhel.md)

[SLES 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-sles.md)

[在 Ubuntu 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-ubuntu.md)

[設定跨平台可用性群組](sql-server-linux-availability-group-cross-platform.md)

