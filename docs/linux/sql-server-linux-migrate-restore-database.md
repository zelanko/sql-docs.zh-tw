---
title: 從 Windows 的 SQL Server 資料庫移轉至 Linux |Microsoft Docs
description: 本教學課程會示範如何取得 Windows 上的 SQL Server 資料庫備份，並將它還原到執行 SQL Server 2017 的 Linux 機器。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 8cc1010f2492054a467abfc53e859d39a86e1c78
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086700"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>從 Windows 的 SQL Server 資料庫移轉至 Linux 使用備份與還原

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 的備份和還原功能會從在 Windows 上的 SQL Server 的資料庫移轉至 SQL Server 2017 Linux 上的建議的方式。 在本教學課程中，您將逐步完成將資料庫移至 Linux 中，使用備份和還原技術所需的步驟。

> [!div class="checklist"]
> * 使用 SSMS 建立在 Windows 上的備份檔案
> * 安裝在 Windows 上的 Bash 殼層
> * 從 Bash 殼層中，移至 Linux 的備份檔案
> * 使用 TRANSACT-SQL 在 Linux 上的備份檔案
> * 執行查詢，以確認移轉

您也可以建立 SQL Server Always On 可用性群組將從 Windows 的 SQL Server 資料庫移轉到 Linux。 請參閱[sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md)。

## <a name="prerequisites"></a>先決條件

若要完成本教學課程需要下列必要條件：

* 使用下列 Windows 電腦：
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions)安裝。
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)安裝。
  * 要移轉的目標資料庫。

* Linux 機器會有安裝下列項目：
  * SQL Server 2017 ([RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)，或[Ubuntu](quickstart-install-connect-ubuntu.md)) 的命令列工具。

## <a name="create-a-backup-on-windows"></a>Windows 上建立備份

有數種方式可在 Windows 上建立資料庫的備份檔案。 下列步驟會使用 SQL Server Management Studio (SSMS)。

1. 開始**SQL Server Management Studio** Windows 電腦上。

1. 在 [連接] 對話方塊中，輸入**localhost**。

1. 在 [物件總管] 中，展開**資料庫**。

1. 以滑鼠右鍵按一下您的目標資料庫中，選取**任務**，然後按一下 **備份...**.

   ![使用 SSMS 來建立備份檔案](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. 在 [**資料庫備份**] 對話方塊中，確認**備份類型**是**完整**和**備份至**是**磁碟**. 請注意，名稱和檔案的位置。 例如，名為的資料庫**YourDB** SQL Server 2016 上具有 預設備份路徑的`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`。

1. 按一下 **確定**來備份您的資料庫。

> [!NOTE]
> 另一個選項是執行 TRANSACT-SQL 查詢，以建立備份檔案。 下列 TRANSACT-SQL 命令會為先前的步驟相同的動作執行資料庫稱為**YourDB**:
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>安裝在 Windows 上的 Bash 殼層

若要還原資料庫，您必須先將備份檔案從 Windows 電腦傳輸到目標 Linux 電腦。 在本教學課程中，我們將檔案移到 Linux 從 Bash 殼層 （終端機視窗中） 在 Windows 上執行。

1. 安裝程式支援的 Windows 電腦上的 Bash 殼層**scp** （安全複製） 與**ssh** （遠端登入） 命令。 兩個範例包括：

   * [適用於 Linux 的 Windows 子系統](https://msdn.microsoft.com/commandline/wsl/about)(Windows 10)
   * Git Bash 殼層 ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. 在 Windows 上開啟的 Bash 工作階段。

## <a id="scp"></a> 將備份檔案複製到 Linux

1. 在您的 Bash 工作階段，瀏覽至包含您的備份檔案的目錄。 例如：

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. 使用**scp**檔案傳輸至目標 Linux 電腦的命令。 下列範例傳輸**YourDB.bak**主目錄*user1* Linux 伺服器的 IP 位址上*192.0.2.9*:

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp 命令](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> 有進行檔案傳輸使用 scp 的替代方式。 其中一個是使用[Samba](https://help.ubuntu.com/community/Samba)來設定 Windows 與 Linux 之間 SMB 網路共用。 如需 Ubuntu 的逐步解說，請參閱 <<c0> [ 如何建立網路共用透過 Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)。 建立好之後，您可以為網路檔案共用，是從 Windows，這類 **\\ \\machinenameorip\\共用**。

## <a name="move-the-backup-file-before-restoring"></a>將備份檔案還原之前

到目前為止，備份檔案，就是您在您的使用者主目錄中的 Linux 伺服器上。 之前將資料庫還原到 SQL Server，您必須將備份放在的子目錄 **/var/opt/mssql**。

1. 在相同的 「 Windows 的 Bash 工作階段 」，從遠端連線到目標 Linux 機器，其中**ssh**。 下列範例會連線到 Linux 機器**192.0.2.9**身分**user1**。

   ```bash
   ssh user1@192.0.2.9
   ```

   您現在已在遠端的 Linux 伺服器上執行命令。

1. 進入進階使用者模式。

   ```bash
   sudo su
   ```

1. 建立新的備份目錄。 如果目錄已經存在-p 參數沒有任何作用。

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. 將備份檔案移至該目錄中。 在下列範例中，備份檔案的主目錄中的所在*user1*。 變更命令以符合您的備份檔案的位置和檔案名稱。

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. 結束進階使用者模式。

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>在 Linux 上的將資料庫還原

若要還原資料庫備份，您可以使用**RESTORE DATABASE** TRANSACT-SQL (TQL) 命令。

> [!NOTE]
> 下列步驟會使用**sqlcmd**工具。 如果您尚未安裝 SQL Server Tools，請參閱 <<c0> [ 安裝 SQL Server 命令列工具，在 Linux 上的](sql-server-linux-setup-tools.md)。

1. 在相同的終端機中，啟動**sqlcmd**。 下列範例會連接本機的 SQL Server 執行個體，但**SA**使用者。 輸入的密碼，出現提示時，或藉由新增指定的密碼 **-P**參數。

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. 在`>1`提示中，輸入下列**RESTORE DATABASE**命令 （您無法複製並貼上整個多行命令一次） 的每一行之後按下 ENTER。 取代所有出現之`YourDB`與您的資料庫名稱。

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   您應該會收到的訊息已成功還原資料庫。

1. 列出所有伺服器上的資料庫，以確認還原作業。 應該會列出已還原的資料庫。

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 已移轉的資料庫上執行其他查詢。 下列命令切換至的內容**YourDB**資料庫中，選取資料列的其中一個資料表。

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. 當您完成使用**sqlcmd**，輸入`exit`。

1. 當您完成在遠端工作**ssh**工作階段中，輸入`exit`一次。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何在 Windows 上的資料庫備份，並將它移到執行 SQL Server 2017 的 Linux 伺服器。 您已學到如何以：
> [!div class="checklist"]
> * 使用 SSMS 和 TRANSACT-SQL 來建立在 Windows 上的備份檔案
> * 安裝在 Windows 上的 Bash 殼層
> * 使用**scp**將備份檔案從 Windows 移到 Linux
> * 使用**ssh**遠端連線到您的 Linux 機器
> * 若要準備還原備份的檔案重新放置
> * 使用**sqlcmd**執行 TRANSACT-SQL 命令
> * 資料庫備份與還原**RESTORE DATABASE**命令 
> * 執行查詢，以確認移轉

在 Linux 上的 SQL Server 中接下來，探索其他移轉案例。 

> [!div class="nextstepaction"]
>[將資料庫移轉至 Linux 上的 SQL Server](sql-server-linux-migrate-overview.md)
