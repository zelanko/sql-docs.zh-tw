---
title: "將 SQL Server 資料庫還原在 Docker 中 |Microsoft 文件"
description: "此教學課程顯示如何還原新的 Linux Docker 容器中的 SQL Server 資料庫備份。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 51f60c4fecb56aca3f4fb007f8e6a68601a47d11
ms.openlocfilehash: 1f3cc214be4eaac2199c17c3bea1da7fd02956f1
ms.contentlocale: zh-tw
ms.lasthandoff: 10/14/2017

---
# <a name="restore-a-sql-server-database-in-a-linux-docker-container"></a>Linux Docker 容器中的 SQL Server 資料庫還原

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本教學課程會示範如何移動及 SQL Server 備份檔案還原到 SQL Server 2017 Linux 容器映像上執行 Docker。

> [!div class="checklist"]
> * 提取和執行最新的 SQL Server 2017 Linux 容器映像。
> * World Wide Importers 資料庫檔案複製到容器。
> * 在容器中的將資料庫還原。
> * 執行 TRANSACT-SQL 陳述式，來檢視及修改資料庫。
> * 將已修改的資料庫備份。

## <a name="prerequisites"></a>必要條件

* Docker 引擎 1.8 + 任何支援 Mac/Windows Linux 發佈或 Docker。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。
* 至少 4 GB 的磁碟空間
* 至少 4 GB 的 RAM
* [SQL Server on Linux 的系統需求](sql-server-linux-setup.md#system)。

> [!IMPORTANT]
> 適用於 Mac 的 Docker 和 Docker for Windows 上的預設值是 2 GB 一定 vm，因此您必須將它變更為 4 GB。 如果您在 Mac 或 Windows 上執行，請增加您使用的記憶體設定[Docker 快速入門中的指示](quickstart-install-connect-docker.md)。

## <a name="pull-and-run-the-container-image"></a>提取和執行容器映像

1. 開啟 bash 終端機 Linux/Mac 上的或在 Windows 上的提高權限的 PowerShell 工作階段。

1. 從 Docker Hub 提取 SQL Server 2017 Linux 容器映像。

    ```bash
    sudo docker pull microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker pull microsoft/mssql-server-linux:2017-latest
    ```

    > [!TIP]
    > 本教學課程中，指定 docker 命令範例，就 bash 殼層 (Linux/Mac) 和 PowerShell (Windows)。

1. 若要執行 Docker 容器映像，您可以使用下列命令：

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql1' -p 1401:1433 \
       -v sql1data:/var/opt/mssql \
       -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql1" -p 1401:1433 `
       -v sql1data:/var/opt/mssql `
       -d microsoft/mssql-server-linux:2017-latest
    ```

    此命令會建立 SQL Server 2017 容器 Developer edition （預設值）。 SQL Server 連接埠**1433年**公開主機做為連接埠上**1401年**。 選擇性`-v sql1data:/var/opt/mssql`參數會建立名為的資料磁碟區容器**sql1ddata**。 這用來保存資料的 SQL Server 所建立。

   > [!NOTE]
   > 執行容器中的實際執行 SQL Server 版本的程序有些許不同。 如需詳細資訊，請參閱[容器映像執行生產](sql-server-linux-configure-docker.md#production)。 如果您使用相同的容器名稱和連接埠，本逐步解說的其餘部分仍可使用實際執行的容器。

1. 若要檢視您的 Docker 容器，請使用`docker ps`命令。

    ```bash
    sudo docker ps -a
    ```

    ```PowerShell
    docker ps -a
    ```
 
1. 如果**狀態**資料行會顯示狀態為**向上**、 然後 SQL Server 正在執行中容器和接聽的通訊埠中指定**連接埠**資料行。 如果**狀態**資料行的 SQL Server 容器節目**Exited**，請參閱[疑難排解 > 一節的設定指南](sql-server-linux-configure-docker.md#troubleshooting)。

   ```
   $ sudo docker ps -a

   CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
   941e1bdf8e1d        microsoft/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour    0.0.0.0:1401->1433/tcp   sql1
   ```

## <a name="change-the-sa-password"></a>變更 SA 的密碼

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="copy-a-backup-file-into-the-container"></a>將備份檔案複製到容器

本教學課程使用[Wide World Importers 範例資料庫](../sample/world-wide-importers/wide-world-importers-documentation.md)。 使用下列步驟下載並將 Wide World Importers 資料庫備份檔案複製到您的 SQL Server 容器。

1. 首先，使用**docker exec**建立備份的資料夾。 El comando siguiente crea **/var/選擇/mssql/** SQL Server 容器內的目錄。

   ```bash
   sudo docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

   ```PowerShell
   docker exec -it sql1 mkdir /var/opt/mssql/backup
   ```

1. 接下來，下載[WideWorldImporters Full.bak](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0)主機電腦的檔案。 下列命令瀏覽至首頁/使用者目錄，並下載備份檔案儲存為**wwi.bak**。

   ```bash
   cd ~
   curl -L -o wwi.bak 'https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak'
   ```

   ```PowerShell
   curl -OutFile "wwi.bak" "https://github.com/Microsoft/sql-server-samples/releases/download/wide-world-importers-v1.0/WideWorldImporters-Full.bak"
   ```

1. 使用**docker cp** ，將備份檔案複製到容器中**/var/opt/mssql/backup**目錄。

   ```bash
   sudo docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

   ```PowerShell
   docker cp wwi.bak sql1:/var/opt/mssql/backup
   ```

## <a name="restore-the-database"></a>還原資料庫

備份檔案現在位於容器內。 還原之前備份，請務必知道的邏輯檔案名稱及備份內的檔案類型。 下列 TRANSACT-SQL 命令檢查備份及還原使用執行**sqlcmd**容器中。

> [!TIP]
> 本教學課程使用**sqlcmd**的容器，因為容器會隨附預先安裝此工具。 不過，您也可以執行 TRANSACT-SQL 陳述式與其他用戶端工具以外的容器，例如[Visual Studio Code](sql-server-linux-develop-use-vscode.md)或[SQL Server Management Studio](sql-server-linux-develop-use-ssms.md)。 若要連接，請使用主機連接埠對應至容器中的通訊埠 1433年。 在此範例中，這就是**localhost，1401年**主機電腦上和**Host_IP_Address，1401年**遠端。

1. 執行**sqlcmd**列出邏輯檔案名稱和路徑，在備份的容器。 做法是使用**RESTORE FILELISTONLY** TRANSACT-SQL 陳述式。

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

1. 呼叫**RESTORE DATABASE**命令來還原資料庫的容器。 每個檔案上一個步驟中，指定新路徑。

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

下列步驟會在資料庫中的變更。

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

   您應該會看到一份項目識別項的名稱：

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

   您應該會看到下列文字類似的輸出：

   ```
   (1 rows affected)
   StockItemID StockItemName
   ----------- ------------------------------------
             1 USB missile launcher (Dark Green)
   ```

## <a name="create-a-new-backup"></a>建立新的備份

您已還原資料庫至容器之後，您也可以定期建立資料庫備份，在執行的容器。 步驟的上一個步驟，但以相反，請遵循類似的模式。

1. 使用**備份資料庫**TRANSACT-SQL 命令，在容器中建立的資料庫備份。 本教學課程中建立新的備份檔案， **wwi_2.bak**，在先前建立**/var/opt/mssql/backup**目錄。

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

除了製作資料庫備份對於保護資料，您也可以使用資料磁碟區容器。 建立本教學課程開頭**sql1**容器`-v sql1data:/var/opt/mssql`參數。 **Sql1data**資料磁碟區容器保存**/var/opt/mssql**資料即使在移除此容器。 下列的步驟完全移除**sql1**容器，然後建立新的容器， **sql2**，以保存資料。

1. 停止**sql1**容器。

   ```bash
   sudo docker stop sql1
   ```

   ```PowerShell
   docker stop sql1
   ```

1. 移除容器。 這並不會刪除先前建立**sql1data**資料磁碟區容器和它的永續性的資料。

   ```bash
   sudo docker rm sql1
   ```

   ```PowerShell
   docker rm sql1
   ```

1. 建立新的容器， **sql2**，並重複使用**sql1data**資料磁碟區容器。

    ```bash
    sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
       --name 'sql2' -e 'MSSQL_PID=Developer' -p 1401:1433 \
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

    ```PowerShell
    docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
       --name "sql2" -e "MSSQL_PID=Developer" -p 1401:1433 `
       -v sql1data:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
    ```

1. Wide World Importers 資料庫現在為新的容器。 執行查詢，確認先前所做的變更。

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
   > SA 密碼不是您為指定的密碼**sql2**容器， `MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>`。 所有 SQL Server 資料從還原**sql1**，稍早在本教學課程中包括從已變更的密碼。 作用中，像這樣的一些選項都會被忽略，因為還原 /var/opt/mssql 中的資料。 基於這個理由，密碼是`<YourNewStrong!Passw0rd>`如下所示。

## <a name="next-steps"></a>後續的步驟

在本教學課程中，您將學會如何備份資料庫，在 Windows 上，並將它移至執行 SQL Server 2017 RC2 的 Linux 伺服器。 您已了解如何以：
> [!div class="checklist"]
> * 建立 SQL Server 2017 Linux 容器映像。
> * 將 SQL Server 資料庫備份複製到容器。
> * 執行 TRANSACT-SQL 陳述式內部的容器**sqlcmd**。
> * 建立並從容器擷取備份檔案。
> * 使用在 Docker 中的資料磁碟區容器，可保存 SQL Server 資料。

接著，檢閱其他 Docker 設定及疑難排解案例：

> [!div class="nextstepaction"]
>[SQL Server 2017 docker 設定指南](sql-server-linux-configure-docker.md)

