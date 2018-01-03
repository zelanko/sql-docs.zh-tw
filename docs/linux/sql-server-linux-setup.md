---
title: "Linux 上安裝 SQL Server 2017 |Microsoft 文件"
description: "安裝、 更新及解除安裝 SQL Server on Linux。 本主題涵蓋連線、 離線，且無人看管的案例。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 12/21/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.workload: Active
ms.openlocfilehash: 180c8492531da7c3b9c15ebef28917b52e0869ce
ms.sourcegitcommit: 73043fe1ac5d60b67e33b44053c0a7733b98bc3d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/23/2017
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>SQL Server on Linux 的安裝指南

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主題說明如何安裝、 更新及解除安裝 SQL Server 2017 on Linux。 SQL Server 2017 Red Hat Enterprise Linux (RHEL)、 SUSE Linux Enterprise Server (SLES) 和 Ubuntu 支援。 它也可做為 Docker 映像，可以在 Linux 或 Docker for Windows/mac 上的 Docker 引擎執行

> [!TIP]
> 若要快速地開始，跳至其中的快速入門[RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)， [Ubuntu](quickstart-install-connect-ubuntu.md)，或[Docker](quickstart-install-connect-docker.md)。

## <a id="supportedplatforms"></a>支援的平台

下列 Linux 平台上支援 SQL Server 2017:

| 平台 | 支援的版本 | Get
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 或 7.4 | [取得 RHEL 7.4](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [取得 SLES v12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [取得 Ubuntu 16.04](http://www.ubuntu.com/download/server)
| **Docker 引擎** | 1.8+ | [取得 Docker](http://www.docker.com/products/overview)

Microsoft 僅支援部署及管理 SQL Server 容器使用 OpenShift 和 Kubernetes。

SQL Server 2017 最新的支援原則，請參閱[Microsoft SQL Server 的技術支援人員原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

## <a id="system"></a>系統需求

SQL Server 2017 具有適用於 Linux 的下列系統需求：

|||
|-----|-----|
| **記憶體** | 2 GB |
| **[File System]** | **XFS**或**EXT4** (其他檔案系統，例如**BTRFS**，不支援) |
| **磁碟空間** | 6 GB |
| **處理器速度** | 2 GHz |
| **處理器核心** | 2 核心 |
| **處理器類型** | 只有 x64-相容 |

如果您使用**網路檔案系統 (NFS)**遠端共用實際執行環境，請注意下列的支援需求：

- 使用 NFS 版本**4.2 或更新版本**。 NFS 的舊版本不支援必要的功能，例如 fallocate 和通用的現代的檔案系統的疏鬆檔案建立。
- 只尋找**/var/opt/mssql**上 NFS 掛接的目錄。 不支援其他檔案，例如 SQL Server 系統二進位檔。
- 確定 NFS 用戶端在掛接的遠端共用時，會使用 'nolock' 選項。

## <a id="platforms"></a> 安裝 SQL Server

您可以從命令列，在 Linux 上安裝 SQL Server。 如需指示，請參閱下列快速入門：

- [Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [執行 docker](quickstart-install-connect-docker.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="upgrade"></a>更新 SQL Server

若要更新**mssql 伺服器**封裝最新的版本，請使用其中一個基礎平台上的下列命令：

| 平台 | 套件更新命令 |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

這些命令會下載最新的封裝，並取代二進位檔位於`/opt/mssql/`。 使用者產生的資料庫和系統資料庫不會受到這項作業。

## <a id="rollback"></a>復原 SQL Server

若要復原先前版本的 SQL Server 降級，使用下列步驟：

1. 識別您想要降級至 SQL Server 封裝的版本號碼。 如需封裝的數字的清單，請參閱[版本資訊](sql-server-linux-release-notes.md)。

1. 降級為舊版的 SQL Server。 在下列命令，取代`<version_number>`與您在第一個步驟所識別的 SQL Server 版本號碼。

   | 平台 | 套件更新命令 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> 只支援降級至相同的主要版本，例如 SQL Server 2017 內的版本。

## <a id="versioncheck"></a>檢查已安裝的 SQL Server 版本

若要確認您目前版本和版本的 SQL Server on Linux，請使用下列程序：

1. 如果尚未安裝，請安裝[SQL Server 命令列工具](sql-server-linux-setup-tools.md)。

1. 使用**sqlcmd**執行 TRANSACT-SQL 命令，以顯示您的 SQL Server 版本與版別。

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a>解除安裝 SQL Server

若要移除**mssql 伺服器**Linux 上的套件，請使用其中一個基礎平台上的下列命令：

| 平台 | 封裝移除命令 |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

移除封裝並不會刪除產生的資料庫檔案。 如果您想要刪除資料庫檔案，請使用下列命令：

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="repositories"></a>設定來源儲存機制

當您安裝或升級 SQL Server 時，您收到最新版本的 SQL Server 設定的 Microsoft 儲存機制。

### <a name="repository-options"></a>儲存機制選項

有兩種類型的每個散發的儲存機制：

- **累計更新 (CU)**: 累計更新 (CU) 儲存機制自該版本包含基底的 SQL Server 版本和 bug 修正或改進的封裝。 累計更新的發行版本，例如 SQL Server 2017 特有。 它們會以一般的步調發行。

- **GDR**: GDR 儲存機制 含有該發行以來的基底的 SQL Server 版本和僅重大修正程式和安全性更新的封裝。 這些更新也會新增到下一個 CU 版本。

每個 CU 和 GDR 版本包含完整的 SQL Server 封裝和所有先前的更新，該儲存機制。 從 GDR 發行更新至目前的版本支援適用於 SQL Server 變更設定的儲存機制。 您也可以[降級](#rollback)至您的主要版本內任何發佈 (例如： 2017年)。 更新不支援從 CU GDR 發行的版本。

### <a name="check-your-configured-repository"></a>請檢查設定的儲存機制

如果您想要確認哪些儲存機制已設定，請使用下列平台相關技術。

| 平台 | 程序 |
|-----|-----|
| RHEL | 1.檢視中的檔案**/etc/yum.repos.d**目錄：`sudo ls /etc/yum.repos.d`<br/>2.尋找檔案，以設定 SQL Server 目錄，例如**mssql server.repo**。<br/>3.列印檔案的內容：`sudo cat /etc/yum.repos.d/mssql-server.repo`<br/>4.**名稱**屬性是設定的儲存機制。|
| SLES | 1.執行下列命令：`sudo zypper info mssql-server`<br/>2.**儲存機制**屬性是設定的儲存機制。 |
| Ubuntu | 1.執行下列命令：`sudo cat /etc/apt/sources.list`<br/>2.檢查 mssql 伺服器的套件 URL。 |

儲存機制 URL 的結尾會確認儲存機制類型：

- **mssql 伺服器**： 預覽儲存機制。
- **mssql-伺服器-2017年**: CU 儲存機制。
- **mssql 伺服器-2017 gdr**: GDR 儲存機制。

### <a name="change-the-source-repository"></a>變更來源儲存機制

若要設定 CU 或 GDR 儲存機制，請使用下列步驟：

> [!NOTE]
> [快速入門](#platforms)設定 CU 儲存機制。 如果您遵循這些教學課程，您不需要使用下列步驟以繼續使用目前的儲存機制。 下列步驟才需要變更設定的儲存機制。

1. 如有必要，移除先前設定的儲存機制。

   | 平台 | Repository | 儲存機制移除命令 |
   |---|---|---|
   | RHEL | **全部** | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES | **CTP** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | | **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
   | | **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|
   | Ubuntu | **CTP** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
   | | **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
   | | **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

1. 如**Ubuntu 只**，匯入公用儲存機制 GPG 索引鍵。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 設定新的儲存機制。

   | 平台 | Repository | 命令 |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [安裝](#platforms)或[更新](#upgrade)SQL Server 和任何相關封裝從新的儲存機制。

   > [!IMPORTANT]
   > 此時，如果您選擇使用其中一個安裝教學課程中，例如[快速入門教學課程](#platforms)，請記住您剛才設定的目標儲存機制。 教學課程中不重複該步驟。 特別是如果您設定的 GDR 儲存機制，因為快速入門教學課程會使用目前的儲存機制。

## <a id="unattended"></a>自動的安裝

您可以以下列方式來執行自動的安裝：

- 初始步驟中的後續[快速入門](#platforms)登錄儲存機制和安裝 SQL Server。
- 當您執行`mssql-conf setup`，將[環境變數](sql-server-linux-configure-environment-variables.md)並用`-n`（沒有提示） 選項。

下列範例會設定開發人員的 SQL Server 版本與**MSSQL_PID**環境變數。 它也可接受使用者授權合約 (**ACCEPT_EULA**) 並設定 SA 使用者密碼 (**MSSQL_SA_PASSWORD**)。 `-n`參數執行 unprompted 的安裝位置的組態值取自環境變數。

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

您也可以建立會執行其他動作的指令碼。 例如，您可以安裝其他 SQL Server 封裝。

更詳細的範例指令碼，請參閱下列範例：

- [Red Hat 自動的安裝指令碼](sample-unattended-install-redhat.md)
- [SUSE 自動的安裝指令碼](sample-unattended-install-suse.md)
- [Ubuntu 自動的安裝指令碼](sample-unattended-install-ubuntu.md)

## <a id="offline"></a>離線安裝

如果您的 Linux 電腦不必存取線上儲存機制中使用[快速入門](#platforms)，您可以直接下載封裝檔案。 這些封裝位於 Microsoft 儲存機制 [https://packages.microsoft.com](https://packages.microsoft.com) 中。

> [!TIP]
> 如果您已成功安裝快速入門中的步驟，您不需要下載或以手動方式安裝下列套件。 本節只是為了在離線案例中。

1. **下載您的平台的資料庫引擎套件**。 封裝詳細資料區段中找到套件下載連結[版本資訊](sql-server-linux-release-notes.md)。

1. **將下載的封裝移到 Linux 機器**。 如果您使用不同的電腦下載的套件，將封裝移到您的 Linux 電腦的一個方法是使用**scp**命令。

1. **安裝資料庫引擎封裝**。 使用其中一個基礎平台上的下列命令。 封裝的檔案名稱，在此範例中取代您所下載的確切名稱。

   | 平台 | 套件 [移除] 命令 |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > 您也可以在與安裝 （RHEL 和 SLES） RPM 套件`rpm -ivh`命令，但上表中的命令會自動安裝相依項目若可以從核准的儲存機制。

1. **解決遺失的相依性**： 您可能需要在此時遺失相依性。 如果沒有，您可以略過此步驟。 在 Ubuntu，如果您擁有存取權已核准的儲存機制包含這些相依性，最簡單的解決方案是使用`apt-get -f install`命令。 此命令也會完成 SQL Server 的安裝。 若要手動檢查相依性，使用下列命令：

   | 平台 | 列出的相依性命令 |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   解決遺失的相依性之後, 嘗試重新安裝 mssql 伺服器封裝。

1. **完成 SQL Server 安裝程式**。 使用**mssql conf**完成 SQL Server 安裝程式：

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="next-steps"></a>後續步驟

安裝之後，您也可以安裝其他選用的 SQL Server 封裝。

- [SQL Server 命令列工具](sql-server-linux-setup-tools.md)
- [SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [SQL Server 全文檢索搜尋](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services (Ubuntu)](sql-server-linux-setup-ssis.md)

連接到您的 SQL Server 執行個體，若要開始建立和管理資料庫。 若要開始，請參閱 < 快速入門：

- [Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [執行 docker](quickstart-install-connect-ubuntu.md)
