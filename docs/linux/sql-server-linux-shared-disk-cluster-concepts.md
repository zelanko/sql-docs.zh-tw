---
title: "容錯移轉叢集執行個體的 SQL Server on Linux |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 229c6a989a4707921eae3046e3c9707b05bb0306
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---

# <a name="failover-cluster-instances---sql-server-on-linux"></a>容錯移轉叢集執行個體的 SQL Server on Linux

本文說明有關 SQL Server 容錯移轉叢集執行個體 (FCI) 在 Linux 上的概念。 

若要建立 SQL Server FCI on Linux，請參閱[Linux 上設定 SQL Server FCI](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>叢集的圖層

* RHEL、 在叢集的圖層基礎上 Red Hat Enterprise Linux (RHEL) [HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)。 

    > [!NOTE] 
    > Red Hat HA 附加元件和文件集的存取需要訂用帳戶。 

* SLES，在叢集的圖層根據 SUSE Linux Enterprise[高可用性延伸模組 (HAE)](https://www.suse.com/products/highavailability)。

    如需叢集設定、 資源代理程式的選項、 管理、 最佳做法和建議的詳細資訊，請參閱[SUSE Linux Enterprise 高可用性延伸 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)。

RHEL HA 附加元件和 SUSE HAE 之上[Pacemaker](http://clusterlabs.org/)。

如下圖所顯示存放裝置會呈現至兩個伺服器。 -Corosync 以及 Pacemaker-叢集元件協調通訊和資源管理。 其中一個伺服器具有作用中連接的儲存體資源，以及 SQL Server。 當 Pacemaker 偵測到失敗時叢集的元件管理將資源移動到另一個節點。  

![Red Hat Enterprise Linux 7 共用磁碟的 SQL 叢集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 此時，不是與使用 Windows 上的 WSFC 為結合與 Pacemaker Linux 上的 SQL Server 的整合。 從 SQL、 內沒有存在叢集的認知，所有的協調流程外中，服務由 Pacemaker 控制做為獨立執行個體。 此外，虛擬網路名稱是屬於 WSFC、 沒有對等的 Pacemaker 中相同。 預期的是，@@servername和 sys.servers 返回節點名稱，而叢集 dmv sys.dm_os_cluster_nodes 並且 sys.dm_os_cluster_properties，不將任何記錄。 若要使用連接字串指向字串伺服器名稱並不會使用 IP，則必須註冊在他們的 DNS 伺服器 IP 用來建立所選的伺服器名稱與虛擬 IP 資源 （如下所述）。

## <a name="number-of-instances-and-nodes"></a>執行個體數目和節點

使用 SQL Server on Linux 的其中一個主要差異是，只能有一個安裝的 SQL Server，每個 Linux 伺服器。 該安裝被呼叫執行個體。 這表示，不同於 Windows Server 支援最多 25 個 Fci 每個 Windows Server 容錯移轉叢集 (WSFC)，以 Linux 為基礎的 FCI 將只有單一執行個體。 這一個執行個體也是預設執行個體。沒有在 Linux 上的具名執行個體的概念。 

Pacemaker 叢集只能有最多 16 個節點包含 Corosync，因此單一 FCI 可以跨越多達 16 個伺服器。 FCI 使用的 SQL Server 標準版實作支援最多兩個叢集節點 Pacemaker 叢集在沒有最大 16 個節點。

在 SQL Server FCI，SQL Server 執行個體是在上一個節點或其他作用中。

## <a name="ip-address-and-name"></a>IP 位址和名稱
在 Linux Pacemaker 叢集上，每個 SQL Server FCI 需要自己唯一的 IP 位址和名稱。 如果 FCI 設定跨越多個子網路，一個 IP 位址就必須針對每個子網路。 唯一的名稱和 IP 位址可用來存取 FCI，使應用程式和使用者不需要知道 Pacemaker 叢集中的哪一個基礎伺服器。

在 FCI 在 DNS 中的名稱應該與 FCI 資源建立 Pacemaker 叢集中的名稱相同。
名稱和 IP 位址必須在 DNS 中登錄。

## <a name="shared-storage"></a>共用儲存
所有 Fci，它們是在 Linux 或 Windows Server 上是否都需要某種形式的共用存放裝置。 這個儲存體呈現給可能可以裝載 FCI 的所有伺服器，但只有一部伺服器可以使用的存放裝置 FCI 在任何指定時間。 適用於 Linux 下的共用存放裝置的選項如下：

- iSCSI
- Network File System (NFS)
- 伺服器訊息區塊 (SMB) 在 Windows Server，有稍微不同的選項。 目前不支援 linux Fci 的其中一個選項是使用 TempDB，也就是 SQL Server 的暫存工作區的節點的本機磁碟的能力。

在設定跨越多個位置中，必須與其他同步什麼儲存在一個資料中心。 發生容錯移轉，FCI 將無法上線，而且存放裝置被視為相同。 達到此會需要某些外部方法儲存體複寫是否透過基礎的存放裝置硬體或某些軟體為基礎的公用程式。 

>[!NOTE]
>針對 SQL Server 2017，必須使用 XFS 或 EXT4 格式化以 Linux 為基礎的部署使用直接呈現這類伺服器的磁碟。 目前不支援其他檔案系統。 這裡將會反映任何變更。

呈現共用存放裝置的程序也適用於不同的支援方法：

- 設定共用存放裝置
- 裝載存放裝置做為要做為 FCI 的 Pacemaker 叢集節點的伺服器資料夾
- 必要時，SQL Server 系統資料庫移到共用的存放裝置
- SQL Server 的運作方式與每一部伺服器的測試連接的共用存放裝置

使用 SQL Server on Linux 的一項主要差異是，雖然您可以設定預設的使用者資料和記錄檔位置，系統資料庫必須一直存在在`/var/opt/mssql/data`。 在 Windows Server 上沒有移動包括 TempDB 系統資料庫的能力。 播放到如何共用儲存體已針對 FCI 的此事實。

非系統資料庫的預設路徑可以使用變更`mssql-conf`公用程式。 如需有關如何變更預設值，資訊[變更預設資料或記錄檔的目錄位置](sql-server-linux-configure-mssql-conf.md#datadir)。 您也可以儲存 SQL Server 資料和交易中的其他位置，只要它們具有正確的安全性，即使它不是預設位置。位置必須所述。

下列主題說明如何為以 Linux 為基礎 SQL Server FCI 設定支援的存放裝置類型：

- [設定容錯移轉叢集執行個體-iSCSI-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [設定容錯移轉叢集執行個體-NFS-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [設定容錯移轉叢集執行個體-SMB-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

