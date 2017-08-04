---
title: "SQL Server Always On 可用性群組部署模式 |Microsoft 文件"
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-linux
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e2d26fd9ce79fc8c47c7499313648d565ae1b97
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---

# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>可用性群組組態的高可用性與資料保護

這篇文章會提供支援的部署組態，SQL Server Always On 可用性群組中的 Linux 伺服器上。 可用性群組支援高可用性和資料保護。 自動偵測、 自動容錯移轉和透明容錯移轉後的重新連線提供高可用性。 同步處理的複本提供資料保護。 

>[!NOTE]
>除了高可用性和資料保護，可用性群組可以也提供災害復原、 跨平台移轉，以及讀取向外延展。 本文主要討論實作高可用性與資料保護。 

使用 Windows Server 容錯移轉叢集，常見的組態，高可用性會使用兩個同步複本和一個[檔案共用見證](http://technet.microsoft.com/library/cc731739.aspx)。 檔案共用見證，例如驗證的可用性群組設定-的同步處理的狀態和複本的角色。 此組態可確保所選為容錯移轉目標有最新的資料和可用性群組組態變更的次要複本。 

目前的高可用性解決方案，適用於 Linux 無法滿足外部的見證，例如檔案共用見證，Windows Server 容錯移轉叢集中。 任何 Windows Server 容錯移轉叢集時，可用性群組組態會儲存在參與的 SQL Server 執行個體上 master 資料庫中。 因此，可用性群組需要至少三個同步複本的高可用性與資料保護。 在 Linux 伺服器上建立可用性群組之後，建立叢集資源。 叢集資源設定決定高可用性的組態。

選擇符合特定商務需求對於高可用性、 資料保護和讀取向外延展可用性群組的設計。

>[!IMPORTANT]
>下列設定說明的可用性群組的設計模式和每個模式的功能。 這些設計模式適用於可用性群組`CLUSTER_TYPE = EXTERNAL`的高可用性解決方案。 

設計模式是兩個可用性群組組態。 設定包括：

- **三個同步複本**

- **兩個同步複本**

## <a name="how-the-configuration-affects-default-resource-settings"></a>組態如何影響預設資源設定

叢集資源設定`required_synchronized_secondaries_to_commit`可確保每筆交易寫入次要複本記錄檔的最小數目，再認可主要複本上的交易。 高可用性和資料保護，視組態而定，可能會影響此設定。 當您安裝 SQL Server 資源代理程式- `mssql-server-ha` -並建立可用性群組的叢集資源，請叢集管理員偵測到可用性群組組態和設定`required_synchronized_secondaries_to_commit`據此。 

如果組態中，資源代理程式參數的支援`required_synchronized_secondaries_to_commit`設為提供高可用性與資料保護的值。 如需詳細資訊，請參閱[pacemaker 的了解 SQL Server 資源 agent](#pacemakerNotify)。

下列各節說明叢集資源的預設行為。 

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>三個同步複本

此組態是由三個同步複本所組成。 根據預設，它會提供高可用性與資料保護。 它也可以提供讀取的向外延展。

![三個複本][3]

下表描述的高可用性與資料保護行為取決於包含三個同步複本的可用性群組的設定： 

|`required_synchronized_secondaries_to_commit`|0 |1 \*|2
| --- |:---:|:---:|:---:
|主要複本中斷後自動容錯移轉| |✔| 
|主要複本的一個次要複本中斷之後，才能使用|✔|✔| 
|主要複本的兩個次要複本中斷之後，才能使用|✔| |
|主要複本中斷-可能會遺失資料後的手動容錯移轉|✔| | 

\*預設為叢集中的資源新增可用性群組時設定。

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>兩個同步複本

此設定可啟用資料保護。 可用性群組組態，例如，它可以啟用讀取的向外延展。 兩個同步複本組態不提供自動的高可用性。 

![兩個同步複本][1]

此設定需要兩部伺服器。 這些伺服器填滿的主要複本和次要複本的角色。 

兩個同步複本設定最適合用於資料保護和散發資料庫的讀取工作負載。 根據預設，資源的資料保護設定。 此組態不提供高可用性，因為如果任一個執行個體的 SQL Server 失敗，可能是資料庫不是完全可供使用，或沒有資料遺失的風險。 

下表描述根據包含兩個同步複本的可用性群組的可能值的資料保護行為： 

|`required_synchronized_secondaries_to_commit`|0 \*|1 
| --- |:---|:---
|主要複本中斷後自動容錯移轉| |✔ \*\* | 
|主要複本的次要複本中斷之後，才能使用|✔| |

\*預設為叢集中的資源新增可用性群組時設定。

\*\*在此組態中，主要複本中斷，就會發生自動可用性群組之後會容錯移轉。 應用程式無法連接到可用性群組中，直到主要複本上線-現在為次要複本。 

兩個同步複本組態可能是最經濟的因為它只需要兩個 SQL Server 執行個體在兩部伺服器。

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>了解 SQL Server 資源 pacemaker 代理程式

加入 SQL Server 2017 CTP 1.4`sequence_number`至`sys.availability_groups`允許 Pacemaker 來識別如何最新的次要複本都會與主要複本。 `sequence_number`已開始的單純遞增的 bigint 表示如何最新的本機可用性群組複本。 Pacemaker 更新`sequence_number`與每個可用性群組組態變更。 組態變更的範例包括容錯移轉，複本新增或移除。 數字是在主要伺服器上，更新，然後再複寫至次要複本。 因此具有最新組態的次要複本具有相同的順序編號，與主要資料庫。 

當 Pacemaker 決定升級為主要複本時，會先傳送*預先升級*通知給所有複本。 複本傳回的序號。 接下來，當 Pacemaker 實際上會嘗試升級為主要複本，複本只會升級本身如果其序號最高的序號。 如果它自己的序號不符合最高的序號，複本會拒絕升級作業。 如此一來，只有序號最高的複本可以升級為主要複本，確保不會遺失資料。 

此程序需要至少一個複本可供使用，用於升級與上一個主要資料庫相同的序號。 Pacemaker 資源代理程式集`required_synchronized_secondaries_to_commit`，至少一個同步的次要複本已更新，並可依預設自動容錯移轉目標。 每個監視的動作的值與`required_synchronized_secondaries_to_commit`計算 （和更新，如有必要）。 `required_synchronized_secondaries_to_commit`值是 '的同步複本數目' 除以 2。 在容錯移轉時需要資源代理程式 (`total number of replicas`  -  `required_synchronized_secondaries_to_commit`複本) 來回應預先升級通知。 具有最高的複本`sequence_number`升級為主要。 

例如，可用性群組包含三個同步複本的一個主要複本和兩個同步次要複本。

- `required_synchronized_secondaries_to_commit`為 1。(3 / 2-> 1)。

- 所需的複本，以回應預先升級動作數目為 2;(3-1 = 2)。 

在此案例中，兩個複本都有回應觸發容錯移轉。 成功的主要複本中斷後自動容錯移轉，兩個次要複本必須保持最新狀態並回應預先升級通知。 如果它們是在線上而且同步，也會具有相同的序號。 可用性群組升級其中一個。 如果只有其中一個次要複本會回應預先升級動作，資源代理程式無法保證回應的次要複本具有最高的 sequence_number，且不會觸發容錯移轉。

>[!IMPORTANT]
>當`required_synchronized_secondaries_to_commit`為 0 沒有資料遺失的風險。 在主要複本過時期間，資源代理程式不會自動觸發容錯移轉。 您可以等候主要若要復原，或手動容錯移轉使用`FORCE_FAILOVER_ALLOW_DATA_LOSS`。

您可以選擇要覆寫預設行為，並避免設定可用性群組資源`required_synchronized_secondaries_to_commit`自動。

下列指令碼設定`required_synchronized_secondaries_to_commit`設為 0 到可用性群組上名為`<**ag1**>`。 執行取代之前`<**ag1**>`與可用性群組的名稱。

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

若要還原為預設值，根據執行可用性群組組態：

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>當您執行上述命令時，主要是暫時降級為次要，然後再升級。 資源更新會導致所有複本，以停止並重新啟動。 新值`required_synchronized_secondaries_to_commit`只設定複本會重新啟動後，不立即。

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
