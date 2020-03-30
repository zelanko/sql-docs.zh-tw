---
title: 在 Linux 上安裝 SQL Server 命令列工具
titleSuffix: SQL Server
description: 本文描述如何在 Linux 上安裝 SQL Server 工具。
author: VanMSFT
ms.author: vanto
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: a6ee495dc984273b8a1c20784542d6611edbbbba
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288782"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>在 Linux 上安裝 SQL Server 命令列工具 sqlcmd 和 bcp

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列步驟會安裝命令列工具、Microsoft ODBC 驅動程式及兩者的相依性。 **mssql-tools** 套件包含：

- **sqlcmd**：命令列查詢公用程式。
- **BCP**：大量匯入/匯出公用程式。

安裝適用於您平台的工具：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

本文描述如何安裝命令列工具。 如果您要尋找使用 **sqlcmd** 或 **bcp** 的範例，請參閱本主題結尾的[連結](#next-steps)。

## <a name="a-idrhelinstall-tools-on-rhel-7"></a><a id="RHEL"><a/>在 RHEL 7 上安裝工具

遵循下列步驟，在 Red Hat Enterprise Linux 上安裝 **mssql-tools**。 

1. 進入超級使用者模式。

   ```bash
   sudo su
   ```

1. 下載 Microsoft Red Hat 存放庫組態檔。

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. 結束超級使用者模式。

   ```bash
   exit
   ```

1. 如果您已安裝舊版的 **mssql-tools**，請移除所有舊版的 unixODBC 套件。

   ```bash
   sudo yum remove mssql-tools unixODBC-utf16-devel
   ```

1. 執行下列命令，使用 unixODBC 開發人員套件安裝 **mssql-tools**。

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 若要更新為最新版本的 **mssql-tools**，請執行下列命令：
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **選擇性**：在 Bash Shell 中將 `/opt/mssql-tools/bin/` 新增至您的 **PATH** 環境變數。

   若要讓登入工作階段的 Bash Shell 可存取 **sqlcmd/bcp**，請使用下列命令修改您在 **~/.bash_profile** 檔案中的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要讓互動式/非登入工作階段的 Bash Shell 可存取 **sqlcmd/bcp**，請使用下列命令修改 **~/.bashrc** 檔案中的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a name="install-tools-on-ubuntu-1604"></a><a id="ubuntu"></a>在 Ubuntu 16.04 上安裝工具

使用下列步驟在 Ubuntu 上安裝 **mssql-tools**。

> [!NOTE]
> 從 SQL Server 2019 CU3 開始支援 Ubuntu 18.04。 如果您正在使用 Ubuntu 18.04，請將存放庫路徑從 `/ubuntu/16.04` 變更為 `/ubuntu/18.04`。

1. 匯入公開存放庫 GPG 金鑰。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 註冊 Microsoft Ubuntu 存放庫。

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 更新來源清單，並使用 unixODBC 開發人員套件執行安裝命令。

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 若要更新為最新版本的 **mssql-tools**，請執行下列命令：
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **選擇性**：在 Bash Shell 中將 `/opt/mssql-tools/bin/` 新增至您的 **PATH** 環境變數。

   若要讓登入工作階段的 Bash Shell 可存取 **sqlcmd/bcp**，請使用下列命令修改您在 **~/.bash_profile** 檔案中的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要讓互動式/非登入工作階段的 Bash Shell 可存取 **sqlcmd/bcp**，請使用下列命令修改 **~/.bashrc** 檔案中的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a name="install-tools-on-sles-12"></a><a id="SLES"></a>在 SLES 12 上安裝工具

遵循下列步驟，在 SUSE Linux Enterprise Server 上安裝 **mssql-tools**。 

1. 將 Microsoft SQL Server 存放庫新增至 Zypper。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 使用 unixODBC 開發人員套件安裝 **mssql-tools**。

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 若要更新為最新版本的 **mssql-tools**，請執行下列命令：
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **選擇性**：在 Bash Shell 中將 `/opt/mssql-tools/bin/` 新增至您的 **PATH** 環境變數。

   若要讓登入工作階段的 Bash Shell 可存取 **sqlcmd/bcp**，請使用下列命令修改您在 **~/.bash_profile** 檔案中的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要讓互動式/非登入工作階段的 Bash Shell 可存取 **sqlcmd/bcp**，請使用下列命令修改 **~/.bashrc** 檔案中的 **PATH**：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a name="install-tools-on-macos"></a><a id="macos"></a> 在 macOS 上安裝工具

macOS 現在提供 **sqlcmd** 和 **bcp** 的預覽。 如需詳細資訊，請參閱[公告](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/)。

*安裝 [Homebrew](https://brew.sh) (若尚未安裝)：*

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

若要安裝適用於 Mac El Capitan 和 Sierra 的工具，請使用下列命令：

```
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install mssql-tools
#for silent install: 
#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-tools
```

## <a name="docker"></a><a id="docker"></a> Docker

如果您[在 Docker 容器中執行 SQL Server](quickstart-install-connect-docker.md)，則 SQL Server 命令列工具已包含在 SQL Server Linux 容器映射中。 如果您使用互動式 Bash Shell 來附加至正在執行的容器，則您可以在本機執行這些工具。

## <a name="offline-installation"></a>離線安裝

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

1. 首先，找出並複製適用於您 Linux 發行版本的 **mssql-tools** 套件：

   | Linux 發行版本 | **mssql-tools** 套件位置 |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools) |

1. 此外，也請找出並複製 **msodbcsql** 套件，這是相依性。 **msodbcsql** 套件也相依於 **unixODBC-devel** (Red Hat 和 SLES) 或 **unixODBC dev** (Ubuntu)。 下表列出 **msodbcsql** 套件的位置：

   | Linux 發行版本 | ODBC 套件位置 |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [**msodbcsql**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql)<br/>[**unixodbc-dev**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/u/unixodbc/) |

1. **將已下載套件移至您的 Linux 電腦**。 如果您使用不同電腦來下載套件，將套件移至 Linux 電腦的其中一種方式是使用 **scp** 命令。

1. **安裝套件**：安裝 **mssql-tools** 和 **msodbc** 套件。 如果您遇到任何相依性錯誤，請忽略，直到下一個步驟。

    | 平台 | 套件安裝命令 |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-<version>.rpm`<br/>`sudo yum localinstall mssql-tools-<version>.rpm` |
    | SLES | `sudo zypper install msodbcsql-<version>.rpm`<br/>`sudo zypper install mssql-tools-<version>.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_<version>.deb`<br/>`sudo dpkg -i mssql-tools_<version>.deb` |

1. **解決遺漏的相依性**：此時，您可能會遺漏某些相依性。 如果沒有，則您可以略過此步驟。 在某些情況下。您必須手動找出並安裝這些相依性。

    針對 RPM 套件，您可以使用下列命令來檢查所需的相依性：

    ```bash
    rpm -qpR msodbcsql-<version>.rpm
    rpm -qpR mssql-tools-<version>.rpm
    ```

    針對 Debian 套件，如果您可以存取包含這些相依性的已核准存放庫，最簡單的解決方案就是使用 **apt-get** 命令：

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > 此命令也會完成安裝 SQL Server 套件。

    如果這不適用於您的 Debian 套件，您可以使用下列命令檢查所需的相依性：

    ```bash
    dpkg -I msodbcsql_<version>_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_<version>_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>後續步驟

如需使用 **sqlcmd** 連線至 SQL Server 並建立資料庫的範例，請參閱下列其中一個快速入門：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-ubuntu.md)

如需使用 **bcp** 大量匯入和匯出資料的範例，請參閱[將資料大量複製到 Linux 上的 SQL Server](sql-server-linux-migrate-bcp.md)。
