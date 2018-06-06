---
title: SQL Server Always On 可用性群組部署模式 |Microsoft 文件
ms.custom: sql-linux
ms.date: 10/16/2017
ms.prod: sql
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: linux
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 36115370063292f3a3302dac4596222bb513fb67
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>可用性群組組態的高可用性與資料保護

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章會提供支援的部署組態，SQL Server Always On 可用性群組中的 Linux 伺服器上。 可用性群組支援高可用性和資料保護。 自動偵測、 自動容錯移轉和透明容錯移轉後的重新連線提供高可用性。 同步處理的複本提供資料保護。 

在 Windows Server 容錯移轉叢集 (WSFC)，高可用性的常見組態會使用兩個同步複本和第三個伺服器或檔案共用提供仲裁。 檔案共用見證，例如驗證的可用性群組設定-的同步處理的狀態和複本的角色。 此組態可確保所選為容錯移轉目標有最新的資料和可用性群組組態變更的次要複本。 

在 WSFC 會同步處理容錯移轉仲裁，可用性群組複本之間的檔案共用見證的組態中繼資料。 當可用性群組不是 WSFC 上時，SQL Server 執行個體會儲存在 master 資料庫中的組態中繼資料。

Linux 叢集上的可用性群組，例如具有`CLUSTER_TYPE = EXTERNAL`。 沒有任何 WSFC 裁定容錯移轉。 在此情況下的組態中繼資料是由管理和維護 SQL Server 執行個體。 在此叢集中沒有見證伺服器，因為第三個 SQL Server 執行個體，才能儲存的組態狀態中繼資料。 所有的三個 SQL Server 執行個體一起提供分散式的中繼資料儲存體叢集。 

叢集管理員可以查詢 SQL server 執行個體，在可用性群組中，並協調容錯移轉來維持高可用性。 在 Linux 叢集中，Pacemaker 會是叢集管理員。 

SQL Server 2017 CU 1 會啟用高可用性包含可用性群組的`CLUSTER_TYPE = EXTERNAL`兩個同步複本，再加上設定唯一的複本。 組態的唯一複本可裝載於任何版本的 SQL Server 2017 CU1 或更新版本-包括 SQL Server Express edition。 組態的唯一複本維護在 master 資料庫中的可用性群組的相關組態資訊，但不包含可用性群組中的使用者資料庫。 

## <a name="how-the-configuration-affects-default-resource-settings"></a>組態如何影響預設資源設定

SQL Server 2017 導入了`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`叢集資源設定。 此設定可確保指定的次要複本寫入數目記錄之前的主要複本會認可每一筆交易的交易資料。 當您使用外部叢集管理員時，此設定會影響高可用性和資料保護。 設定的預設值會取決於建立叢集資源時的架構。 當您安裝 SQL Server 資源代理程式- `mssql-server-ha` -並建立可用性群組的叢集資源，請叢集管理員偵測到可用性群組組態和設定`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`據此。 

如果組態中，資源代理程式參數的支援`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`設為提供高可用性與資料保護的值。 如需詳細資訊，請參閱[pacemaker 的了解 SQL Server 資源 agent](#pacemakerNotify)。

下列各節說明叢集資源的預設行為。 

選擇可用性群組設計，以符合特定的業務需求的高可用性、 資料保護和向外延展讀取。

下列設定說明的可用性群組的設計模式和每個模式的功能。 這些設計模式適用於可用性群組`CLUSTER_TYPE = EXTERNAL`的高可用性解決方案。 

- **三個同步複本**
- **兩個同步複本**
- **兩個同步複本和組態的唯一複本**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>三個同步複本

此組態是由三個同步複本所組成。 根據預設，它會提供高可用性與資料保護。 它也可以提供向外延展讀取。

![三個複本][3]

包含三個同步複本的可用性群組可向外延展讀取、 高可用性和資料保護。 下表描述可用性行為。 

| |向外延展讀取|高可用性 （& s) </br> 資料保護 | 資料保護
|:---|---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>*</sup>|2
|主要複本中斷 | 手動容錯移轉。 可能會遺失資料。 新的主要是 R / W |自動容錯移轉。 新的主要是 R / W |自動容錯移轉。 新的主要不是適用於使用者交易，直到復原先前主要資料庫加入可用性群組做為次要。 
|一個次要複本中斷  | 主要是 R / W 如果主要沒有自動容錯移轉會失敗。 |主要是 R / W 如果主要沒有自動容錯移轉也會失敗。 | 主要不適用於使用者交易。 
<sup>*</sup> 預設值

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>兩個同步複本

此設定可啟用資料保護。 可用性群組組態，例如，它可以啟用向外延展讀取。 兩個同步複本組態不提供自動的高可用性。 

![兩個同步複本][1]

包含兩個同步複本的可用性群組提供向外延展讀取和資料保護。 下表描述可用性行為。 

| |向外延展讀取 |資料保護
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|主要複本中斷 | 手動容錯移轉。 可能會遺失資料。 新的主要是 R / W| 自動容錯移轉。 新的主要不是適用於使用者交易，直到復原先前主要資料庫加入可用性群組做為次要。
|一個次要複本中斷  |主要是 R/W，以公開方式執行資料遺失。 |主要不適用於使用者交易直到次要的復原。
<sup>*</sup> 預設值

>[!NOTE]
>先前的案例是在 SQL Server 2017 CU 1 之前的行為。 

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>兩個同步複本和組態的唯一複本

包含兩個 （或以上） 的同步複本和組態的唯一複本的可用性群組提供資料保護，而且可能也提供高可用性。 下圖表示此架構：

![只有可用性群組組態][2]

1. 同步的使用者資料複寫至次要複本。 它也包含可用性群組組態中繼資料。
2. 可用性群組組態中繼資料同步複寫。 它不包含使用者資料。

在可用性群組圖表中，主要複本會將組態資料推送至次要複本並設定唯一的複本。 次要複本也會接收使用者資料。 組態的唯一複本不會接收使用者資料。 次要複本正在同步的可用性模式。 組態的唯一複本不包含可用性群組-可用性群組的相關的中繼資料中的資料庫。 組態的唯一複本上的設定資料會以同步方式認可。

>[!NOTE]
>設定只會複寫 availabilility 群組是新的 SQL Server 2017 CU1。 SQL Server 可用性群組中的所有執行個體必須是 SQL Server 2017 CU1 或更新版本。 

預設值為`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`為 0。 下表描述可用性行為。 

| |高可用性 （& s) </br> 資料保護 | 資料保護
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|主要複本中斷 | 自動容錯移轉。 新的主要是 R / W | 自動容錯移轉。 新的主要不適用於使用者交易。 
|次要複本中斷 | 主要是 R/W，公開執行資料遺失 （如果主要失敗，且無法復原）。 如果主要沒有自動容錯移轉也會失敗。 | 主要不適用於使用者交易。 沒有任何容錯移轉至主要複本也會失敗。 
|組態的唯一複本中斷 | 主要是 R / W 如果主要沒有自動容錯移轉也會失敗。 | 主要是 R / W 如果主要沒有自動容錯移轉也會失敗。 
|同步的次要 + 組態只複本中斷| 主要不適用於使用者交易。 沒有自動容錯移轉。 | 主要不適用於使用者交易。 如果容錯移轉沒有任何複本主要也會失敗。 
<sup>*</sup> 預設值

>[!NOTE]
>裝載組態的唯一複本的 SQL Server 執行個體也可以裝載其他資料庫。 它也可以做為多個可用性群組的組態資料庫。 

## <a name="requirements"></a>需求

* 與組態的唯一複本可用性群組中的所有複本都必須都是 SQL Server 2017 CU 1 或更新版本。
* 任何版本的 SQL Server 可以裝載設定唯一的複本，包括 SQL Server Express。 
* 可用性群組必須至少一個次要複本-除了主要複本。
* 組態的唯一複本不會計入每個 SQL Server 執行個體的複本數目上限。 SQL Server standard edition 則允許多達三個複本，SQL Server Enterprise Edition 則允許最多 9。

## <a name="considerations"></a>考量

* 不能超過一個組態時，每個可用性群組的唯一複本。 
* 組態的唯一複本不可為主要複本。
* 您無法修改組態的唯一複本的可用性模式。 若要變更同步或非同步的次要複本設定的唯一複本，請移除設定的唯一複本，並加入所需的可用性模式的次要複本。 
* 組態的唯一複本為同步的可用性群組中繼資料。 沒有任何使用者資料。 
* 包含一個主要複本和一個組態時，唯一的複本，但沒有次要複本的可用性群組不是有效的。 
* 您無法在 SQL Server Express edition 執行個體上建立可用性群組。 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>了解 SQL Server 資源 pacemaker 代理程式

加入 SQL Server 2017 CTP 1.4`sequence_number`至`sys.availability_groups`允許 Pacemaker 來識別如何最新的次要複本都會與主要複本。 `sequence_number` 已開始的單純遞增的 bigint 表示如何最新的本機可用性群組複本。 Pacemaker 更新`sequence_number`與每個可用性群組組態變更。 組態變更的範例包括容錯移轉，複本新增或移除。 數字是在主要伺服器上，更新，然後再複寫至次要複本。 因此具有最新組態的次要複本具有相同的順序編號，與主要資料庫。 

當 Pacemaker 決定升級為主要複本時，會先傳送*預先升級*通知給所有複本。 複本傳回的序號。 接下來，當 Pacemaker 實際上會嘗試升級為主要複本，複本只會升級本身如果其序號最高的序號。 如果它自己的序號不符合最高的序號，複本會拒絕升級作業。 如此一來，只有序號最高的複本可以升級為主要複本，確保不會遺失資料。 

此程序需要至少一個複本可供使用，用於升級與上一個主要資料庫相同的序號。 Pacemaker 資源代理程式集`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`，至少一個同步的次要複本已更新，並可依預設自動容錯移轉目標。 每個監視的動作的值與`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`計算 （和更新，如有必要）。 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`值是 '的同步複本數目' 除以 2。 在容錯移轉時需要資源代理程式 (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`複本) 來回應預先升級通知。 具有最高的複本`sequence_number`升級為主要。 

例如，可用性群組包含三個同步複本的一個主要複本和兩個同步次要複本。

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 為 1。(3 / 2-> 1)。

- 所需的複本，以回應預先升級動作數目為 2;(3-1 = 2)。 

在此案例中，兩個複本都有回應觸發容錯移轉。 成功的主要複本中斷後自動容錯移轉，兩個次要複本必須保持最新狀態並回應預先升級通知。 如果它們是在線上而且同步，也會具有相同的序號。 可用性群組升級其中一個。 如果只有其中一個次要複本會回應預先升級動作，資源代理程式無法保證回應的次要複本具有最高的 sequence_number，且不會觸發容錯移轉。

>[!IMPORTANT]
>當 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 為 0 時，有遺失資料的風險。 在主要複本過時期間，資源代理程式不會自動觸發容錯移轉。 您可以等候主要若要復原，或手動容錯移轉使用`FORCE_FAILOVER_ALLOW_DATA_LOSS`。

您可以選擇要覆寫預設行為，並避免設定可用性群組資源`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`自動。

下列指令碼設定`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`設為 0 到可用性群組上名為`<**ag1**>`。 執行之前，請以您的可用性群組名稱取代 `<**ag1**>`。

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

若要還原為預設值，根據執行可用性群組組態：

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>當您執行上述命令時，主要是暫時降級為次要，然後再升級。 資源更新會導致所有複本，以停止並重新啟動。 新值`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`只設定複本會重新啟動後，不立即。

## <a name="see-also"></a>另請參閱

[在 Linux 上的可用性群組](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
