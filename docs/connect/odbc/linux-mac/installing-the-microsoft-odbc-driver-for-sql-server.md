---
title: 安裝的 Microsoft ODBC Driver for SQL Server on Linux 及 macOS |Microsoft 文件
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 44afb66dfdc98ea2160f54d394f48e1ce03df1cd
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Installing the Microsoft ODBC Driver for SQL Server on Linux and macOS (在 Linux 及 macOS 上安裝 Microsoft ODBC Driver for SQL Server)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

這篇文章說明如何安裝[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux 及 macOS，以及選擇性的命令列工具，適用於 SQL Server (`bcp`和`sqlcmd`) 和 unixODBC 開發標頭。

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 for SQL Server 

> [!IMPORTANT]
> 如果您已安裝 v17`msodbcsql`簡短可用的封裝，您應該將它移除之前安裝`msodbcsql17`封裝。 這樣可避免衝突。 `msodbcsql17`可以並存安裝套件`msodbcsql`v13 封裝。

### <a name="debian-8-and-9"></a>Debian 8 和 9
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

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

### <a name="redhat-enterprise-server-6-and-7"></a>RedHat Enterprise Server 6 和 7
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

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

### <a name="suse-linux-enterprise-server-11sp4-and-12"></a>SUSE Linux Enterprise Server 11SP4 和 12

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

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

### <a name="ubuntu-1404-1604-and-1710"></a>Ubuntu 14.04 16.04 和 17.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 14.04
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 17.10
curl https://packages.microsoft.com/config/ubuntu/17.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

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

### <a name="os-x-1011-el-capitan-macos-1012-sierra-and-macos-1013-high-sierra"></a>OS X 10.11 (El Capitan)、 macOS 10.12 （利也） 及 macOS 10.13 （高利也）

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql17 mssql-tools
```

## <a name="microsoft-odbc-driver-131-for-sql-server"></a>Microsoft ODBC Driver 13.1 for SQL Server 

### <a name="debian-8"></a>Debian 8
```
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
```
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
```
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

```
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

```
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
```
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
```
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
```
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

### <a name="os-x-1011-el-capitan-and-macos-1012-sierra"></a>OS X 10.11 (El Capitan) 及 macOS 10.12 （利也）

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
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
```
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
```
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
```
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

```
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
如果您希望/需要[!INCLUDE[msCoName](../../../includes/msconame_md.md)]沒有網際網路連線的電腦上安裝 ODBC Driver 13，您必須手動解析封裝相依性。 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 有下列的直接相依性：
- Ubuntu: libc6 (> = 2.21)，test-libstdc + + 6 (> = 4.9)，libkrb5-3、 libcurl3、 openssl debconf (> = 0.5)，unixodbc (> = 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

接著，每個這些封裝會有自己的相依性，這可能會或可能不會出現在系統上。 此問題的一般解決方案，請參閱您的發佈封裝管理員文件： [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos)， [Ubuntu](http://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian)，和[SUSE](https://en.opensuse.org/Portal:Zypper)

它也是很常見手動下載所有的相依套件並將它們放在一起安裝在電腦上，然後手動安裝，每個封裝的[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 封裝。

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - 下載最新`msodbcsql``.rpm`從這裡： http://packages.microsoft.com/rhel/7/prod/
  - 安裝相依性和驅動程式
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- 下載最新`msodbcsql``.deb`從這裡： http://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- 安裝相依性和驅動程式 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- 下載最新`msodbcsql``.rpm`從這裡： http://packages.microsoft.com/sles/12/prod/
- 安裝與驅動程式的相依性

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

當您完成封裝安裝時，您可以確認[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 可以透過執行 ldd 並檢查其輸出遺漏程式庫來尋找所有相依性：
```
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-linux"></a>Microsoft ODBC Driver 11 for SQL Server on Linux

您可以使用驅動程式之前，安裝 unixODBC 驅動程式管理員。 如需詳細資訊，請參閱[Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)。

**安裝步驟**  

> [!IMPORTANT]  
> 這些指示是指`msodbcsql-11.0.2270.0.tar.gz`，這是 Red Hat linux 的安裝檔案。 如果您要安裝 SUSE Linux 的預覽，則檔案名稱是`msodbcsql-11.0.2260.0.tar.gz`。  
  
若要安裝驅動程式：

1.  請確定您擁有根權限。  

2.  將變更下載放置檔案的所在目錄`msodbcsql-11.0.2270.0.tar.gz`。 請確定您有與您的 Linux 版本相符的 \*.tar.gz 檔案。 若要將檔案解壓縮，請執行下列命令， `tar xvzf msodbcsql-11.0.2270.0.tar.gz`。  
  
3.  若要變更`msodbcsql-11.0.2270.0`目錄該處您應會見名為的檔案和**為 install.sh**。  
  
4.  若要檢視可用的安裝選項清單，請執行下列命令： **./install.sh**。  
  
5.  備份 **odbcinst.ini**。 驅動程式安裝會更新 **odbcinst.ini**。 odbcinst.ini 包含會向 unixODBC 驅動程式管理員註冊的驅動程式清單。 若要探索 odbcinst.ini 在電腦上的位置，執行下列命令： ```odbc_config --odbcinstini```。  
  
6.  安裝驅動程式之前，請執行下列命令： `./install.sh verify`。 輸出`./install.sh verify`報告您的電腦是否具有必要的軟體可支援 ODBC driver on Linux。  
  
7.  當您準備好安裝 ODBC driver on Linux 時，執行命令： `./install.sh install`。 如果您要指定安裝命令 (`bin-dir`或`lib-dir`) 之後, 指定該命令**安裝**選項。  
  
8.  檢閱授權合約之後，請輸入 **YES** 繼續安裝。  
  
安裝會將驅動程式在`/opt/microsoft/msodbcsql/11.0.2270.0`。 驅動程式及其支援檔案必須在`/opt/microsoft/msodbcsql/11.0.2270.0`。  
  
若要確認已成功註冊 Microsoft ODBC driver on Linux，執行下列命令： ```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```。  
  
[使用 ODBC Driver on Linux 的現有 MSDN C++ ODBC 範例](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) ，會顯示使用 ODBC Driver on Linux 連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的程式碼範例。  
  
**解除安裝**  
  
您可以執行下列命令來解除安裝 Linux 上的 ODBC driver 11:  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>連接問題的疑難排解  
如果您無法連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用 ODBC 驅動程式中，使用下列資訊來識別問題。  
  
最常見的連接問題是安裝了兩個 UnixODBC 驅動程式管理員複本。 請在 /usr 中搜尋 libodbc\*.so\*。 如果您看見多個檔案版本，表示您 (可能) 安裝了多個驅動程式管理員。 您的應用程式可能使用了錯誤的版本。
  
藉由編輯以啟用連接記錄您`/etc/odbcinst.ini`檔案以包含這些項目有下列區段：

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
如果連接再次失敗，且未出現記錄檔，表示您的電腦上 (可能) 有兩個驅動程式管理員複本。 否則，記錄輸出應如下所示：  
  
```  
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
如果 ASCII 字元編碼不是 utf-8，例如： 
  
```  
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
有一個以上已安裝的驅動程式管理員和應用程式使用其中一個，或驅動程式管理員未正確建置的錯誤。  
  
如需解決連接失敗的詳細資訊，請參閱：  
  
-   [疑難排解 SQL 連接性問題的步驟](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [SQL Server 2005 連接問題的疑難排解 - 第 1 部分](http://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [使用連接信號緩衝區在 SQL Server 2008 中進行連接的疑難排解](http://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [SQL Server 驗證疑難排解員](http://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [錯誤詳細資料 (http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    應變更 URL 中指定的錯誤號碼 (11001)，以符合您所看到的錯誤。  
  
## <a name="driver-files"></a>驅動程式檔案
ODBC Driver on Linux 及 MacOS 包含下列元件：

### <a name="linux"></a>Linux

|元件|Description|  
|---------------|-----------------|  
|libmsodbcsql-17。X.so.X.X 或 libmsodbcsql 13。X.so.X.X|共用的物件 (`so`) 包含的所有驅動程式的功能的動態程式庫檔案。 這個檔案安裝在`/opt/microsoft/msodbcsql17/lib64/`驅動程式 17 和`/opt/microsoft/msodbcsql/lib64/`Driver 13。|  
|`msodbcsqlr17.rll`或`msodbcsqlr13.rll`|隨附驅動程式程式庫的資源檔。 這個檔案安裝在 `[driver .so directory]../share/resources/en_US/`| 
|msodbcsql.h|包含新的定義，使用驅動程式所需的所有標頭檔。<br /><br /> **注意**  ：您無法在相同的程式中參考 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h 會安裝在`/opt/microsoft/msodbcsql17/include/`驅動程式 17 和`/opt/microsoft/msodbcsql/include/`Driver 13。 |
|LICENSE.txt|包含的使用者授權合約條款的文字檔案。 這個檔案放在`/usr/share/doc/msodbcsql17/`驅動程式 17 和`/usr/share/doc/msodbcsql/`Driver 13。|
|RELEASE_NOTES|包含版本資訊的文字檔案。 這個檔案放在`/usr/share/doc/msodbcsql17/`驅動程式 17 和`/usr/share/doc/msodbcsql/`Driver 13。|


### <a name="macos"></a>MacOS

|元件|Description|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib or libmsodbcsql.13.dylib|動態程式庫 (`dylib`) 檔案，其中包含的所有驅動程式的功能。 這個檔案安裝在`/usr/local/lib/`。|  
|`msodbcsqlr17.rll`或`msodbcsqlr13.rll`|隨附驅動程式程式庫的資源檔。 這個檔案安裝在`[driver .dylib directory]../share/msodbcsql17/resources/en_US/`驅動程式 17 和`[driver .dylib directory]../share/msodbcsql/resources/en_US/`Driver 13。 | 
|msodbcsql.h|包含新的定義，使用驅動程式所需的所有標頭檔。<br /><br /> **注意**  ：您無法在相同的程式中參考 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h 會安裝在`/usr/local/include/msodbcsql17/`驅動程式 17 和`/usr/local/include/msodbcsql/`Driver 13。 |
|LICENSE.txt|包含的使用者授權合約條款的文字檔案。 這個檔案放在`/usr/local/share/doc/msodbcsql17/`驅動程式 17 和`/usr/local/share/doc/msodbcsql/`Driver 13。 |
|RELEASE_NOTES|包含版本資訊的文字檔案。 這個檔案放在`/usr/local/share/doc/msodbcsql17/`驅動程式 17 和`/usr/local/share/doc/msodbcsql/`Driver 13。 |

## <a name="resource-file-loading"></a>資源檔載入

驅動程式必須載入資源檔案才能運作。 這個檔案稱為`msodbcsqlr17.rll`或`msodbcsqlr13.rll`根據驅動程式版本。 位置`.rll`檔案是相對於驅動程式本身的位置 (`so`或`dylib`)，如上表所述。 驅動程式也會嘗試載入版 17.1`.rll`從預設目錄，如果從相對路徑載入失敗。 預設資源檔路徑為：

Linux: `/opt/microsoft/msodbcsql17/share/resources/en_US/`

macOS: `/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>另請參閱

[安裝驅動程式管理員](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[版本資訊](../../../connect/odbc/linux-mac/release-notes.md)

[系統需求](../../../connect/odbc/linux-mac/system-requirements.md)
