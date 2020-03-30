---
title: 可用性群組部署模式 - Linux 上的 SQL Server
description: 了解 Linux 伺服器上 SQL Server Always On 可用性群組的支援部署設定。
ms.custom: seo-lt-2019
ms.date: 04/17/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: 2fea849a46dea302dccba3ae8648db3654c35798
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558471"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>可用性群組設定的高可用性和資料保護

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供 Linux 伺服器上 SQL Server Always On 可用性群組的支援部署設定。 可用性群組支援高可用性和資料保護。 容錯移轉後的自動失敗偵測、自動容錯移轉和透明重新連線提供高可用性。 同步處理的複本則提供資料保護。 

在 Windows Server 容錯移轉叢集 (WSFC) 上，高可用性的常見設定會使用兩個同步複本和第三個伺服器或檔案共用來提供仲裁。 檔案共用見證會驗證可用性群組設定，例如同步處理的狀態，以及複本的角色。 此設定可確保選擇作為容錯移轉目標的次要複本，具有最新的資料和可用性群組設定變更。 

WSFC 會同步處理可用性群組複本與檔案共用見證之間，容錯移轉仲裁的設定中繼資料。 當可用性群組不在 WSFC 上時，SQL Server 執行個體會將設定中繼資料存放在 master 資料庫中。

例如，Linux 叢集上的可用性群組具有 `CLUSTER_TYPE = EXTERNAL`。 沒有任何 WSFC 可仲裁容錯移轉。 在此情況下，設定中繼資料會由 SQL Server 執行個體進行管理和維護。 由於此叢集中沒有見證伺服器，因此需要第三個 SQL Server 執行個體來儲存設定狀態中繼資料。 這三個 SQL Server 執行個體同時提供叢集的分散式中繼資料儲存體。 

叢集管理員可以查詢可用性群組中的 SQL Server 執行個體，並協調容錯移轉以維持高可用性。 在 Linux 叢集中，Pacemaker 是叢集管理員。 

SQL Server 2017 CU 1 可針對將 `CLUSTER_TYPE = EXTERNAL` 用於兩個同步複本，加上僅限設定複本的可用性群組，啟用高可用性。 僅限設定複本可以裝載於任何版本的 SQL Server 2017 CU1 或更新版本 (包括 SQL Server Express Edition) 上。 僅限設定複本會維護 master 資料庫中可用性群組的設定資訊，但不包含可用性群組中的使用者資料庫。 

## <a name="how-the-configuration-affects-default-resource-settings"></a>設定如何影響預設資源設定

SQL Server 2017 引進 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 叢集資源設定。 此設定可確保在主要複本認可每個交易之前，指定的次要複本數目會寫入交易資料以進行記錄。 當您使用外部叢集管理員時，這項設定會影響高可用性和資料保護。 設定的預設值取決於建立叢集資源時其架構。 當您安裝 SQL Server 資源代理程式 `mssql-server-ha` 並為可用性群組建立叢集資源時，叢集管理員會偵測可用性群組設定並設定 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`。 

如果設定支援，資源代理程式參數 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 會設定為提供高可用性和資料保護的值。 如需詳細資訊，請參閱[了解 SQL Server 的 Pacemaker 資源代理程式](#pacemakerNotify)。

下列各節說明叢集資源的預設行為。 

請選擇可用性群組設計，以符合高可用性、資料保護及讀取級別的特定商務需求。

下列設定描述可用性群組的設計模式，以及每個模式的功能。 這些設計模式適用於高可用性解決方案中 `CLUSTER_TYPE = EXTERNAL` 的可用性群組。 

- **三個同步複本**
- **兩個同步複本**
- **兩個同步複本和僅限設定複本**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>三個同步複本

此設定包含三個同步複本。 根據預設，它提供高可用性和資料保護。 它也可以提供讀取級別。

![三個複本][3]

具有三個同步複本的可用性群組可提供讀取級別、高可用性和資料保護。 下表描述可用性行為。 

| |讀取級別|高可用性與 </br> 資料保護 | 資料保護|
|:---|---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>\*</sup>|2|
|主要複本中斷 |自動容錯移轉。 新的主要複本是 R/W。 |自動容錯移轉。 新的主要複本是 R/W。 |自動容錯移轉。 在先前的主要複本復原並聯結可用性群組作為次要複本之前，新的主要複本無法供使用者交易使用。 |
|一個次要複本中斷  | 主要複本是 R/W。 如果主要複本失敗，則不會進行自動容錯移轉。 |主要複本是 R/W。 如果主要複本也失敗，則不會進行自動容錯移轉。 | 主要複本無法供使用者交易使用。 |

<sup>\*</sup> 預設

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>兩個同步複本

此設定可啟用資料保護。 就像其他可用性群組設定一樣，它可以啟用讀取級別。 兩個同步複本設定並不提供自動高可用性。 兩個複本設定僅適用於 SQL Server 2017 RTM，SQL Server 2017 的更高版本 (CU1 和更新版本) 不再支援此設定。

![兩個同步複本][1]

具有兩個同步複本的可用性群組提供讀取級別和資料保護。 下表描述可用性行為。 

| |讀取級別 |資料保護|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|主要複本中斷 | 手動容錯移轉。 可能會遺失資料。 新的主要複本是 R/W。| 自動容錯移轉。 在先前的主要複本復原並聯結可用性群組作為次要複本之前，新的主要複本無法供使用者交易使用。|
|一個次要複本中斷  |主要複本是 R/W，執行時暴露在遺失資料風險下。 |在次要複本復原之前，主要複本無法供使用者交易使用。|

<sup>\*</sup> 預設

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>兩個同步複本和僅限設定複本

具有兩個 (或以上) 同步複本和僅限設定複本的可用性群組可提供資料保護，還可能會提供高可用性。 下圖呈現這個架構：

![僅限設定的可用性群組][2]

1. 將使用者資料同步複寫到次要複本。 它也包含可用性群組的設定中繼資料。
2. 同步複寫可用性群組的設定中繼資料。 它不會包含使用者資料。

在可用性群組圖表中，主要複本會將設定資料推送至次要複本和僅限設定複本。 次要複本也會接收使用者資料。 僅限設定複本不會接收使用者資料。 次要複本處於同步可用性模式。 僅限設定複本不包含可用性群組中的資料庫，只包含有關可用性群組的中繼資料。 只會以同步方式認可僅限設定複本上的設定資料。

> [!NOTE]
> 具有僅限設定複本的可用性群組是 SQL Server 2017 CU1 的新增功能。 可用性群組中的所有 SQL Server 執行個體都必須是 SQL Server 2017 CU1 或更新版本。 

`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 的預設值為 0。 下表描述可用性行為。 

| |高可用性與 </br> 資料保護 | 資料保護|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|主要複本中斷 | 自動容錯移轉。 新的主要複本是 R/W。 | 自動容錯移轉。 新的主要複本無法供使用者交易使用。 |
|次要複本中斷 | 主要複本是 R/W，執行時暴露在遺失資料風險下 (如果主要複本失敗且無法復原)。 如果主要複本也失敗，則不會進行自動容錯移轉。 | 主要複本無法供使用者交易使用。 如果主要複本也失敗，則沒有任何可容錯移轉的複本。 |
|僅限設定複本中斷 | 主要複本是 R/W。 如果主要複本也失敗，則不會進行自動容錯移轉。 | 主要複本是 R/W。 如果主要複本也失敗，則不會進行自動容錯移轉。 |
|同步次要 + 僅限設定複本中斷| 主要複本無法供使用者交易使用。 不會進行自動容錯移轉。 | 主要複本無法供使用者交易使用。 如果主要複本也失敗，則沒有任何可容錯移轉的複本。 |

<sup>\*</sup> 預設

> [!NOTE]
> 裝載僅限設定複本的 SQL Server 執行個體也可以裝載其他資料庫。 它也可以參與作為多個可用性群組的僅限設定資料庫。 

## <a name="requirements"></a>需求

- 具有僅限設定複本的可用性群組中所有複本，都必須是 SQL Server 2017 CU 1 或更新版本。
- 任何版本的 SQL Server 都可以裝載僅限設定複本，包括 SQL Server Express。 
- 除了主要複本之外，可用性群組至少需要一個次要複本。
- 僅限設定複本不會計入每個 SQL Server 執行個體的複本數目上限。 SQL Server Standard Edition 最多允許三個複本，SQL Server Enterprise Edition 最多允許 9 個。

## <a name="considerations"></a>考量

- 每個可用性群組不能有一個以上的僅限設定複本。 
- 僅限設定複本不能是主要複本。
- 您無法修改僅限設定複本的可用性模式。 若要從僅限設定複本變更為同步或非同步次要複本，請移除僅限設定複本，並新增具有所需可用性模式的次要複本。 
- 僅限設定複本會與可用性群組的中繼資料同步。 沒有使用者資料。 
- 具有一個主要複本和一個僅限設定複本，但沒有次要複本的可用性群組無效。 
- 您無法在 SQL Server Express Edition 的執行個體上建立可用性群組。 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>了解 SQL Server 的 Pacemaker 資源代理程式

SQL Server 2017 CTP 1.4 已將 `sequence_number` 新增至 `sys.availability_groups`，以允許 Pacemaker 識別次要複本與主要複本保持同步的方式。 `sequence_number` 是依序遞增的 BIGINT，表示本機可用性群組複本的最新狀態。 Pacemaker 會以每個可用性群組的設定變更來更新 `sequence_number`。 設定變更的範例包括容錯移轉、新增或移除複本。 這個數字會在主要複本上更新，然後複寫到次要複本。 因此，具有最新設定的次要複本與主要複本序號相同。 

當 Pacemaker 決定要將複本升級為主要複本時，它會先傳送「預先升級」  通知到所有複本。 這些複本會傳回序號。 接下來，當 Pacemaker 實際嘗試將複本升級為主要複本時，如果該複本的序號為所有序號中最高者，則只會升級複本本身。 如果它自己的序號不符合最高序號，則複本會拒絕升級作業。 如此一來，只有序號最高的複本可以升級為主要複本，確保不會遺失資料。 

此處理序至少需要一個可供升級且其序號與前一個主要複本相同的複本。 Pacemaker 資源代理程式會設定 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`，以便至少有一個同步次要複本是最新狀態，且預設可作為自動容錯移轉的目標。 透過每個監視動作，會計算 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 的值 (並在必要時更新)。 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 值是「同步複本的數目」除以 2。 在容錯移轉時，資源代理程式需要 (`total number of replicas` - `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 個複本) 來回應預先升級通知。 具有最高 `sequence_number` 的複本會升級為主要複本。 

例如，具有三個同步複本 (一個主要複本和兩個同步次要複本) 的可用性群組。

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 為 1；(3 / 2 -> 1)。

- 要回應預先升級動作的必要複本數為 2；(3 - 1 = 2)。 

在此案例中，兩個複本必須回應才能觸發容錯移轉。 若要在主要複本中斷後成功進行自動容錯移轉，這兩個次要複本都必須是最新狀態，且回應預先升級通知。 如果它們在線上且同步，則其序號相同。 可用性群組會升級其中一個複本。 如果只有其中一個次要複本回應預先升級動作，資源代理程式無法保證回應的次要複本具有最高 sequence_number，因此不會觸發容錯移轉。

> [!IMPORTANT]
> 當 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 為 0 時，有遺失資料的風險。 在主要複本中斷期間，資源代理程式不會自動觸發容錯移轉。 您可以等候主要複本復原，或使用 `FORCE_FAILOVER_ALLOW_DATA_LOSS` 進行手動容錯移轉。

您可以選擇覆寫預設行為，並防止可用性群組資源自動設定 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`。

下列指令碼會將名為 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 的可用性群組上 `<**ag1**>` 設為 0。 執行之前，請以您的可用性群組名稱取代 `<**ag1**>`。

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

若要還原為預設值，請根據可用性群組設定執行：

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

> [!NOTE]
> 當您執行上述命令時，主要複本會暫時降級為次要複本，然後再次升級。 資源更新會導致所有複本停止並重新啟動。 只有在重新啟動複本之後，才會設定 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 的新值，而不是立即設定。

## <a name="see-also"></a>另請參閱

[Linux 上的可用性群組](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
