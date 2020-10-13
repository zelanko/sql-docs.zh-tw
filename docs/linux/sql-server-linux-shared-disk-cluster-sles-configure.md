---
title: 設定 SQL Server 的 SLES 共用磁碟叢集
description: 透過設定適用於 SQL Server 的 SUSE Linux Enterprise Server (SLES) 共用磁碟叢集來實作高可用性。
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.openlocfilehash: c32a526c35d4a4cf236794e1ada6dc66cfac6ba6
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784719"
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>設定 SQL Server 的 SLES 共用磁碟叢集

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本指南提供在 SUSE Linux Enterprise Server (SLES) 上，為 SQL Server 建立兩個節點共用磁碟叢集的指示。 叢集層會以建置於 [Pacemaker](https://clusterlabs.org/) \(英文\) 之上的 SUSE [高可用性擴充功能 (HAE)](https://www.suse.com/products/highavailability) \(英文\) 為基礎。 

如需叢集設定、資源代理程式選項、管理、最佳做法和建議的詳細資訊，請參閱 [SUSE Linux Enterprise 高可用性擴充功能 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html) \(英文\)。

## <a name="prerequisites"></a>Prerequisites

若要完成下列端對端案例，您需要兩部電腦來部署兩個節點叢集，以及另一個伺服器來設定 NFS 共用。 以下步驟概述這些伺服器的設定方式。

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>在每個叢集節點上安裝和設定作業系統

第一個步驟是在叢集節點上設定作業系統。 在此逐步解說中，使用含 HA 附加元件有效訂閱的 SLES。

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>在每個叢集節點上安裝和設定 SQL Server

1. 在這兩個節點上安裝和設定 SQL Server。 如需詳細指示，請參閱[安裝 Linux 上的 SQL Server](sql-server-linux-setup.md)。
2. 基於設定目的，將一個節點指定為主要，並將另一個指定為次要。 本指南後續將會使用這些字詞。 
3. 在次要節點上，停止並停用 SQL Server。 下列範例會停止並停用 SQL Server：

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > 在安裝期間，將為 SQL Server 執行個體產生伺服器主要金鑰，並將其置於 `/var/opt/mssql/secrets/machine-key`。 在 Linux 上，SQL Server 一律會以名為 mssql 的本機帳戶執行。 因為它是本機帳戶，所以不會在節點之間共用其身分識別。 因此，您需要將加密金鑰從主要節點複製到每個次要節點，讓每個本機 mssql 帳戶可以存取它來將伺服器主要金鑰解密。
4. 在主要節點上，建立 Pacemaker 的 SQL Server 登入，並授與該登入執行 `sp_server_diagnostics` 的權限。 Pacemaker 會使用此帳戶來驗證哪個節點正在執行 SQL Server。

    ```bash
    sudo systemctl start mssql-server
    ```
    使用 'sa' 帳戶連線到 SQL Server 主要資料庫，然後執行下列動作：

    ```sql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. 在主要節點上，停止並停用 SQL Server。
6. 遵循 [SUSE 文件](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) \(英文\) 的指示，為每個叢集節點設定及更新 hosts 檔案。 'hosts' 檔案必須包含每個叢集節點的 IP 位址和名稱。

    若要檢查目前節點的 IP 位址，請執行：

    ```bash
    sudo ip addr show
    ```

    在每個節點上設定電腦名稱。 為每個節點提供不超過 15 個字元的唯一名稱。 若要設定電腦名稱，請使用 [yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) \(英文\) 將它新增至 `/etc/hostname`，您也可以[手動](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html) \(英文\) 設定。

    下列範例顯示 `/etc/hosts`，其中包含名為 `SLES1` 和 `SLES2` 的兩個額外節點。

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > 所有叢集節點都必須能夠透過 SSH 互相存取。 hb_report 或 crm_report 之類的工具 (用於疑難排解) 和 Hawk 的 History Explorer 都要求節點之間的無密碼 SSH 存取，否則它們只能從目前的節點收集資料。 如果您使用非標準 SSH 連接埠，請使用 -X 選項 ([請參閱 man 頁面](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html) \(英文\))。 例如，如果您的 SSH 連接埠是 3479，則以下列方式叫用 crm_report：
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >如需詳細資訊，請參閱[管理指南].(https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

在下一節中，您將設定共用儲存體，並將資料庫檔案移至該儲存體。  

## <a name="configure-shared-storage-and-move-database-files"></a>設定共用儲存體和移動資料庫檔案

有多種解決方案可用於提供共用儲存體。 本逐步解說示範如何使用 NFS 設定共用儲存體。 我們建議您遵循最佳做法，並使用 Kerberos 來保護 NFS： 

- [與 NFS 共用檔案系統](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

如果您不遵循此指導方針，那麼任何可以存取您的網路並假冒 SQL 節點 IP 位址的人，都能存取您的資料檔案。 一如往常，請務必在生產環境中使用您的系統之前，先針對它建立威脅模型。 

另一個儲存體選項是使用 SMB 檔案共用。

- [SUSE 文件的 Samba 小節](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>設定 NFS 伺服器

若要設定 NFS 伺服器，請參閱 SUSE 文件中的下列步驟：[設定 NFS 伺服器](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server) \(英文\)。

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>設定所有叢集節點，以連線到 NFS 共用儲存體

在設定用戶端 NFS 以掛接 SQL Server 資料庫檔案路徑指向共用儲存體位置之前，請確定您將資料庫檔案儲存到暫存位置，以便稍後在共用上複製這些檔案：

1. **僅在主要節點上**，將資料庫檔案儲存至暫存位置。 下列指令碼會建立新的暫存目錄、將資料庫檔案複製到新的目錄，並移除舊的資料庫檔案。 當 SQL Server 以本機使用者 mssql 的身分執行時，您必須確定在資料轉送到掛接的共用之後，本機使用者具有共用的讀寫存取權。 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    在所有叢集節點上設定 NFS 用戶端：

    - [設定用戶端](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients) \(英文\)

    > [!NOTE]
    > 建議遵循 SUSE 的最佳做法和有關高可用性 NFS 儲存體的建議：[含 DRBD 和 Pacemaker 的高可用性 NFS 儲存體](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html) \(英文\)。

2. 驗證 SQL Server 是否使用新的檔案路徑成功啟動。 請在每個節點上執行此動作。 此時，一次只能有一個節點執行 SQL Server。 它們不能同時執行，因為它們會嘗試同時存取資料檔案 (為了避免不小心在這兩個節點上啟動 SQL Server，請使用檔案系統叢集資源來確保共用不會由不同的節點掛接兩次)。 下列命令會啟動 SQL Server、檢查狀態，然後停止 SQL Server。

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

此時，SQL Server 的兩個執行個體都設定為使用共用儲存體上的資料庫檔案來執行。 下一步是針對 Pacemaker 設定 SQL Server。 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>在每個叢集節點上安裝和設定 Pacemaker

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

## <a name="configure-the-cluster-resources-for-sql-server"></a>設定 SQL Server 的叢集資源

下列步驟說明如何設定 SQL Server 的叢集資源。 您必須自訂兩個設定。

- **SQL Server 資源名稱**：叢集 SQL Server 資源的名稱。 
- **逾時值**：逾時值是當資源在上線時，叢集等待的時間量。 就 SQL Server 而言，這是您預期 SQL Server 讓 `master` 資料庫上線所需的時間。 

針對您的環境，更新下列指令碼中的值。 在一個節點上執行，以設定和啟動叢集服務。

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

認可設定之後，SQL Server 會在與虛擬 IP 資源相同的節點上啟動。 

如需詳細資訊，請參閱[設定和管理叢集資源 (命令列)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config) \(英文\)。 

### <a name="verify-that-sql-server-is-started"></a>驗證已啟動 SQL Server。 

若要驗證 SQL Server 已啟動，請執行 **crm status** 命令：

```bash
crm status
```

當 Pacemaker 已成功啟動為叢集資源時，其結果如下列範例所顯示。 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>管理叢集資源

若要管理您的叢集資源，請參閱下列 SUSE 主題：[管理叢集資源](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm ) \(英文\)

### <a name="manual-failover"></a>手動容錯移轉

雖然資源設定為在發生硬體或軟體故障時，會自動容錯移轉 (或遷移) 至叢集的其他節點，但您也可以使用 Pacemaker GUI 或命令列，手動將資源移至叢集中另一個節點。 

針對此工作使用 migrate 命令。 例如，若要將 SQL 資源遷移到名為 SLES2 的叢集節點，請執行： 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>其他資源

[SUSE Linux Enterprise 高可用性擴充功能](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) \(英文\) 
