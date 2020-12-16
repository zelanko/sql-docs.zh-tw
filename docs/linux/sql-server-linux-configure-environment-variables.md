---
title: 在 Linux 上設定 SQL Server 的環境變數
description: 此文章說明如何使用環境變數在 Linux 上設定特定的 SQL Server 2017 設定。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 737004c651ff7cb335557cbbfe61e9df516e2f48
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471619"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>使用環境變數在 Linux 上設定 SQL Server 設定

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

您可以使用數個不同的環境變數來設定 Linux 上的 SQL Server 2017。 在下列兩種案例中會使用這些變數：

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

您可以使用數個不同的環境變數來設定 Linux 上的 SQL Server 2019。 在下列兩種案例中會使用這些變數：

::: moniker-end

- 使用 `mssql-conf setup` 命令來設定初始設定。
- [在 Docker 中設定新的 SQL Server 容器](quickstart-install-connect-docker.md)。

> [!TIP]
> 如果您需要在這些設定案例之後設定 SQL Server，請參閱[使用 mssql-conf 工具在 Linux 上設定 SQL Server](sql-server-linux-configure-mssql-conf.md)。

## <a name="environment-variables"></a>環境變數

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| 環境變數 | 描述 |
|-----|-----|
| **ACCEPT_EULA** | 將 **ACCEPT_EULA** 變數設為任意值可確認您接受 [終端使用者授權合約](https://go.microsoft.com/fwlink/?LinkId=746388)。 此為 SQL Server 映像的必要設定。 |
| **MSSQL_SA_PASSWORD** | 設定 SA 使用者密碼。 |
| **MSSQL_PID** | 設定 SQL Server 版本或產品金鑰。 可能的值包括： </br></br>**評估**</br>**開發人員**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**產品金鑰**</br></br>如果指定產品金鑰，則其格式必須為 #####-#####-#####-#####-#####，其中 '#' 是數字或字母。|
| **MSSQL_LCID** | 為 SQL Server 設定要使用的語言識別碼。 例如 1036 是法文。 |
| **MSSQL_COLLATION** | 設定 SQL Server 的預設定序。 這會覆寫語言識別碼 (LCID) 與定序的預設對應。 |
| **MSSQL_MEMORY_LIMIT_MB** | 設定 SQL Server 可使用的記憶體數量上限 (MB)。 預設為實體記憶體總計的 80%。 |
| **MSSQL_TCP_PORT** | SQL Server 進行接聽的 TCP 連接埠 (預設值為 1433)。 |
| **MSSQL_IP_ADDRESS** | 設定 IP 位址。 目前 IP 位址必須是 IPv4 樣式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 設定預設備份目錄位置。 |
| **MSSQL_DATA_DIR** | 變更新 SQL Server 資料庫資料檔 (.mdf) 的建立目錄。 |
| **MSSQL_LOG_DIR** | 變更新 SQL Server 資料庫記錄檔 (.ldf) 的建立目錄。 |
| **MSSQL_DUMP_DIR** | 變更 SQL Server 預設將存放記憶體傾印及其他疑難排解檔案的目錄。 |
| **MSSQL_ENABLE_HADR** | 啟用可用性群組。 例如 '1' 為啟用，'0' 為停用 |
| **MSSQL_AGENT_ENABLED** | 啟用 SQL Server Agent。 例如 'true' 為啟用，'false' 為停用。 代理程式預設為停用。  |
| **MSSQL_MASTER_DATA_FILE** | 設定 master 資料庫資料檔的位置。 在第一次執行 SQL Server 之前，必須命名為 **master.mdf**。 |
| **MSSQL_MASTER_LOG_FILE** | 設定 master 資料庫記錄檔的位置。 在第一次執行 SQL Server 之前，必須命名為  。 |
| **MSSQL_ERROR_LOG_FILE** | 設定錯誤記錄檔的位置。 |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

| 環境變數 | 描述 |
|-----|-----|
| **ACCEPT_EULA** | 將 **ACCEPT_EULA** 變數設為任意值可確認您接受 [終端使用者授權合約](https://go.microsoft.com/fwlink/?LinkId=746388)。 此為 SQL Server 映像的必要設定。 |
| **MSSQL_SA_PASSWORD** | 設定 SA 使用者密碼。 |
| **MSSQL_PID** | 設定 SQL Server 版本或產品金鑰。 可能的值包括： </br></br>**評估**</br>**開發人員**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**產品金鑰**</br></br>如果指定產品金鑰，則其格式必須為 #####-#####-#####-#####-#####，其中 '#' 是數字或字母。|
| **MSSQL_LCID** | 為 SQL Server 設定要使用的語言識別碼。 例如 1036 是法文。 |
| **MSSQL_COLLATION** | 設定 SQL Server 的預設定序。 這會覆寫語言識別碼 (LCID) 與定序的預設對應。 |
| **MSSQL_MEMORY_LIMIT_MB** | 設定 SQL Server 可使用的記憶體數量上限 (MB)。 預設為實體記憶體總計的 80%。 |
| **MSSQL_TCP_PORT** | SQL Server 進行接聽的 TCP 連接埠 (預設值為 1433)。 |
| **MSSQL_IP_ADDRESS** | 設定 IP 位址。 目前 IP 位址必須是 IPv4 樣式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 設定預設備份目錄位置。 |
| **MSSQL_DATA_DIR** | 變更新 SQL Server 資料庫資料檔 (.mdf) 的建立目錄。 |
| **MSSQL_LOG_DIR** | 變更新 SQL Server 資料庫記錄檔 (.ldf) 的建立目錄。 |
| **MSSQL_DUMP_DIR** | 變更 SQL Server 預設將存放記憶體傾印及其他疑難排解檔案的目錄。 |
| **MSSQL_ENABLE_HADR** | 啟用可用性群組。 例如 '1' 為啟用，'0' 為停用 |
| **MSSQL_AGENT_ENABLED** | 啟用 SQL Server Agent。 例如 'true' 為啟用，'false' 為停用。 代理程式預設為停用。  |
| **MSSQL_MASTER_DATA_FILE** | 設定 master 資料庫資料檔的位置。 在第一次執行 SQL Server 之前，必須命名為 **master.mdf**。 |
| **MSSQL_MASTER_LOG_FILE** | 設定 master 資料庫記錄檔的位置。 在第一次執行 SQL Server 之前，必須命名為  。 |
| **MSSQL_ERROR_LOG_FILE** | 設定錯誤記錄檔的位置。 |

::: moniker-end

## <a name="use-with-initial-setup"></a>與初始設定搭配使用

此範例會使用已設定的環境變數來執行 `mssql-conf setup`。 以下是已指定的環境變數：

- **ACCEPT_EULA** 會接受使用者授權合約。
- **MSSQL_PID** 會指定自由授權的 SQL Server Developer Edition 供非生產環境使用。
- **MSSQL_SA_PASSWORD** 會設定強式密碼。
- **MSSQL_TCP_PORT** 會將 SQL Server 進行接聽的 TCP 連接埠設定成 1234。

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>與 Docker 搭配使用

此範例 Docker 命令會使用下列環境變數來建立新的 SQL Server 容器：

- **ACCEPT_EULA** 會接受使用者授權合約。
- **MSSQL_PID** 會指定自由授權的 SQL Server Developer Edition 供非生產環境使用。
- **MSSQL_SA_PASSWORD** 會設定強式密碼。
- **MSSQL_TCP_PORT** 會將 SQL Server 進行接聽的 TCP 連接埠設定成 1234。 這意謂著在此範例中，必須使用 `-p 1234:1234` 命令來對應自訂 TCP 連接埠，而不是將連接埠 1433 (預設值) 對應至主機連接埠。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

如果您是在 Linux/macOS 上執行 Docker，請搭配單引號使用下列語法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

如果您是在 Windows 上執行 Docker，請搭配雙引號使用下列語法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> 在容器中執行生產版本的程序將有些微差異。 如需詳細資訊，請參閱[執行生產容器映像](./sql-server-linux-docker-container-deployment.md#production)。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

如果您是在 Linux/macOS 上執行 Docker，請搭配單引號使用下列語法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

如果您是在 Windows 上執行 Docker，請搭配雙引號使用下列語法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

## <a name="next-steps"></a>後續步驟

如需這裡未列出的其他 SQL Server 設定，請參閱[使用 mssql-conf 工具在 Linux 上設定 SQL Server](sql-server-linux-configure-mssql-conf.md)。

如需有關如何在 Linux 上安裝及執行 SQL Server 的詳細資訊，請參閱 [在 Linux 上安裝 SQL Server](sql-server-linux-setup.md)。