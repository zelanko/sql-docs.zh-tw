---
title: 開始使用 Docker （Linux 上執行 SQL Server） 上的 SQL Server 容器
titleSuffix: SQL Server
description: 本快速入門示範如何使用 Docker 來執行 SQL Server 2017 和 2019年容器映像。 您隨後便可使用 sqlcmd 來建立及查詢資料庫。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/10/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.custom: sql-linux, seodec18
ms.prod_service: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: f4e6298cb1165f75dcd9a6aa6c77a1628650c0f6
ms.sourcegitcommit: 1f53b6a536ccffd701fc87e658ddac714f6da7a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/10/2019
ms.locfileid: "54206314"
---
# <a name="quickstart-run-sql-server-container-images-with-docker"></a>快速入門：以 Docker 執行 SQL Server 容器映像

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本快速入門中，您將使用 Docker 來提取與執行 SQL Server 2017 容器映像，[mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/)。 然後與 **sqlcmd**連線來建立您的第一個資料庫並執行查詢。

> [!TIP]
> 如果您想要試用 SQL Server 2019 預覽影像，請參閱[這篇文章的 SQL Server 2019 預覽版](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本快速入門中，您必須使用 Docker 來提取及執行 SQL Server 2019 預覽容器映像[mssql server](https://hub.docker.com/r/microsoft/mssql-server)。 然後與 **sqlcmd**連線來建立您的第一個資料庫並執行查詢。

::: moniker-end

此映像包含以 Ubuntu 16.04 為基礎，在 Linux 上執行的 SQL Server。 您可於適用於 Mac/Windows 的 Docker 上將其與 Docker 引擎 1.8 以上版本搭配使用。 本快速入門中特別著重在使用上的 SQL Server **linux**映像。 Windows 映像則不涵蓋在內，但您可於 [mssql-server-windows-developer Docker Hub 頁面](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)進一步加以了解。

## <a id="requirements"></a> 必要條件

- 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。
- Docker **overlay2**存放裝置驅動程式。 這是大部分使用者的預設值。 如果您發現您不使用此儲存體提供者，並且需要變更，請參閱指示和中的警告[docker 文件，以設定 overlay2](https://docs.docker.com/storage/storagedriver/overlayfs-driver/#configure-docker-with-the-overlay-or-overlay2-storage-driver)。
- 至少 2 GB 的磁碟空間。
- 至少 2 GB 的 RAM。
- [Linux 上的 SQL Server 系統需求](sql-server-linux-setup.md#system)。

<!--The following H2 is versioned for 2017 and 2019. Much of the content is duplicated, so
any changes to one section should be duplicated in the other-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="pullandrun2017"></a> 提取及執行容器映像

1. 從 Microsoft Container Registry 提取 SQL Server 2017 Linux 容器映像。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > 如果您想要試用 SQL Server 2019 預覽影像，請參閱[這篇文章的 SQL Server 2019 預覽版](quickstart-install-connect-docker.md?view=sql-server-linux-ver15#pullandrun2019)。

   上述命令會提取最新的 SQL Server 2017 容器映像。 若要提取特定映像，您需要新增欄位與標籤名稱 (例如，`mcr.microsoft.com/mssql/server:2017-GA-ubuntu`)。 若要查看所有可用映像，請參閱[mssql server Docker hub 頁面](https://hub.docker.com/r/microsoft/mssql-server)。

   在本文中的 bash 命令`sudo`用。 在 MacOS 上，`sudo`可能不需要。 在 Linux 上，如果您不想要使用`sudo`若要執行 Docker，您可以設定**docker**群組，並將使用者新增至該群組。 如需詳細資訊，請參閱 <<c0> [ 後續安裝步驟適用於 Linux](https://docs.docker.com/install/linux/linux-postinstall/)。

2. 若要以 Docker 執行容器映像，您可以從 Bash 殼層 (Linux/macOS) 或提高權限的 PowerShell 命令提示字元使用下列命令。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!NOTE]
   > 密碼應遵循 SQL Server 預設密碼原則，否則容器將無法設定 SQL Server 並停止運作。 根據預設，密碼必須至少為 8 個字元，且包含下列四組的三種字元：大寫字母、 小寫字母、 10 進位數字和符號。 執行 [docker logs](https://docs.docker.com/engine/reference/commandline/logs/) 命令即可查看錯誤記錄。

   > [!NOTE]
   > 根據預設，這會建立 SQL Server 2017 Developer 版本的映像。 在容器中執行生產版本的程序將有些微差異。 如需詳細資訊，請參閱[執行生產容器映像](sql-server-linux-configure-docker.md#production)。

   下表提供了前述 `docker run` 範例的參數描述：

   | 參數 | 描述 |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  將 **ACCEPT_EULA** 變數設為任意值可確認您接受[終端使用者授權合約](https://go.microsoft.com/fwlink/?LinkId=746388)。 此為 SQL Server 映像的必要設定。 |
   | **-e ' SA_PASSWORD =\<YourStrong ！Passw0rd\>'** | 指定您自己的強式密碼，該密碼長度至少需為 8 個字元且符合 [SQL Server 密碼需求](../relational-databases/security/password-policy.md)。 此為 SQL Server 映像的必要設定。 |
   | **-p 1433:1433** | 將主機環境上的 TCP 通訊埠 (第一個值) 對應至容器中的 TCP 連接埠 (第二個值)。 在此範例中，SQL Server 正在容器中的 TCP 1433 上接聽，這公開給連接埠 1433，在主機上。 |
   | **--name sql1** | 指定容器名稱，而不隨機產生名稱。 執行多個容器時無法重複使用此相同名稱。 |
   | **mcr.microsoft.com/mssql/server:2017-latest** | SQL Server 2017 Linux 容器映像。 |

3. 若要檢視 Docker 容器，請使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   您應該會看到類似下列螢幕擷取畫面的結果：

   ![Docker ps 命令輸出](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. 如果**狀態**資料行會顯示狀態為**向上**、 然後 SQL Server 正在執行中容器和接聽的通訊埠中指定**連接埠**資料行。 如果**狀態**資料行的 SQL Server 容器節目**Exited**，請參閱[疑難排解 > 一節的設定指南](sql-server-linux-configure-docker.md#troubleshooting)。

`-h` (主機名稱) 參數也相當實用，但為求簡明因此未在本教學課程中使用。 此參數可將容器的內部名稱變更為自訂值。 這是您在下列 Transact-SQL 查詢中會看到的傳回名稱：

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

建議您將 `-h` 與 `--name` 設為相同的值，這會讓識別目標容器更輕鬆。

::: moniker-end
<!--End of 2017 "Pull and run" section-->

<!--This is the 2019 version of the "Pull and run" section-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="pullandrun2019"></a> 提取及執行容器映像

1. 從 Docker Hub 提取 SQL Server 2019 預覽 Linux 容器映像。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
   ```

   > [!TIP]
   > 本快速入門使用 SQL Server 2019 預覽 Docker 映像。 如果您想要執行 SQL Server 2017 映像，請參閱[這篇文章的 SQL Server 2017 版本](quickstart-install-connect-docker.md?view=sql-server-linux-2017#pullandrun2017)。

   前一個命令會提取最新 SQL Server 2019 預覽容器映像 Ubuntu 為基礎。 若要改為使用 RedHat 為基礎的容器映像，請參閱[執行 RHEL 為基礎的容器映像](sql-server-linux-configure-docker.md#rhel)。 若要提取特定映像，您需要新增欄位與標籤名稱 (例如，`mcr.microsoft.com/mssql/server:2017-GA`)。 若要查看所有可用的映像，請參閱 [mssql-server-linux Docker Hub 頁面](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)。

   在本文中的 bash 命令`sudo`用。 在 MacOS 上，`sudo`可能不需要。 在 Linux 上，如果您不想要使用`sudo`若要執行 Docker，您可以設定**docker**群組，並將使用者新增至該群組。 如需詳細資訊，請參閱 <<c0> [ 後續安裝步驟適用於 Linux](https://docs.docker.com/install/linux/linux-postinstall/)。

2. 若要以 Docker 執行容器映像，您可以從 Bash 殼層 (Linux/macOS) 或提高權限的 PowerShell 命令提示字元使用下列命令。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1433:1433 --name sql1 \
      -d mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1433:1433 --name sql1 `
      -d mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu
   ```

   > [!NOTE]
   > 密碼應遵循 SQL Server 預設密碼原則，否則容器將無法設定 SQL Server 並停止運作。 根據預設，密碼必須至少為 8 個字元，且包含下列四組的三種字元：大寫字母、 小寫字母、 10 進位數字和符號。 執行 [docker logs](https://docs.docker.com/engine/reference/commandline/logs/) 命令即可查看錯誤記錄。

   > [!NOTE]
   > 根據預設，這會建立容器與 Developer 版本的 SQL Server 2019 預覽。

   下表提供了前述 `docker run` 範例的參數描述：

   | 參數 | 描述 |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  將 **ACCEPT_EULA** 變數設為任意值可確認您接受[終端使用者授權合約](https://go.microsoft.com/fwlink/?LinkId=746388)。 此為 SQL Server 映像的必要設定。 |
   | **-e ' SA_PASSWORD =\<YourStrong ！Passw0rd\>'** | 指定您自己的強式密碼，該密碼長度至少需為 8 個字元且符合 [SQL Server 密碼需求](../relational-databases/security/password-policy.md)。 此為 SQL Server 映像的必要設定。 |
   | **-p 1433:1433** | 將主機環境上的 TCP 通訊埠 (第一個值) 對應至容器中的 TCP 連接埠 (第二個值)。 在此範例中，SQL Server 正在容器中的 TCP 1433 上接聽，這公開給連接埠 1433，在主機上。 |
   | **--name sql1** | 指定容器名稱，而不隨機產生名稱。 執行多個容器時無法重複使用此相同名稱。 |
   | **mcr.microsoft.com/mssql/server:2019-CTP2.2-ubuntu** | SQL Server 2019 CTP 2.2 Linux 容器映像。 |

3. 若要檢視 Docker 容器，請使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   您應該會看到類似下列螢幕擷取畫面的結果：

   ![Docker ps 命令輸出](./media/sql-server-linux-setup-docker/docker-ps-command.png)

4. 如果**狀態**資料行會顯示狀態為**向上**、 然後 SQL Server 正在執行中容器和接聽的通訊埠中指定**連接埠**資料行。 如果**狀態**資料行的 SQL Server 容器節目**Exited**，請參閱[疑難排解 > 一節的設定指南](sql-server-linux-configure-docker.md#troubleshooting)。

`-h` (主機名稱) 參數也相當實用，但為求簡明因此未在本教學課程中使用。 此參數可將容器的內部名稱變更為自訂值。 這是您在下列 Transact-SQL 查詢中會看到的傳回名稱：

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

建議您將 `-h` 與 `--name` 設為相同的值，這會讓識別目標容器更輕鬆。

::: moniker-end
<!--End of 2019 "Pull and run" section-->

## <a id="sapassword"></a> 變更 SA 密碼

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>連接至 SQL Server

下列步驟會在容器中使用 SQL Server 命令列工具 **sqlcmd** 以連線至 SQL Server。

1. 使用 `docker exec -it` 命令在您執行的容器中啟動互動式 Bash 殼層。 下列範例中的 `sql1` 是您在建立容器時由 `--name` 參數指定的名稱。

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. 進入容器後，以 sqlcmd 進行本機連線。 預設路徑並不包含 sqlcmd，因此您必須指定完整路徑。

   ```bash
   /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   > [!TIP]
   > 您可以在命令列中省略密碼，不要在提示時輸入密碼。

1. 如果成功，您應該會收到 **sqlcmd** 命令提示字元：`1>`。

## <a name="create-and-query-data"></a>建立及查詢資料

下列各節將逐步引導您使用 **sqlcmd** 和 Transact-SQL，來建立新的資料庫、新增資料及執行簡單的查詢。

### <a name="create-a-new-database"></a>建立新的資料庫

下列步驟會建立名為 `TestDB` 的新資料庫。

1. 從 **sqlcmd** 命令提示字元，貼上下列 Transact-SQL 命令以建立測試資料庫：

   ```sql
   CREATE DATABASE TestDB
   ```

1. 在下一行，撰寫查詢以傳回您伺服器上所有資料庫的名稱：

   ```sql
   SELECT Name from sys.Databases
   ```

1. 上述兩個命令不會立即執行。 您必須在新的一行鍵入 `GO`，以執行上述命令：

   ```sql
   GO
   ```

### <a name="insert-data"></a>插入資料

接下來，建立新的資料表 `Inventory`，然後插入兩個新的資料列。

1. 從 **sqlcmd** 命令提示字元，將內容切換至 `TestDB` 資料庫：

   ```sql
   USE TestDB
   ```

1. 建立名為 `Inventory` 的新資料表：

   ```sql
   CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
   ```

1. 將資料插入新的資料表：

   ```sql
   INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
   ```

1. 鍵入 `GO` 以執行上述命令：

   ```sql
   GO
   ```

### <a name="select-data"></a>選取資料

現在，執行查詢以從 `Inventory` 資料表傳回資料。

1. 從 **sqlcmd** 命令提示字元，輸入查詢以從 `Inventory` 資料表傳回 quantity (數量) 大於 152 的資料列：

   ```sql
   SELECT * FROM Inventory WHERE quantity > 152;
   ```

1. 執行命令：

   ```sql
   GO
   ```

### <a name="exit-the-sqlcmd-command-prompt"></a>結束 sqlcmd 命令提示字元

1. 若要結束您的 **sqlcmd** 工作階段，請鍵入 `QUIT`：

   ```sql
   QUIT
   ```

1. 若要結束容器中的互動式命令提示字元，請鍵入 `exit`。 結束互動式 Bash 殼層後，容器會繼續執行。

## <a id="connectexternal"></a> 從容器外部連線

您也可以從支援 SQL 連線的任何外部 Linux、Windows 或 macOS 工具連線到 Docker 機器上的 SQL Server 執行個體。

下列步驟在您容器的外部使用了 **sqlcmd** 以連線至容器中執行的 SQL Server。 這些步驟會假設您已經在容器外部安裝 SQL Server 命令列工具。 使用其他工具時，適用相同的原則，但各工具連接的程序。

1. 找出裝載您容器之電腦的 IP 位址。 在 Linux 上，使用**ifconfig** 或 **ip addr**。在 Windows 上，使用 **ipconfig**。

1. 執行 sqlcmd 來指定 IP 位址和容器中 1433 通訊埠所對應的連接埠。 在此範例中，這是相同的連接埠 1433，主機電腦上。 如果您在主機電腦上指定不同的對應連接埠，您會在此使用。

   ```bash
   sqlcmd -S 10.3.2.4,1433 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1433 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. 執行 Transact-SQL 命令。 完成後，鍵入 `QUIT`。

其他常用的 SQL Server 連線工具包括：

- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows 上的 SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [Azure Data Studio （預覽）](../azure-data-studio/what-is.md)
- [mssql-cli (預覽)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

## <a name="remove-your-container"></a>移除容器

若要移除本教學課程中用到的 SQL Server 容器，請執行下列命令：

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> 停止及移除容器會永久刪除容器中的所有 SQL Server 資料。 如果您要保留您的資料，請[建立備份檔案並複製至容器之外](tutorial-restore-backup-in-sql-server-container.md)，或使用[容器資料持續性技術](sql-server-linux-configure-docker.md#persist)。

## <a name="docker-demo"></a>Dock 示範

在您嘗試使用適用於 Docker 的 SQL Server 容器映像後，或許會想要了解如何使用 Docker 來改善開發與測試。 下方影片會示範如何在持續整合與部署案例中使用 Docker。

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>後續步驟

如需如何將資料庫備份檔案還原至容器中的教學課程，請參閱[在 Linux Docker 容器中還原 SQL Server 資料庫](tutorial-restore-backup-in-sql-server-container.md)。 若要探索其他案例，例如執行多個容器，資料持續性和疑難排解，請參閱[Docker 上的設定 SQL Server 容器映像](sql-server-linux-configure-docker.md)。

此外，也可以前往 [mssql-docker GitHub 存放庫](https://github.com/Microsoft/mssql-docker) 取得資源、意見反應和已知問題。
