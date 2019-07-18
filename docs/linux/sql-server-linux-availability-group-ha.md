---
title: SQL Server Always On 可用性群組部署模式
ms.date: 04/17/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: 637d67767e17344d63498f8cb6a141fa78b11ecb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996423"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>可用性群組組態的高可用性和資料保護

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章會提供支援的部署組態，SQL Server Always On 可用性群組中的 Linux 伺服器上。 可用性群組支援高可用性和資料保護。 自動的失敗偵測、 自動容錯移轉和透明容錯移轉之後的重新連線提供高可用性。 同步處理的複本提供資料保護。 

在 Windows Server 容錯移轉叢集 (WSFC)，以獲得高可用性的常見組態會使用兩個同步複本和第三個伺服器或檔案共用提供仲裁。 檔案共用見證，例如驗證的可用性群組設定-狀態同步處理，以及複本角色。 此組態可確保選擇為容錯移轉目標的最新的資料和可用性群組組態變更的次要複本。 

WSFC 會同步處理容錯移轉可用性群組複本之間的檔案共用見證的仲裁組態中繼的資料。 當可用性群組不是在 WSFC 上時，SQL Server 執行個體會儲存在 master 資料庫中的組態中繼資料。

例如，Linux 叢集上的可用性群組有`CLUSTER_TYPE = EXTERNAL`。 沒有任何 WSFC 裁定容錯移轉。 在此情況下的組態中繼資料是由管理和維護 SQL Server 執行個體。 在此叢集中沒有見證伺服器，因為第三個 SQL Server 執行個體，才能儲存的組態狀態中繼資料。 所有的三個 SQL Server 執行個體一起提供分散式的中繼資料儲存體叢集。 

「 叢集管理員可以查詢的 SQL Server 可用性群組 」 中的執行個體，並協調容錯移轉，以維持高可用性。 在 Linux 叢集中，Pacemaker 會是 「 叢集管理員。 

SQL Server 2017 CU 1 可讓可用性群組的高可用性`CLUSTER_TYPE = EXTERNAL`兩個同步複本，再加上僅限設定的複本。 僅限設定的複本可裝載於 SQL Server 2017 CU1 或更新版本-任何版本，包括 SQL Server Express edition。 僅限設定的複本會維護在 master 資料庫的可用性群組的組態資訊，但不包含可用性群組中的使用者資料庫。 

## <a name="how-the-configuration-affects-default-resource-settings"></a>設定如何影響預設資源設定

SQL Server 2017 引進`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`叢集資源設定。 此設定可確保指定的數目的次要複本寫入記錄之前的主要複本會認可每一筆交易的交易資料。 當您使用的外部叢集管理員時，此設定會影響高可用性和資料保護。 在建立叢集資源時，設定的預設值取決於架構。 當您安裝 SQL Server 資源代理程式- `mssql-server-ha` -建立可用性群組的叢集資源，「 叢集管理員會偵測可用性群組組態和設定`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`據此。 

如果支援的組態中，資源代理程式參數`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`設為提供高可用性和資料保護的值。 如需詳細資訊，請參閱 <<c0> [ 了解 SQL Server 資源代理程式，為 pacemaker](#pacemakerNotify)。

下列各節說明叢集資源的預設行為。 

選擇特定的商務需求的高可用性、 資料保護和讀取級別可用性群組的設計。

下列組態會描述可用性群組設計模式，以及每個模式的功能。 這些設計模式可套用至可用性群組搭配`CLUSTER_TYPE = EXTERNAL`高可用性解決方案。 

- **三個同步複本**
- **兩個同步複本**
- **兩個同步複本和僅限設定的複本**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>三個同步複本

此組態是由三個同步複本所組成。 根據預設，它會提供高可用性和資料保護。 它也提供讀取級別。

![三個複本][3]

讀取級別、 高可用性和資料保護，可以提供具有三個同步複本的可用性群組。 下表描述可用性的行為。 

| |讀取級別|高可用性 （& s) </br> 資料保護 | 資料保護|
|:---|---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>\*</sup>|2|
|主要複本中斷 |自動容錯移轉。 新的主要複本是 R / W |自動容錯移轉。 新的主要複本是 R / W |自動容錯移轉。 新的主要複本不是適用於使用者交易，直到先前的主要複本復原並聯結可用性群組做為次要。 |
|一個次要複本中斷  | 主要複本是 R / W 如果主要沒有自動容錯移轉會失敗。 |主要複本是 R / W 如果主要沒有自動容錯移轉也會失敗。 | 主要不適用於使用者交易。 |

<sup>\*</sup> 預設值

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>兩個同步複本

此設定可啟用資料保護。 類似可用性群組組態，它可以讓讀取級別。 兩個同步複本組態未提供自動的高可用性。 兩個複本設定只適用於 SQL Server 2017 RTM，且不再支援更高版本 (CU1 及更新版本) 的 SQL Server 2017 的版本...

![兩個同步複本][1]

具有兩個同步複本的可用性群組提供讀取級別和資料保護。 下表描述可用性的行為。 

| |讀取級別 |資料保護|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|主要複本中斷 | 手動容錯移轉。 可能會遺失資料。 新的主要複本是 R / W| 自動容錯移轉。 新的主要複本不是適用於使用者交易，直到先前的主要複本復原並聯結可用性群組做為次要。|
|一個次要複本中斷  |主要複本是 R/W，執行時暴露資料遺失。 |主要不適用於使用者交易直到次要複本復原為止。|

<sup>\*</sup> 預設值

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>兩個同步複本和僅限設定的複本

具有兩個 （含） 以上的同步複本和僅限設定複本的可用性群組提供資料保護，並可能也會提供高可用性。 下圖顯示此架構：

![設定唯一的可用性群組][2]

1. 使用者資料的次要複本的同步複寫。 它也包含可用性群組的組態中繼資料。
2. 可用性群組組態中繼資料的同步複寫。 它不包含使用者資料。

在可用性群組圖表中，主要複本會將組態資料推送至次要複本和僅限設定的複本。 次要複本也會收到使用者資料。 僅限設定的複本不會不會收到使用者資料。 次要複本都是同步的可用性模式。 僅限設定的複本不包含可用性群組-可用性群組的相關的中繼資料中的資料庫。 僅限設定的複本上的設定資料會以同步方式認可。

> [!NOTE]
> 僅限設定複本 availabilility 群組是新的 SQL Server 2017 CU1。 SQL Server 可用性群組中的所有執行個體必須是 SQL Server 2017 CU1 或更新版本。 

預設值為`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`為 0。 下表描述可用性的行為。 

| |高可用性 （& s) </br> 資料保護 | 資料保護|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|主要複本中斷 | 自動容錯移轉。 新的主要複本是 R / W | 自動容錯移轉。 新的主要不適用於使用者交易。 |
|次要複本中斷 | 主要複本是 R/W，公開執行資料遺失 （如果有主要失敗，且無法復原）。 如果主要沒有自動容錯移轉也會失敗。 | 主要不適用於使用者交易。 如果主要複本也失敗，容錯移轉至沒有複本。 |
|設定唯一的複本中斷 | 主要複本是 R / W 如果主要沒有自動容錯移轉也會失敗。 | 主要複本是 R / W 如果主要沒有自動容錯移轉也會失敗。 |
|同步次要 + 組態只複本中斷| 主要不適用於使用者交易。 沒有自動容錯移轉。 | 主要不適用於使用者交易。 如果容錯移轉沒有任何複本主要也會失敗。 |

<sup>\*</sup> 預設值

> [!NOTE]
> 裝載僅限設定複本的 SQL Server 執行個體也可以裝載其他資料庫。 它也可以做為多個可用性群組組態資料庫。 

## <a name="requirements"></a>需求

- 僅限設定複本的可用性群組中所有複本都必須都是 SQL Server 2017 CU 1 或更新版本。
- 任何版本的 SQL Server 可以裝載僅限設定複本，包括 SQL Server Express。 
- 可用性群組必須至少一個次要複本的詳細資訊-除了主要複本。
- 組態的唯一複本不會計入每個 SQL Server 執行個體的複本數目上限。 SQL Server standard 版本允許最多三個複本時，SQL Server Enterprise Edition 則允許最多 9。

## <a name="considerations"></a>考量

- 有一個僅限設定複本的每個可用性群組。 
- 僅限設定的複本不是主要複本。
- 您無法修改的僅限設定複本的可用性模式。 若要從僅限設定複本變更為同步或非同步的次要複本，移除僅限設定複本，並新增所需的可用性模式的次要複本。 
- 僅限設定的複本是同步的可用性群組中繼資料。 沒有任何使用者資料。 
- 具有一個主要複本和一個組態時，唯一的複本，但沒有次要複本的可用性群組不是有效的。 
- 您無法在 SQL Server Express edition 執行個體上建立可用性群組。 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>了解 SQL Server pacemaker 資源代理程式

加入 SQL Server 2017 CTP 1.4`sequence_number`至`sys.availability_groups`允許 Pacemaker 找出如何最新的次要複本會與主要複本。 `sequence_number` 是單純遞增的 BIGINT，表示如何最新的本機可用性群組複本。 Pacemaker 更新`sequence_number`每個可用性群組組態變更。 組態變更的範例包括容錯移轉、 複本新增或移除。 數字會在主要伺服器上，更新，然後複寫到次要複本。 因此次要複本具有最新的組態必須與主要資料庫相同的序號。 

當 Pacemaker 決定要升階為主要複本時，它會先傳送*預先升級*通知到所有複本。 的複本恢復的序號。 接下來，當 Pacemaker 實際嘗試將複本升級為主要，複本只會升級複本本身如果序號最高的序號。 如果它自己的序號不符合最高的序號，複本會拒絕升級作業。 如此一來，只有序號最高的複本可以升級為主要複本，確保不會遺失資料。 

此程序用於升級與先前的主要資料庫相同的序號必須至少一個複本可供使用。 Pacemaker 資源代理程式集`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`，至少一個同步次要複本是最新狀態並可依預設自動容錯移轉的目標。 每個監視動作的值與`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`計算 （和更新，如有必要）。 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`值是 '的同步複本數目' 除以 2。 在容錯移轉時需要的資源代理程式 (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`複本) 來回應預先升級通知。 具有最高的複本`sequence_number`升級為主要。 

例如，可用性群組具有三個同步複本-一個主要複本和兩個同步次要複本。

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 為 1;(3 / 2]-> [1)。

- 複本回應預先升級動作的必要的數目為 2;(3-1 = 2)。 

在此案例中，兩個複本必須回應才能觸發容錯移轉。 主要複本中斷後有成功的自動容錯移轉，這兩個次要複本必須是最新狀態，並回應預先升級通知。 如果它們是在線上而且同步，它們會有相同的序號。 可用性群組升級其中一個。 如果只有其中一個次要複本回應預先升級動作，資源代理程式無法保證回應的次要複本具有最高 sequence_number，且不會觸發容錯移轉。

> [!IMPORTANT]
> 當 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 為 0 時，有遺失資料的風險。 主要複本在中斷期間，資源代理程式不會自動觸發容錯移轉。 您可以等候主要複本以復原，或手動容錯移轉使用`FORCE_FAILOVER_ALLOW_DATA_LOSS`。

您可以選擇要覆寫預設行為，並避免設定可用性群組資源`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`自動。

下列指令碼會將`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`為 0，可用性群組上名為`<**ag1**>`。 執行之前，請以您的可用性群組名稱取代 `<**ag1**>`。

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

若要還原為預設值，根據執行的可用性群組組態：

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

> [!NOTE]
> 當您執行上述命令時，主要是暫時降級為次要，然後又升級一次。 資源更新會導致所有複本停止並重新啟動。 新值`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`只會在複本會重新啟動後，不會立即所設定。

## <a name="see-also"></a>另請參閱

[在 Linux 上的可用性群組](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
