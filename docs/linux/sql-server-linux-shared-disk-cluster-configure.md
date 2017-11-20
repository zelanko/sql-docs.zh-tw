---
title: "設定容錯移轉叢集執行個體的 SQL Server 上 Linux (RHEL) |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 11b7c2e6a782a2e1215a75e746c6def1b42f90a1
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>設定容錯移轉叢集執行個體的 SQL Server 上 Linux (RHEL)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server 共用的磁碟的雙節點容錯移轉叢集執行個體提供高可用性的伺服器層級的備援性。 在本教學課程中，您可以了解如何在 Linux 上建立 SQL Server 的雙節點容錯移轉叢集執行個體。 您將完成的特定步驟包括：

> [!div class="checklist"]
> * 安裝及設定 Linux
> * 安裝及設定 SQL Server
> * 設定主機檔案。
> * 設定共用存放裝置，並移動資料庫檔案
> * 安裝和設定每個叢集節點上 Pacemaker
> * 設定容錯移轉叢集執行個體

本文說明如何建立 SQL Server 共用的磁碟的雙節點容錯移轉叢集執行個體 (FCI)。 本文包括指示和範例指令碼 Red Hat Enterprise Linux (RHEL)。 Ubuntu 分佈是 RHEL 類似，因此指令碼範例將通常 Ubuntu 上也能運作。 

概念性資訊，請參閱[SQL Server 容錯移轉叢集執行個體 (FCI) 在 Linux 上](sql-server-linux-shared-disk-cluster-concepts.md)。

## <a name="prerequisites"></a>必要條件

若要完成以下的端對端案例中，您需要將兩個節點叢集和儲存體的另一部伺服器部署的兩部電腦。 下列步驟概述這些伺服器設定的方式。

## <a name="set-up-and-configure-linux"></a>安裝及設定 Linux

第一個步驟是設定叢集節點上的作業系統。 在叢集中每個節點，設定 linux 散發套件。 兩個節點上使用相同的通訊群組和版本。 使用一或其他的下列發佈：
    
* RHEL HA 附加元件的有效訂用帳戶

## <a name="install-and-configure-sql-server"></a>安裝及設定 SQL Server

1. 安裝和設定兩個節點上的 SQL Server。  如需詳細指示，請參閱[安裝 SQL Server on Linux](sql-server-linux-setup.md)。
1. 將一個節點指定為主要伺服器與另一個則為次要，基於的組態。 使用下列這些詞彙本指南。  
1. 在次要節點，停止並停用 SQL Server。
    下列範例會停止，並停用 SQL Server: 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > 在時間設定，伺服器主要金鑰產生 SQL Server 執行個體，而且位於`var/opt/mssql/secrets/machine-key`。 On Linux，一律以呼叫 mssql 本機帳戶執行 SQL Server。 因為它是本機帳戶，其識別身分不被共用在節點之間。 因此，您要複製的加密金鑰從主要節點，每個次要節點讓每個本機 mssql 帳戶可以存取它來解密 Server 主要金鑰。 

1.  主要節點上，為 Pacemaker 建立 SQL server 登入並授與登入執行的權限`sp_server_diagnostics`。 若要確認哪一個節點執行 SQL Server，pacemaker 會使用此帳戶。 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   連接到 SQL Server `master` sa 帳戶的資料庫中，執行下列命令：

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   或者，您可以以更細微的層級設定權限。 Pacemaker 登入需要`VIEW SERVER STATE`sp_server_diagnostics，與查詢健全狀況狀態`setupadmin`和`ALTER ANY LINKED SERVER`執行 sp_dropserver 和 sp_addserver 更新 FCI 執行個體名稱的資源名稱。 

1. 主要節點上，停止並停用 SQL Server。 

## <a name="configure-the-hosts-file"></a>設定主機檔案。

每個叢集節點上，設定主機檔案。 主機檔案必須包含每個叢集節點名稱與 IP 位址。

1. 檢查每個節點的 IP 位址。 下列指令碼會顯示目前節點的 IP 位址。 

    ```bash
    sudo ip addr show
    ```

1. 每個節點上設定的電腦名稱。 為每個節點指定唯一的名稱是 15 個字元或更少。 將電腦名稱，將它加入至`/etc/hosts`。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hosts`。 

   ```bash
   sudo vi /etc/hosts
   ```
   下列範例所示`/etc/hosts`具有名為兩個節點新增`sqlfcivm1`和`sqlfcivm2`。

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

## <a name="configure-storage--move-database-files"></a>設定存放裝置 （& s) 移動資料庫檔案  

您要提供給這兩個節點均可存取的儲存體。 您可以使用 iSCSI、 NFS 或 SMB。 設定存放裝置、 儲存體呈現給叢集節點，並再將資料庫檔案移至新的存放裝置。 下列文件說明的步驟，針對每一個儲存類型：

- [設定容錯移轉叢集執行個體-iSCSI-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [設定容錯移轉叢集執行個體-NFS-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [設定容錯移轉叢集執行個體-SMB-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>安裝和設定每個叢集節點上 Pacemaker

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
1. 設定安裝 Pacemaker 和 Corosync 套件時建立的預設使用者密碼。 在這兩個節點上使用相同的密碼。 

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

FCI 會建立資源群組中。 這是有點更容易，因為資源群組的必要性的條件約束。 不過，將資源新增到資源群組，他們應該啟動的順序。 它們應該開始的順序為： 

1. 儲存體資源
2. 網路資源
3. 應用程式資源

這個範例會建立群組 NewLinFCIGrp FCI。 資源群組的名稱必須是唯一從 Pacemaker 中建立任何資源。

1.  建立磁碟資源。 如果不是問題，您會收到任何回應。 若要建立的磁碟資源的方式取決於儲存類型。 以下是每個儲存類型的範例。 使用適用於您叢集的存放裝置的存放裝置類型的範例。

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName > 是的 iSCSI 磁碟相關聯的資源名稱

    \<VolumeGroupName > 磁碟區群組的名稱  

    \<LogicalVolumeName > 是建立邏輯磁碟區的名稱  

    \<FolderToMountiSCSIDIsk > 是要掛接磁碟的資料夾 （如系統資料庫和預設位置，它會是 /var/opt/mssql/data）

    \<FileSystemType > 會根據項目格式化的方式，以及支援哪些發佈是 EXT4 或 XFS。 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName > 是的 NFS 共用與相關聯的資源名稱

    \<IPAddressOfNFSServer > 是您要使用的 NFS 伺服器的 IP 位址

    \<FolderOnNFSServer > NFS 共用的名稱

    \<FolderToMountNFSShare > 是要掛接磁碟的資料夾 （如系統資料庫和預設位置，它會是 /var/opt/mssql/data）

     範例如下所示：

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<伺服器名稱 > 是 SMB 共用的伺服器名稱

    \<共用名稱 > 是共用的名稱

    \<資料夾名稱 > 的最後一個步驟中建立的資料夾名稱
    
    \<使用者名稱 > 是要存取此共用的使用者名稱

    \<密碼 > 使用者的密碼

    \<ADDomain > 是 AD DS 網域 （如果使用 Windows Server 為基礎的 SMB 共用時適用）

    \<mssqlUID > 是 mssql 使用者的 UID

    \<mssqlGID > 是在 mssql 使用者 GID

    \<RGName > 的資源群組名稱
 
2.  建立將由 FCI 的 IP 位址。 如果不是問題，您會收到任何回應。

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName > 是的 IP 位址相關聯的資源名稱

    \<IPAddress > 是適用於 FCI 的 IP 位址

    \<NetworkCard > 是子網路 (也就是 eth0) 相關聯的網路卡

    \<網路遮罩 > 是子網路 （也就是 24 小時） 的網路遮罩

    \<RGName > 的資源群組名稱
 
3.  建立 FCI 資源。 如果不是問題，您會收到任何回應。

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName > 不僅資源的名稱，但是 FCI 與相關聯的易記名稱。 這是什麼使用者和應用程式將用來連接。 

    \<RGName > 資源群組的名稱。
 
4.  執行命令`sudo pcs resource`。 FCI 應在線上。
 
5.  連接到使用 SSMS 或 sqlcmd 使用 DNS/資源名稱，在 FCI 的 FCI。

6.  發出陳述式`SELECT @@SERVERNAME`。 它應該會傳回 FCI 的名稱。

7.  發出陳述式`SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`。 它應該會傳回 FCI 執行之節點的名稱。

8.  手動容錯 FCI 在節點上。 請參閱底下指示[營運的 Fedramp 容錯移轉叢集執行個體-SQL Server on Linux](sql-server-linux-shared-disk-cluster-operate.md)。

9.  最後，回到原始節點 FCI 會失敗，並移除共置條件約束。

<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
-->
## <a name="summary"></a>摘要

在本教學課程中，當您完成下列工作。

> [!div class="checklist"]
> * 安裝及設定 Linux
> * 安裝及設定 SQL Server
> * 設定主機檔案。
> * 設定共用存放裝置，並移動資料庫檔案
> * 安裝和設定每個叢集節點上 Pacemaker
> * 設定容錯移轉叢集執行個體

## <a name="next-steps"></a>後續的步驟

- [操作容錯移轉叢集執行個體-SQL Server on Linux](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->

