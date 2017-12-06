---
title: "設定 SQL Server 的 Red Hat Enterprise Linux 共用的叢集 |Microsoft 文件"
description: "藉由設定 Red Hat Enterprise Linux 共用的磁碟叢集的 SQL Server 實作高可用性。"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.workload: On Demand
ms.openlocfilehash: d5a621f6bcd1605b7f48ada14607b3e55ef6d6de
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="configure-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>設定 SQL Server 的 Red Hat Enterprise Linux 共用的磁碟叢集

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本指南提供 Red Hat Enterprise Linux 上的 SQL Server 中建立兩個節點共用的磁碟叢集的指示。 叢集的圖層以基礎上 Red Hat Enterprise Linux (RHEL) [HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)之上[Pacemaker](http://clusterlabs.org/)。 在上一個節點或其他作用中的 SQL Server 執行個體。

> [!NOTE] 
> Red Hat HA 附加元件和文件集的存取需要訂用帳戶。 

如下圖所顯示存放裝置會呈現至兩個伺服器。 -Corosync 以及 Pacemaker-叢集元件協調通訊和資源管理。 其中一個伺服器具有作用中連接的儲存體資源，以及 SQL Server。 當 Pacemaker 偵測到失敗時叢集的元件管理將資源移動到另一個節點。  

![Red Hat Enterprise Linux 7 共用磁碟的 SQL 叢集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

如需叢集設定、 資源代理程式選項，以及管理的詳細資訊，請瀏覽[RHEL 參考文件](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html)。


> [!NOTE] 
> 此時，不是為結合以在 Windows 上的 WSFC Pacemaker 與 SQL Server 的整合。 從 SQL、 內沒有存在叢集的認知，所有的協調流程外中，服務由 Pacemaker 控制做為獨立執行個體。 也，例如叢集 dmv sys.dm_os_cluster_nodes 和 sys.dm_os_cluster_properties 將任何記錄。
若要使用連接字串指向字串伺服器名稱並不會使用 IP，則必須註冊在他們的 DNS 伺服器 IP 用來建立所選的伺服器名稱與虛擬 IP 資源 （如下所述）。

下列各節逐步解說的步驟來設定容錯移轉叢集解決方案。 

## <a name="prerequisites"></a>必要條件

若要完成以下的端對端案例中，您需要兩部電腦部署兩個節點叢集並設定 NFS 伺服器的另一部伺服器。 下列步驟概述這些伺服器設定的方式。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>安裝和設定每個叢集節點上的作業系統

第一個步驟是設定叢集節點上的作業系統。 這個逐步解說，使用 RHEL 與有效的訂用帳戶的 HA 附加元件。 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>安裝和設定每個叢集節點上的 SQL Server

1. 安裝和設定兩個節點上的 SQL Server。  如需詳細指示，請參閱[安裝 SQL Server on Linux](sql-server-linux-setup.md)。

1. 將一個節點指定為主要伺服器與另一個則為次要，基於的組態。 使用下列這些詞彙本指南。  

1. 在次要節點，停止並停用 SQL Server。

   下列範例會停止，並停用 SQL Server: 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> 伺服器主要金鑰是於安裝時期，產生 SQL Server 執行個體，並且在置於`/var/opt/mssql/secrets/machine-key`。 On Linux，一律以呼叫 mssql 本機帳戶執行 SQL Server。 因為它是本機帳戶，其識別身分不被共用在節點之間。 因此，您要複製的加密金鑰從主要節點，每個次要節點讓每個本機 mssql 帳戶可以存取它來解密 Server 主要金鑰。 

1. 主要節點上，為 Pacemaker 建立 SQL server 登入並授與登入執行的權限`sp_server_diagnostics`。 若要確認哪一個節點執行 SQL Server，pacemaker 會使用此帳戶。 

   ```bash
   sudo systemctl start mssql-server
   ```

   連接到 SQL Server `master` sa 帳戶的資料庫中，執行下列命令：

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   或者，您可以以更細微的層級設定權限。 Pacemaker 登入需要`VIEW SERVER STATE`sp_server_diagnostics，與查詢健全狀況狀態`setupadmin`和`ALTER ANY LINKED SERVER`執行 sp_dropserver 和 sp_addserver 更新 FCI 執行個體名稱的資源名稱。 

1. 主要節點上，停止並停用 SQL Server。 

1. 設定每個叢集節點的主機檔案。 主機檔案必須包含每個叢集節點名稱與 IP 位址。 

    檢查每個節點的 IP 位址。 下列指令碼會顯示目前節點的 IP 位址。 

   ```bash
   sudo ip addr show
   ```

   每個節點上設定的電腦名稱。 為每個節點指定唯一的名稱是 15 個字元或更少。 將電腦名稱，將它加入至`/etc/hosts`。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hosts`。 

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

下一節中將設定共用存放裝置，並將資料庫檔案移至該儲存體。 

## <a name="configure-shared-storage-and-move-database-files"></a>設定共用存放裝置，並移動資料庫檔案 

有各式各樣的解決方案，提供共用存放裝置。 本逐步解說示範如何使用 NFS 設定共用存放裝置。 我們建議您遵循最佳作法，並使用 Kerberos 來保護 NFS 的安全 (請見這裡提供範例： https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/)。 

>[!Warning]
>如果您未保護 NFS，然後可以存取您的網路和詐騙 SQL 節點的 IP 位址的任何人都將能夠存取您的資料檔案。 如往常，請確定您的威脅模型系統在生產環境中使用它之前。 另一個儲存體選項是使用 SMB 檔案共用。

### <a name="configure-shared-storage-with-nfs"></a>使用 NFS 設定共用存放裝置

> [!IMPORTANT] 
> 裝載具有版本的 NFS 伺服器上的資料庫檔案 < 4 在此版本中不支援。 這包括使用 NFS 共用的磁碟容錯移轉叢集資料庫以及非叢集執行個體上。 我們正在研究如何啟用即將發行版本中的其他 NFS 伺服器版本。 

NFS 伺服器上執行下列作業：

1. 安裝 `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 啟用和啟動`rpcbind`

   ```bash
   sudo systemctl enable rpcbind && systemctl start rpcbind
   ```

1. 啟用和啟動`nfs-server`
 
   ```bash
   systemctl enable nfs-server && systemctl start nfs-server
   ```
 
1.  編輯`/etc/exports`匯出您要共用的目錄。 您必須針對您想要每個共用 1 行。 例如： 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. 匯出的共用

   ```bash
   sudo exportfs -rav
   ```

1. 請確認路徑共用/匯出，NFS 伺服器從執行

   ```bash
   sudo showmount -e
   ```

1. SELinux 中加入的例外狀況

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. 開啟防火牆的伺服器。

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>設定所有叢集節點連接到 NFS 共用儲存體

執行下列步驟在所有叢集節點上。

1.  從 NFS 伺服器上，安裝`nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 開啟 用戶端和 NFS 伺服器上的防火牆

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. 確認您可以看到用戶端電腦上的 NFS 共用

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. 重複上述步驟，在所有叢集節點上。

如需有關使用 NFS 的詳細資訊，請參閱下列資源：

* [NFS 伺服器和 firewalld |堆疊 Exchange](http://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [掛接 NFS 磁碟區 |Linux 網路系統管理員指南](http://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [NFS 伺服器設定](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/3/html/Reference_Guide/s1-nfs-server-export.html)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>掛接點的共用存放裝置的資料庫檔案目錄

1.  **只有在主要節點上**，將資料庫檔案儲存到暫存位置。下列指令碼中，建立新的暫存目錄、 將資料庫檔案複製到新的目錄，並移除舊的資料庫檔案。 當 SQL Server 執行為本機使用者 mssql 時，您需要確定資料傳輸到掛接共用之後，本機使用者會有共用的讀寫存取。 

   ``` 
   $ su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  在所有叢集節點上編輯`/etc/fstab`檔案以納入 mount 命令。  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   下列指令碼會顯示編輯的範例。  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>如果下方的建議，請使用檔案系統 (FS) 資源，，無須以保留 /etc/fstab 中的 [掛接] 命令。 Pacemaker 會負責啟動 FS 叢集資源時，掛接的資料夾。 範圍的協助，則會的 ensurethe FS 永遠都不裝載兩次。 

1.  執行`mount -a`系統更新的掛接的路徑的命令。  

1.  複製的資料庫和記錄檔儲存到`/var/opt/mssql/tmp`新裝載的共用`/var/opt/mssql/data`。 這只需要進行**主要節點上**。 請確定讀的寫權限授予 'mssql' 的本機使用者。

   ``` 
   $ chown mssql /var/opt/mssql/data
   $ chgrp mssql /var/opt/mssql/data
   $ su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  驗證 SQL Server 已成功啟動具有新的檔案路徑。 每個節點上執行這項操作。 此時只有一個節點應該一次執行 SQL Server。 用戶端無法同時執行相同的時間因為它們將會同時嘗試存取資料檔案，同時 （若要避免不小心在這兩個節點上啟動 SQL Server，請使用檔案系統的叢集資源，以確定兩次由不同的節點所未裝載共用）。 下列命令會啟動 SQL Server、 檢查狀態，然後再停止 SQL Server。
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
此時這兩個 SQL Server 執行個體設定為執行與共用存放裝置上的資料庫檔案。 下一個步驟是針對 Pacemaker 設定 SQL Server。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>安裝和設定每個叢集節點上 Pacemaker


2. 在這兩個叢集節點上，建立檔案以儲存 SQL Server 使用者名稱和密碼，以供 Pacemaker 登入使用。 下列命令會建立並填入這個檔案：

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
   sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. 在這兩個叢集節點上，開啟 Pacemaker 防火牆連接埠。 若要使用 `firewalld` 開啟這些連接埠，請執行下列命令：

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

   

2. 設定安裝 Pacemaker 和 Corosync 套件時建立的預設使用者密碼。 在這兩個節點上使用相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```

   

3. 啟用並啟動 `pcsd` 服務和 Pacemaker。 這將會允許節點在重新開機後重新加入叢集。 在這兩個節點上執行下列命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 安裝 SQL Server 的 FCI 資源代理程式。 在這兩個節點上執行下列命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="create-the-cluster"></a>建立叢集 

1. 其中一個節點上建立叢集。

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 …> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 …>
   sudo pcs cluster start --all
   ```

   > RHEL HA 附加元件的 VMWare 及 KVM 柵欄代理程式。 範圍必須停用所有其他 hypervisor 上。 不建議在生產環境中停用圍欄代理程式。 從開始時間範圍內，有 HyperV 或雲端環境中沒有圍欄代理程式。 如果您執行其中一個組態，您需要停用範圍。 \**建議您不要在生產系統中 ！**

   下列命令會停用圍欄代理程式。

   ```bash
   sudo pcs property set stonith-enabled=false
   sudo pcs property set start-failure-is-fatal=false
   ```

2. 設定 SQL Server、 檔案系統和虛擬 IP 資源的叢集資源，並將設定推送到叢集。 您將需要下列資訊：

   - **SQL Server Resource Name>**： 叢集的 SQL Server 資源的名稱。 
   - **逾時值**： 逾時值是叢集等候的時間量時資源上線。 SQL Server，這是您預期要讓 SQL Server 的時間`master`資料庫上線。  
   - **浮動 IP 資源名稱**： 虛擬 IP 位址資源的名稱。
   - **IP 位址**： 用戶端將用來連接到 SQL Server 的叢集執行個體的 IP 位址。 
   - **檔案系統資源名稱**： 檔案系統資源的名稱。
   - **裝置**: NFS 共用的路徑
   - **裝置**： 掛接在共用的本機路徑
   - **fstype**： 檔案共用型別 (也就是 nfs)

   更新您的環境下的指令碼中的值。 若要設定並啟動叢集的服務的一個節點上執行。  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci op defaults timeout=<timeout_in_seconds>
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   例如，下列指令碼會建立名為的 SQL Server 叢集資源`mssqlha`，以及使用 IP 位址浮動 IP 資源`10.0.0.99`。 它也會建立檔案系統資源，並加入條件約束，因此所有資源會共都置於相同的 SQL 資源節點上。 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci op defaults timeout=60s
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   將設定推送之後，SQL Server 將會啟動其中一個節點上。 

3. 確認 SQL Server 已啟動。 

   ```bash
   sudo pcs status 
   ```

   下列範例示範如何 Pacemaker 已成功時的結果會啟動 SQL Server 的叢集執行個體。 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    slqfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>其他資源

* [叢集從頭](http://clusterlabs.org/doc/Cluster_from_Scratch.pdf)從 Pacemaker 指南

## <a name="next-steps"></a>後續的步驟

[Red Hat Enterprise Linux 共用的磁碟叢集上操作 SQL Server](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
