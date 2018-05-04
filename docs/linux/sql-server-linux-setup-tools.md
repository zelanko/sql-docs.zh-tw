---
title: Linux 上安裝 SQL Server 命令列工具 |Microsoft 文件
description: 本文說明如何在 Linux 上安裝 SQL Server 工具。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 21f3d62d1a154bec56ca7c5b5308bc3f9914a1ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Sqlcmd 和 bcp 的 SQL Server 命令列工具 Linux 上安裝

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列步驟安裝命令列工具、 Microsoft ODBC 驅動程式，以及它們的相依性。 **Mssql 工具**封裝包含：

- **sqlcmd**： 查詢命令列公用程式。
- **bcp**： 大量匯入匯出的公用程式。

安裝適用於您的平台的工具：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

本文說明如何安裝命令列工具。 如果您要尋找的使用方式的範例**sqlcmd**或**bcp**，請參閱[連結](#next-steps)本主題的結尾。

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>RHEL 7 上安裝工具

使用下列步驟來安裝**mssql 工具**Red Hat Enterprise Linux 上。 

1. 輸入超級使用者模式。

   ```bash
   sudo su
   ```

1. 下載 Microsoft Red Hat 儲存機制設定檔。

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. 結束超級使用者模式。

   ```bash
   exit
   ```

1. 如果您在舊版的**mssql 工具**安裝，請移除任何舊版 unixODBC 封裝。

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 執行下列命令安裝**mssql 工具**unixODBC 開發人員套件。

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 若要更新至最新版**mssql 工具**執行下列命令：
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **選擇性**： 新增`/opt/mssql-tools/bin/`到您**路徑**bash 殼層中的環境變數。

   若要讓**sqlcmd/bcp** bash 殼層登入工作階段，從存取修改您**路徑**中 **~/.bash_profile**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要讓**sqlcmd/bcp** bash 殼層互動式/非登入工作階段，從存取修改**路徑**中 **~/.bashrc**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>Ubuntu 16.04 上安裝工具

使用下列步驟來安裝**mssql 工具**Ubuntu 上。 

1. 匯入公用儲存機制 GPG 索引鍵。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 註冊 Microsoft Ubuntu 儲存機制。

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 更新 [來源] 清單並執行與 unixODBC 開發人員套件的安裝命令。

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 若要更新至最新版**mssql 工具**執行下列命令：
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **選擇性**： 新增`/opt/mssql-tools/bin/`到您**路徑**bash 殼層中的環境變數。

   若要讓**sqlcmd/bcp** bash 殼層登入工作階段，從存取修改您**路徑**中 **~/.bash_profile**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要讓**sqlcmd/bcp** bash 殼層互動式/非登入工作階段，從存取修改**路徑**中 **~/.bashrc**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>SLES 12 上安裝工具

使用下列步驟來安裝**mssql 工具**SUSE Linux Enterprise Server 上。 

1. 加入 Zypper Microsoft SQL Server 儲存機制。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 安裝**mssql 工具**unixODBC 開發人員套件。

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 若要更新至最新版**mssql 工具**執行下列命令：
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **選擇性**： 新增`/opt/mssql-tools/bin/`到您**路徑**bash 殼層中的環境變數。

   若要讓**sqlcmd/bcp** bash 殼層登入工作階段，從存取修改您**路徑**中 **~/.bash_profile**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要讓**sqlcmd/bcp** bash 殼層互動式/非登入工作階段，從存取修改**路徑**中 **~/.bashrc**檔案使用下列命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a> MacOS 上安裝工具

預覽**sqlcmd**和**bcp** macOS 上現已提供。 如需詳細資訊，請參閱[公告](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/)。

*安裝[Homebrew](https://brew.sh)如果您還沒有它：*

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

若要針對 Mac El Capitan 和利也安裝工具，使用下列命令：

```
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox mssql-tools
#for silent install: 
#ACCEPT_EULA=y brew install --no-sandbox mssql-tools
```

## <a id="docker"></a> Docker

從 SQL Server 2017 CTP 2.0 開始，SQL Server 命令列工具隨附的 Docker 映像。 如果您附加至影像的互動式命令提示字元中，您可以在本機執行工具。

## <a name="offline-installation"></a>離線安裝

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

下表提供最新工具封裝的位置：

| 工具套件 | 版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM 工具套件 | 14.0.5.0-1 | [mssql 工具 RPM 套件](https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| SLES RPM 工具套件 | 14.0.5.0-1 | [mssql 工具 RPM 套件](https://packages.microsoft.com/sles/12/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 工具套件 | 14.0.5.0-1 | [mssql 工具 Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |
| Ubuntu 16.10 Debian 工具套件 | 14.0.5.0-1 | [mssql 工具 Debian 封裝](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |

這些封裝相依於**msodbcsql**，而且必須先安裝。 **Msodbcsql**套件也具有相依性  **unixODBC 對內**(RPM) 或**unixodbc dev** (Debian)。 位置**msodbcsql**下表列出封裝：

| msodbcsql 封裝 | 版本 | 下載 |
|-----|-----|-----|
| Red Hat RPM msodbcsql 封裝 | 13.1.6.0-1 | [msodbcsql RPM 套件](https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| SLES RPM msodbcsql 封裝 | 13.1.6.0-1 | [msodbcsql RPM 套件](https://packages.microsoft.com/sles/12/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian msodbcsql 封裝 | 13.1.6.0-1 | [msodbcsql Debian 封裝](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |
| Ubuntu 16.10 Debian msodbcsql 封裝 | 13.1.6.0-1 | [msodbcsql Debian 封裝](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |

若要手動安裝這些套件，請使用下列步驟：

1. **下載的封裝移到 Linux 機器**。 如果您使用不同的電腦下載的套件，將封裝移到您的 Linux 電腦的一個方法是使用**scp**命令。

1. **安裝和封裝**： 安裝**mssql 工具**和**msodbc**封裝。 如果您收到的任何相依性錯誤，請忽略直到下一個步驟。

    | 平台 | 封裝安裝命令 |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | SLES | `sudo zypper install msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo zypper install mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_13.1.6.0-1_amd64.deb`<br/>`sudo dpkg -i mssql-tools_14.0.5.0-1_amd64.deb` |

1. **解決遺失的相依性**： 您可能需要在此時遺失相依性。 如果沒有，您可以略過此步驟。 在某些情況下，您必須以手動方式找出並安裝這些相依性。

    RPM 套件時，您可以檢查必要的相依性，使用下列命令：

    ```bash
    rpm -qpR msodbcsql-13.1.6.0-1.x86_64.rpm
    rpm -qpR mssql-tools-14.0.5.0-1.x86_64.rpm
    ```

    Debian 套件時，如果您擁有存取權已核准的儲存機制包含這些相依性，最簡單的解決方案是使用**apt get**命令：

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > 此命令會完成的 SQL Server 封裝的安裝。

    如果這不適用於您 Debian 封裝，您可以檢查必要的相依性，使用下列命令：

    ```bash
    dpkg -I msodbcsql_13.1.6.0-1_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_14.0.5.0-1_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>後續的步驟

如需如何使用的範例**sqlcmd**若要連接到 SQL Server，並建立資料庫，請參閱下列快速入門：

- [Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [執行 docker](quickstart-install-connect-ubuntu.md)

如需如何使用的範例**bcp**大量匯入和匯出資料，請參閱[大量複製資料到 SQL Server on Linux](sql-server-linux-migrate-bcp.md)。
