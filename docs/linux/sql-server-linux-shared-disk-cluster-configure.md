---
title: 設定 FCI - Linux 上的 SQL Server (RHEL)
description: 了解如何為 SQL Server 在 Red Hat Enterprise Linux (RHEL) 上設定容錯移轉叢集執行個體 (FCI)。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: f468697c165eefca98e5d5d7492b9a3d5eab25e8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897276"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>設定容錯移轉叢集執行個體 - Linux 上的 SQL Server (RHEL)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

SQL Server 雙節點共用磁碟容錯移轉叢集執行個體能提供伺服器層級的備援，以達成高可用性。 在本教學課程中，您會了解如何針對 Linux 上的 SQL Server 建立雙節點容錯移轉叢集執行個體。 您將會完成的特定步驟包括：

> [!div class="checklist"]
> * 安裝及設定 Linux
> * 安裝及設定 SQL Server
> * 設定 hosts 檔案
> * 設定共用儲存體和移動資料庫檔案
> * 在每個叢集節點上安裝和設定 Pacemaker
> * 設定容錯移轉叢集執行個體

此文章說明如何針對 SQL Server 建立雙節點共用磁碟容錯移轉叢集執行個體 (FCI)。 此文章包含適用於 Red Hat Enterprise Linux (RHEL) 的指示和指令碼範例。 由於 Ubuntu 散發套件與 RHEL 類似，因此指令碼範例通常也能在 Ubuntu 上運作。 

如需概念性資訊，請參閱 [Linux 上的 SQL Server 容錯移轉叢集執行個體 (FCI)](sql-server-linux-shared-disk-cluster-concepts.md)。

## <a name="prerequisites"></a>必要條件

若要完成下列端對端情節，您需要兩部電腦來部署兩個節點叢集，以及另一部伺服器作為儲存體。 以下步驟概述這些伺服器的設定方式。

## <a name="set-up-and-configure-linux"></a>安裝及設定 Linux

第一個步驟是在叢集節點上設定作業系統。 在叢集中的每個節點上設定 Linux 散發套件。 在兩個節點上都使用相同的散發套件和版本。 使用下列其中一個散發套件：
    
* 具有適用於 HA 附加元件之有效訂用帳戶的 RHEL

## <a name="install-and-configure-sql-server"></a>安裝及設定 SQL Server

1. 在這兩個節點上安裝和設定 SQL Server。  如需詳細指示，請參閱[安裝 Linux 上的 SQL Server](sql-server-linux-setup.md)。
1. 基於設定目的，將一個節點指定為主要，並將另一個指定為次要。 本指南後續將會使用這些字詞。  
1. 在次要節點上，停止並停用 SQL Server。
    下列範例會停止並停用 SQL Server： 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > 在安裝期間，系統會針對 SQL Server 執行個體產生伺服器主要金鑰，並將其置於 `var/opt/mssql/secrets/machine-key`。 在 Linux 上，SQL Server 一律會以名為 mssql 的本機帳戶執行。 因為它是本機帳戶，所以不會在節點之間共用其身分識別。 因此，您需要將加密金鑰從主要節點複製到每個次要節點，讓每個本機 mssql 帳戶可以存取它來將伺服器主要金鑰解密。 

1.  在主要節點上，建立 Pacemaker 的 SQL Server 登入，並授與該登入執行 `sp_server_diagnostics` 的權限。 Pacemaker 會使用此帳戶來驗證哪個節點正在執行 SQL Server。 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   使用 SA 帳戶連線到 SQL Server `master` 資料庫，然後執行下列動作：

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   或者，您可以以更細微的層級設定權限。 Pacemaker 登入需要 `VIEW SERVER STATE` 以搭配 sp_server_diagnostics 來查詢健康情況狀態，且需要 `setupadmin` 和 `ALTER ANY LINKED SERVER` 來透過執行 sp_dropserver 和 sp_addserver 以搭配資源名稱更新 FCI 執行個體名稱。 

1. 在主要節點上，停止並停用 SQL Server。 

## <a name="configure-the-hosts-file"></a>設定 hosts 檔案

在每個叢集節點上，設定 hosts 檔案。 Hosts 檔案必須包含每個叢集節點的 IP 位址和名稱。

1. 檢查每個節點的 IP 位址。 下列指令碼會顯示您目前節點的 IP 位址。 

    ```bash
    sudo ip addr show
    ```

1. 在每個節點上設定電腦名稱。 為每個節點提供不超過 15 個字元的唯一名稱。 將電腦名稱新增至 `/etc/hosts` 來設定電腦名稱。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hosts`。 

   ```bash
   sudo vi /etc/hosts
   ```
   下列範例顯示 `/etc/hosts`，其中包含名為 `sqlfcivm1` 和 `sqlfcivm2` 的兩個額外節點。

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

## <a name="configure-storage--move-database-files"></a>設定儲存體與移動資料庫檔案  

您必須提供兩個節點都可以存取的儲存體。 您可以使用 iSCSI、NFS 或 SMB。 設定儲存體，將該儲存體呈現給叢集節點，然後將資料庫檔案移至新的儲存體。 下列文章會說明適用於每個儲存體類型的步驟：

- [設定容錯移轉叢集執行個體 - iSCSI - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [設定容錯移轉叢集執行個體 - NFS - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [設定容錯移轉叢集執行個體 - SMB - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每個叢集節點上安裝和設定 Pacemaker

1. 在這兩個叢集節點上，建立檔案以儲存 SQL Server 使用者名稱和密碼，以供 Pacemaker 登入使用。 

    下列命令會建立並填入這個檔案：

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd    
    ```

1. 在這兩個叢集節點上，開啟 Pacemaker 防火牆連接埠。 若要使用 `firewalld` 開啟這些連接埠，請執行下列命令：

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 如果您使用其他防火牆，其中沒有內建的高可用性設定，您需要開啟下列連接埠，Pacemaker 才能與叢集中的其他節點通訊
   >
   > * TCP：連接埠 2224、3121、21064
   > * UDP：連接埠 5405

1. 在每個節點上安裝 Pacemaker 套件。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
1. 設定安裝 Pacemaker 和 Corosync 封裝時建立的預設使用者密碼。 在這兩個節點上使用相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```
1. 啟用並啟動 `pcsd` 服務和 Pacemaker。 這將會允許節點在重新開機後重新加入叢集。 在這兩個節點上執行下列命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. 安裝 SQL Server 的 FCI 資源代理程式。 在這兩個節點上執行下列命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-the-failover-cluster-instance"></a>設定容錯移轉叢集執行個體

系統將會在資源群組中建立 FCI。 這會讓您比較輕鬆，因為資源群組能減輕條件約束的需求。 不過，請依照資源應啟動的順序將它們新增至資源群組。 它們應啟動的順序是： 

1. 儲存體資源
2. 網路資源
3. 應用程式資源

此範例將會在 NewLinFCIGrp 群組中建立 FCI。 資源群組的名稱在於 Pacemaker 中所建立的任何資源之間必須是唯一的。

1.  建立磁碟資源。 如果沒有發生問題，您將不會收到任何回應。 建立磁碟資源的方法會取決於儲存體類型。 下列是適用於每個儲存體類型的範例。 使用適用於您叢集存放區之儲存體類型的範例。

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName> 是與 iSCSI 磁碟相關聯之資源的名稱

    \<VolumeGroupName> 是磁碟區群組的名稱  

    \<LogicalVolumeName> 是所建立之邏輯磁碟區的名稱  

    \<FolderToMountiSCSIDIsk> 是要掛接磁碟的資料夾 (針對系統資料庫與預設位置，其會是 /var/opt/mssql/data)

    \<FileSystemType> 會是 EXT4 或 XFS，這取決於項目的格式化方式，以及散發套件所支援的內容。 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName> 是與 NFS 共用相關聯之資源的名稱

    \<IPAddressOfNFSServer> 是您將會使用之 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer> 是 NFS 共用的名稱

    \<FolderToMountNFSShare> 是要掛接磁碟的資料夾 (針對系統資料庫與預設位置，其會是 /var/opt/mssql/data)

    以下顯示一個範例：

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<ServerName> 是使用 SMB 共用之伺服器的名稱

    \<ShareName> 是共用的名稱

    \<FolderName> 是在最後步驟中所建立之資料夾的名稱
    
    \<UserName> 是要存取共用之使用者的名稱

    \<Password> 是使用者的密碼

    \<ADDomain> 是 AD DS 網域 (若在使用 Windows Server 型 SMB 共用時適用的話)

    \<mssqlUID> 是 mssql 使用者的 UID

    \<mssqlGID> 是 mssql 使用者的 GID

    \<RGName> 是資源群組的名稱
 
2.  建立將會由 FCI 使用的 IP 位址。 如果沒有發生問題，您將不會收到任何回應。

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName> 是與 IP 位址相關聯之資源的名稱

    \<IPAddress> 是 FCI 的 IP 位址

    \<NetworkCard> 是與子網路相關聯的網路卡 (例如 eth0)

    \<NetMask> 是子網路的網路遮罩 (例如 24)

    \<RGName> 是資源群組的名稱
 
3.  建立 FCI 資源。 如果沒有發生問題，您將不會收到任何回應。

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName> 不僅是資源的名稱，也是與 FCI 相關聯的易記名稱。 這將會是使用者和應用程式用來連線的名稱。 

    \<RGName> 是資源群組的名稱。
 
4.  執行命令 `sudo pcs resource`。 FCI 應該會上線。
 
5.  使用 FCI 的 DNS/資源名稱，搭配 SSMS 或 sqlcmd 連線至 FCI。

6.  發出陳述式 `SELECT @@SERVERNAME`。 它應該會傳回 FCI 的名稱。

7.  發出陳述式 `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`。 它應該會傳回 FCI 執行所在的節點名稱。

8.  手動將 FCI 容錯移轉至其他節點。 請參閱[操作容錯移轉叢集執行個體 - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-operate.md)底下的指示。

9.  最後，將 FCI 容錯回復至原始節點，並移除共置條件約束。

<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

-->
## <a name="summary"></a>摘要

在本教學課程中，您已完成下列工作。

> [!div class="checklist"]
> * 安裝及設定 Linux
> * 安裝及設定 SQL Server
> * 設定 hosts 檔案
> * 設定共用儲存體和移動資料庫檔案
> * 在每個叢集節點上安裝和設定 Pacemaker
> * 設定容錯移轉叢集執行個體

## <a name="next-steps"></a>後續步驟

- [操作容錯移轉叢集執行個體 - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
