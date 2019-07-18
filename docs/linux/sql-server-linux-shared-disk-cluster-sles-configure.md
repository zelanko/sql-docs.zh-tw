---
title: 設定 SQL Server 的 SLES 共用的磁碟叢集
description: 藉由設定 SUSE Linux Enterprise Server (SLES) 共用的磁碟叢集的 SQL Server 中實作高可用性。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: 70701d5c0103da089444177db1143066d0c862cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032229"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>設定 SQL Server 的 SLES 共用的磁碟叢集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本指南提供指示來建立適用於 SQL Server 在 SUSE Linux Enterprise Server (SLES) 的兩個節點的共用的磁碟叢集。 叢集層根據 SUSE[高可用性延伸模組 (HAE)](https://www.suse.com/products/highavailability)之上建置[Pacemaker](https://clusterlabs.org/)。 

如需有關叢集設定、 資源代理程式選項、 管理、 最佳做法和建議的詳細資訊，請參閱 < [SUSE Linux Enterprise 高可用性延伸模組 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html)。

## <a name="prerequisites"></a>必要條件

若要完成下列的端對端案例中，您需要部署兩個節點叢集並設定 NFS 共用的另一部伺服器的兩部機器。 下列步驟概述這些伺服器設定的方式。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>安裝和設定每個叢集節點上的作業系統

第一個步驟是設定叢集節點上的作業系統。 此逐步解說中，使用 SLES 與有效的訂用帳戶的 HA 附加元件。

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>安裝和設定每個叢集節點上的 SQL Server

1. 安裝和設定兩個節點上的 SQL Server。 如需詳細指示，請參閱 < [Linux 上安裝 SQL Server](sql-server-linux-setup.md)。
2. 將一個節點指定為主要，另一個則設為次要，基於的組態。 使用下列這些詞彙本指南。 
3. 在次要節點，停止並停用 SQL Server。 下列範例會停止，並停用 SQL Server:

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > 於安裝時期 Server 主要金鑰是產生 SQL Server 執行個體，並放在`/var/opt/mssql/secrets/machine-key`。 在 Linux 上，一律以呼叫 mssql 的本機帳戶執行 SQL Server。 因為它是本機帳戶時，不會在節點之間共用其身分識別。 因此，您要複製的加密金鑰從主要節點，每個次要節點以便每個本機 mssql 帳戶可以存取它來解密伺服器主要金鑰。
4. 主要節點上，為 Pacemaker 建立 SQL server 登入，並授與登入執行的權限`sp_server_diagnostics`。 Pacemaker 會使用此帳戶，來確認哪一個節點正在執行 SQL Server。

    ```bash
    sudo systemctl start mssql-server
    ```
    連接到 SQL Server master 資料庫中使用 'sa' 帳戶並執行下列命令：

    ```sql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. 主要節點上，停止並停用 SQL Server。
6. 請遵照[SUSE 文件中](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html)設定和更新每個叢集節點的主機檔案。 每個叢集節點的名稱與 IP 位址，必須包含 '主機' 檔案。

    若要檢查目前的節點執行的 IP 位址：

    ```bash
    sudo ip addr show
    ```

    每個節點上設定的電腦名稱。 為每個節點指定唯一的名稱為 15 個字元或更少。 將電腦名稱，將它加入至`/etc/hostname`使用[yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html)或是[手動](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html)。

    下列範例所示`/etc/hosts`新增名為兩個節點項目`SLES1`和`SLES2`。

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > 所有叢集節點必須都能夠透過 SSH 互相存取。 hb_report 或 crm_report 之類的工具 (用於疑難排解) 和 Hawk 的 History Explorer 都要求節點之間的無密碼 SSH 存取，否則它們只能從目前的節點收集資料。 如果您使用非標準 SSH 連接埠，請使用-X 選項 ([請參閱 man 頁面](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html))。 例如，如果您的 SSH 連接埠是 3479，叫用與 crm_report:
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >如需詳細資訊，請參閱 [系統管理指南]。(https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

在下一節中，您會設定共用存放裝置，並將您的資料庫檔案移至該儲存體。  

## <a name="configure-shared-storage-and-move-database-files"></a>設定共用存放裝置，並移動資料庫檔案

有各式各樣的解決方案提供共用存放裝置。 此逐步解說會示範設定 NFS 共用的儲存體。 我們建議您遵循最佳作法，並使用 Kerberos 來保護 NFS: 

- [與 NFS 共用檔案系統](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

如果您未遵循本指導方針，可以存取您的網路和詐騙 SQL 節點的 IP 位址的任何人都能夠存取您的資料檔案。 一如往常，請確定您的威脅模型系統在生產環境中使用它之前。 

另一個儲存體選項是使用 SMB 檔案共用：

- [Samba > 一節的 SUSE 文件](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>設定 NFS 伺服器

若要設定 NFS 伺服器，請參閱 SUSE 文件中的下列步驟：[設定 NFS 伺服器](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server)。

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>設定連接到共用的 NFS 儲存體的所有叢集節點

之前設定用戶端 NFS 掛接的 SQL Server 資料庫檔案路徑以指向共用的存放位置，請確定您將資料庫檔案儲存到暫存位置以便能夠將它們複製稍後共用：

1. **只有在主要節點上**，將資料庫檔案儲存到暫存位置。 下列程式碼會建立新的暫存目錄、 將資料庫檔案複製到新的目錄中，並移除舊的資料庫檔案。 SQL Server 執行為本機使用者 mssql 時，您必須確定資料傳輸到掛接的共用之後，本機使用者會有共用的讀寫存取。 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    所有叢集節點上設定 NFS 用戶端：

    - [設定用戶端](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > 建議您遵循 SUSE 的最佳作法和高度可用的 NFS 儲存體相關的建議：[高可用性的 NFS 儲存體搭配 DRBD 與 Pacemaker](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html)。

2. 驗證 SQL Server 已成功開始新的檔案路徑。 每個節點上執行這項操作。 此時只有一個節點應該一次執行 SQL Server。 它們無法同時執行相同的時間因為它們將會同時嘗試存取資料檔案，同時 （若要避免不小心在這兩個節點上啟動 SQL Server，請使用檔案系統叢集資源，請確定兩次是由不同的節點未裝載共用）。 下列命令啟動 SQL Server、 檢查狀態，然後再停止 SQL Server。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

此時兩個 SQL Server 執行個體被設定為執行與共用存放裝置上的資料庫檔案。 下一個步驟是設定 SQL Server 的 Pacemaker。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>安裝並在每個叢集節點上設定 Pacemaker

1. **在這兩個叢集節點上，建立檔案以儲存 SQL Server 使用者名稱和密碼，以供 Pacemaker 登入使用**。 下列命令會建立並填入這個檔案：

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **所有叢集節點都必須能夠透過 SSH 互相存取**。 hb_report 或 crm_report 之類的工具 (用於疑難排解) 和 Hawk 的 History Explorer 都要求節點之間的無密碼 SSH 存取，否則它們只能從目前的節點收集資料。 如果您使用非標準 SSH 連接埠，請使用 -X 選項 (請參閱 man 頁面)。 例如，如果您的 SSH 連接埠是 3479，則以下列方式叫用 hb_report：

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    如需詳細資訊，請參閱 [SUSE 文件中的系統需求和建議 (英文)](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)。

3. **安裝高可用性延伸模組**。 若要安裝延伸模組，請依照下列 SUSE 主題中的步驟執行：
    
    [安裝和設定快速入門 (英文)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **安裝 SQL Server 的 FCI 資源代理程式**。 在這兩個節點上執行下列命令：

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **自動設定第一個節點**。 下一個步驟是透過設定第一個節點 SLES1，以設定執行單節點的叢集。 依照 SUSE 主題[設定第一個節點 (英文)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node) 中的指示執行。

    完成時，使用 `crm status` 檢查叢集狀態：
    ```bash
    crm status
    ```

    這應該會顯示已設定一個節點 (SLES1)。

6. **將節點加入現有叢集**。 接下來，將 SLES2 節點加入至叢集。 依照 SUSE 主題[加入第二個節點 (英文)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node) 中的指示執行。
    
    完成時，使用 **crm status** 來檢查叢集狀態。 如果您已成功加入第二個節點，則輸出將如下所示︰
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** 是虛擬 IP 叢集資源，它是在初始單節點叢集設定期間所設定。

7.  **移除程序**。 如果您需要從叢集移除節點，請使用 **ha-cluster-remove** 啟動程序指令碼。 如需詳細資訊，請參閱[啟動程序指令碼概觀 (英文)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap)。  

## <a name="configure-the-cluster-resources-for-sql-server"></a>設定 SQL Server 叢集資源

下列步驟說明如何設定 SQL Server 叢集資源。 有兩個您需要自訂的設定。

- **SQL Server Resource Name&gt**:叢集的 SQL Server 資源的名稱。 
- **逾時值**:逾時值是時間的資源帶上線時，叢集會等待量。 針對 SQL Server，這是您預期的 SQL Server，才會將時間`master`資料庫上線。 

更新下列指令碼，為您的環境中的值。 若要設定及啟動叢集的服務的一個節點上執行。

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

例如，下列指令碼會建立名為 mssqlha 的 SQL Server 叢集資源。 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

設定認可之後，將會與虛擬 IP 資源相同的節點上啟動 SQL Server。 

如需詳細資訊，請參閱 <<c0> [ 設定和管理叢集資源 （命令列）](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)。 

### <a name="verify-that-sql-server-is-started"></a>確認 SQL Server 已啟動。 

若要確認 SQL Server 已啟動，執行**crm 狀態**命令：

```bash
crm status
```

下列範例顯示的結果，當 Pacemaker 已順利啟動為叢集資源。 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>管理叢集資源

若要管理您的叢集資源，請參閱下列 SUSE 主題：[管理叢集資源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>手動容錯移轉

雖然資源會設定成自動容錯移轉 （或移轉） 到其他節點的叢集發生硬體或軟體失敗時，您可以手動將資源移動到另一個節點在叢集中使用 Pacemaker GUI 或命令列. 

這項工作中使用 [移轉] 命令。 比方說，若要移轉至叢集中的節點名稱 SLES2 SQL 資源執行： 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>其他資源

[SUSE Linux Enterprise 高可用性延伸模組-系統管理指南](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
