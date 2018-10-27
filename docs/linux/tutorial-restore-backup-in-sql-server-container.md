---
title: 在 Docker 中的 SQL Server 資料庫還原 |Microsoft Docs
description: 本教學課程會示範如何還原新的 Linux Docker 容器中的 SQL Server 資料庫備份。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: cf3027bc998a7170d7bf75c7801f517e015bd05d
ms.sourcegitcommit: ef15fa253d98c62538bf9b6fe191af7f8ef8f6c8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2018
ms.locfileid: "49991191"
---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>在 Linux Docker 容器中的 SQL Server 資料庫還原

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

本教學課程會示範如何移動，並將 SQL Server 備份檔案還原到在 Docker 上執行的 SQL Server 2017 Linux 容器映像。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

本教學課程會示範如何移動，並將 SQL Server 備份檔案還原到在 Docker 上執行的 SQL Server 2019 CTP 2.0 Linux 容器映像。

::: moniker-end

> [!div class="checklist"]
> * 提取，並執行最新的 SQL Server Linux 容器映像。
> * Wide World Importers 資料庫檔案複製到容器。
> * 在容器中的將資料庫還原。
> * 執行 TRANSACT-SQL 陳述式，來檢視和修改資料庫。
> * 備份已修改的資料庫。

## <a name="prerequisites"></a>先決條件

* 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。
* 至少 2 GB 的磁碟空間
* 至少 2 GB 的記憶體
* [Linux 上的 SQL Server 系統需求](sql-server-linux-setup.md#system)。

## <a name="pull-and-run-the-container-image"></a>提取及執行容器映像

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 開啟 bash 終端機，在 Linux/Mac 上的或在 Windows 上提升權限的 PowerShell 工作階段。

1. 從 Docker Hub 提取 SQL Server 2017 Linux 容器映像。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:2017-latest
   ```

   > [!TIP]
   > 在本教學課程中，docker 命令範例可以同時用於 bash 殼層 (Linux/Mac) 和 PowerShell (Windows)。

1. 若要執行 Docker 容器映像，您可以使用下列命令：

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

   此命令會建立 SQL Server 2017 容器與開發人員版本 （預設值）。 SQL Server 連接埠**1433年**在連接埠與主機上公開**1401年**。 選擇性`-v sql1data:/var/opt/mssql`參數會建立名為的資料磁碟區容器**sql1ddata**。 這用來保存 SQL Server 所建立的資料。

   > [!NOTE]
   > 在容器中執行生產 SQL Server 版本的程序會稍有不同。 如需詳細資訊，請參閱[執行生產容器映像](sql-server-linux-configure-docker.md#production)。 如果您使用相同的容器名稱和連接埠，本逐步解說的其餘部分仍適用於實際執行的容器。

1. 若要檢視 Docker 容器，請使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. 如果**狀態**資料行會顯示狀態為**向上**、 然後 SQL Server 正在執行中容器和接聽的通訊埠中指定**連接埠**資料行。 如果**狀態**資料行的 SQL Server 容器節目**Exited**，請參閱[疑難排解 > 一節的設定指南](sql-server-linux-configure-docker.md#troubleshooting)。

  ```bash
  $ sudo docker ps -a

  CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
  941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
  ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 開啟 bash 終端機，在 Linux/Mac 上的或在 Windows 上提升權限的 PowerShell 工作階段。

1. 從 Docker Hub 提取 SQL Server 2019 CTP 2.0 Linux 容器映像。

   ```bash
   sudo docker pull mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   > [!TIP]
   > 在本教學課程中，docker 命令範例可以同時用於 bash 殼層 (Linux/Mac) 和 PowerShell (Windows)。

1. 若要執行 Docker 容器映像，您可以使用下列命令：

   ```bash
   sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      --name 'sql1' -p 1401:1433 \
      -v sql1data:/var/opt/mssql \
      -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      --name "sql1" -p 1401:1433 `
      -v sql1data:/var/opt/mssql `
      -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
   ```

   此命令會建立 SQL Server 2019 CTP 2.0 容器與開發人員版本 （預設值）。 SQL Server 連接埠**1433年**在連接埠與主機上公開**1401年**。 選擇性`-v sql1data:/var/opt/mssql`參數會建立名為的資料磁碟區容器**sql1ddata**。 這用來保存 SQL Server 所建立的資料。

1. 若要檢視 Docker 容器，請使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

   ```PowerShell
   docker ps -a
   ```

1. 如果**狀態**資料行會顯示狀態為**向上**、 然後 SQL Server 正在執行中容器和接聽的通訊埠中指定**連接埠**資料行。 如果**狀態**資料行的 SQL Server 容器節目**Exited**，請參閱[疑難排解 > 一節的設定指南](sql-server-linux-configure-docker.md#troubleshooting)。

   ```bash
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

::: moniker-end

## <a name="change-the-sa-password"></a>變更 SA 密碼

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>將備份檔案複製到容器

本教學課程會使用[Wide World Importers 範例資料庫](../sample/world-wide-importers/wide-world-importers-documentation.md)。 您可以使用下列步驟來下載及 Wide World Importers 資料庫備份檔案複製到您的 SQL Server 容器。

1. 首先，使用**docker exec**建立備份的資料夾。 下列命令會建立 **/var/opt/mssql/backup**目錄內的 SQL Server 容器。

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. 接下來，下載[Wideworldimporters-full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0)到主機電腦的檔案。 下列命令瀏覽至首頁/使用者目錄，並下載做為備份的檔案**wwi.bak**。

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. 使用**docker cp**若要將備份檔案複製到容器中 **/var/opt/mssql/backup**目錄。

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>還原資料庫

備份檔案的位置現在是在容器內。 還原之前備份，請務必知道的邏輯檔案名稱和備份內的檔案類型。 下列 TRANSACT-SQL 命令檢查備份及還原使用執行**sqlcmd**容器中。

> [!TIP]
> 本教學課程會使用**sqlcmd**的容器中，因為容器是使用預先安裝此工具。 不過，您也可以執行 TRANSACT-SQL 陳述式和其他用戶端工具以外的容器，例如[Visual Studio Code](sql-server-linux-develop-use-vscode.md)或是[SQL Server Management Studio](sql-server-linux-manage-ssms.md)。 若要連線，請使用主機連接埠對應至容器中的連接埠 1433年。 在此範例中，這就是**localhost，1401年**主機電腦上並**Host_IP_Address，1401年**遠端。

1. 執行**sqlcmd**內要列出邏輯檔案名稱和路徑，在備份內的容器。 做法是使用**RESTORE FILELISTONLY** TRANSACT-SQL 陳述式。

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

   您應該會看到類似下面的輸出：

   ```
   LogicalName   PhysicalName
   ------------------------------------------
   WWI_Primary   D:\Data\WideWorldImporters.mdf
   WWI_UserData   D:\Data\WideWorldImporters_UserData.ndf
   WWI_Log   E:\Log\WideWorldImporters.ldf
   WWI_InMemory_Data_1   D:\Data\WideWorldImporters_InMemory_Data_1
   ```

1. 呼叫**RESTORE DATABASE**命令，以還原在容器內的資料庫。 每個檔案在上一個步驟中，指定新路徑。

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

   您應該會看到類似下面的輸出：

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

## <a name="verify-the-restored-database"></a>確認還原的資料庫

執行下列查詢，以顯示您的容器中的資料庫名稱清單：

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

您應該會看到**WideWorldImporters**中的資料庫清單。

## <a name="make-a-change"></a>進行變更

下列步驟會在資料庫中進行變更。

1. 執行查詢，以檢視中的前 10 個項目**Warehouse.StockItems**資料表。

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

   您應該會看到的項目識別碼和名稱的清單：

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

1. 以下列更新的第一個項目描述**更新**陳述式：

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

   您應該會看到類似下列文字的輸出：

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>建立新的備份

您已將您資料庫還原至容器之後，您也可以定期建立資料庫備份，在執行的容器。 上一個步驟，但反向，步驟會遵循類似的模式。

1. 使用**BACKUP DATABASE** TRANSACT-SQL 命令，以在容器中建立的資料庫備份。 本教學課程中建立新的備份檔案， **wwi_2.bak**，在先前建立 **/var/opt/mssql/backup**目錄。

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

   您應該會看到類似下面的輸出：

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

1. 接下來，將複製出容器和主機電腦的備份檔案。

   ```bash
   cd ~
   sudo docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

   ```PowerShell
   cd ~
   docker cp sql1:/var/opt/mssql/backup/wwi_2.bak wwi_2.bak
   ls -l wwi*
   ```

## <a name="use-the-persisted-data"></a>使用必要的資料

除了資料庫備份來保護您的資料，您也可以使用資料磁碟區容器。 本教學課程中建立的開頭**sql1**容器`-v sql1data:/var/opt/mssql`參數。 **Sql1data**持續資料磁碟區容器發生 **/var/opt/mssql**即使容器已移除的資料。 下列步驟會完全移除**sql1**容器，然後再建立新的容器， **sql2**，與保存的資料。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 停止**sql1**容器。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 移除容器。 這並不會刪除之前建立**sql1data**資料磁碟區容器和它的永續性的資料。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 建立新的容器**sql2**，並重複使用**sql1data**資料磁碟區容器。

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

1. Wide World Importers 資料庫現在位於新的容器。 執行查詢，以確認先前您所做的變更。

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
   > SA 密碼不是您指定的密碼**sql2**容器， `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`。 從還原的 SQL Server 資料的所有**sql1**，稍早在本教學課程中，包括從已變更的密碼。 作用中，像這樣的一些選項會被忽略，因為還原 /var/opt/mssql 中的資料。 基於這個理由，密碼是`<YourNewStrong!Passw0rd>`如下所示。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 停止**sql1**容器。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 移除容器。 這並不會刪除之前建立**sql1data**資料磁碟區容器和它的永續性的資料。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 建立新的容器**sql2**，並重複使用**sql1data**資料磁碟區容器。

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
    ```

1. Wide World Importers 資料庫現在位於新的容器。 執行查詢，以確認先前您所做的變更。

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
   > SA 密碼不是您指定的密碼**sql2**容器， `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`。 從還原的 SQL Server 資料的所有**sql1**，稍早在本教學課程中，包括從已變更的密碼。 作用中，像這樣的一些選項會被忽略，因為還原 /var/opt/mssql 中的資料。 基於這個理由，密碼是`<YourNewStrong!Passw0rd>`如下所示。

::: moniker-end

## <a name="next-steps"></a>後續步驟

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

在本教學課程中，您已了解如何在 Windows 上的資料庫備份，並將它移到執行 SQL Server 2017 的 Linux 伺服器。 您已學到如何以：

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

在本教學課程中，您已了解如何在 Windows 上的資料庫備份，並將它移至執行 SQL Server 2019 CTP 2.0 在 Linux 伺服器。 您已學到如何以：

::: moniker-end

> [!div class="checklist"]
> * 建立 SQL Server Linux 容器映像。
> * SQL Server 資料庫備份複製到容器。
> * 執行 TRANSACT-SQL 陳述式內的容器**sqlcmd**。
> * 建立及擷取容器中的備份檔案。
> * 使用在 Docker 中的資料磁碟區容器，可保存 SQL Server 資料。

接下來，請檢閱其他的 Docker 設定及疑難排解案例：

> [!div class="nextstepaction"]
>[在 Docker 上的 SQL Server 2017 的設定指南](sql-server-linux-configure-docker.md)
