---
title: Linux 上的 SQL Server 安裝指南 |Microsoft Docs
description: 安裝、 更新及解除安裝 Linux 上的 SQL Server。 本文章涵蓋線上、 離線，和自動安裝案例。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: f277ca5984523ea25a0a7a8f02cde025d6e14789
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419383"
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>在 Linux 上的 SQL Server 的安裝指引

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供安裝、 更新及解除安裝 SQL Server 2017 和 Linux 上的 SQL Server 2019 預覽的指引。

> [!TIP]
> 本指南 coves 數個部署案例。 如果您只想逐步安裝指示，請跳至其中一個快速入門：
> - [RHEL 快速入門](quickstart-install-connect-red-hat.md)
> - [SLES 快速入門](quickstart-install-connect-suse.md)
> - [在 Ubuntu 快速入門](quickstart-install-connect-ubuntu.md)
> - [Docker 快速入門](quickstart-install-connect-docker.md)

如需常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](../linux/sql-server-linux-faq.md)。

## <a id="supportedplatforms"></a> 支援的平台

Red Hat Enterprise Linux (RHEL)、 SUSE Linux Enterprise Server (SLES) 和 Ubuntu 上支援 SQL Server 2017。 它也支援以 Docker 映像，可以在 Linux 或 Docker for Windows/mac 上的 Docker 引擎執行

| 平台 | 支援的版本 | Get
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 或 7.4 | [取得 RHEL 7.4](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [取得 SLES v12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [取得 Ubuntu 16.04](http://www.ubuntu.com/download/server)
| **Docker 引擎** | 1.8+ | [取得 Docker](http://www.docker.com/products/overview)

Microsoft 也支援部署和管理 SQL Server 容器使用 OpenShift 和 Kubernetes。

> [!NOTE]
> 測試並如先前所列的散發套件支援在 Linux 上 SQL Server。 如果您選擇不支援的作業系統上安裝 SQL Server，請檢閱**的支援原則**一節[Microsoft SQL Server 的技術支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)若要了解支援影響。

## <a id="system"></a> 系統需求

SQL Server 2017 都有適用於 Linux 的系統需求如下：

|||
|-----|-----|
| **記憶體** | 2 GB |
| **[File System]** | **XFS**或是**EXT4** (其他檔案系統，例如**BTRFS**，不支援) |
| **磁碟空間** | 6 GB |
| **處理器速度** | 2 GHz |
| **處理器核心** | 2 個核心 |
| **處理器類型** | 只有 x64-相容 |

如果您使用**網路檔案系統 (NFS)** 遠端共用，在實際執行環境，請注意下列的支援需求：

- 使用 NFS 版本**4.2 或更新版本**。 NFS 較舊版本不支援必要的功能，例如 fallocate 及通用的最新的檔案系統的疏鬆檔案建立。
- 只找出 **/var/opt/mssql**上 NFS 掛接的目錄。 不支援其他檔案，例如 SQL Server 的系統二進位檔案。
- 請確定 NFS 用戶端在掛接的遠端共用時，會使用 'nolock' 選項。

## <a id="repositories"></a> 設定來源儲存機制

當您安裝或升級 SQL Server 時，您會從您設定的 Microsoft 存放庫取得最新版本的 SQL Server。 快速入門使用 SQL Server 2017 累積更新**CU**存放庫。 但您可以改為設定**GDR**存放庫或**預覽 (vNext)** 存放庫。 如需有關儲存機制和設定方式的詳細資訊，請參閱[在 Linux 上的 SQL server 設定存放庫](sql-server-linux-change-repo.md)。

> [!IMPORTANT]
> 如果您先前安裝的 CTP 或 SQL Server 2017 RC 版本，您必須移除預覽存放庫，並註冊公開上市 (GA) 其中一個。 如需詳細資訊，請參閱 <<c0> [ 在 Linux 上的 SQL server 設定存放庫](sql-server-linux-change-repo.md)。

## <a id="platforms"></a> 安裝 SQL Server 2017

您可以從命令列，在 Linux 上安裝 SQL Server 2017。 如需逐步指示，請參閱下列快速入門：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-docker.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="sqlvnext"></a> 安裝 SQL Server 2019 preview

您可以使用相同的快速入門連結上一節中的 Linux 上安裝 SQL Server 2019 預覽。 不過，您必須註冊**預覽 (vNext)** 存放庫，而不是**CU**存放庫。 快速入門會提供有關如何執行這項操作的指示。  

安裝之後，請考慮進行額外的組態變更，以獲得最佳效能。 如需詳細資訊，請參閱 <<c0> [ 效能最佳做法和 Linux 上的 SQL Server 組態指導方針](sql-server-linux-performance-best-practices.md)。

## <a id="upgrade"></a> 更新 SQL Server

若要更新**mssql server**封裝最新版本，請使用其中一個基礎平台上的下列命令：

| 平台 | 套件更新命令 |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

這些命令會下載最新的套件，並取代二進位檔位於`/opt/mssql/`。 使用者產生的資料庫和系統資料庫不會受到這項作業。

> [!TIP]
> 如果您第一次[變更設定的儲存機制](sql-server-linux-change-repo.md)，就可能**更新**命令來升級您的 SQL Server 版本。 如果兩個存放庫間可支援的升級路徑，這是只有大小寫。

## <a id="rollback"></a> 復原 SQL Server

若要回復至上一版的 SQL Server 降級，使用下列步驟：

1. 找出您想要降級至 SQL Server 套件的版本號碼。 如需封裝的數字的清單，請參閱 <<c0> [ 版本資訊](sql-server-linux-release-notes.md)。

1. 降級至舊版的 SQL Server。 在下列命令中，取代`<version_number>`您在第一個步驟中識別的 SQL Server 版本號碼。

   | 平台 | 套件更新命令 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> 它僅支援在相同的主要版本，例如 SQL Server 2017 版本降級。

## <a id="versioncheck"></a> 檢查已安裝的 SQL Server 版本

若要確認您的目前版本和 Linux 上的 SQL Server 的版本，請使用下列程序：

1. 如果尚未安裝，安裝[SQL Server 命令列工具](sql-server-linux-setup-tools.md)。

1. 使用**sqlcmd**執行 TRANSACT-SQL 命令，以顯示您的 SQL Server 版本和版本。

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> 解除安裝 SQL Server

若要移除**mssql server** Linux 上的封裝，請使用其中一個基礎平台上的下列命令：

| 平台 | 套件移除命令 |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

移除封裝，並不會刪除產生的資料庫檔案。 如果您想要刪除的資料庫檔案，請使用下列命令：

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="unattended"></a> 自動的安裝

您可以以下列方式來執行自動的安裝：

- 請遵循中步驟的初始[快速入門](#platforms)註冊存放庫，並安裝 SQL Server。
- 當您執行`mssql-conf setup`，將[環境變數](sql-server-linux-configure-environment-variables.md)並用`-n`（沒有提示） 選項。

下列範例會設定之 SQL Server Developer edition **MSSQL_PID**環境變數。 它也會接受使用者授權合約 (**ACCEPT_EULA**) 並設定 SA 使用者密碼 (**MSSQL_SA_PASSWORD**)。 `-n`參數執行無提示的安裝位置的組態值取自環境變數。

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

您也可以建立會執行其他動作的指令碼。 例如，您可以安裝其他 SQL Server 封裝。

如需更詳細的範例指令碼，請參閱下列範例：

- [Red Hat 自動的安裝指令碼](sample-unattended-install-redhat.md)
- [SUSE 自動的安裝指令碼](sample-unattended-install-suse.md)
- [Ubuntu 自動的安裝指令碼](sample-unattended-install-ubuntu.md)

## <a id="offline"></a> 離線安裝

如果您的 Linux 機器沒有存取中使用的線上儲存機制[快速入門](#platforms)，您可以直接下載封裝檔案。 這些封裝位於 Microsoft 儲存機制[ https://packages.microsoft.com ](https://packages.microsoft.com)。

> [!TIP]
> 如果您已成功安裝快速入門中的步驟，您不需要下載或以手動方式安裝 SQL Server 封裝。 本節是僅供離線案例。

1. **下載您的平台的資料庫引擎套件**。 封裝詳細資料區段中找到套件的下載連結[版本資訊](sql-server-linux-release-notes.md)。

1. **將下載的封裝移至您的 Linux 機器**。 如果您使用不同的電腦下載的套件時，將封裝移到您的 Linux 機器的一個方法是使用**scp**命令。

1. **安裝資料庫引擎套件**。 使用其中一個基礎平台上的下列命令。 套件檔案名稱，在此範例中取代為您下載的確切名稱。

   | 平台 | 封裝安裝命令 |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > 您也可以使用安裝 RPM 套件 （RHEL 和 SLES）`rpm -ivh`命令，但上表中的命令會自動安裝相依項目如果可從核准的存放庫。

1. **解決遺失的相依性**： 您可能必須在此時遺失相依性。 如果沒有，您可以略過此步驟。 在 Ubuntu 上，如果您有存取權已核准的存放庫包含這些相依性，最簡單的解決方案是使用`apt-get -f install`命令。 此命令也會完成 SQL Server 的安裝。 若要手動檢查相依性，使用下列命令：

   | 平台 | 列出的相依性命令 |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   解決遺失的相依性之後, 嘗試重新安裝 mssql server 封裝。

1. **完成 SQL Server 安裝程式**。 使用**mssql conf**完成 SQL Server 安裝程式：

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="licensing-and-pricing"></a>授權與價格

SQL Server 授權適用於 Linux 和 Windows。 如需有關 SQL Server 授權與價格，請參閱[SQL Server 授權如何](https://www.microsoft.com/sql-server/sql-server-2017-pricing)。

## <a name="optional-sql-server-features"></a>選擇性的 SQL Server 功能

安裝完成後，您也可以安裝或啟用選擇性的 SQL Server 功能。

- [SQL Server 命令列工具](sql-server-linux-setup-tools.md)
- [SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [SQL Server 全文檢索搜尋](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> 如需常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](sql-server-linux-faq.md)。
