---
title: 適用於 SQL Server 運作 Red Hat Enterprise Linux 共用的叢集
description: 設定適用於 SQL Server 的 Red Hat Enterprise Linux 共用的磁碟叢集，以實作高可用性。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.openlocfilehash: e20824630fa9740ba8d9bc7d1c63e87fe08d1632
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833120"
---
# <a name="operate-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>操作 SQL server 的 Red Hat Enterprise Linux 共用的磁碟叢集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文件說明如何使用 Red Hat Enterprise Linux 的共用的磁碟容錯移轉叢集，適用於 SQL Server 執行下列工作。

- 手動容錯移轉叢集
- 監視容錯移轉叢集 SQL Server 服務
- 新增叢集節點
- 移除叢集節點
- 變更 SQL Server 資源監視頻率

## <a name="architecture-description"></a>結構描述

叢集層以在 Red Hat Enterprise Linux (RHEL) 為基礎[HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)之上建置[Pacemaker](https://clusterlabs.org/)。 Corosync 和 Pacemaker 協調叢集間通訊和資源管理。 SQL Server 執行個體是在上一個節點或其他使用中。

下圖說明在 Linux 叢集中使用 SQL Server 元件。 

![Red Hat Enterprise Linux 7 共用磁碟的 SQL 叢集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

如需有關叢集設定、 資源代理程式選項，以及管理的詳細資訊，請瀏覽[RHEL 參考文件](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)。

## <a name = "failManual"></a>容錯移轉叢集以手動方式

`resource move`命令建立條件約束，強制啟動目標節點上的資源。  在執行後`move`命令，執行資源`clear`會移除條件約束，因此可以一次移動的資源，或具有自動容錯移轉的資源。 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

下列範例會移動**mssqlha**資源，以名為的節點**sqlfcivm2**，使資源可以稍後再移動至另一個節點，然後移除條件約束。  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>監視容錯移轉叢集 SQL Server 服務

檢視目前的叢集狀態：

```bash
sudo pcs status  
```

檢視即時狀態的叢集和資源：

```bash
sudo crm_mon 
```

檢視位置的資源代理程式記錄檔 `/var/log/cluster/corosync.log`

## <a name="add-a-node-to-a-cluster"></a>將節點加入至叢集

1. 檢查每個節點的 IP 位址。 下列指令碼會顯示目前節點的 IP 位址。 

   ```bash
   ip addr show
   ```

3. 新的節點需要唯一的名稱為 15 個字元或更少。 根據預設，在 Red Hat Linux 電腦名稱是`localhost.localdomain`。 這個預設名稱可能不是唯一的而且太長。 將新的節點設定的電腦名稱。 將電腦名稱，將它加入至`/etc/hosts`。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hosts`。 

   ```bash
   sudo vi /etc/hosts
   ```

   下列範例所示`/etc/hosts`新增名為的三個節點項目`sqlfcivm1`， `sqlfcivm2`，和`sqlfcivm3`。

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   檔案應該是每個節點上相同。 

1. 新的節點上停止 SQL Server 服務。

1. 請依照下列指示來掛接的共用位置的資料庫檔案目錄：

   從 NFS 伺服器上，安裝 `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   開啟用戶端和 NFS 伺服器上的防火牆 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   編輯 /etc/fstab 檔案，以納入的掛接命令： 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   執行`mount -a`，變更才會生效。
   
1. 在新的節點上建立要儲存的 SQL Server 使用者名稱和密碼 Pacemaker 登入的檔案。 下列命令會建立並填入這個檔案：

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. 在新的節點，開啟 Pacemaker 防火牆連接埠。 若要使用 `firewalld` 開啟這些連接埠，請執行下列命令：

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > 如果您使用其他防火牆沒有內建的高可用性組態，下列連接埠必須開啟 pacemaker 才能與叢集中其他節點通訊
   >
   > * TCP:連接埠 2224，3121 21064
   > * UDP:連接埠 5405

1. 新的節點上安裝 Pacemaker 套件。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. 設定安裝 Pacemaker 和 Corosync 封裝時建立的預設使用者密碼。 與現有節點使用相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```
 
3. 啟用並啟動 `pcsd` 服務和 Pacemaker。 這可讓新的節點重新開機後重新加入叢集。 新的節點上執行下列命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 安裝 SQL Server 的 FCI 資源代理程式。 新的節點上執行下列命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. 從叢集中現有的節點，在驗證新的節點，並將它新增至叢集：

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    下列範例會將名為的節點**vm3**到叢集。

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>從叢集移除節點

若要從叢集移除節點執行下列命令：

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>變更 sqlservr 資源監視間隔的頻率

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

下列範例會設定為 2 秒 mssql 資源的監視間隔：

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>疑難排解 SQL server 的 Red Hat Enterprise Linux 共用的磁碟叢集

疑難排解叢集，它可能有助於了解三個精靈搭配來管理叢集資源。 

| 精靈 | 描述 
| ----- | -----
| Corosync | 提供仲裁成員資格和叢集節點之間通訊。
| Pacemaker | 位於 Corosync 之上，並提供資源的狀態機器。 
| PCSD | 管理 Pacemaker 和 Corosync 透過`pcs`工具

必須執行 PCSD，才能使用`pcs`工具。 

### <a name="current-cluster-status"></a>目前的叢集狀態 

`sudo pcs status` 傳回每個節點的叢集、 仲裁、 節點、 資源和協助程式狀態的基本資訊。 

狀況良好的 pacemaker 仲裁輸出的範例為︰

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

在範例中，`partition with quorum`表示節點多數仲裁在線上。 如果叢集遺失節點多數仲裁`pcs status`會傳回`partition WITHOUT quorum`和所有資源將會都停止。 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]` 傳回目前參與叢集的所有節點的名稱。 如果未加入任何節點，`pcs status`傳回`OFFLINE: [<nodename>]`。

`PCSD Status` 顯示每個節點的叢集狀態。

### <a name="reasons-why-a-node-may-be-offline"></a>節點可能離線的原因

當節點離線，請檢查下列項目。

- **防火牆**

    下列連接埠必須開啟 pacemaker 才能才能夠進行通訊的所有節點上。
    
    - \* * TCP:2224, 3121, 21064

- **Pacemaker 或執行 Corosync 服務**

- **節點通訊**

- **節點名稱對應**

## <a name="additional-resources"></a>其他資源

* [叢集從頭](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf)從 Pacemaker 的指南

## <a name="next-steps"></a>後續步驟

[設定 SQL Server 的 Red Hat Enterprise Linux 共用的磁碟叢集](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

