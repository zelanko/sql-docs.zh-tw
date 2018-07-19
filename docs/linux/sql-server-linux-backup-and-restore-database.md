---
title: 備份和還原在 Linux 上的 SQL Server 資料庫 |Microsoft Docs
description: 了解如何備份和還原在 Linux 上的 SQL Server 資料庫。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/14/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.openlocfilehash: 6e4699fb2ffadc3aaad73c4032073ff8567c856c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38006090"
---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>在 Linux 上的備份和還原 SQL Server 資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

您可以備份資料庫從 SQL Server 2017 Linux 上使用相同的工具，為其他平台。 在 Linux 伺服器上，您可以使用**sqlcmd**連接到 SQL Server，並進行備份。 從 Windows，您可以連接到 Linux 上的 SQL Server，並進行備份與使用者介面。 備份的功能是相同的跨平台。 在本機、 遠端磁碟機，或為，比方說，備份的資料庫[Microsoft Azure Blob 儲存體服務](../relational-databases/backup-restore/sql-server-backup-to-url.md)。

## <a name="backup-a-database"></a>備份資料庫

在下例**sqlcmd**會連接到本機的 SQL Server 執行個體，並採用完整備份使用者資料庫呼叫`demodb`。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'/var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
```

當您執行命令時，SQL Server 將會提示輸入密碼。 您輸入密碼之後，命令介面會傳回備份進度的結果。 例如：

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

如果您的資料庫處於完整復原模式，您也可以進行更細微的還原選項的交易記錄備份。 在下列範例中， **sqlcmd**會連接到本機的 SQL Server 執行個體，並接受交易記錄備份。

```bash
sqlcmd -S localhost -U SA -Q "BACKUP LOG [demodb] TO DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak' WITH NOFORMAT, NOINIT, NAME = N'demodb_LogBackup', NOSKIP, NOREWIND, NOUNLOAD, STATS = 5"
```

## <a name="restore-a-database"></a>還原資料庫

在下例**sqlcmd**連接到 SQL Server 的本機執行個體，並還原 demodb 資料庫。 請注意，`NORECOVERY`選項用來允許額外的還原作業的記錄檔的備份。 如果您不打算還原其他的記錄檔，移除`NORECOVERY`選項。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE DATABASE [demodb] FROM DISK = N'/var/opt/mssql/data/demodb.bak' WITH FILE = 1, NOUNLOAD, REPLACE, NORECOVERY, STATS = 5"
```

> [!TIP]
> 如果您不小心使用 with NORECOVERY，但不是需要額外的記錄檔備份，執行命令`RESTORE DATABASE demodb`搭配任何其他參數。 這會完成還原，並讓資料庫保持運作。

### <a name="restore-the-transaction-log"></a>還原交易記錄檔

下列命令會還原先前的交易記錄備份。

```bash
sqlcmd -S localhost -U SA -Q "RESTORE LOG demodb FROM DISK = N'/var/opt/mssql/data/demodb_LogBackup.bak'"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>備份及還原與 SQL Server Management Studio (SSMS)

您可以從 Windows 電腦使用 SSMS，以連線至 Linux 資料庫並進行備份，以透過使用者介面。

>[!NOTE] 
> 您可以使用最新版的 SSMS 來連接到 SQL Server。 若要下載並安裝最新版本，請參閱[下載 SSMS](../ssms/download-sql-server-management-studio-ssms.md)。 如需有關如何使用 SSMS 的詳細資訊，請參閱 <<c0> [ 使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

下列步驟會逐步進行使用 SSMS 備份。 

1. 啟動 SSMS 並連接到您在 Linux 上的 SQL Server 2017 中的伺服器。

1. 在 物件總管 中，以滑鼠右鍵按一下您的資料庫中，按一下**任務**，然後按一下 **備份...**.

1. 在 **資料庫備份** 對話方塊中，確認參數和選項，然後按一下 **確定**。
 
SQL Server 完成資料庫備份。

### <a name="restore-with-sql-server-management-studio-ssms"></a>還原使用 SQL Server Management Studio (SSMS) 

下列步驟會引導您使用 SSMS 將資料庫還原。

1. 在 SSMS 中以滑鼠右鍵按一下**資料庫**，按一下 **還原資料庫...**. 

1. 底下**來源**按一下 **裝置：** ，然後按一下 省略符號 （...）。

1. 找出您的資料庫備份檔案，然後按一下**確定**。 

1. 底下**還原計劃**，確認備份檔案和設定。 按一下 [確定] 。 

1. SQL Server 還原資料庫。 

## <a name="see-also"></a>另請參閱

* [建立完整資料庫備份 (SQL Server)](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)
* [備份交易記錄 (SQL Server)](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)
* [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md)
* [SQL Server 備份至 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)
