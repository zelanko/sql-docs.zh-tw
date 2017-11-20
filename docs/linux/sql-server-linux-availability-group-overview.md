---
title: "Always On 可用性群組的 SQL Server on Linux |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c5c7e602ac1beedb028072b4c82578e9948af43d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="availability-groups-for-sql-server-on-linux"></a>SQL Server on Linux 的可用性群組

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server Always On 可用性群組是高可用性 (HA)，災害復原 (DR)，並向外延展方案。 它提供高可用性群組的直接連結存放裝置上的資料庫。 它支援整合式的 HA 和 DR、 自動失敗偵測、 快速透明容錯移轉，以及讀取的負載平衡多個次要複本。 此一組廣泛的功能可讓您達成您的工作負載最佳化可用性 Sla。

SQL Server 可用性群組，SQL Server 2012 中首度引進，並經過改進每個版本。 現在 Linux 上使用這項功能。 為了符合嚴格的業務續航力需求的 SQL Server 工作負載，可用性群組上所有支援的執行[Linux 作業系統分佈](sql-server-linux-release-notes.md)。 此外，所有功能，讓可用性群組的彈性、 整合式且有效率的 HA DR 解決方案都可以使用 Linux 以及。 其中包括： 

- **多重資料庫容錯移轉**可用性群組支援一組使用者資料庫，稱為可用性資料庫的容錯移轉環境。
- **快速失敗偵測和容錯移轉**為高可用性的叢集資源，可用性群組會受惠立即容錯移轉偵測和容錯移轉動作的內建的叢集智慧。
- **使用虛擬 IP 資源的透明容錯移轉**可讓用戶端使用主要發生容錯移轉的單一連接字串。 需要叢集管理員與整合。
- **多個同步和非同步次要複本**可用性群組支援最多八個次要複本。 同步複本與主要複本會等候認可主要複本會等候寫入至磁碟上的交易記錄的交易的交易。 主要複本不會等候非同步同步複本上的寫入。  
- **手動或自動容錯移轉**到同步的次要複本的容錯移轉可以觸發自動叢集，或在要求上的資料庫管理員。
- **作用中次要資料庫可供讀取和備份工作負載**可以設定一或多個次要複本，以支援唯讀存取的次要資料庫和 （或） 以允許在次要資料庫上進行備份。
- **自動植入**SQL Server 會自動建立每個資料庫的次要複本的可用性群組中。
- **唯讀路由**SQL Server 將路由至已設定為允許唯讀工作負載的次要複本的可用性群組接聽連入連線。 
- **資料庫層級的健全狀況監視和容錯移轉觸發程序**增強資料庫層級的監視和診斷功能。 
- **災害復原設定**與分散式的可用性群組或多重子網路可用性群組設定。 
- **向外延展讀取功能**中 SQL Server 2017 您可以向外延展唯讀作業建立可用性群組，不論 HA。 


如需有關 SQL Server 可用性群組的詳細資訊，請參閱[SQL Server Always On 可用性群組](http://msdn.microsoft.com/library/hh510230.aspx)。

## <a name="availability-group-terminology"></a>可用性群組的詞彙

可用性群組支援一組特定的使用者資料庫-所謂的可用性資料庫-一同進行容錯移轉，容錯移轉環境。 可用性群組支援一組讀寫主要資料庫以及一到八組對應的次要資料庫。 此外，您可以將次要資料庫用於唯讀存取及/或某些備份作業。 可用性群組都會定義一組兩個或多個容錯移轉夥伴，稱為可用性複本。 可用性複本是可用性群組的元件。 如需詳細資訊，請參閱[概觀的 Alwayson 可用性群組 (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)。

下列詞彙說明 SQL Server 可用性群組解決方案的主要部分：

 可用性群組  
 一組一起容錯移轉之資料庫 (「可用性資料庫」) 的容器。  
  
 可用性資料庫  
 屬於可用性群組的資料庫。 對於每個可用性資料庫而言，可用性群組會維護單一讀寫複本 (「主要資料庫」) 以及一到八個唯讀複本 (「次要資料庫」)。  
  
 主要資料庫  
 可用性資料庫的讀寫複本。  
  
 次要資料庫  
 可用性資料庫的唯讀複本。  
  
 可用性複本  
 具現化的 SQL server 的特定執行個體所裝載的可用性群組會維護屬於可用性群組每個可用性資料庫的本機副本。 有兩種類型的可用性複本存在：單一 *「主要複本」* 以及一到八個 *「次要複本」*。  
  
 「主要複本」  
 可用性複本，該複本可讓主要資料庫用於用戶端的讀寫連接，同時也將每個主要資料庫的交易記錄檔記錄傳送到每個次要複本。  
  
 次要複本  
 可用性複本，該複本會維護每個可用性資料庫的次要副本，並且當做可用性群組的潛在容錯移轉目標。 (選擇性) 可支援以唯讀方式存取次要資料庫的次要複本，可以支援在次要資料庫上建立備份。  
  
 可用性群組接聽程式  
 用戶端可連接的伺服器名稱，以便存取可用性群組之主要或次要複本中的資料庫。 可用性群組接聽程式會將內送連接導向至主要複本或唯讀次要複本。  


## <a name="new-in-sql-server-2017-for-availability-groups"></a>SQL Server 2017 新可用性群組

SQL Server 2017 導入了可用性群組的新功能。

**CLUSTER_TYPE**使用`CREATE AVAILABILITY GROUP`。 識別伺服器叢集管理員會管理可用性群組的類型。 可以是下列類型之一：

   - **WSFC** Winows server 容錯移轉叢集。 在 Windows 中，它是 CLUSTER_TYPE 的預設值。
   - **外部**Pacemaker 與 Linux，比方說，不是 Windows server 容錯移轉叢集-叢集管理員。
   - **無**沒有叢集管理員。 用於向外延展讀取可用性群組。

如需有關這些選項的詳細資訊，請參閱[CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx)或[ALTER AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878601.aspx)。

**同步次要複本上認可的保證**

Use `required_synchronized_secondaries_to_commit`with `CREATE AVAILABILITY GROUP` or `ALTER AVAILABILITY GROUP`. 當`required_synchronized_secondaries_to_commit`設為高於 0，資料庫會等候指定的數目上認可交易之前的主要複本的交易**同步的次要**複本資料庫交易記錄檔。 如果不足，無法同步次要複本不在線上，直到有足夠的次要複本通訊繼續，將會拒絕所有連線至主要複本。

**向外延展讀取可用性群組**

建立可用性群組不含叢集以支援向外延展讀取工作負載。 請參閱[向外延展讀取可用性群組](../database-engine/availability-groups/windows/read-scale-availability-groups.md)。

## <a name="next-steps"></a>後續的步驟

[設定可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

[設定向外延展讀取可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-rs.md)

[RHEL 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-rhel.md)

[SLES 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-sles.md)

[在 Ubuntu 上加入可用性群組叢集資源](sql-server-linux-availability-group-cluster-ubuntu.md)

