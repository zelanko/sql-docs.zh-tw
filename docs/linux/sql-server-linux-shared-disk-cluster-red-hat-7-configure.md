---
title: 在 Linux 上設定 SQL Server 的 RHEL FCI
description: 了解如何在 Linux 上設定 SQL Server 的高可用性 Red Hat Enterprise Linux (RHEL) 共用磁碟容錯移轉叢集執行個體 (FCI)。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.openlocfilehash: 493239906f83b74735f9fcd4b6673fb2748abfff
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897297"
---
# <a name="configure-rhel-failover-cluster-instance-fci-cluster-for-sql-server"></a>設定 SQL Server 的 RHEL 容錯移轉叢集執行個體 (FCI) 叢集

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本指南提供在 Red Hat Enterprise Linux 上，為 SQL Server 建立雙節點共用磁碟容錯移轉叢集的指示。 叢集層是以建置於 [Pacemaker](https://clusterlabs.org/) 之上的 Red Hat Enterprise Linux (RHEL) [HA 附加元件](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf)為基礎。 SQL Server 執行個體在其中一個節點上為作用中狀態。

> [!NOTE] 
> 存取 Red Hat HA 附加元件與文件皆需要訂用帳戶。 

如下圖所示，會向兩部伺服器提供儲存體。 群集元件 (Corosync 和 Pacemaker) 會協調通訊和資源管理。 其中一部伺服器具有針對儲存體資源和 SQL Server 的作用中連線。 當 Pacemaker 偵測到失敗時，群集元件會負責將資源移至另一個節點。  

![Red Hat Enterprise Linux 7 共用磁碟 SQL 叢集](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

如需叢集設定、資源代理程式選項和管理的詳細資訊，請造訪 [RHEL 參考文件](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html) \(英文\)。


> [!NOTE] 
> 目前，SQL Server 與 Pacemaker 整合程度尚不如 Windows 與 WSFC 的結合。 從 SQL 內並無法得知叢集是否存在，所有協調流程都是從外而入，且服務會以獨立執行個體的形式由 Pacemaker 所控制。 例如，叢集 dmvs sys.dm_os_cluster_nodes 和 sys.dm_os_cluster_properties 將不會有任何記錄。
若要使用指向字串伺服器名稱的連接字串而不使用 IP，他們必須在其 DNS 伺服器中搭配指定的伺服器名稱註冊用來建立虛擬 IP 資源的 IP (如下列各節中所述)。

下列各節將逐步解說設定容錯移轉叢集解決方案的步驟。 

## <a name="prerequisites"></a>Prerequisites

若要完成下列端對端情節，您需要兩部電腦來部署兩個節點叢集，以及另一個伺服器來設定 NFS 伺服器。 以下步驟概述這些伺服器的設定方式。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>在每個叢集節點上安裝和設定作業系統

第一個步驟是在叢集節點上設定作業系統。 在此逐步解說中，針對 HA 附加元件搭配有效的訂用帳戶來使用 RHEL。 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>在每個叢集節點上安裝和設定 SQL Server

1. 在這兩個節點上安裝和設定 SQL Server。  如需詳細指示，請參閱[安裝 Linux 上的 SQL Server](sql-server-linux-setup.md)。

1. 基於設定目的，將一個節點指定為主要，並將另一個指定為次要。 本指南後續將會使用這些字詞。  

1. 在次要節點上，停止並停用 SQL Server。

   下列範例會停止並停用 SQL Server： 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> 在安裝期間，將為 SQL Server 執行個體產生伺服器主要金鑰，並將其置於 `/var/opt/mssql/secrets/machine-key`。 在 Linux 上，SQL Server 一律會以名為 mssql 的本機帳戶執行。 因為它是本機帳戶，所以不會在節點之間共用其身分識別。 因此，您需要將加密金鑰從主要節點複製到每個次要節點，讓每個本機 mssql 帳戶可以存取它來將伺服器主要金鑰解密。 

1. 在主要節點上，建立 Pacemaker 的 SQL Server 登入，並授與該登入執行 `sp_server_diagnostics` 的權限。 Pacemaker 會使用此帳戶來驗證哪個節點正在執行 SQL Server。 

   ```bash
   sudo systemctl start mssql-server
   ```

   使用 SA 帳戶連線到 SQL Server `master` 資料庫，然後執行下列動作：

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   或者，您可以以更細微的層級設定權限。 Pacemaker 登入需要 `VIEW SERVER STATE` 以使用 sp_server_diagnostics 查詢健康狀態，`setupadmin` 和 `ALTER ANY LINKED SERVER` 藉由執行 sp_dropserver 和 sp_addserver 以資源名稱更新 FCI 執行個體名稱。 

1. 在主要節點上，停止並停用 SQL Server。 

1. 為每個叢集節點設定 hosts 檔案。 主機檔案必須包含每個叢集節點的 IP 位址和名稱。 

    檢查每個節點的 IP 位址。 下列指令碼會顯示您目前節點的 IP 位址。 

   ```bash
   sudo ip addr show
   ```

   在每個節點上設定電腦名稱。 為每個節點提供不超過 15 個字元的唯一名稱。 將電腦名稱新增至 `/etc/hosts` 來設定電腦名稱。 下列指令碼可讓您使用 `vi` 編輯 `/etc/hosts`。 

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

在下一節中，您將設定共用儲存體，並將資料庫檔案移至該儲存體。 

## <a name="configure-shared-storage-and-move-database-files"></a>設定共用儲存體和移動資料庫檔案 

有多種解決方案可用於提供共用儲存體。 本逐步解說示範如何使用 NFS 設定共用儲存體。 我們建議您遵循最佳作法，並使用 Kerberos 來保護 NFS 安全 (您可以在這裡找到範例： https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/) \(英文\)。 

>[!Warning]
>如果您不保護 NFS，那麼任何可以存取您的網路並假冒 SQL 節點 IP 位址的人，都能存取您的資料檔案。 一如往常，請務必在生產環境中使用您的系統之前，先針對它建立威脅模型。 另一個儲存體選項是使用 SMB 檔案共用。

### <a name="configure-shared-storage-with-nfs"></a>使用 NFS 設定共用儲存體

> [!IMPORTANT] 
> 在此版本中，不支援將資料庫檔案裝載在版本 < 4 的 NFS 伺服器上。 這包括針對共用磁碟容錯移轉叢集，以及非叢集執行個體上的資料庫使用 NFS。 我們正致力於在即將推出的版本中，啟用其他 NFS 伺服器版本。 

在 NFS 伺服器上執行下列動作：

1. 安裝 `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 啟用並啟動 `rpcbind`

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. 啟用並啟動 `nfs-server`
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  編輯 `/etc/exports` 以匯出您要共用的目錄。 您想要的每個共用都需要 1 行。 例如： 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. 匯出共用

   ```bash
   sudo exportfs -rav
   ```

1. 確認路徑為共用/匯出，並從 NFS 伺服器執行

   ```bash
   sudo showmount -e
   ```

1. 在 SELinux 中新增例外狀況

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. 開啟伺服器的防火牆。

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>設定所有叢集節點，以連線到 NFS 共用儲存體

請在所有叢集節點上執行下列步驟。

1.  安裝 `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. 在用戶端和 NFS 伺服器上開啟防火牆

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

1. 在所有叢集節點上重複這些步驟。

如需使用 NFS 的相關資訊，請參閱下列資源：

* [NFS 伺服器和 firewalld | 堆疊交換](https://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld) \(英文\)
* [裝載 NFS 磁碟區 | Linux 網路系統管理員指南](https://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html) \(英文\)
* [NFS 伺服器設定 | Red Hat 客戶入口網站](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/storage_administration_guide/nfs-serverconfig) \(英文\)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>裝載資料庫檔案目錄以指向共用儲存體

1.  **僅在主要節點上**，將資料庫檔案儲存至暫存位置。下列指令碼會建立新的暫存目錄、將資料庫檔案複製到新的目錄，並移除舊的資料庫檔案。 當 SQL Server 以本機使用者 mssql 的身分執行時，您必須確定在資料轉送到掛接的共用之後，本機使用者具有共用的讀寫存取權。 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  在所有叢集節點上，編輯 `/etc/fstab` 檔案以包含掛接指令。  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   下列指令碼顯示一個編輯範例。  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>如果此處使用建議的檔案系統 (FS) 資源，則不需要在 /etc/fstab 中保留掛接指令。 Pacemaker 會在啟動 FS 叢集資源時負責裝載資料夾。 有了隔離的協助後，就能確保 FS 永遠不會裝載兩次。 

1.  針對系統執行 `mount -a` 命令以更新裝載的路徑。  

1.  將您儲存至 `/var/opt/mssql/tmp` 的資料庫和記錄檔，複製到新的裝載共用 `/var/opt/mssql/data`。 這只需要**在主要節點上**完成。 請確定您將讀取寫入權限授與 'mssql' 本機使用者。

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  驗證 SQL Server 是否使用新的檔案路徑成功啟動。 請在每個節點上執行此動作。 此時，一次只能有一個節點執行 SQL Server。 它們不能同時執行，因為它們會嘗試同時存取資料檔案 (為了避免不小心在這兩個節點上啟動 SQL Server，請使用檔案系統叢集資源來確保共用不會由不同的節點掛接兩次)。 下列命令會啟動 SQL Server、檢查狀態，然後停止 SQL Server。
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
此時，SQL Server 的兩個執行個體都設定為使用共用儲存體上的資料庫檔案來執行。 下一步是針對 Pacemaker 設定 SQL Server。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每個叢集節點上安裝和設定 Pacemaker


2. 在這兩個叢集節點上，建立檔案以儲存 SQL Server 使用者名稱和密碼，以供 Pacemaker 登入使用。 下列命令會建立並填入這個檔案：

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   echo '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwd
   echo '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwd
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

    

2. 設定安裝 Pacemaker 和 Corosync 封裝時建立的預設使用者密碼。 在這兩個節點上使用相同的密碼。 

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

## <a name="configure-fencing-agent"></a>設定隔離代理程式

STONITH 裝置提供隔離代理程式。 [在 Azure 的 Red Hat Enterprise Linux 中設定 Pacemaker](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker/#1-create-the-stonith-devices) 提供範例，說明如何在 Azure 中為此叢集建立 STONITH 裝置。 修改環境的指示。

## <a name="create-the-cluster"></a>建立叢集 

1. 在其中一個節點上建立叢集。

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 ...> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 ...>
   sudo pcs cluster start --all
   ```

2. 設定 SQL Server、檔案系統和虛擬 IP 資源的叢集資源，並將設定推送至叢集。 您需要下列資訊：

   - **SQL Server 資源名稱**：叢集 SQL Server 資源的名稱。 
   - **浮動 IP 資源名稱**：虛擬 IP 位址資源的名稱。
   - **IP 位址**：用戶端將用來連線至 SQL Server 叢集執行個體的 IP 位址。 
   - **檔案系統資源名稱**：檔案系統資源的名稱。
   - **裝置**：NFS 共用路徑
   - **裝置**：裝載至共用的本機路徑
   - **fstype**：檔案共用類型 (例如 nfs)

   針對您的環境，更新下列指令碼中的值。 在一個節點上執行，以設定和啟動叢集服務。  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   例如，下列指令碼會建立名為 `mssqlha` 的 SQL Server 叢集資源，以及具有 IP 位址 `10.0.0.99` 的浮動 IP 資源。 它也會建立 Filesystem 資源並新增限制式，讓所有資源都與 SQL 資源共存於相同的節點上。 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   推送設定之後，SQL Server 會在一個節點上啟動。 

3. 驗證已啟動 SQL Server。 

   ```bash
   sudo pcs status 
   ```

   下列範例會顯示 Pacemaker 已成功啟動 SQL Server 叢集執行個體時的結果。 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    sqlfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>其他資源

* Pacemaker 的[從頭開始建立叢集](https://clusterlabs.org/doc/Cluster_from_Scratch.pdf)指南

## <a name="next-steps"></a>後續步驟

[在 Red Hat Enterprise Linux 共用磁碟叢集上執行 SQL Server](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
