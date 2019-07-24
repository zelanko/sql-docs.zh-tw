---
title: 使用環境變數設定 SQL Server 設定
description: 本文說明如何在 Linux 上使用環境變數來設定特定的 SQL Server 2017 設定。
author: VanMSFT
ms.author: vanto
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 51589a2183043c5c8ea8d1f9bf5d4af6fcc1eea3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419245"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>在 Linux 上使用環境變數設定 SQL Server 設定

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

您可以使用數個不同的環境變數, 在 Linux 上設定 SQL Server 2017。 在兩種情況下會使用這些變數:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

您可以使用數個不同的環境變數, 在 Linux 上設定 SQL Server 2019 preview。 在兩種情況下會使用這些變數:

::: moniker-end

- 使用`mssql-conf setup`命令設定初始設定。
- [在 Docker 中](quickstart-install-connect-docker.md)設定新的 SQL Server 容器。

> [!TIP]
> 如果您需要在這些設定案例之後設定 SQL Server, 請參閱[使用 mssql 會議工具設定 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md)。

## <a name="environment-variables"></a>環境變數

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 環境變數 | 描述 |
|-----|-----|
| **ACCEPT_EULA** | 將 **ACCEPT_EULA** 變數設為任意值可確認您接受[終端使用者授權合約](https://go.microsoft.com/fwlink/?LinkId=746388)。 此為 SQL Server 映像的必要設定。 |
| **MSSQL_SA_PASSWORD** | 設定 SA 使用者密碼。 |
| **MSSQL_PID** | 設定 [SQL Server 版] 或 [產品金鑰]。 可能的值包括： </br></br>**Evaluation**</br>**開發人員**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**產品金鑰**</br></br>如果指定產品金鑰, 則其格式必須是 # # # # #-# # # # #-# # # # #-# # # # #-# # # # #, 其中 ' # ' 是數位或字母。|
| **MSSQL_LCID** | 設定要用於 SQL Server 的語言識別項。 例如, 1036 是法文。 |
| **MSSQL_COLLATION** | 設定 SQL Server 的預設定序。 這會覆寫語言識別項 (LCID) 與定序的預設對應。 |
| **MSSQL_MEMORY_LIMIT_MB** | 設定 SQL Server 可以使用的最大記憶體數量 (以 MB 為單位)。 根據預設, 它是總實體記憶體的 80%。 |
| **MSSQL_TCP_PORT** | 設定 SQL Server 接聽的 TCP 埠 (預設值 1433)。 |
| **MSSQL_IP_ADDRESS** | 設定 IP 位址。 目前, IP 位址必須是 IPv4 樣式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 設定預設的備份目錄位置。 |
| **MSSQL_DATA_DIR** | 變更建立新 SQL Server 資料庫資料檔案 (.mdf) 的目錄。 |
| **MSSQL_LOG_DIR** | 變更建立新 SQL Server 資料庫記錄檔 (.ldf) 的目錄。 |
| **MSSQL_DUMP_DIR** | 根據預設, 變更 SQL Server 將用來存放記憶體傾印和其他疑難排解檔案的目錄。 |
| **MSSQL_ENABLE_HADR** | 啟用可用性群組。 例如, ' 1 ' 已啟用, 且已停用 ' 0 ' |
| **MSSQL_AGENT_ENABLED** | 啟用 SQL Server Agent。 例如, ' true ' 已啟用, 且已停用 ' false '。 預設會停用 agent。  |
| **MSSQL_MASTER_DATA_FILE** | 設定 master 資料庫資料檔案的位置。 必須命名為**master .mdf** , 直到第一次執行 SQL Server 為止。 |
| **MSSQL_MASTER_LOG_FILE** | 設定 master 資料庫記錄檔的位置。 必須命名為**mastlog** , 直到第一次執行 SQL Server 為止。 |
| **MSSQL_ERROR_LOG_FILE** | 設定錯誤記錄檔的位置。 |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| 環境變數 | 描述 |
|-----|-----|
| **ACCEPT_EULA** | 將 **ACCEPT_EULA** 變數設為任意值可確認您接受[終端使用者授權合約](https://go.microsoft.com/fwlink/?LinkId=746388)。 此為 SQL Server 映像的必要設定。 |
| **MSSQL_SA_PASSWORD** | 設定 SA 使用者密碼。 |
| **MSSQL_PID** | 設定 [SQL Server 版] 或 [產品金鑰]。 可能的值包括： </br></br>**Evaluation**</br>**開發人員**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**產品金鑰**</br></br>如果指定產品金鑰, 則其格式必須是 # # # # #-# # # # #-# # # # #-# # # # #-# # # # #, 其中 ' # ' 是數位或字母。|
| **MSSQL_LCID** | 設定要用於 SQL Server 的語言識別項。 例如, 1036 是法文。 |
| **MSSQL_COLLATION** | 設定 SQL Server 的預設定序。 這會覆寫語言識別項 (LCID) 與定序的預設對應。 |
| **MSSQL_MEMORY_LIMIT_MB** | 設定 SQL Server 可以使用的最大記憶體數量 (以 MB 為單位)。 根據預設, 它是總實體記憶體的 80%。 |
| **MSSQL_TCP_PORT** | 設定 SQL Server 接聽的 TCP 埠 (預設值 1433)。 |
| **MSSQL_IP_ADDRESS** | 設定 IP 位址。 目前, IP 位址必須是 IPv4 樣式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 設定預設的備份目錄位置。 |
| **MSSQL_DATA_DIR** | 變更建立新 SQL Server 資料庫資料檔案 (.mdf) 的目錄。 |
| **MSSQL_LOG_DIR** | 變更建立新 SQL Server 資料庫記錄檔 (.ldf) 的目錄。 |
| **MSSQL_DUMP_DIR** | 根據預設, 變更 SQL Server 將用來存放記憶體傾印和其他疑難排解檔案的目錄。 |
| **MSSQL_ENABLE_HADR** | 啟用可用性群組。 例如, ' 1 ' 已啟用, 且已停用 ' 0 ' |
| **MSSQL_AGENT_ENABLED** | 啟用 SQL Server Agent。 例如, ' true ' 已啟用, 且已停用 ' false '。 預設會停用 agent。  |
| **MSSQL_MASTER_DATA_FILE** | 設定 master 資料庫資料檔案的位置。 必須命名為**master .mdf** , 直到第一次執行 SQL Server 為止。 |
| **MSSQL_MASTER_LOG_FILE** | 設定 master 資料庫記錄檔的位置。 必須命名為**mastlog** , 直到第一次執行 SQL Server 為止。 |
| **MSSQL_ERROR_LOG_FILE** | 設定錯誤記錄檔的位置。 |

::: moniker-end

## <a name="use-with-initial-setup"></a>搭配初始設定使用

這個範例會`mssql-conf setup`使用已設定的環境變數來執行。 已指定下列環境變數:

- **ACCEPT_EULA**接受使用者授權合約。
- **MSSSQL_PID**會指定免費授權的開發人員版本 SQL Server 以進行非生產環境的使用。
- **MSSQL_SA_PASSWORD**會設定強式密碼。
- **MSSQL_TCP_PORT**會設定 SQL Server 接聽1234的 TCP 通訊埠。

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>搭配 Docker 使用

此範例 docker 命令會使用下列環境變數來建立新的 SQL Server 容器:

- **ACCEPT_EULA**接受使用者授權合約。
- **MSSSQL_PID**會指定免費授權的開發人員版本 SQL Server 以進行非生產環境的使用。
- **MSSQL_SA_PASSWORD**會設定強式密碼。
- **MSSQL_TCP_PORT**會設定 SQL Server 接聽1234的 TCP 通訊埠。 這表示不會將埠 1433 (預設值) 對應到主機埠, 而是必須使用此範例中的`-p 1234:1234`命令來對應自訂 TCP 通訊埠。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

如果您是在 Linux/macOS 上執行 Docker, 請使用下列語法加上單引號:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

如果您是在 Windows 上執行 Docker, 請使用下列語法加上雙引號:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> 在容器中執行生產版本的程序將有些微差異。 如需詳細資訊，請參閱[執行生產容器映像](sql-server-linux-configure-docker.md#production)。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

如果您是在 Linux/macOS 上執行 Docker, 請使用下列語法加上單引號:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

如果您是在 Windows 上執行 Docker, 請使用下列語法加上雙引號:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>後續步驟

如需此處未列出的其他 SQL Server 設定, 請參閱[使用 mssql 會議工具設定 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md)。

如需有關如何安裝和執行 Linux 上的 SQL Server 的詳細資訊, 請參閱[安裝 Linux 上的 SQL Server](sql-server-linux-setup.md)。
