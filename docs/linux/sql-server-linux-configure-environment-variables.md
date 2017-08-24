---
title: "使用環境變數設定 SQL Server 設定 |Microsoft 文件"
description: "本主題描述如何在 Linux 上設定特定的 SQL Server 2017 設定使用環境變數。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/21/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 4951f503a7b5c395f86cb6daf2ba705ca69fbd83
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>使用 Linux 上的環境變數設定 SQL Server 設定

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

若要在 Linux 上設定 SQL Server 2017 RC2，您可以使用數個不同的環境變數。 兩個案例中使用這些變數：

- 若要設定與初始設定`mssql-conf setup`命令。
- 若要設定新[在 Docker 中的 SQL Server 容器](quickstart-install-connect-docker.md)。

> [!TIP]
> 如果您需要設定 SQL Server 之後安裝案例，請參閱[設定 SQL Server on Linux mssql conf 工具](sql-server-linux-configure-mssql-conf.md)。

## <a name="environment-variables"></a>環境變數

| 環境變數 | Description |
|-----|-----|
| **ACCEPT_EULA** | SQL Server 授權合約時設定為任何值 (例如，' Y')。 |
| **MSSQL_SA_PASSWORD** | 設定 SA 的使用者密碼。 |
| **MSSQL_PID** | 設定 SQL Server 版本或產品金鑰。 可能的值包括： 評估、 Developer、 Express、 Web、 Standard、 Enterprise 或 # # #-# # #-# # #-# # #-# # #，此處的 '#' 是數字或字母的形式的產品金鑰。 |
| **MSSQL_LCID** | 設定要用於 SQL Server 的語言識別碼。 例如 1036年為法文。 |
| **MSSQL_COLLATION** | 設定 SQL Server 的預設定序。 這會覆寫定序的語言識別碼 (LCID) 的預設的對應。 |
| **MSSQL_MEMORY_LIMIT_MB** | 設定 SQL Server 可以使用的記憶體 （以 mb 為單位） 的最大數量。 根據預設，它是總實體記憶體的 80%。 |
| **MSSQL_TCP_PORT** | 設定 SQL Server 會接聽 （預設值 1433年） 的 TCP 連接埠。 |
| **MSSQL_IP_ADDRESS** | 設定 IP 位址。 目前的 IP 位址必須是 IPv4 樣式 (0.0.0.0)。 |
| **MSSQL_BACKUP_DIR** | 設定預設備份目錄位置。 |
| **MSSQL_DATA_DIR** | 會建立新的 SQL Server 資料庫資料檔案 (.mdf) 將目錄變更。 |
| **MSSQL_LOG_DIR** | 變更建立新的 SQL Server 資料庫記錄檔 (.ldf) 檔案所在的目錄。 |
| **MSSQL_DUMP_DIR** | 變更其中 SQL Server 將存款記憶體傾印和其他的疑難排解檔預設目錄。 |
| **MSSQL_ENABLE_HADR** | 啟用可用性群組。 |

## <a name="example-initial-setup"></a>範例： 初始設定

這個範例會執行`mssql-conf setup`設定環境變數。 下列環境變數會指定：

- **ACCEPT_EULA**接受使用者授權合約。
- **MSSSQL_PID**指定自由授權開發人員的 SQL Server 版供非生產環境使用。
- **MSSQL_SA_PASSWORD**設定強式密碼。
- **MSSQL_TCP_PORT**設定 SQL Server 接聽 1234年的 TCP 連接埠。

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="example-docker"></a>範例： Docker

此範例的 docker 命令會建立新的 SQL Server 2017 容器，使用下列環境變數：

- **ACCEPT_EULA**接受使用者授權合約。
- **MSSSQL_PID**指定自由授權開發人員的 SQL Server 版供非生產環境使用。
- **MSSQL_SA_PASSWORD**設定強式密碼。
- **MSSQL_TCP_PORT**設定 SQL Server 接聽 1234年的 TCP 連接埠。 這表示，而不是對應通訊埠 1433 （預設值） 的主機連接埠，自訂的 TCP 連接埠必須與對應`-p 1234:1234`命令在此範例中。

如果您在 Linux/macOS 上執行 Docker，請使用單引號中使用下列語法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 --cap-add SYS_PTRACE -p 1234:1234 -d microsoft/mssql-server-linux
```

如果您在 Windows 上執行 Docker，請用雙引號使用下列語法：

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 --cap-add SYS_PTRACE -p 1234:1234 -d microsoft/mssql-server-linux
```

## <a name="next-steps"></a>後續的步驟

如需此處未列出其他 SQL Server 設定，請參閱[設定 SQL Server on Linux mssql conf 工具](sql-server-linux-configure-mssql-conf.md)。

如需有關如何安裝及執行 SQL Server on Linux 的詳細資訊，請參閱[安裝 SQL Server on Linux](sql-server-linux-setup.md)。

