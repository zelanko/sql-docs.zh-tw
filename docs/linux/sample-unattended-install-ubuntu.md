---
title: 在 Ubuntu 上自動安裝 SQL Server
titleSuffix: SQL Server
description: SQL Server 指令碼範例 - 在 Ubuntu 上自動安裝
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: b71bad98aa6e9172b69efa67ce8708f1479fa691
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67910487"
---
# <a name="sample-unattended-sql-server-installation-script-for-ubuntu"></a>範例：於 Ubuntu 自動安裝 SQL Server 指令碼

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此範例 Bash 指令碼會在 Ubuntu 16.04 上安裝 SQL Server 2017，不需要經過互動式輸入。 其中提供安裝資料庫引擎、SQL Server 命令列工具、SQL Server Agent，以及執行後續安裝步驟的範例。 您可以選擇性地安裝全文檢索搜尋，並建立系統管理使用者。

> [!TIP]
> 如果您不需要自動安裝指令碼，安裝 SQL Server 最快的方式就是遵循 [Ubuntu 的快速入門](quickstart-install-connect-ubuntu.md)。 如需其他安裝資訊，請參閱 [Linux 上的 SQL Server 安裝指引](sql-server-linux-setup.md)。

## <a name="prerequisites"></a>Prerequisites

- 您需要至少 2 GB 的記憶體才能在 Linux 上執行 SQL Server。
- 檔案系統必須是 **XFS** 或 **EXT4**。 不支援其他檔案系統 (例如 **BTRFS**)。
- 如需其他系統需求，請參閱 [SQL Server 在 Linux 上的系統需求](sql-server-linux-setup.md#system)。

## <a name="sample-script"></a>範例指令碼

```bash
#!/bin/bash -e

# Use the following variables to control your install:

# Password for the SA user (required)
MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'

# Product ID of the version of SQL server you're installing
# Must be evaluation, developer, express, web, standard, enterprise, or your 25 digit product key
# Defaults to developer
MSSQL_PID='evaluation'

# Install SQL Server Agent (recommended)
SQL_INSTALL_AGENT='y'

# Install SQL Server Full Text Search (optional)
# SQL_INSTALL_FULLTEXT='y'

# Create an additional user with sysadmin privileges (optional)
# SQL_INSTALL_USER='<Username>'
# SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'

if [ -z $MSSQL_SA_PASSWORD ]
then
  echo Environment variable MSSQL_SA_PASSWORD must be set for unattended install
  exit 1
fi

echo Adding Microsoft repositories...
sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
sudo add-apt-repository "${repoargs}"
repoargs="$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
sudo add-apt-repository "${repoargs}"

echo Running apt-get update -y...
sudo apt-get update -y

echo Installing SQL Server...
sudo apt-get install -y mssql-server

echo Running mssql-conf setup...
sudo MSSQL_SA_PASSWORD=$MSSQL_SA_PASSWORD \
     MSSQL_PID=$MSSQL_PID \
     /opt/mssql/bin/mssql-conf -n setup accept-eula

echo Installing mssql-tools and unixODBC developer...
sudo ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev

# Add SQL Server tools to the path by default:
echo Adding SQL Server tools to your path...
echo PATH="$PATH:/opt/mssql-tools/bin" >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc

# Optional SQL Server Agent installation:
if [ ! -z $SQL_INSTALL_AGENT ]
then
  echo Installing SQL Server Agent...
  sudo apt-get install -y mssql-server-agent
fi

# Optional SQL Server Full Text Search installation:
if [ ! -z $SQL_INSTALL_FULLTEXT ]
then
    echo Installing SQL Server Full-Text Search...
    sudo apt-get install -y mssql-server-fts
fi

# Configure firewall to allow TCP port 1433:
echo Configuring UFW to allow traffic on port 1433...
sudo ufw allow 1433/tcp
sudo ufw reload

# Optional example of post-installation configuration.
# Trace flags 1204 and 1222 are for deadlock tracing.
# echo Setting trace flags...
# sudo /opt/mssql/bin/mssql-conf traceflag 1204 1222 on

# Restart SQL Server after installing:
echo Restarting SQL Server...
sudo systemctl restart mssql-server

# Connect to server and get the version:
counter=1
errstatus=1
while [ $counter -le 5 ] && [ $errstatus = 1 ]
do
  echo Waiting for SQL Server to start...
  sleep 3s
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "SELECT @@VERSION" 2>/dev/null
  errstatus=$?
  ((counter++))
done

# Display error if connection failed:
if [ $errstatus = 1 ]
then
  echo Cannot connect to SQL Server, installation aborted
  exit $errstatus
fi

# Optional new user creation:
if [ ! -z $SQL_INSTALL_USER ] && [ ! -z $SQL_INSTALL_USER_PASSWORD ]
then
  echo Creating user $SQL_INSTALL_USER
  /opt/mssql-tools/bin/sqlcmd \
    -S localhost \
    -U SA \
    -P $MSSQL_SA_PASSWORD \
    -Q "CREATE LOGIN [$SQL_INSTALL_USER] WITH PASSWORD=N'$SQL_INSTALL_USER_PASSWORD', DEFAULT_DATABASE=[master], CHECK_EXPIRATION=ON, CHECK_POLICY=ON; ALTER SERVER ROLE [sysadmin] ADD MEMBER [$SQL_INSTALL_USER]"
fi

echo Done!
```

### <a name="running-the-script"></a>執行指令碼

執行指令碼

1. 將範例貼到您慣用的文字編輯器中，並以易記的名稱 (例如 `install_sql.sh`) 儲存。

1. 自訂 `MSSQL_SA_PASSWORD`、`MSSQL_PID` 及您想要變更的其他變數。

1. 將指令碼標示為可執行檔

   ```bash
   chmod +x install_sql.sh
   ```

1. 執行指令碼

   ```bash
   ./install_sql.sh
   ```

### <a name="understanding-the-script"></a>了解指令碼
Bash 指令碼的第一個工作就是設定一些變數。 這些變數可以是指令碼變數 (如範例所示) 或環境變數。 SQL Server 安裝**需要**`MSSQL_SA_PASSWORD` 變數，其他變數是針對指令碼所建立的自訂變數。 範例指令碼會執行下列步驟：

1. 匯入公開 Microsoft GPG 金鑰。

1. 為 SQL Server 和命令列工具註冊 Microsoft 存放庫。

1. 更新本機存放庫

1. 安裝 SQL Server

1. 使用 ```MSSQL_SA_PASSWORD``` 設定 SQL Server，並自動接受使用者授權合約。

1. 自動接受 SQL Server 命令列工具的使用者授權合約、予以安裝，然後安裝 unixODBC-dev 套件。

1. 將 SQL Server 命令列工具新增至方便使用的路徑。

1. 如果已設定指令碼變數 ```SQL_INSTALL_AGENT``` (預設為開啟)，請安裝 SQL Server Agent。

1. 如果已設定變數 ```SQL_INSTALL_FULLTEXT```，請選擇性地安裝 SQL Server 全文檢索搜尋。

1. 解除系統防火牆上 TCP 通訊埠 1433 的封鎖，這是從另一個系統連線到 SQL Server 的必要動作。

1. 選擇性地設定用於死結追蹤的追蹤旗標。 (需要取消程式碼行的註解)

1. SQL Server 現已安裝，若要讓它運作，請重新啟動此程序。

1. 確認已正確安裝 SQL Server，同時隱藏所有錯誤訊息。

1. 如果 ```SQL_INSTALL_USER``` 和 ```SQL_INSTALL_USER_PASSWORD``` 都已設定，請建立新的伺服器管理員使用者。

## <a name="next-steps"></a>後續步驟

簡化多個自動安裝，並建立獨立的 Bash 指令碼，設定適當的環境變數。 您可以移除範例指令碼所使用的所有變數，並放在專屬的 Bash 指令碼中。

```bash
#!/bin/bash
export MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>'
export MSSQL_PID='evaluation'
export SQL_INSTALL_AGENT='y'
export SQL_INSTALL_USER='<Username>'
export SQL_INSTALL_USER_PASSWORD='<YourStrong!Passw0rd>'
export SQL_INSTALL_AGENT='y'
```

然後依照下列方式執行 Bash 指令碼：
```bash
. ./my_script_name.sh
```

如需 Linux 上的 SQL Server 詳細資訊，請參閱 [Linux 上的 SQL Server 概觀](sql-server-linux-overview.md)。
