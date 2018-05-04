---
title: 備份和還原在 Linux 上的 SQL Server 資料庫 |Microsoft 文件
description: 瞭解如何備份和還原在 Linux 上的 SQL Server 資料庫。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/14/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: 2bfd68973c255bbbe0aacfd8caa350e9f979efbe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>在 Linux 上的備份和還原 SQL Server 資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

您可以從 Linux 上的 SQL Server 2017 採取資料庫的備份，與為其他平台的相同工具。 在 Linux 伺服器上，您可以使用**sqlcmd**連接到 SQL Server 並進行備份。 在 Windows 中，您可以連接到 SQL Server on Linux，並進行備份與使用者介面。 備份的功能是相同的跨平台。 例如，備份資料庫，在本機、 遠端磁碟機，或為[Microsoft Azure Blob 儲存體服務](../relational-databases/backup-restore/sql-server-backup-to-url.md)。

## <a name="backup-a-database"></a>備份資料庫

在下列範例中**sqlcmd**會連接到本機 SQL Server 執行個體並呼叫使用者資料庫的備份完整`demodb`。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

當您執行命令時，SQL Server 將會提示輸入密碼。 您輸入密碼之後，殼層將會傳回備份進度的結果。 例如：

```
Password:
10 percent processed.
21 percent processed.
32 percent processed.
40 percent processed.
51 percent processed.
61 percent processed.
72 percent processed.
80 percent processed.
91 percent processed.
Processed 296 pages for database 'demodb', file 'demodb' on file 1.
100 percent processed.
Processed 2 pages for database 'demodb', file 'demodb_log' on file 1.
BACKUP DATABASE successfully processed 298 pages in 0.064 seconds (36.376 MB/sec).
```

### <a name="backup-the-transaction-log"></a>備份交易記錄檔

如果您的資料庫處於完整復原模式，您也可以進行更細微的還原選項的交易記錄備份。 在下列範例中， **sqlcmd**會連接到本機 SQL Server 執行個體，並接受交易記錄備份。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>還原資料庫

在下列範例中**sqlcmd**會連接到本機 SQL Server 執行個體，並根據 demodb 資料庫還原。 請注意，`NORECOVERY`選項用來允許其他的還原作業的記錄檔的備份。 如果您不打算還原額外的記錄檔，移除`NORECOVERY`選項。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> 如果您不小心使用 NORECOVERY，但不是需要額外的記錄檔備份，執行命令`RESTORE DATABASE demodb`不使用其他參數。 這會完成還原，並讓資料庫保持運作。

### <a name="restore-the-transaction-log"></a>還原交易記錄檔

下列命令會還原先前的交易記錄備份。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>備份及還原與 SQL Server Management Studio (SSMS)

您可以從 Windows 電腦使用 SSMS，連接到 Linux 資料庫並進行備份，以透過使用者介面。

>[!NOTE] 
> 使用最新版本的 SSMS 連接到 SQL Server。 若要下載並安裝最新版本，請參閱[下載 SSMS](../ssms/download-sql-server-management-studio-ssms.md)。 如需有關如何使用 SSMS 的詳細資訊，請參閱[使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

備份使用 SSMS 逐步解說下列步驟。 

1. 啟動 SSMS 並連接到在 Linux 上的 SQL Server 2017 中的伺服器。

1. 在 物件總管 中，以滑鼠右鍵按一下您在資料庫上，按一下**工作**，然後按一下 **備份...**.

1. 在**資料庫備份**] 對話方塊中，確認參數和選項，然後按一下 [**確定**。
 
SQL Server 完成資料庫備份。

### <a name="restore-with-sql-server-management-studio-ssms"></a>Restore with SQL Server Management Studio (SSMS) 

下列步驟會引導您完成使用 SSMS 將資料庫還原。

1. 在 SSMS 中以滑鼠右鍵按一下**資料庫**按一下**還原資料庫...**. 

1. 在下**來源**按一下**裝置：**然後按一下省略符號 （...）。

1. 找出您的資料庫備份檔案並按一下**確定**。 

1. 在下**還原計劃**，確認備份檔案和設定。 按一下 **[確定]**。 

1. SQL Server 還原資料庫。 

## <a name="see-also"></a>另請參閱

* [建立完整資料庫備份 (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [備份交易記錄 (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
