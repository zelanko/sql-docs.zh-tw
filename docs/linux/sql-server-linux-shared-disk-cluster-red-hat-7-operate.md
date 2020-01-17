---
title: 在 Linux 上操作 SQL Server 的 RHEL FCI
description: 了解如何操作 SQL Server 的 Red Hat Enterprise Linux (RHEL) 共用磁碟容錯移轉叢集執行個體 (FCI) 以確保高可用性，例如手動容錯移轉 FCI，以及在叢集新增或移除節點。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: 76c59c6c7b821bfcc9eb76ca3a694a1c69095ce1
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558523"
---
# <a name="operate-rhel-failover-cluster-instance-fci-for-sql-server"></a>操作 SQL Server 的 RHEL 容錯移轉叢集執行個體 (FCI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文件說明如何使用 Red Hat Enterprise Linux，針對共用磁碟容錯移轉叢集上的 SQL Server 執行下列工作。

- 手動容錯移轉叢集
- 監視容錯移轉叢集 SQL Server 服務
- 新增叢集節點
- 移除叢集節點
- 變更 SQL Server 資源監視頻率

## <a name="architecture-description"></a>架構描述

叢集層是以建置於 [Pacemaker](https://clusterlabs.org/) 之上的 Red Hat Enterprise Linux (RHEL) [HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)為基礎。 Corosync 和 Pacemaker 協調叢集通訊和資源管理。 SQL Server 執行個體在其中一個節點上為作用中狀態。

下圖說明了使用 SQL Server 的 Linux 叢集中的元件。 

![Red Hat Enterprise Linux 7 共用磁碟 SQL 叢集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

如需叢集設定、資源代理程式選項和管理的詳細資訊，請造訪 [RHEL 參考文件](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html) \(英文\)。

## <a name = "failManual"></a>手動容錯移轉叢集

`resource move` 命令會建立限制式，強制在目標節點上啟動資源。  執行 `move` 命令之後，執行資源 `clear` 將會移除限制式，因此可以再次移動資源，或讓資源自動容錯移轉。 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

下列範例會將 **mssqlha** 資源移至名為 **sqlfcivm2** 的節點，然後移除限制式，讓資源可以在之後移至不同的節點。  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>監視容錯移轉叢集 SQL Server 服務

檢視目前的叢集狀態：

```bash
sudo pcs status  
```

檢視叢集和資源的即時狀態：

```bash
sudo crm_mon 
```

在 `/var/log/cluster/corosync.log` 檢視資源代理程式記錄

## <a name="add-a-node-to-a-cluster"></a>將節點新增至叢集

1. 檢查每個節點的 IP 位址。 下列指令碼會顯示您目前節點的 IP 位址。 

   ```bash
   ip addr show
   ```

3. 新節點需要一個不超過 15 個字元的唯一名稱。 根據預設，在 Red Hat Linux 中，電腦名稱是 `localhost.localdomain`。 這個預設名稱可能不是唯一的，而且太長。 將電腦名稱稱設定為新的節點。 將電腦名稱新增至 `/etc/hosts` 來設定電腦名稱。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hosts`。 

   ```bash
   sudo vi /etc/hosts
   ```

   下列範例顯示 `/etc/hosts`，以及適用於三個節點 (名稱為 `sqlfcivm1`、`sqlfcivm2` 和 `sqlfcivm3`) 的新增項目。

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   每個節點上的檔案應該都相同。 

1. 停止新節點上的 SQL Server 服務。

1. 依照指示將資料庫檔案目錄裝載到共用位置：

   從 NFS 伺服器，安裝 `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   在用戶端和 NFS 伺服器上開啟防火牆 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   編輯 /etc/fstab 檔案以包含裝載命令： 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   執行 `mount -a` 讓變更生效。
   
1. 在新的節點上，建立檔案以儲存 SQL Server 使用者名稱和密碼，以供 Pacemaker 登入使用。 下列命令會建立並填入這個檔案：

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. 在新的節點上，開啟 Pacemaker 防火牆連接埠。 若要使用 `firewalld` 開啟這些連接埠，請執行下列命令：

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > 如果您使用其他防火牆，其中沒有內建的高可用性設定，您需要開啟下列連接埠，Pacemaker 才能與叢集中的其他節點通訊
   >
   > * TCP：連接埠 2224、3121、21064
   > * UDP：連接埠 5405

1. 在每個節點上安裝 Pacemaker 套件。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. 設定安裝 Pacemaker 和 Corosync 封裝時建立的預設使用者密碼。 使用與現有節點相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```
 
3. 啟用並啟動 `pcsd` 服務和 Pacemaker。 這將會允許新的節點在重新開機後重新加入叢集。 在新的節點上執行下列命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 安裝 SQL Server 的 FCI 資源代理程式。 在新的節點上執行下列命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. 在叢集中現有的節點上，對新節點進行驗證並將其新增至叢集：

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    下列範例會將名為 **vm3** 的節點新增至叢集。

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>從叢集中移除節點

若要從叢集中移除節點，請執行下列命令：

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>變更 sqlservr 資源監視間隔的頻率

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

下列範例會將 mssql 資源的監視間隔設定為 2 秒：

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>針對適用於 SQL Server 的 Red Hat Enterprise Linux 共用磁碟叢集進行疑難排解

在對叢集進行疑難排解時，可能有助於了解三個守護程式如何共同合作來管理叢集資源。 

| 精靈 | 描述 
| ----- | -----
| Corosync | 提供叢集節點之間的仲裁成員資格和訊息傳遞。
| Pacemaker | 位於 Corosync 頂端，並針對資源提供狀態機器。 
| PCSD | 透過 `pcs` 工具管理 Pacemaker 和 Corosync

必須執行 PCSD 才能使用 `pcs` 工具。 

### <a name="current-cluster-status"></a>目前的叢集狀態 

`sudo pcs status` 會傳回每個節點的叢集、仲裁、節點、資源和背景程式狀態的相關基本資訊。 

狀況良好的 Pacemaker 仲裁輸出範例如下：

```
Cluster name: MyAppSQL 
Last updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1 
Stack: corosync 
Current DC: sqlvmnode1  (version 1.1.13-10.el7_2.4-44eb2dd) - partition with quorum 
3 nodes and 1 resource configured 

Online: [ sqlvmnode1 sqlvmnode2 sqlvmnode3] 

Full list of resources: 

mssqlha (ocf::sql:fci): Started sqlvmnode1 

PCSD Status: 
sqlvmnode1: Online 
sqlvmnode2: Online 
sqlvmnode3: Online 

Daemon Status: 
corosync: active/disabled 
pacemaker: active/enabled 
```

在此範例中，`partition with quorum` 表示節點的多數仲裁已上線。 如果叢集失去節點的多數仲裁，則 `pcs status` 會傳回 `partition WITHOUT quorum`，而且所有資源都會停止。 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]` 會傳回目前參與叢集的所有節點名稱。 如果沒有任何節點參與，則 `pcs status` 會傳回 `OFFLINE: [<nodename>]`。

`PCSD Status` 顯示每個節點的叢集狀態。

### <a name="reasons-why-a-node-may-be-offline"></a>節點可能處於離線狀態的原因

當節點離線時，請檢查下列項目。

- **防火牆**

    下列連接埠必須在所有節點上開啟，Pacemaker 才能夠進行通訊。
    
    - **TCP：2224、3121、21064

- **Pacemaker 或 Corosync 服務正在執行**

- **節點通訊**

- **節點名稱對應**

## <a name="additional-resources"></a>其他資源

* Pacemaker 的[從頭開始建立叢集](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf)指南

## <a name="next-steps"></a>後續步驟

[設定適用於 SQL Server 的 Red Hat Enterprise Linux 共用磁碟叢集](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

