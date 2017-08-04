---
title: "從 Windows 的 SQL Server 資料庫移轉至 Linux |Microsoft 文件"
description: "本主題說明如何取得 Windows 上的 SQL Server 資料庫備份，並將它還原到執行 SQL Server 2017 RC2 的 Linux 機器。"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9ac64d1a-9fe5-446e-93c3-d17b8f55a28f
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 2e23ba46381b1fb80b8ac335f6d7630f02a222bb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="migrate-a-sql-server-database-from-windows-to-linux-using-backup-and-restore"></a>從 Windows 的 SQL Server 資料庫移轉至 Linux 使用備份與還原

SQL Server 的備份和還原功能會從在 Windows 上的 SQL Server 資料庫移轉至 SQL Server 2017 RC2 Linux 上的建議的方式。 本主題提供這項技術的逐步指示。 在本教學課程中，您將會：

- 下載 Windows 電腦上的 AdventureWorks 備份檔案
- 傳送到 Linux 機器的備份
- 使用 TRANSACT-SQL 命令將資料庫還原

> [!NOTE] 
> 本教學課程假設您已安裝[SQL Server 2017 RC2](sql-server-linux-setup.md)和[SQL Server 工具](sql-server-linux-setup-tools.md)目標 Linux 伺服器上。

## <a name="download-the-adventureworks-database-backup"></a>下載 AdventureWorks 資料庫備份

雖然您可以使用相同的步驟還原任何資料庫，在 AdventureWorks 範例資料庫會提供良好的範例。 它是現有的資料庫備份檔案。

>[!NOTE] 
> 若要將資料庫還原至 SQL Server on Linux，則必須採取從 SQL Server 2014 或 SQL Server 2016 的來源備份。 SQL Server 組建編號的備份不能大於還原 SQL Server 組建編號。  

1. 在您的 Windows 電腦，請移至[https://msftdbprodsamples.codeplex.com/downloads/get/880661](https://msftdbprodsamples.codeplex.com/downloads/get/880661)並下載**Adventure Works 2014 完整 Database Backup.zip**。

   > [!TIP] 
   > 雖然本教學課程示範如何備份和還原 Windows 和 Linux 之間，您也可以直接到 Linux 機器下載 AdventureWorks 範例使用在 Linux 上的瀏覽器。

2. 開啟 zip 檔案，並將您的電腦上資料夾 AdventureWorks2014.bak 檔案解壓縮。

## <a name="transfer-the-backup-file-to-linux"></a>備份的檔案傳輸至 Linux

若要還原資料庫，您必須先將備份檔案從 Windows 電腦傳輸到目標 Linux 機器。

1. 適用於 Windows、 安裝 Bash 殼層。 有數個選項，包括下列：

   - 下載的開放原始碼 Bash 殼層中，例如[PuTTY](http://www.putty.org/)。
   - 或者，在 Windows 10 上使用 新[內建 Bash 殼層 (beta)](https://msdn.microsoft.com/en-us/commandline/wsl/about)。
   - 或者，如果您使用 Git 時，使用[Git Bash 殼層](https://git-scm.com/downloads)。

2. 開啟 Bash 殼層 （終端機），並瀏覽至目錄包含**AdventureWorks2014.bak**。

3. 使用**scp** （安全複製） 命令，將檔案傳輸至目標 Linux 機器。 下列範例傳輸**AdventureWorks2014.bak**的主目錄的*user1*指名的伺服器上*linuxserver1*。

   ```bash
   sudo scp AdventureWorks2014.bak user1@linuxserver1:./
   ```
   
   在上述範例中，您可以改為提供的 IP 位址，來取代的伺服器名稱。

有多個使用 scp 的替代方案。 其中一個是使用[Samba](https://help.ubuntu.com/community/Samba)設定 Windows 和 Linux 之間 SMB 網路共用。 如需 Ubuntu 的逐步解說，請參閱[如何建立網路共用透過 Samba](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)。 一旦建立，您可以存取網路檔案共用在 Windows 中的這類 **\\ \\machinenameorip\\共用**。

## <a name="move-the-backup-file"></a>將備份檔案

此時，備份檔案是在 Linux 伺服器上。 之前將資料庫還原到 SQL Server，您必須將備份放的子目錄中**/var/opt/mssql**。

1. 開啟包含備份目標 Linux 機器上的終端機。

2. 進入進階使用者模式。

   ```bash
   sudo su
   ```

3. 建立新的備份目錄。 如果目錄已經存在-p 參數沒有任何作用。

   ```bash
   mkdir -p /var/opt/mssql/backup
   ```

4. 將備份檔案移至該目錄。 在下列範例中，備份檔案所在的主目錄*user1*。 變更要比對的位置命令**AdventureWorks2014.bak**您的電腦上。

   ```bash
   mv /home/user1/AdventureWorks2014.bak /var/opt/mssql/backup/
   ```

5. 結束進階使用者模式。

   ```bash
   exit
   ```

## <a name="restore-the-database-backup"></a>還原資料庫備份

若要還原備份，您可以使用還原資料庫 TRANSACT-SQL (TQL) 命令。

> [!NOTE] 
> 下列步驟使用 sqlcmd 工具。 如果您尚未安裝 SQL Server 工具，請參閱[安裝 SQL Server on Linux](sql-server-linux-setup.md)。

1. 在相同的終端機中，啟動**sqlcmd**。 下列範例會連接到本機的 SQL Server 執行個體與*SA*使用者。 輸入提示或使用-P 參數指定的密碼時的密碼。

   ```bash
   sqlcmd -S localhost -U SA
   ```

2. 連接之後，請輸入下列**還原資料庫**命令，在每一行後面按 ENTER。 還原下例**AdventureWorks2014.bak**檔案從*/var/opt/mssql/backup*目錄。

   ```sql
   RESTORE DATABASE AdventureWorks
   FROM DISK = '/var/opt/mssql/backup/AdventureWorks2014.bak'
   WITH MOVE 'AdventureWorks2014_Data' TO '/var/opt/mssql/data/AdventureWorks2014_Data.mdf',
   MOVE 'AdventureWorks2014_Log' TO '/var/opt/mssql/data/AdventureWorks2014_Log.ldf'
   GO
   ```

   您應該會收到的訊息，將會成功還原資料庫。

3. 確認還原第一次將內容變更為 AdventureWorks 資料庫。 

   ```sql
   USE AdventureWorks
   GO
   ```

4. 執行下列查詢會列出中的前 10 大產品**Production.Products**資料表。

   ```sql
   SELECT TOP 10 Name, ProductNumber FROM Production.Product ORDER BY Name
   GO
   ```

![Production.Products 查詢輸出](./media/sql-server-linux-migrate-restore-database/sql-server-linux-adventureworks-query.png)

## <a name="next-steps"></a>後續的步驟

如需有關其他資料庫和資料移轉技術的詳細資訊，請參閱[將資料庫移轉至 SQL Server on Linux](sql-server-linux-migrate-overview.md)。 

