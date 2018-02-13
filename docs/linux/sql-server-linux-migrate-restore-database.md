---
title: "從 Windows 的 SQL Server 資料庫移轉至 Linux |Microsoft 文件"
description: "本教學課程會示範如何取得 Windows 上的 SQL Server 資料庫備份，並將它還原到執行 SQL Server 2017 Linux 機器。"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.workload: On Demand
ms.openlocfilehash: f68f5aae50460dc1e39a24ac1213ac477c96d552
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>從 Windows 的 SQL Server 資料庫移轉至 Linux 使用備份與還原

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 的備份和還原功能會從 SQL Server 在 Windows 上的資料庫移轉至 SQL Server 2017 Linux 上的建議的方式。 在本教學課程中，您將逐步進行備份時，將資料庫移至 Linux 和還原技術所需的步驟。

> [!div class="checklist"]
> * 使用 SSMS 建立在 Windows 上的備份檔案
> * 在 Windows 上安裝 Bash 殼層
> * 將備份檔案從 Bash 殼層移至 Linux
> * 使用 TRANSACT-SQL Linux 上的備份檔案還原
> * 執行查詢，以驗證移轉

您也可以建立 SQL Server Alwayson 可用性群組將從 Windows 的 SQL Server 資料庫移轉至 Linux。 請參閱[sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md)。

## <a name="prerequisites"></a>필수 구성 요소

若要完成本教學課程中，需要下列必要條件：

* 具有下列的 Windows 電腦：
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions)安裝。
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)安裝。
  * 若要移轉的目標資料庫。

* Linux 機器會有安裝下列項目：
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)，或[Ubuntu](quickstart-install-connect-ubuntu.md)) 與命令列工具。

## <a name="create-a-backup-on-windows"></a>在 Windows 上建立備份

有幾種方式可以在 Windows 上建立資料庫的備份檔案。 下列步驟會使用 SQL Server Management Studio (SSMS)。

1. 啟動**SQL Server Management Studio** Windows 電腦上。

1. 在 [連接] 對話方塊中，輸入**localhost**。

1. 在 [物件總管] 中，展開**資料庫**。

1. 以滑鼠右鍵按一下您的目標資料庫中，選取**工作**，然後按一下 **備份...**.

   ![使用 SSMS 建立備份檔案](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. 在**資料庫備份** 對話方塊中，確認**備份類型**是**完整**和**備份至**是**磁碟**。 請注意名稱和檔案的位置。 例如，名為資料庫**YourDB** SQL Server 2016 上有預設的備份路徑的`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`。

1. 按一下**確定**來備份您的資料庫。

> [!NOTE]
> 另一個選項是執行 TRANSACT-SQL 查詢，以建立備份檔案。 下列 TRANSACT-SQL 命令執行資料庫的動作與先前的步驟相同，呼叫**YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>在 Windows 上安裝 Bash 殼層

若要還原資料庫，您必須先將備份檔案從 Windows 電腦傳輸到目標 Linux 機器。 在本教學課程中，我們將檔案移至 Linux Bash 殼層 （終端機視窗） 從在 Windows 上執行。

1. 支援在 Windows 電腦上安裝 Bash 殼層**scp** （安全複製） 和**ssh** （遠端登入） 命令。 兩個範例包括：

   * [適用於 Linux 的 Windows 子系統](https://msdn.microsoft.com/commandline/wsl/about)(Windows 10)
   * Git Bash 殼層 ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. 在 Windows 上開啟 Bash 工作階段。

## <a id="scp"></a> 將備份檔案複製到 Linux

1. 在您 Bash 工作階段中，瀏覽至包含您的備份檔案的目錄。 例如：

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. 使用**scp**檔案傳輸至目標 Linux 機器的命令。 下列範例傳輸**YourDB.bak**的主目錄的*user1* Linux 伺服器的 IP 位址上*192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp 命令](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> 沒有進行檔案傳輸使用 scp 的替代方案。 其中一個是使用[Samba](https://help.ubuntu.com/community/Samba)來設定 Windows 和 Linux 之間 SMB 網路共用。 如需 Ubuntu 的逐步解說，請參閱[如何建立網路共用透過 Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)。 一旦建立，您可以存取網路檔案共用在 Windows 中的這類 **\\ \\machinenameorip\\共用**。

## <a name="move-the-backup-file-before-restoring"></a>將備份檔案還原之前

此時，備份檔案是在使用者的主目錄中的 Linux 伺服器上。 之前將資料庫還原到 SQL Server，您必須將備份放的子目錄中**/var/opt/mssql**。

1. 相同 Windows 撞工作階段中，從遠端連線到您的目標 Linux 機器，與**ssh**。 下列範例會連接到 Linux 機器**192.0.2.9**身分**user1**。

   ```bash
   ssh user1@192.0.2.9
   ```

   您現在遠端的 Linux 伺服器上執行命令。

1. 進入進階使用者模式。

   ```bash
   sudo su
   ```

1. 建立新的備份目錄。 如果目錄已經存在-p 參數沒有任何作用。

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. 將備份檔案移至該目錄。 在下列範例中，備份檔案所在的主目錄*user1*。 變更以符合您的備份檔案的位置和檔案名稱的命令。

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. 結束進階使用者模式。

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>還原您在 Linux 上的資料庫

若要還原資料庫備份，您可以使用**RESTORE DATABASE** TRANSACT-SQL (TQL) 命令。

> [!NOTE]
> 下列步驟會使用**sqlcmd**工具。 如果您尚未安裝 SQL Server 工具，請參閱[Linux 上的安裝 SQL Server 命令列工具](sql-server-linux-setup-tools.md)。

1. 在相同的終端機中，啟動**sqlcmd**。 下列範例會連接到本機的 SQL Server 執行個體與**SA**使用者。 輸入的密碼，出現提示時，或藉由新增指定的密碼**-P**參數。

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. 在`>1`提示字元中，輸入下列**RESTORE DATABASE**命令之後每一行 （您不能複製及貼上整個多行命令一次）, 按下 ENTER。 取代所有出現之`YourDB`與您的資料庫名稱。

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   您應該會收到的訊息，將會成功還原資料庫。

1. 列出所有伺服器上的資料庫，以驗證還原。 應該會列出已還原的資料庫。

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 您已移轉的資料庫上執行其他查詢。 下列命令會針對內容**YourDB**資料庫，並從其資料表的其中一個選取的資料列。

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. 當您完成使用**sqlcmd**，型別`exit`。

1. 當您完成在遠端工作**ssh**工作階段中，輸入`exit`一次。

## <a name="next-steps"></a>後續的步驟

在本教學課程中，您將學會如何備份資料庫，在 Windows 上，並將它移至執行 SQL Server 2017 的 Linux 伺服器。 您已了解如何以：
> [!div class="checklist"]
> * 使用 SSMS 和 TRANSACT-SQL 來建立在 Windows 上的備份檔案
> * 在 Windows 上安裝 Bash 殼層
> * 使用**scp**從 Windows 的備份的檔案移至 Linux
> * 使用**ssh**遠端連線到您的 Linux 電腦
> * 若要準備還原備份的檔案重新放置
> * 使用**sqlcmd**執行 Transact SQL 命令
> * 使用還原資料庫備份**RESTORE DATABASE**命令 
> * 執行查詢，以驗證移轉

接下來，瀏覽其他移轉案例適用於 SQL Server on Linux。 

> [!div class="nextstepaction"]
>[將資料庫移轉至 SQL Server on Linux](sql-server-linux-migrate-overview.md)
