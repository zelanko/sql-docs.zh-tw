---
title: 將 SQL Server 資料庫從 Windows 移轉至 Linux
description: 本教學課程說明如何在 Windows 上進行 SQL Server 的資料庫備份，並將其還原至執行 SQL Server 的 Linux 電腦。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/16/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.openlocfilehash: 8f8436e463a969921ef3e37ebf89f48bc94b49dc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895178"
---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>使用備份與還原將 SQL Server 資料庫從 Windows 移轉至 Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

SQL Server 的備份與還原功能是將資料庫從 Windows 上的 SQL Server 移轉至 Linux 上的 SQL Server 時建議使用的方式。 在本教學課程中，您將逐步完成使用備份與還原技術將資料庫移至 Linux 所需的步驟。

> [!div class="checklist"]
> * 使用 SSMS 在 Windows 上建立備份檔案
> * 在 Windows 上安裝 Bash Shell
> * 從 Bash Shell 將備份檔案移至 Linux
> * 使用 Transact-SQL 在 Linux 上還原備份檔案
> * 執行查詢以確認移轉

您也可以建立 SQL Server Always On 可用性群組，將 SQL Server 資料庫從 Windows 移轉至 Linux。 請參閱 [sql-server-linux-availability-group-cross-platform](sql-server-linux-availability-group-cross-platform.md)。

## <a name="prerequisites"></a>Prerequisites

必須擁有下列先決條件，才能完成本教學課程：

* 具有下列各項的 Windows 電腦：
  * 已安裝 [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions)。
  * 已安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
  * 要移轉的目標資料庫。

* 已安裝下列各項的 Linux 電腦：
  * 具有命令列工具的 SQL Server ([RHEL](quickstart-install-connect-red-hat.md)、[SLES](quickstart-install-connect-suse.md) 或 [Ubuntu](quickstart-install-connect-ubuntu.md))。

## <a name="create-a-backup-on-windows"></a>在 Windows 上建立備份

有數種方式可以在 Windows 上建立資料庫的備份檔案。 下列步驟使用 SQL Server Management Studio (SSMS)。

1. 在 Windows 電腦上啟動 **SQL Server Management Studio**。

1. 在 [連線] 對話方塊中輸入 **localhost**。

1. 在 [物件總管] 中展開 [資料庫]  。

1. 以滑鼠右鍵按一下目標資料庫，選取 [工作]  ，然後按一下 [備份...]  。

   ![使用 SSMS 建立備份檔案](./media/sql-server-linux-migrate-restore-database/ssms-create-backup.png)

1. 在 [備份資料庫]  對話方塊中，確認 [備份類型]  是 [完整]  ，而 [備份至]  是[磁碟]  。 請記下檔案的名稱和位置。 例如，在 SQL Server 2016 上名為 **YourDB** 的資料庫具有預設備份路徑 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak`。

1. 按一下 [確定]  以備份您的資料庫。

> [!NOTE]
> 另一個選項是執行 Transact-SQL 查詢以建立備份檔案。 下列 Transact-SQL 命令會針對名為 **YourDB**的資料庫執行與先前步驟相同的動作：
>
> ```sql
> BACKUP DATABASE [YourDB] TO  DISK =
> N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\YourDB.bak'
> WITH NOFORMAT, NOINIT, NAME = N'YourDB-Full Database Backup',
> SKIP, NOREWIND, NOUNLOAD, STATS = 10
> GO
> ```

## <a name="install-a-bash-shell-on-windows"></a>在 Windows 上安裝 Bash Shell

若要還原資料庫，您必須先將備份檔案從 Windows 電腦傳輸到目標 Linux 電腦。 在本教學課程中，我們會從 Windows 上執行的 Bash Shell (終端機視窗) 將檔案移至 Linux。

1. 在 Windows 電腦上安裝支援 **scp** (安全複製) 和 **ssh** (遠端登入) 命令的 Bash Shell。 兩個範例如下：

   * [適用於 Linux 的 Windows 子系統](https://msdn.microsoft.com/commandline/wsl/about) (Windows 10)
   * Git Bash Shell ([https://git-scm.com/downloads](https://git-scm.com/downloads))

1. 在 Windows 上開啟 Bash 工作階段。

## <a name="copy-the-backup-file-to-linux"></a><a id="scp"></a> 將備份檔案複製到 Linux

1. 在您的 Bash 工作階段中，瀏覽至包含備份檔案的目錄。 例如：

   ```bash
   cd 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\'
   ```

1. 使用 **scp** 命令將檔案傳輸到目標 Linux 電腦。 下列範例會將 **YourDB.bak** 傳輸到 Linux 伺服器 (IP 位址為 *192.0.2.9*) 上的 *user1* 主目錄：

   ```bash
   scp YourDB.bak user1@192.0.2.9:./
   ```
   ![scp 命令](./media/sql-server-linux-migrate-restore-database/scp-command.png)

> [!TIP]
> 使用 scp 來進行檔案傳輸有一些替代方案。 其中一個是使用 [Samba](https://help.ubuntu.com/community/Samba) 來設定 Windows 與 Linux 之間的 SMB 網路共用。 如需 Ubuntu 的逐步解說，請參閱 [How to Create a Network Share Via Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!) (如何透過 Samba 建立網路共用)。 建立之後，您就可以從 Windows 將它當作網路檔案共用來存取，例如 **\\\\machinenameorip\\share**。

## <a name="move-the-backup-file-before-restoring"></a>在還原之前移動備份檔案

此時，備份檔案是在您 Linux 伺服器上的使用者主目錄中。 將資料庫還原至 SQL Server 之前，您必須將備份放在 **/var/opt/mssql** 子目錄中。

1. 在相同的 Windows Bash 工作階段中，使用 **ssh** 從遠端連線到您的目標 Linux 電腦。 下列範例會以使用者 **user1** 的身分連線到 Linux 電腦 **192.0.2.9**。

   ```bash
   ssh user1@192.0.2.9
   ```

   您現在正在遠端 Linux 伺服器上執行命令。

1. 進入超級使用者模式。

   ```bash
   sudo su
   ```

1. 建立新的備份目錄。 如果目錄已存在，-p 參數就不會執行任何動作。

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

1. 將備份檔案移至該目錄。 在下列範例中，備份檔案位於 *user1* 主目錄中。 請變更命令，使其符合備份檔案的位置和檔案名稱。

   ```bash
   mv /home/user1/YourDB.bak /var/opt/mssql/backup/
   ```

1. 結束超級使用者模式。

   ```bash
   exit
   ```

## <a name="restore-your-database-on-linux"></a>在 Linux 上還原資料庫

若要還原資料庫備份，您可以使用 **RESTORE DATABASE** Transact-SQL (TQL) 命令。

> [!NOTE]
> 下列步驟使用 **sqlcmd** 工具。 如果您尚未安裝 SQL Server 工具，請參閱[在 Linux 上安裝 SQL Server 命令列工具](sql-server-linux-setup-tools.md)。

1. 在相同的終端機中啟動 **sqlcmd**。 下列範例會使用 **SA** 使用者連線到本機 SQL Server 執行個體。 請在出現提示時輸入密碼，或是新增 **-P** 參數來指定密碼。

   ```bash
   sqlcmd -S localhost -U SA
   ```

1. 在 `>1` 提示字元中，輸入下列 **RESTORE DATABASE** 命令，並在每一行之後按 ENTER 鍵 (您無法一次複製並貼上整個多行命令)。 請以您的資料庫名稱取代所有出現的 `YourDB`。

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```

   您應該會收到已成功還原資料庫的訊息。

   `RESTORE DATABASE` 可能會傳回如下列範例所示的錯誤：

   ```bash
   File 'YourDB_Product' cannot be restored to 'Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf'. Use WITH MOVE to identify a valid location for the file.
   Msg 5133, Level 16, State 1, Server servername, Line 1
   Directory lookup for the file "Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf" failed with the operating system error 2(The system cannot find the file specified.).
   ```
   
   在此情況下，資料庫包含次要檔案。 如果未在 `RESTORE DATABASE` 的 `MOVE` 子句中指定這些檔案，還原程式會嘗試在與原始伺服器相同的路徑中建立這些檔案。 

   您可以列出備份中包含的所有檔案：
   ```sql
   RESTORE FILELISTONLY FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   GO
   ```
   您應該會取得如下所示的清單 (只列出兩個第一個資料行)：
   ```sql
   LogicalName         PhysicalName                                                                 ..............
   ----------------------------------------------------------------------------------------------------------------------
   YourDB              Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB.mdf          ..............
   YourDB_Product      Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Product.ndf  ..............
   YourDB_Customer     Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Customer.ndf ..............
   YourDB_log          Z:\Microsoft SQL Server\MSSQL11.GLOBAL\MSSQL\Data\YourDB\YourDB_Log.ldf      ..............
   ```
   
   您可以使用這份清單來為其他檔案建立 `MOVE` 子句。 在此範例中，`RESTORE DATABASE` 是：

   ```sql
   RESTORE DATABASE YourDB
   FROM DISK = '/var/opt/mssql/backup/YourDB.bak'
   WITH MOVE 'YourDB' TO '/var/opt/mssql/data/YourDB.mdf',
   MOVE 'YourDB_Product' TO '/var/opt/mssql/data/YourDB_Product.ndf',
   MOVE 'YourDB_Customer' TO '/var/opt/mssql/data/YourDB_Customer.ndf',
   MOVE 'YourDB_Log' TO '/var/opt/mssql/data/YourDB_Log.ldf'
   GO
   ```


1. 列出伺服器上的所有資料庫，以確認還原。 應該會列出已還原的資料庫。

   ```sql
   SELECT Name FROM sys.Databases
   GO
   ```

1. 在您移轉的資料庫上執行其他查詢。 下列命令會將內容切換至 **YourDB** 資料庫，並從它的其中一個資料表選取資料列。

   ```sql
   USE YourDB
   SELECT * FROM YourTable
   GO
   ```

1. 當您完成使用 **sqlcmd** 時，請鍵入 `exit`。

1. 當您完成在遠端 **ssh** 工作階段中的工作時，請再次鍵入 `exit`。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何在 Windows 上備份資料庫，並將其移至執行 SQL Server 的 Linux 伺服器。 您已了解如何︰
> [!div class="checklist"]
> * 使用 SSMS 和 Transact-SQL 在 Windows 上建立備份檔案
> * 在 Windows 上安裝 Bash Shell
> * 使用 **scp** 將備份檔案從 Windows 移至 Linux
> * 使用 **ssh** 從遠端連線到您的 Linux 電腦
> * 重新放置備份檔案以準備進行還原
> * 使用 **sqlcmd** 來執行 Transact-SQL 命令
> * 使用 **RESTORE DATABASE** 命令還原資料庫備份 
> * 執行查詢以確認移轉

接下來，請探索 Linux 上 SQL Server 的其他移轉案例。 

> [!div class="nextstepaction"]
>[將資料庫移轉至 Linux 上的 SQL Server](sql-server-linux-migrate-overview.md)
