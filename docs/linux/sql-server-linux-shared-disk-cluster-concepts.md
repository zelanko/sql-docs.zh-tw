---
title: 容錯移轉叢集執行個體 - Linux 上的 SQL Server
description: Linux 上 SQL Server 容錯移轉叢集執行個體的概念包括叢集層、執行個體數目、IP 位址和名稱，以及共用儲存體。
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1b2b852a1c1acecefa3b702bb140d9128d04a212
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784644"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>容錯移轉叢集執行個體 - Linux 上的 SQL Server

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

此文章說明與 Linux 上的 SQL Server 容錯移轉叢集執行個體 (FCI) 相關的概念。 

若要在 Linux 上建立 SQL Server FCI，請參閱[在 Linux 上設定 SQL Server FCI](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>群集層

* 在 RHEL 中，群集層是以 Red Hat Enterprise Linux (RHEL) [HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)為基礎。 

    > [!NOTE] 
    > 存取 Red Hat HA 附加元件與文件皆需要訂用帳戶。 

* 在 SLES 中，群集層是以 SUSE Linux Enterprise [高可用性擴充功能 (HAE)](https://www.suse.com/products/highavailability) \(英文\) 為基礎。

    如需叢集設定、資源代理程式選項、管理、最佳做法和建議的詳細資訊，請參閱 [SUSE Linux Enterprise 高可用性擴充功能 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html) \(英文\)。

RHEL HA 附加元件和 SUSE HAE 都是以 [Pacemaker](https://clusterlabs.org/) \(英文\) 為基礎。

如下圖所示，會向兩部伺服器提供儲存體。 群集元件 (Corosync 和 Pacemaker) 會協調通訊和資源管理。 其中一部伺服器具有針對儲存體資源和 SQL Server 的作用中連線。 當 Pacemaker 偵測到失敗時，群集元件會負責將資源移至另一個節點。  

![Red Hat Enterprise Linux 7 共用磁碟 SQL 叢集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 目前，SQL Server 與 Linux 上的 Pacemaker 之間的整合程度，尚不如 Windows 上的 WSFC。 從 SQL 內並無法得知叢集是否存在，所有協調流程都是從外而入，且服務會以獨立執行個體的形式由 Pacemaker 所控制。 此外，虛擬網路名稱為 WSFC 特定，Pacemaker 中沒有相同的對應項。 系統預期 @@servername 和 sys.servers 會傳回節點名稱，而叢集 dmvs sys.dm_os_cluster_nodes 和 sys.dm_os_cluster_properties 將不會有任何記錄。 若要使用指向字串伺服器名稱的連接字串而不使用 IP，他們必須在其 DNS 伺服器中搭配指定的伺服器名稱註冊用來建立虛擬 IP 資源的 IP (如下列各節中所述)。

## <a name="number-of-instances-and-nodes"></a>執行個體和節點的數目

Linux 上的 SQL Server 的其中一個主要差異，在於每部 Linux 伺服器只能具有單一 SQL Server 安裝。 該安裝被稱為執行個體。 這代表與針對每個 Windows Server 容錯移轉叢集 (WSFC) 皆支援最多 25 個 FCI 的 Windows Server 相比，Linux 型 FCI 將只會有單一執行個體。 這個單一執行個體也會是預設執行個體；Linux 上並沒有具名執行個體的概念。 

在涉及 Corosync 時，Pacemaker 叢集只能有最多 16 個節點，因此單一 FCI 可以跨越最多 16 部伺服器。 實作 SQL Server Standard Edition 的 FCI 針對每個叢集僅支援最多兩個節點，即使 Pacemaker 叢集具有最多 16 個節點。

在 SQL Server FCI 中，SQL Server 執行個體只會在其中一個節點上處於作用中狀態。

## <a name="ip-address-and-name"></a>IP 位址和名稱
在 Linux Pacemaker 叢集上，每個 SQL Server FCI 都需要屬於它的唯一 IP 位址和名稱。 如果 FCI 設定跨越多個子網路，每個子網路都會需要單一 IP 位址。 唯一名稱和 IP 位址是用來存取 FCI，使應用程式和使用者不需要知道 Pacemaker 叢集的基礎伺服器是哪個。

FCI 在 DNS 中的名稱應該要和在 Pacemaker 叢集中所建立之 FCI 資源的名稱相同。
名稱和 IP 位址都必須在 DNS 中註冊。

## <a name="shared-storage"></a>共用儲存
所有的 FCI (無論其是位於 Linux 或 Windows Server) 都需要某種形式的共用儲存體。 此儲存體會向可以裝載 FCI 的所有伺服器呈現，但任何時候都只有單一伺服器可以針對 FCI 使用該儲存體。 Linux 底下的可用共用儲存體選項為：

- iSCSI
- 網路檔案系統 (NFS)
- 伺服器訊息區 (SMB)：在 Windows Server 底下，選項則稍有不同。 一個目前不支援 Linux 型 FCI 的選項，是使用 TempDB (其為 SQL Server 的暫存工作區) 節點的本機磁碟。

在橫跨多個位置的設定中，儲存在單一資料中心的內容必須與另一個資料中心同步。 在發生容錯移轉的情況下，FCI 將能上線，且儲存體將會保持一致。 若要達成此目的，將會需要針對儲存體複寫使用某種外部方法；無論是透過基礎儲存體硬體，或是某種以軟體為基礎的公用程式來達成。 

>[!NOTE]
>針對 SQL Server，使用直接向伺服器呈現磁碟的 Linux 型部署，必須搭配 XFS 或 EXT4 進行格式化。 目前不支援其他檔案系統。 若有任何變更，將會在此反映。

呈現共用儲存體的程序，對於上述不同的支援方法皆相同：

- 設定共用儲存體
- 針對將作為 FCI 之 Pacemaker 叢集節點的伺服器將儲存體裝載為資料夾
- 若有需要，請將 SQL Server 系統資料庫移至共用儲存體
- 從每個連線至共用儲存體的伺服器上測試 SQL Server 是否能順利運作

Linux 上的 SQL Server 的其中一個主要差異，在於雖然您可以設定預設使用者資料和記錄檔的位置，系統資料庫一律必須存在於 `/var/opt/mssql/data`。 在 Windows Server 上，您可以選擇移動系統資料庫 (包括 TempDB)。 此事實將會影響針對 FCI 設定共用儲存體的方式。

非系統資料庫的預設路徑可以使用 `mssql-conf` 公用程式來變更。 如需如何變更預設值的相關資訊，請參閱[變更預設的資料或記錄檔目錄位置](sql-server-linux-configure-mssql-conf.md#datadir)。 您也可以將 SQL Server 資料和交易儲存在其他位置，前提是它們必須具備適當的安全性 (即便它不是預設位置)；該位置必須要被陳述。

下列文章說明如何針對 Linux 型 SQL Server FCI 設定支援的儲存體類型：

- [設定容錯移轉叢集執行個體 - iSCSI - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [設定容錯移轉叢集執行個體 - NFS - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [設定容錯移轉叢集執行個體 - SMB - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-smb.md)
