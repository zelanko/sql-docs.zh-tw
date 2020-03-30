---
title: 在 Linux 上備份與還原 SQL Server 資料庫
description: 了解如何在 Linux 上備份與還原 SQL Server 資料庫。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: 88ef620a24bc2ce623ea6fb072871dadeffbcf6d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68823109"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>在 Linux 上備份與還原 SQL Server 資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

您可以使用許多不同的選項，從 Linux 上的 SQL Server 2017 備份資料庫。 在 Linux 伺服器上，您可以使用 **sqlcmd** 來連線至 SQL Server 並進行備份。 在 Windows 中，您可以連線至 Linux 上的 SQL Server，並藉由使用者介面來進行備份。 備份功能在不同平台上都相同。 例如，您可以在本機將資料庫備份至遠端磁碟機或 [Microsoft Azure Blob 儲存體服務。](../relational-databases/backup-restore/sql-server-backup-to-url.md)

## <a name="backup-a-database"></a>備份資料庫

在下列範例中，**sqlcmd** 會連線至本機 SQL Server 執行個體，並取得稱為 `demodb` 的使用者資料庫完整備份。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

執行命令時，SQL Server 會提示您輸入密碼。 輸入密碼之後，Shell 會傳回備份進度的結果。 例如：

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

### <a name="backup-the-transaction-log"></a>備份交易記錄

如果您的資料庫處於完整復原模式，您也可以進行交易記錄備份，以獲得更細微的還原選項。 在下列範例中，**sqlcmd** 會連線至本機 SQL Server 執行個體，並進行交易記錄備份。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>還原資料庫

在下列範例中，**sqlcmd** 會連線至 SQL Server 的本機執行個體，並還原 demodb 資料庫。 請注意，`NORECOVERY` 選項用於允許記錄檔案備份的其他還原。 如果您不打算還原其他記錄檔，請移除 `NORECOVERY` 選項。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> 如果您不小心使用 NORECOVERY，但沒有其他記錄檔備份，請執行命令 `RESTORE DATABASE demodb`，而不使用其他參數。 這會完成還原，並讓您的資料庫保持運作。

### <a name="restore-the-transaction-log"></a>還原交易記錄

下列命令會還原先前的交易記錄備份。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 進行備份和還原

您可以從 Windows 電腦使用 SSMS 連線至 Linux 資料庫，並透過使用者介面進行備份。

>[!NOTE] 
> 使用最新版的 SSMS 連線至 SQL Server。 若要下載並安裝最新版本，請參閱[下載 SSMS](../ssms/download-sql-server-management-studio-ssms.md)。 如需如何使用 SSMS 的詳細資訊，請參閱[使用 SSMS 管理 Linux 上的 SQL Server](sql-server-linux-manage-ssms.md)。

下列步驟會逐步解說如何使用 SSMS 進行備份。 

1. 啟動 SSMS，並連線至您在 Linux 上 SQL Server 2017 中的伺服器。

1. 在 [物件總管] 中，以滑鼠右鍵按一下資料庫，按一下 [工作]  ，然後按一下 [備份...]  。

1. 在 [備份資料庫]  對話方塊中，確認參數和選項，然後按一下 [確定]  。
 
SQL Server 完成資料庫備份。

### <a name="restore-with-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 還原 

下列步驟會逐步引導您使用 SSMS 還原資料庫。

1. 在 SSMS 中，以滑鼠右鍵按一下 [資料庫]  ，然後按一下 [還原資料庫...]  。 

1. 在 [來源]  下方按一下 [裝置：]  ，然後按一下省略符號 [...]。

1. 找出您的資料庫備份檔案，然後按一下 [確定]  。 

1. 在 [還原計畫]  下方，確認備份檔案和設定。 按一下 [確定]  。 

1. SQL Server 會還原資料庫。 

## <a name="see-also"></a>另請參閱

* [建立完整資料庫備份 (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [備份交易記錄 (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
