---
title: "開始使用 docker 的 SQL Server 2017 |Microsoft 文件"
description: "本快速入門示範如何使用 Docker 執行 SQL Server 2017 容器映像。 接著，您會建立並查詢資料庫，以使用 sqlcmd。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/31/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
ms.workload: Active
ms.openlocfilehash: 1f018dd2b60365d89e912e7ef38499f8a4d14d9b
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="run-the-sql-server-2017-container-image-with-docker"></a>執行 SQL Server 2017 容器映像使用 Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本快速入門中，您必須使用 Docker 來提取及執行 SQL Server 2017 容器映像， [mssql-伺服器-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/)。 然後以連接**sqlcmd**來建立您的第一個資料庫和執行查詢。

此映像包含根據 Ubuntu 16.04 Linux 上執行的 SQL Server。 它可以用 Docker 引擎 1.8 + Docker 或 Linux 上的 Mac/windows。

> [!NOTE]
> 本快速入門特別著重於使用 mssql-server-**linux**映像。 未涵蓋的 Windows 映像，但您可以深入了解上[mssql server-windows developer Docker Hub 頁面](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)。

## <a id="requirements"></a> 必要條件

- Docker 引擎 1.8 + 任何支援 Mac/Windows Linux 發佈或 Docker。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。
- 最小值為 2 GB 的磁碟空間
- 最小值為 2 GB 的 RAM
- [SQL Server on Linux 的系統需求](sql-server-linux-setup.md#system)。

## <a name="pull-and-run-the-container-image"></a>提取和執行容器映像

1. 從 Docker Hub 提取 SQL Server 2017 Linux 容器映像。

   ```bash
   sudo docker pull microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker pull microsoft/mssql-server-linux:2017-latest
   ```

   前一個命令中提取最新的 SQL Server 2017 容器映像。 如果您想要提取的特定映像，您加上冒號和標記名稱 (例如， `microsoft/mssql-server-linux:2017-GA`)。 若要查看所有可用的映像，請參閱[mssql-伺服器-linux Docker 中樞頁面](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/)。

1. 若要執行 Docker 容器映像，您可以使用下列命令從 bash 殼層 (Linux/macOS) 或提高權限的 PowerShell 命令提示字元。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -p 1401:1433 --name sql1 \
      -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -p 1401:1433 --name sql1 `
      -d microsoft/mssql-server-linux:2017-latest
   ```

   > [!NOTE]
   > 密碼應該遵循 SQL Server 的預設密碼原則，否則容器不可以設定 SQL server 將會停止運作。 根據預設，密碼必須至少為 8 個字元，並包含下列四個集合的其中三種字元： 大寫字母、 小寫字母、 基本 10 個數字和符號。 您可以檢查錯誤記錄檔，藉由執行[docker 記錄](https://docs.docker.com/engine/reference/commandline/logs/)命令。

   > [!NOTE]
   > 根據預設，這會與 Developer 版本的 SQL Server 2017 建立容器。 執行容器中的實際執行版本的程序有些許不同。 如需詳細資訊，請參閱[容器映像執行生產](sql-server-linux-configure-docker.md#production)。

   下表提供在舊版的參數說明`docker run`範例：

   | 매개 변수 | Description |
   |-----|-----|
   | **-e 'ACCEPT_EULA=Y'** |  設定**ACCEPT_EULA**變數設為任何值，以確認您接受[使用者授權合約](http://go.microsoft.com/fwlink/?LinkId=746388)。 需要設定 SQL Server 映像。 |
   | **-e 'MSSQL_SA_PASSWORD=\<YourStrong!Passw0rd\>'** | 指定您自己的強式密碼至少為 8 個字元，並符合[SQL Server 密碼需求](../relational-databases/security/password-policy.md)。 需要設定 SQL Server 映像。 |
   | **-p 1401:1433** | 將主機環境上的 TCP 通訊埠對應 （第一個值） 與容器中的 TCP 連接埠 （第二個值）。 在此範例中，SQL Server 接聽 TCP 1433 容器中，這連接埠，公開 1401，主機上。 |
   | **--name sql1** | 指定容器，而不是一個隨機產生的自訂名稱。 如果您執行多個容器，您無法重複使用這個相同的名稱。 |
   | **microsoft/mssql-server-linux:2017-latest** | SQL Server 2017 Linux 容器映像。 |

1. 若要檢視您的 Docker 容器，請使用`docker ps`命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

   您應該會看到類似下列的螢幕擷取畫面的輸出：

   ![Docker ps 命令輸出](./media/sql-server-linux-setup-docker/docker-ps-command.png)

1. 如果**狀態**資料行會顯示狀態為**向上**、 然後 SQL Server 正在執行中容器和接聽的通訊埠中指定**連接埠**資料行。 如果**狀態**資料行的 SQL Server 容器節目**Exited**，請參閱[疑難排解 > 一節的設定指南](sql-server-linux-configure-docker.md#troubleshooting)。

`-h` （主機名稱） 參數也很有用，但它不會用於本教學課程中為了簡單起見。 這個自訂的值變更容器的內部名稱。 這是傳回的名稱，您會看到下列 TRANSACT-SQL 查詢：

```sql
SELECT @@SERVERNAME,
    SERVERPROPERTY('ComputerNamePhysicalNetBIOS'),
    SERVERPROPERTY('MachineName'),
    SERVERPROPERTY('ServerName')
```

設定`-h`和`--name`為相同的值是很容易地識別目標容器的好方法。

## <a name="change-the-sa-password"></a>變更 SA 的密碼

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="connect-to-sql-server"></a>連接至 SQL Server

下列步驟是使用 SQL Server 命令列工具， **sqlcmd**，連接到 SQL Server 的容器。

1. 使用`docker exec -it`命令來啟動的互動式 bash 殼層內執行的容器。 在下列範例中`sql1`名稱所指定`--name`參數建立容器時。

   ```bash
   sudo docker exec -it sql1 "bash"
   ```

   ```PowerShell
   docker exec -it sql1 "bash"
   ```

1. 一次的容器中，連接在本機使用 sqlcmd。 Sqlcmd 不在路徑中，依預設，所以您不必指定完整路徑。

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

1. 若要結束互動式命令提示字元在容器中，輸入`exit`。 您的容器會繼續執行之後結束互動式 bash 殼層。

## <a id="connectexternal"></a> 從連線容器外

您也可以連接到 SQL Server 執行個體在 Docker 電腦上從任何外部 Linux、 Windows 或 macOS 工具，可支援 SQL 連線。

下列步驟會使用**sqlcmd**您容器連接到容器中執行的 SQL Server 之外。 這些步驟假設您已經安裝您的容器之外的 SQL Server 命令列工具。 使用其他工具 時，適用相同的主體，而每項工具的唯一連接的程序。

1. 尋找主控您的容器之電腦的 IP 位址。 在 Linux 上使用**ifconfig**或**ip 位址**。在 Windows 中，使用**ipconfig**。

1. 執行指定的 IP 位址和連接埠對應到您的容器中的通訊埠 1433年的 sqlcmd。 在此範例中，這是在主機上的連接埠 1401年。

   ```bash
   sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourNewStrong!Passw0rd>'
   ```

   ```PowerShell
   sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourNewStrong!Passw0rd>"
   ```

1. 執行 TRANSACT-SQL 命令。 完成後，請輸入`QUIT`。

其他常見的工具，以連接到 SQL Server 包括：

- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [SQL Server Management Studio (SSMS) Windows 上](sql-server-linux-develop-use-ssms.md)
- [SQL Server 作業 Studio （預覽）](../sql-operations-studio/what-is.md)
- [mssql-cli (Preview)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)

## <a name="remove-your-container"></a>移除您的容器

如果您想要移除此教學課程中使用的 SQL Server 容器，請執行下列命令：

```bash
sudo docker stop sql1
sudo docker rm sql1
```

```PowerShell
docker stop sql1
docker rm sql1
```

> [!WARNING]
> 停止並移除容器，永久刪除容器中的任何 SQL Server 資料。 如果您要保留您的資料，[建立，並將容器之外的備份檔案複製](tutorial-restore-backup-in-sql-server-container.md)或使用[容器資料持續性技術](sql-server-linux-configure-docker.md#persist)。

## <a name="docker-demo"></a>Docker 示範

您嘗試使用 Docker 的 SQL Server 的容器映像之後，您可能想要知道如何使用 Docker 來提升開發和測試。 下列影片示範如何使用 Docker 連續整合和部署案例中。

> [!VIDEO https://channel9.msdn.com/Events/Connect/2017/T152/player]

## <a name="next-steps"></a>後續的步驟

如需如何將資料庫備份檔案還原到容器的教學課程，請參閱[Linux Docker 容器中的 SQL Server 資料庫還原](tutorial-restore-backup-in-sql-server-container.md)。 若要瀏覽其他案例中的，執行多個容器，例如資料持續性和疑難排解，請參閱[設定 SQL Server 2017 容器映像 docker](sql-server-linux-configure-docker.md)。

此外，請參閱[mssql docker GitHub 儲存機制](https://github.com/Microsoft/mssql-docker)資源、 意見反應，和已知的問題。
