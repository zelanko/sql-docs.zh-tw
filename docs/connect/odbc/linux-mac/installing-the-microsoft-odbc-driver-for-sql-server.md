---
title: 安裝 Microsoft ODBC Driver for SQL Server (Linux)
description: 了解如何在 Linux 用戶端上安裝 Microsoft ODBC Driver for SQL Server，以啟用資料庫連線能力。
ms.date: 04/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06baa1fb2029f1d34e747db4c70763ae400c60fe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82153268"
---
# <a name="install-the-microsoft-odbc-driver-for-sql-server-linux"></a>安裝 Microsoft ODBC Driver for SQL Server (Linux)

本文說明如何在 Linux 上安裝 Microsoft ODBC Driver for SQL Server， 以及如何使用適用於 SQL Server (`bcp` 和 `sqlcmd`) 與 unixODBC 開發標頭的選擇性命令列工具。

本文提供從 Bash Shell 安裝 ODBC 驅動程式的命令。 如果想要直接下載套件，請參閱[下載 ODBC Driver for SQL Server](../download-odbc-driver-for-sql-server.md)。

## <a name="microsoft-odbc-17"></a><a id="17"></a> Microsoft ODBC 17

下列各節說明如何從不同 Linux 發行版本的 Bash Shell 安裝 Microsoft ODBC Driver 17。

- [Alpine Linux](#alpine17)
- [Debian](#debian17)
- [Red Hat Enterprise Linux 與 Oracle](#redhat17)
- [SUSE Linux Enterprise Server](#suse17)
- [Ubuntu](#ubuntu17)

> [!IMPORTANT]
> 如果您已安裝短暫提供的第 17 版 `msodbcsql` 套件，您應該先移除它，再安裝 `msodbcsql17` 套件。 如此可避免衝突。 `msodbcsql17` 套件可以和 `msodbcsql` 第 13 版套件並存安裝。

### <a name="alpine-linux"></a><a id="alpine17"></a> Alpine Linux

```bash
#Download the desired package(s)
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.2-1_amd64.apk
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.2.2-1_amd64.apk


#(Optional) Verify signature, if 'gpg' is missing install it using 'apk add gnupg':
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.2-1_amd64.sig
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.2.2-1_amd64.sig

curl https://packages.microsoft.com/keys/microsoft.asc  | gpg --import -
gpg --verify msodbcsql17_17.5.2.2-1_amd64.sig msodbcsql17_17.5.2.2-1_amd64.apk
gpg --verify mssql-tools_17.5.2.2-1_amd64.sig mssql-tools_17.5.2.2-1_amd64.apk


#Install the package(s)
sudo apk add --allow-untrusted msodbcsql17_17.5.2.2-1_amd64.apk
sudo apk add --allow-untrusted mssql-tools_17.5.2.2-1_amd64.apk
```

> [!NOTE]
> Alpine 支援需要驅動程式 17.5 版或更新版本。

### <a name="debian"></a><a id="debian17"></a> Debian

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 10
curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
# optional: kerberos library for debian-slim distributions
sudo apt-get install libgssapi-krb5-2
```

> [!NOTE]
> 您可以改為設定 debconf 變數 'msodbcsql/ACCEPT_EULA' 來替代設定環境變數 'ACCEPT_EULA'：`echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`

### <a name="red-hat-enterprise-server-and-oracle-linux"></a><a id="redhat17"></a> Red Hat Enterprise Server 與 Oracle Linux

```bash
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 8 and Oracle Linux 8
curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo

exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server"></a><a id="suse17"></a> SUSE Linux Enterprise Server

```bash
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
#Ensure SUSE Linux Enterprise 11 Security Module has been installed 
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

#SUSE Linux Enterprise Server 15
zypper ar https://packages.microsoft.com/config/sles/15/prod.repo
#(Only for driver 17.3 and below)
SUSEConnect -p sle-module-legacy/15/x86_64

exit
sudo ACCEPT_EULA=Y zypper install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="ubuntu"></a><a id="ubuntu17"></a> Ubuntu

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 19.10
curl https://packages.microsoft.com/config/ubuntu/19.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

> [!NOTE]
> - Ubuntu 18.04 支援需要驅動程式 17.2 版或更高版本。
> - Ubuntu 18.10 支援需要驅動程式 17.3 版或更高版本。

> [!NOTE]
> 您可以改為設定 debconf 變數 'msodbcsql/ACCEPT_EULA' 來替代設定環境變數 'ACCEPT_EULA'：`echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`

## <a name="previous-versions"></a>舊版

下列各節提供在 Linux 上安裝舊版 Microsoft ODBC 驅動程式的指示。 涵蓋下列驅動程式版本：

- [Microsoft ODBC Driver 13.1 for SQL Server](#13.1)
- [Microsoft ODBC Driver 13 for SQL Server](#13)
- [Microsoft ODBC Driver 11 for SQL Server](#11)

## <a name="odbc-131"></a><a id="13.1"></a> ODBC 13.1

下列各節說明如何從不同 Linux 發行版本的 Bash Shell 安裝 Microsoft ODBC Driver 13.1。

### <a name="debian-8"></a>Debian 8

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11"></a>SUSE Linux Enterprise Server 11

```bash
sudo su
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```bash
sudo su
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1610"></a>Ubuntu 16.10

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

## <a name="odbc-13"></a><a id="13"></a> ODBC 13

下列各節說明如何從不同 Linux 發行版本的 Bash Shell 安裝 Microsoft ODBC Driver 13。

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```bash
sudo su 
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo 
zypper update 
sudo ACCEPT_EULA=Y zypper install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
zypper install unixODBC-utf16-devel
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="offline-installation"></a>離線安裝

如果您希望/需要在沒有網際網路連線的電腦上安裝 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13，您必須手動解析套件相依性。 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 有下列直接相依性：
- Ubuntu: libc6 (>= 2.21), libstdc++6 (>= 4.9), libkrb5-3, libcurl3, openssl, debconf (>= 0.5), unixodbc (>= 2.3.1-1)
- Red Hat：```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SUSE：```glibc, libuuid1, krb5, openssl, unixODBC```

這些每個套件都有自己的相依性，而這些不一定會存在於系統上。 如需此問題的一般解決方案，請參閱散發套件的套件管理員文件：[Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos) \(英文\)、[Ubuntu](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian) \(英文\) 和 [SUSE](https://en.opensuse.org/Portal:Zypper) \(英文\)。

也很常發生手動下載所有相依的套件並將它們一起放在安裝電腦上，然後依次手動安裝每個套件，最後安裝 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 套件。

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7

- 從這裡下載最新的 `msodbcsql` `.rpm`：[https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/)。
- 安裝相依性和驅動程式。
  
```bash
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04

- 從這裡下載最新的 `msodbcsql` `.deb`：[https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/)。
- 安裝相依性和驅動程式。

```bash
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

- 從這裡下載最新的 `msodbcsql` `.rpm`：[https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/)。
- 安裝相依性和驅動程式。

```bash
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

在套件安裝完成後，即可執行 ldd 並查看其輸出是否有缺少的程式庫，以此確認 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 能夠找到其所有相依性：

```bash
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```

## <a name="odbc-11"></a><a id="11"></a> ODBC 11

下列各節說明如何在 Linux 上安裝 Microsoft ODBC Driver 11。 您必須先安裝 unixODBC 驅動程式管理員，才能使用驅動程式。 如需詳細資訊，請參閱[安裝驅動程式管理員](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)。

### <a name="installation-steps"></a>安裝步驟  

> [!IMPORTANT]  
> 這些指令參照 `msodbcsql-11.0.2270.0.tar.gz`，這是 Red Hat Linux 的安裝檔案。 如果您要安裝 SUSE Linux (預覽)，檔案名稱為 `msodbcsql-11.0.2260.0.tar.gz`。  
  
若要安裝驅動程式：

1. 請確定您擁有根權限。  

2. 切換至用於放置所下載檔案 `msodbcsql-11.0.2270.0.tar.gz` 的目錄。 請確定您有與您的 Linux 版本相符的 \*.tar.gz 檔案。 若要擷取檔案，請執行下列命令：`tar xvzf msodbcsql-11.0.2270.0.tar.gz`。  
  
3. 切換至 `msodbcsql-11.0.2270.0` 目錄，在該處您應會看到稱為 **install.sh** 的檔案。  
  
4. 若要檢視可用的安裝選項清單，請執行下列命令： **./install.sh**。  
  
5. 備份 **odbcinst.ini**。 驅動程式安裝會更新 **odbcinst.ini**。 odbcinst.ini 包含會向 unixODBC 驅動程式管理員註冊的驅動程式清單。 若要探索 odbcinst.ini 在電腦上的位置，請執行下列命令：```odbc_config --odbcinstini```。  
  
6. 安裝驅動程式之前，請執行下列命令：`./install.sh verify`。 `./install.sh verify` 的輸出會報告您的電腦是否具有必要的軟體可支援 ODBC Driver on Linux。  
  
7. 當您準備好要安裝 ODBC Driver on Linux 時，請執行下列命令：`./install.sh install`。 如果您要指定安裝命令 (`bin-dir` 或 `lib-dir`)，請在 **install** 選項之後指定該命令。  
  
8. 檢閱授權合約之後，請輸入 **YES** 繼續安裝。  
  
安裝會將驅動程式放在 `/opt/microsoft/msodbcsql/11.0.2270.0`。 驅動程式及其支援檔案必須位於 `/opt/microsoft/msodbcsql/11.0.2270.0`。  
  
若要確認已成功註冊 Microsoft ODBC Driver on Linux，請執行下列命令：```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```。  
  
### <a name="uninstall"></a>解除安裝  
  
您可以執行下列命令，以解除安裝 ODBC Driver 11 on Linux：  
  
1. `rm -f /usr/bin/sqlcmd`
  
2. `rm -f /usr/bin/bcp`  
  
3. `rm -rf /opt/microsoft/msodbcsql`  
  
4. `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="driver-files"></a>驅動程式檔案

Linux 上的 ODBC 驅動程式包含下列元件：

|元件|描述|  
|---------------|-----------------|  
|libmsodbcsql-17.X.so.X.X 或 libmsodbcsql-13.X.so.X.X|共用物件 (`so`) 動態程式庫檔案，其中包含驅動程式的所有功能。 針對 Driver 17，這個檔案會安裝在 `/opt/microsoft/msodbcsql17/lib64/`，針對 Driver 13 則在 `/opt/microsoft/msodbcsql/lib64/`。|  
|`msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`|隨附驅動程式程式庫的資源檔。 這個檔案會安裝在 `[driver .so directory]../share/resources/en_US/`| 
|msodbcsql.h|標頭檔，其中包含使用驅動程式所需的所有新定義。<br /><br /> **注意：** 您無法在同一個程式中參考 msodbcsql.h 和 odbcss.h。<br /><br /> 針對 Driver 17，msodbcsql.h 會安裝在 `/opt/microsoft/msodbcsql17/include/`，針對 Driver 13 則在 `/opt/microsoft/msodbcsql/include/`。 |
|LICENSE.txt|文字檔案，其中包含授權條款。 針對 Driver 17，這個檔案會放在 `/usr/share/doc/msodbcsql17/`，針對 Driver 13 則在 `/usr/share/doc/msodbcsql/`。|
|RELEASE_NOTES|文字檔案，其中包含版本資訊。 針對 Driver 17，這個檔案會放在 `/usr/share/doc/msodbcsql17/`，針對 Driver 13 則在 `/usr/share/doc/msodbcsql/`。|

## <a name="resource-file-loading"></a>載入資源檔

驅動程式需要載入資源檔，才能運作。 這個檔案稱為 `msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`，視驅動程式版本而定。 `.rll` 檔案的位置是相對於驅動程式本身 (`so` 或 `dylib`) 的位置，如上表所述。 到 17.1 版為止，驅動程式也會嘗試從預設目錄載入 `.rll`，如果從相對路徑載入失敗的話。 Linux 上的預設資源檔路徑為 `/opt/microsoft/msodbcsql17/share/resources/en_US/`。

## <a name="troubleshooting"></a>疑難排解

如果無法使用 ODBC 驅動程式建立與 SQL Server 的連線，請參閱已知問題一文中的[針對連線問題進行疑難排解](known-issues-in-this-version-of-the-driver.md#connectivity)。

## <a name="next-steps"></a>後續步驟

在安裝驅動程式後，即可嘗試使用 [C++ ODBC 範例應用程式](../../odbc/cpp-code-example-app-connect-access-sql-db.md)。 如需開發 ODBC 應用程式的詳細資訊，請參閱[開發應用程式](../../../odbc/reference/develop-app/developing-applications.md)。

如需詳細資訊，請參閱 ODBC 驅動程式的[版本資訊](release-notes-odbc-sql-server-linux-mac.md)與[系統需求](system-requirements.md)。
