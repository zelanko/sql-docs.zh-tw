---
title: 在 Docker 中還原 SQL Server 資料庫
description: 本教學課程說明如何在新的 Linux Docker 容器中還原 SQL Server 資料庫備份。
author: VanMSFT
ms.author: vanto
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 '
ms.openlocfilehash: b5fcfbf30028c904be96ca17be1ebb7feeb6f91d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471419"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>在 Linux Docker 容器中還原 SQL Server 資料庫

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

本教學課程說明如何將 SQL Server 備份檔案移動及還原至在 Docker 上執行的 SQL Server 2017 Linux 容器映像中。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

本教學課程說明如何將 SQL Server 備份檔案移動及還原至執行於 Docker 上的 SQL Server 2019 Linux 容器映像中。

::: moniker-end

> [!div class="checklist"]
> * 提取並執行最新的 SQL Server Linux 容器映像。
> * 將 Wide World Importers 資料庫檔案複製到容器中。
> * 在容器中還原資料庫。
> * 執行 Transact-SQL 陳述式以檢視及修改資料庫。
> * 備份已修改的資料庫。

## <a name="prerequisites"></a>Prerequisites

* 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。
* 至少 2 GB 的磁碟空間
* 至少 2 GB 的記憶體
* [Linux 上的 SQL Server 系統需求](sql-server-linux-setup.md#system)。

## <a name="pull-and-run-the-container-image"></a>提取及執行容器映像

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 在 Linux/Mac 上開啟 Bash 終端機，或在 Windows 上開啟已提高權限的 PowerShell 工作階段。

1. 從 Docker Hub 提取 SQL Server 2017 Linux 容器映像。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > 在這整個教學課程中，針對 Bash 殼層 (Linux/Mac) 和 PowerShell (Windows) 都有提供 Docker 命令範例。

1. 若要使用 Docker 來執行容器映像，您可以使用下列命令：

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   此命令會建立具有 Developer 版本 (預設值) 的 SQL Server 2017 容器。 SQL Server 連接埠 **1433** 在主機上會公開為連接埠 **1401**。 選擇性的 `-v sql1data:/var/opt/mssql` 參數會建立名為 **sql1ddata** 的資料磁碟區容器。 這會用來保存 SQL Server 所建立的資料。

   > [!IMPORTANT]
   > 此範例使用 Docker 中的資料磁碟區容器。 請注意，如果您改為選擇對應主機目錄，此方法在 Mac 和 Windows 上的 Docker 有限制。 如需詳細資訊，請參閱[在 Docker 上設定 SQL Server 容器映像](./sql-server-linux-docker-container-configure.md#persist)。

1. 若要檢視 Docker 容器，請使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. 若 **STATUS** 欄位顯示的狀態含 **Up**，表示 SQL Server 正在容器中執行且接聽於 **PORTS** 欄位中指定的連接埠。 若 SQL Server 容器的 **STATUS** 欄位顯示 **Exited**，請參閱 [設定指南的＜疑難排解＞一節](./sql-server-linux-docker-container-troubleshooting.md)。

  ```bash
  $ sudo docker ps -a

  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
  941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
  ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

1. 在 Linux/Mac 上開啟 Bash 終端機，或在 Windows 上開啟已提高權限的 PowerShell 工作階段。

1. 從 Docker Hub 提取 SQL Server 2019 Linux 容器映像。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```

   > [!TIP]
   > 在這整個教學課程中，針對 Bash 殼層 (Linux/Mac) 和 PowerShell (Windows) 都有提供 Docker 命令範例。

1. 若要使用 Docker 來執行容器映像，您可以使用下列命令：

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
   ```

   此命令會建立 Developer 版本 (預設值) 的 SQL Server 2019 容器。 SQL Server 連接埠 **1433** 在主機上會公開為連接埠 **1401**。 選擇性的 `-v sql1data:/var/opt/mssql` 參數會建立名為 **sql1ddata** 的資料磁碟區容器。 這會用來保存 SQL Server 所建立的資料。

1. 若要檢視 Docker 容器，請使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. 若 **STATUS** 欄位顯示的狀態含 **Up**，表示 SQL Server 正在容器中執行且接聽於 **PORTS** 欄位中指定的連接埠。 若 SQL Server 容器的 **STATUS** 欄位顯示 **Exited**，請參閱 [設定指南的＜疑難排解＞一節](./sql-server-linux-docker-container-troubleshooting.md)。

   ```bash
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

::: moniker-end

## <a name="change-the-sa-password"></a>變更 SA 密碼

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>將備份檔案複製到容器中

本教學課程使用 [Wide World Importers 範例資料庫](../samples/wide-world-importers-what-is.md)。 使用下列步驟將 Wide World Importers 資料庫備份檔案下載並複製到您的 SQL Server 容器中。

1. 首先，使用 **docker exec** 來建立備份資料夾。 下列命令會在 SQL Server 容器內建立 **/var/opt/mssql/backup** 目錄。

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. 接著，將 [WideWorldImporters-Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) 檔案下載到您的主機電腦。 下列命令會瀏覽至 home/user 目錄，並將備份檔案下載成 **wwi.bak**。

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. 使用 **docker cp** 將備份檔案複製到 **/var/opt/mssql/backup** 目錄中的容器。

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>還原資料庫

備份檔案現在已位於容器內。 還原備份之前，請務必了解備份內的邏輯檔案名稱和檔案類型。 下列 Transact-SQL 命令會使用容器中的 **sqlcmd** 來檢查備份及執行還原。

> [!TIP]
> 此教學課程會使用容器內的 **sqlcmd**，因為容器已預先安裝此工具。 不過，您也可以將 Transact-SQL 陳述式與容器外的其他用戶端工具 (例如 [Visual Studio Code](../tools/visual-studio-code/sql-server-develop-use-vscode.md) 或 [SQL Server Management Studio](sql-server-linux-manage-ssms.md)) 搭配執行。 若要連線，請使用已對應至容器中連接埠 1433 的主機連接埠。 在此範例中，這是主機電腦上的 **localhost,1401**，以及遠端的 **Host_IP_Address,1401**。

1. 執行容器內的 **sqlcmd** 以列出備份內的邏輯檔案名稱和路徑。 這會使用 **RESTORE FILELISTONLY** Transact-SQL 陳述式來完成。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost \
      -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE FILELISTONLY FROM DISK = "/var/opt/mssql/backup/wwi.bak"' \
      | tr -s ' ' | cut -d ' ' -f 1-2
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd -S localhost `
      -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/wwi.bak'"
   ```

   您應該會看到類似以下的輸出：

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. 呼叫 **RESTORE DATABASE** 命令以在容器內還原資料庫。 為上一個步驟中的每個檔案指定新路徑。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'RESTORE DATABASE WideWorldImporters FROM DISK = "/var/opt/mssql/backup/wwi.bak" WITH MOVE "WWI_Primary" TO "/var/opt/mssql/data/WideWorldImporters.mdf", MOVE "WWI_UserData" TO "/var/opt/mssql/data/WideWorldImporters_userdata.ndf", MOVE "WWI_Log" TO "/var/opt/mssql/data/WideWorldImporters.ldf", MOVE "WWI_InMemory_Data_1" TO "/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "RESTORE DATABASE WideWorldImporters FROM DISK = '/var/opt/mssql/backup/wwi.bak' WITH MOVE 'WWI_Primary' TO '/var/opt/mssql/data/WideWorldImporters.mdf', MOVE 'WWI_UserData' TO '/var/opt/mssql/data/WideWorldImporters_userdata.ndf', MOVE 'WWI_Log' TO '/var/opt/mssql/data/WideWorldImporters.ldf', MOVE 'WWI_InMemory_Data_1' TO '/var/opt/mssql/data/WideWorldImporters_InMemory_Data_1'"
   ```

   您應該會看到類似以下的輸出：

   ```
   Processed 1464 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   Processed 33 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   Processed 3862 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Converting database 'WideWorldImporters' from version 852 to the current version 869.
   Database 'WideWorldImporters' running the upgrade step from version 852 to version 853.
   Database 'WideWorldImporters' running the upgrade step from version 853 to version 854.
   Database 'WideWorldImporters' running the upgrade step from version 854 to version 855.
   Database 'WideWorldImporters' running the upgrade step from version 855 to version 856.
   Database 'WideWorldImporters' running the upgrade step from version 856 to version 857.
   Database 'WideWorldImporters' running the upgrade step from version 857 to version 858.
   Database 'WideWorldImporters' running the upgrade step from version 858 to version 859.
   Database 'WideWorldImporters' running the upgrade step from version 859 to version 860.
   Database 'WideWorldImporters' running the upgrade step from version 860 to version 861.
   Database 'WideWorldImporters' running the upgrade step from version 861 to version 862.
   Database 'WideWorldImporters' running the upgrade step from version 862 to version 863.
   Database 'WideWorldImporters' running the upgrade step from version 863 to version 864.
   Database 'WideWorldImporters' running the upgrade step from version 864 to version 865.
   Database 'WideWorldImporters' running the upgrade step from version 865 to version 866.
   Database 'WideWorldImporters' running the upgrade step from version 866 to version 867.
   Database 'WideWorldImporters' running the upgrade step from version 867 to version 868.
   Database 'WideWorldImporters' running the upgrade step from version 868 to version 869.
   RESTORE DATABASE successfully processed 58455 pages in 18.069 seconds (25.273 MB/sec).
   ```

## <a name="verify-the-restored-database"></a>驗證還原的資料庫

執行下列查詢以顯示您容器中的資料庫名稱清單：

```bash
sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
   -Q 'SELECT Name FROM sys.Databases'
```

```PowerShell
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
   -Q "SELECT Name FROM sys.Databases"
```

您應該會在資料庫清單中看見 **WideWorldImporters**。

## <a name="make-a-change"></a>進行變更

下列步驟會在資料庫中進行變更。

1. 執行查詢以檢視 **Warehouse.StockItems** 資料表中排名前 10 名的項目。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT TOP 10 StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems ORDER BY StockItemID"
   ```

   您應該會看到一份項目識別碼和名稱的清單：

   ```
   StockItemID StockItemName
   ----------- -----------------
             1 USB missile launcher (Green)
             2 USB rocket launcher (Gray)
             3 Office cube periscope (Black)
             4 USB food flash drive - sushi roll
             5 USB food flash drive - hamburger
             6 USB food flash drive - hot dog
             7 USB food flash drive - pizza slice
             8 USB food flash drive - dim sum 10 drive variety pack
             9 USB food flash drive - banana
            10 USB food flash drive - chocolate bar
   ```

1. 使用下列 **UPDATE** 陳述式來更新第一個項目的描述：

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName="USB missile launcher (Dark Green)" WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "UPDATE WideWorldImporters.Warehouse.StockItems SET StockItemName='USB missile launcher (Dark Green)' WHERE StockItemID=1; SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   您應該會看到類似以下文字的輸出：

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>建立新的備份

將資料庫還原到容器中之後，您可能也會想要在執行中的容器內定期建立資料庫備份。 步驟會依照先前步驟的類似模式，但順序相反。

1. 使用 **BACKUP DATABASE** Transact-SQL 命令在容器中建立資料庫備份。 本教學課程會在先前建立的 **/var/opt/mssql/backup** 目錄中建立新的備份檔案 **wwi_2.bak**。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "BACKUP DATABASE [WideWorldImporters] TO DISK = N'/var/opt/mssql/backup/wwi_2.bak' WITH NOFORMAT, NOINIT, NAME = 'WideWorldImporters-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
   ```

   您應該會看到類似以下的輸出：

   ```
   10 percent processed.
   20 percent processed.
   30 percent processed.
   40 percent processed.
   50 percent processed.
   60 percent processed.
   70 percent processed.
   Processed 1200 pages for database 'WideWorldImporters', file 'WWI_Primary' on file 1.
   Processed 53096 pages for database 'WideWorldImporters', file 'WWI_UserData' on file 1.
   80 percent processed.
   Processed 3865 pages for database 'WideWorldImporters', file 'WWI_InMemory_Data_1' on file 1.
   Processed 938 pages for database 'WideWorldImporters', file 'WWI_Log' on file 1.
   100 percent processed.
   BACKUP DATABASE successfully processed 59099 pages in 25.056 seconds (18.427 MB/sec).
   ```

1. 接著，將備份檔案從容器中複製到主機電腦上。

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls wwi*
   ```

## <a name="use-the-persisted-data"></a>使用保存的資料

除了使用資料庫備份來保護您的資料之外，您也可以使用資料磁碟區容器。 本教學課程一開始已使用 `-v sql1data:/var/opt/mssql` 參數建立 **sql1** 容器。 **sql1data** 資料磁碟區容器即使在該容器被移除後，也會保存 **/var/opt/mssql** 資料。 下列步驟會將 **sql1** 容器完全移除，然後使用保存的資料來建立新容器 **sql2**。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 停止 **sql1** 容器。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 移除容器。 這不會刪除先前建立的 **sql1data** 資料磁碟區容器及其當中保存的資料。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 建立新容器 **sql2**，然後重複使用 **sql1data** 資料磁碟區容器。

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
      -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

1. Wide World Importers 資料庫現在已位於新的容器中。 執行查詢以確認您先前進行的變更。

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > SA 密碼不是您為 **sql2** 容器指定的密碼 `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`。 所有 SQL Server 資料都已從 **sql1** 還原，包括本教學課程稍早變更的密碼。 實際上，由於還原 /var/opt/mssql 中的資料，因此會忽略一些類似這樣的選項。 因此，如這裡所示，密碼是 `<YourNewStrong!Passw0rd>`。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

1. 停止 **sql1** 容器。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 移除容器。 這不會刪除先前建立的 **sql1data** 資料磁碟區容器及其當中保存的資料。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 建立新容器 **sql2**，然後重複使用 **sql1data** 資料磁碟區容器。

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CU3-ubuntu-18.04
    ```

1. Wide World Importers 資料庫現在已位於新的容器中。 執行查詢以確認您先前進行的變更。

   ```bash
   sudo docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourNewStrong!Passw0rd>' \
      -Q 'SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1'
   ```

   ```PowerShell
   docker exec -it sql2 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourNewStrong!Passw0rd>" `
      -Q "SELECT StockItemID, StockItemName FROM WideWorldImporters.Warehouse.StockItems WHERE StockItemID=1"
   ```

   > [!NOTE]
   > SA 密碼不是您為 **sql2** 容器指定的密碼 `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`。 所有 SQL Server 資料都已從 **sql1** 還原，包括本教學課程稍早變更的密碼。 實際上，由於還原 /var/opt/mssql 中的資料，因此會忽略一些類似這樣的選項。 因此，如這裡所示，密碼是 `<YourNewStrong!Passw0rd>`。

::: moniker-end

## <a name="next-steps"></a>後續步驟

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本教學課程中，您已了解如何在 Windows 上備份資料庫，然後將其移至執行 SQL Server 2017 的 Linux 伺服器。 您已了解如何︰

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 "

在本教學課程中，您已了解如何在 Windows 上備份資料庫，然後將其移至執行 SQL Server 2019 的 Linux 伺服器。 您已了解如何︰

::: moniker-end

> [!div class="checklist"]
> * 建立 SQL Server Linux 容器映像。
> * 將 SQL Server 資料庫備份複製到容器中。
> * 使用 **sqlcmd** 在容器內執行 Transact-SQL 陳述式。
> * 從容器建立並擷取備份檔案。
> * 使用 Docker 中的資料磁碟區容器來保存 SQL Server 資料。

接下來，請檢閱其他 Docker 設定和疑難排解案例：

> [!div class="nextstepaction"]
>[Docker 上 SQL Server 2017 的設定指南](./sql-server-linux-docker-container-deployment.md)