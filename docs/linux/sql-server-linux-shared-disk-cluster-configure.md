---
title: 設定容錯移轉叢集執行個體-SQL Server 上 Linux (RHEL) |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.openlocfilehash: 00ae511095e046623df080e7cc6f9704aedc87ef
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712931"
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>設定容錯移轉叢集執行個體-SQL Server 上 Linux (RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 共用的磁碟的雙節點容錯移轉叢集執行個體提供高可用性的伺服器層級備援。 在本教學課程中，您將了解如何在 Linux 上建立 SQL Server 的雙節點容錯移轉叢集執行個體。 您將完成的特定步驟包括：

> [!div class="checklist"]
> * 安裝和設定 Linux
> * 安裝和設定 SQL Server
> * 設定主機檔案
> * 設定共用存放裝置，並移動資料庫檔案
> * 安裝並在每個叢集節點上設定 Pacemaker
> * 設定容錯移轉叢集執行個體

這篇文章說明如何建立 SQL Server 的兩個節點的共用的磁碟容錯移轉叢集執行個體 (FCI)。 本文說明和指令碼範例包含 Red Hat Enterprise Linux (RHEL)。 Ubuntu 散發套件在指令碼範例通常會很類似於 RHEL 也在 Ubuntu 上運作。 

如需概念性資訊，請參閱 < [SQL Server 容錯移轉叢集執行個體 (FCI) 在 Linux 上](sql-server-linux-shared-disk-cluster-concepts.md)。

## <a name="prerequisites"></a>先決條件

若要完成下列的端對端案例中，您需要將兩個節點叢集和儲存體的另一部伺服器部署的兩部機器。 下列步驟概述這些伺服器設定的方式。

## <a name="set-up-and-configure-linux"></a>安裝和設定 Linux

第一個步驟是設定叢集節點上的作業系統。 在叢集中的每個節點上設定 linux 散發套件。 在這兩個節點上使用相同的散發套件和版本。 使用其中一種下列散發套件：
    
* RHEL 與有效的訂用帳戶，為 HA 附加元件

## <a name="install-and-configure-sql-server"></a>安裝和設定 SQL Server

1. 安裝和設定兩個節點上的 SQL Server。  如需詳細指示，請參閱 < [Linux 上安裝 SQL Server](sql-server-linux-setup.md)。
1. 將一個節點指定為主要，另一個則設為次要，基於的組態。 使用下列這些詞彙本指南。  
1. 在次要節點，停止並停用 SQL Server。
    下列範例會停止，並停用 SQL Server: 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > 在設定的時間，伺服器主要金鑰會產生 SQL Server 執行個體，並放在`var/opt/mssql/secrets/machine-key`。 在 Linux 上，一律以呼叫 mssql 的本機帳戶執行 SQL Server。 因為它是本機帳戶時，不會在節點之間共用其身分識別。 因此，您要複製的加密金鑰從主要節點，每個次要節點以便每個本機 mssql 帳戶可以存取它來解密伺服器主要金鑰。 

1.  主要節點上，為 Pacemaker 建立 SQL server 登入，並授與登入執行的權限`sp_server_diagnostics`。 Pacemaker 會使用此帳戶，來確認哪一個節點正在執行 SQL Server。 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   連接到 SQL Server`master`資料庫與 sa 帳戶，然後執行下列命令：

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   或者，您可以以更細微的層級設定權限。 Pacemaker 登入需要對於`VIEW SERVER STATE`sp_server_diagnostics，與查詢健全狀況狀態`setupadmin`和`ALTER ANY LINKED SERVER`執行 sp_dropserver 和 sp_addserver 更新 FCI 執行個體名稱的資源名稱。 

1. 主要節點上，停止並停用 SQL Server。 

## <a name="configure-the-hosts-file"></a>設定主機檔案

每個叢集節點，設定主機檔案。 主機檔案必須包含的每個叢集節點名稱與 IP 位址。

1. 檢查每個節點的 IP 位址。 下列指令碼會顯示目前節點的 IP 位址。 

    ```bash
    sudo ip addr show
    ```

1. 每個節點上設定的電腦名稱。 為每個節點指定唯一的名稱為 15 個字元或更少。 將電腦名稱，將它加入至`/etc/hosts`。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hosts`。 

   ```bash
   sudo vi /etc/hosts
   ```
   下列範例所示`/etc/hosts`新增名為兩個節點項目`sqlfcivm1`和`sqlfcivm2`。

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

## <a name="configure-storage--move-database-files"></a>設定儲存體，並移動資料庫檔案  

您需要提供兩個節點均可存取的儲存體。 您可以使用 iSCSI、 NFS、 或 SMB。 設定儲存體，呈現到叢集節點中，儲存體，然後將資料庫檔案移到新的存放裝置。 下列文章會說明每個儲存體類型的步驟：

- [設定容錯移轉叢集執行個體-iSCSI-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [設定容錯移轉叢集執行個體-NFS-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [設定容錯移轉叢集執行個體-SMB-Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>安裝並在每個叢集節點上設定 Pacemaker

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

   > 如果您使用其他防火牆沒有內建的高可用性組態，下列連接埠必須開啟 pacemaker 才能與叢集中其他節點通訊
   >
   > * TCP:連接埠 2224，3121 21064
   > * UDP:連接埠 5405

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

FCI 會建立資源群組中。 這是有點更容易，因為資源群組不需要條件約束。 不過，將資源新增到資源群組，他們應啟動的順序。 它們應該啟動的順序為： 

1. 儲存體資源
2. 網路資源
3. 應用程式資源

此範例會建立 FCI NewLinFCIGrp 群組中。 資源群組的名稱必須是唯一從在 Pacemaker 中建立的任何資源。

1.  建立的磁碟資源。 如果不是問題，您會收到任何回應。 若要建立的磁碟資源的方式取決於儲存體類型。 以下是每個儲存體類型的範例。 使用適用於您叢集的儲存體的儲存體類型的範例。

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName > 是的 iSCSI 磁碟相關聯的資源名稱

    \<VolumeGroupName > 磁碟區群組的名稱  

    \<LogicalVolumeName > 是已建立的邏輯磁碟區的名稱  

    \<FolderToMountiSCSIDIsk > 是要掛接磁碟的資料夾 （若是系統資料庫和預設位置，它會是 /var/opt/mssql/data）

    \<FileSystemType > 會根據項目格式化的方式和支援何種分佈是 EXT4 或 XFS。 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName > 是的 NFS 共用與相關聯的資源名稱

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer > 是的 NFS 共用名稱

    \<FolderToMountNFSShare > 是要掛接磁碟的資料夾 （若是系統資料庫和預設位置，它會是 /var/opt/mssql/data）

    以下顯示一個範例：

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<伺服器名稱 > 是 SMB 共用的伺服器名稱

    \<共用名稱 > 是共用的名稱

    \<資料夾名稱 > 是的最後一個步驟中建立的資料夾名稱
    
    \<使用者名稱 > 是要存取共用的使用者名稱

    \<密碼 > 使用者的密碼

    \<ADDomain > （如果使用 Windows Server 為基礎的 SMB 共用時適用） 是 AD DS 網域

    \<mssqlUID > 是 mssql 使用者的 UID

    \<mssqlGID > 是在 mssql 使用者 GID

    \<RGName > 是的資源群組名稱
 
2.  建立可供 FCI 的 IP 位址。 如果不是問題，您會收到任何回應。

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName > 是的 IP 位址相關聯的資源名稱

    \<IPAddress > 為 FCI 中的 IP 位址

    \<NetworkCard > 是子網路 (也就是 eth0) 相關聯的網路卡

    \<網路遮罩 > 是子網路 (也就是 24) 的網路遮罩

    \<RGName > 是的資源群組名稱
 
3.  建立 FCI 資源。 如果不是問題，您會收到任何回應。

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName > 不僅資源的名稱，而且 FCI 與相關聯的易記名稱。 這是什麼使用者和應用程式將用來連接。 

    \<RGName > 是資源群組的名稱。
 
4.  執行命令`sudo pcs resource`。 FCI 應在線上。
 
5.  連接到使用 SSMS 或 sqlcmd 使用 DNS/資源的名稱，在 FCI 的 FCI。

6.  發出陳述式`SELECT @@SERVERNAME`。 它應該會傳回 FCI 的名稱。

7.  發出陳述式`SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`。 它應該會傳回 FCI 所在節點的名稱。

8.  手動容錯 FCI 在節點上。 請參閱底下指示[操作容錯移轉叢集執行個體-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-operate.md)。

9.  最後，容錯回復至原始節點 FCI，並移除共置條件約束。

<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

-->
## <a name="summary"></a>總結

在本教學課程中，您已完成下列工作的內容。

> [!div class="checklist"]
> * 安裝和設定 Linux
> * 安裝和設定 SQL Server
> * 設定主機檔案
> * 設定共用存放裝置，並移動資料庫檔案
> * 安裝並在每個叢集節點上設定 Pacemaker
> * 設定容錯移轉叢集執行個體

## <a name="next-steps"></a>後續步驟

- [操作容錯移轉叢集執行個體-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
