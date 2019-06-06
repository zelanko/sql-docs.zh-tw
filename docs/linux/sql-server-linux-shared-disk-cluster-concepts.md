---
title: 容錯移轉叢集執行個體-在 Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e42c5cc42b1b6d0de6d9674070f53df33bda31b4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705305"
---
# <a name="failover-cluster-instances---sql-server-on-linux"></a>容錯移轉叢集執行個體-在 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明 SQL Server 容錯移轉叢集執行個體 (FCI) 在 Linux 上的相關概念。 

若要在 Linux 上建立 SQL Server FCI，請參閱[Linux 上設定 SQL Server FCI](sql-server-linux-shared-disk-cluster-configure.md)

## <a name="the-clustering-layer"></a>叢集層

* RHEL，叢集的圖層基礎上 Red Hat Enterprise Linux (RHEL) [HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)。 

    > [!NOTE] 
    > Red Hat HA 附加元件和文件集的存取需要訂用帳戶。 

* 在 SLES，叢集的圖層根據 SUSE Linux Enterprise[高可用性延伸模組 (HAE)](https://www.suse.com/products/highavailability)。

    如需有關叢集設定、 資源代理程式選項、 管理、 最佳做法和建議的詳細資訊，請參閱 < [SUSE Linux Enterprise 高可用性延伸模組 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)。

RHEL HA 附加元件和 SUSE HAE 之上[Pacemaker](https://clusterlabs.org/)。

下圖所示，兩部伺服器被提供儲存體。 -Corosync 和 Pacemaker-叢集元件協調通訊和資源管理。 其中一個伺服器具有作用中的連接到儲存體資源和 SQL Server。 當 Pacemaker 偵測到失敗時叢集的元件會管理資源移動到另一個節點。  

![Red Hat Enterprise Linux 7 共用磁碟的 SQL 叢集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 


> [!NOTE]
> 到目前為止，不是與使用 Windows 上為 WSFC，結合與 Linux 上的 Pacemaker 的 SQL Server 的整合。 從 SQL，在沒有知識存在的叢集，所有的協調流程中超出而且服務由 Pacemaker 控制做為獨立執行個體。 此外，虛擬網路名稱是特有 WSFC 的相同的 Pacemaker 沒有對等。 預期的是，@@servername和 sys.servers 返回節點名稱，而叢集 dmv sys.dm_os_cluster_nodes 並且 sys.dm_os_cluster_properties，不將任何記錄。 若要使用的連接字串指向字串伺服器名稱，未使用的 IP，他們必須註冊在他們的 DNS 伺服器用來建立虛擬 IP 資源 （如下列各節所述） 的 IP 與所選的伺服器名稱。

## <a name="number-of-instances-and-nodes"></a>執行個體數目和節點

Linux 上的 SQL Server 的一個主要差異是，只能有一個安裝的 SQL Server，每一部 Linux 伺服器。 該安裝被呼叫執行個體。 這表示，不同於 Windows Server 支援最多 25 個 Fci，每個 Windows Server 容錯移轉叢集 (WSFC)，在以 Linux 為基礎的 FCI 只會有單一執行個體。 這一個執行個體也是預設執行個體;沒有在 Linux 上的具名執行個體的概念。 

Pacemaker 叢集只能有最多 16 個節點包含 Corosync，因此單一 FCI 可以跨越多達 16 部伺服器。 FCI 實作的 SQL Server Standard Edition 支援最多兩個叢集的節點，Pacemaker 叢集在沒有最大 16 個節點。

在 SQL Server FCI，SQL Server 執行個體為上一個節點或其他作用中。

## <a name="ip-address-and-name"></a>IP 位址和名稱
在 Linux Pacemaker 叢集上，每個 SQL Server FCI 會需要它自己唯一的 IP 位址和名稱。 如果 FCI 設定跨越多個子網路，一個 IP 位址必須針對每個子網路。 唯一的名稱和 IP 位址用來存取 FCI，使應用程式和終端使用者不需要知道的 Pacemaker 叢集的基礎伺服器。

FCI 在 DNS 中的名稱應該與建立 Pacemaker 叢集內的 FCI 資源名稱相同。
必須在 DNS 中註冊的名稱和 IP 位址。

## <a name="shared-storage"></a>共用存放裝置
所有 Fci，無論它們是在 Linux 或 Windows Server，都需要某種形式的共用存放裝置。 此存放裝置會向所有的伺服器，可能可以裝載 FCI 中，但只有一部伺服器可以在任何時候 fci 中使用的儲存體。 適用於 Linux 下的共用儲存體的選項如下：

- iSCSI
- Network File System (NFS)
- 伺服器訊息區 (SMB) 在 Windows Server，有稍微不同的選項。 目前不支援以 Linux 為基礎的 Fci 的其中一個選項是使用 TempDB，也就是 SQL Server 的暫存工作區的節點的本機磁碟的能力。

在這種設定方式跨越多個位置，必須與其他同步在一個資料中心儲存的內容。 發生容錯移轉時，FCI 會上線，存放裝置被視為相同。 達到此目標需要某些外部方法的儲存體複寫是否透過基礎的儲存體硬體或某些軟體為基礎的公用程式。 

>[!NOTE]
>針對 SQL Server，必須使用 XFS 或 EXT4 格式化以 Linux 為基礎的部署使用直接向這類伺服器的磁碟。 目前不支援其他檔案系統。 這裡將會反映任何變更。

提供共用存放裝置的程序也適用於不同的支援方法：

- 設定共用存放裝置
- 將儲存體掛接為資料夾的伺服器上要做為 FCI 的 Pacemaker 叢集的節點
- 如有需要，將 SQL Server 系統資料庫移到共用存放裝置
- SQL Server 的運作方式與每一部伺服器的測試連線的共用存放裝置

Linux 上的 SQL Server 的一項主要差異是，雖然您可以設定預設的使用者資料和記錄檔位置，系統資料庫必須一律存在於`/var/opt/mssql/data`。 在 Windows Server 上沒有移動包括 TempDB 系統資料庫的能力。 這項事實播放到共用的儲存體已針對 FCI。

非系統資料庫的預設路徑可以使用變更`mssql-conf`公用程式。 如需如何變更預設值，[變更預設的資料或記錄檔目錄位置](sql-server-linux-configure-mssql-conf.md#datadir)。 您也可以儲存 SQL Server 資料和交易中的其他位置，只要它們有適當的安全性，即使它不是預設位置;位置必須所述。

下列主題說明如何以 Linux 為主的 SQL Server FCI 設定支援的存放裝置類型：

- [設定容錯移轉叢集執行個體-iSCSI-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [設定容錯移轉叢集執行個體-NFS-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [設定容錯移轉叢集執行個體-SMB-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-smb.md)
