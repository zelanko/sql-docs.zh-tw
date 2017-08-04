---
title: "備份和還原在 Linux 上的 SQL Server 資料庫 |Microsoft 文件"
description: "瞭解如何備份和還原在 Linux 上的 SQL Server 資料庫。"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: d30090fb-889f-466e-b793-5f284fccc4e6
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 6bd05a89f0c06bc03de931b898be18f3cbea0c8c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="backup-and-restore-sql-server-databases-on-linux"></a>在 Linux 上的備份和還原 SQL Server 資料庫

您可以從 Linux 上的 SQL Server 2017 RC2 採取資料庫的備份，與為其他平台的相同工具。 在 Linux 伺服器上，您可以使用`sqlcmd`連接到 SQL Server 並進行備份。 在 Windows 中，您可以連接到 SQL Server on Linux，並進行備份與使用者介面。 備份的功能是相同的跨平台。 例如，備份資料庫，在本機、 遠端磁碟機，或為[Microsoft Azure Blob 儲存體服務](http://msdn.microsoft.com/library/dn435916.aspx)。 

## <a name="backup-with-sqlcmd"></a>使用 sqlcmd 的備份

在下列範例中`sqlcmd`會連接到本機 SQL Server 執行個體並呼叫使用者資料庫的備份完整`demodb`。

```bash
sqlcmd -H localhost -U SA -Q "BACKUP DATABASE [demodb] TO DISK = N'var/opt/mssql/data/demodb.bak' WITH NOFORMAT, NOINIT, NAME = 'demodb-full', SKIP, NOREWIND, NOUNLOAD, STATS = 10"
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

### <a name="backup-log-with-sqlcmd"></a>使用 sqlcmd 的備份記錄檔

在下列範例中，`sqlcmd`會連接到本機 SQL Server 執行個體，並採用結尾記錄備份。 結尾記錄備份完成之後，資料庫會處於還原狀態。 

```bash
sqlcmd -H localhost -U SA -Q "BACKUP LOG [demodb] TO  DISK = N'var/opt/mssql/data/demodb_LogBackup_2016-11-14_18-09-53.bak' WITH NOFORMAT, NOINIT,  NAME = N'demodb_LogBackup_2016-11-14_18-09-53', NOSKIP, NOREWIND, NOUNLOAD,  NORECOVERY ,  STATS = 5"
```


## <a name="restore-with-sqlcmd"></a>還原使用 sqlcmd

在下列範例中`sqlcmd`會連接到 SQL Server 的本機執行個體，並會將資料庫還原。

```bash
sqlcmd -H localhost -U SA -Q "RESTORE DATABASE [demodb] FROM  DISK = N'var/opt/mssql/data/demodb.bak' WITH  FILE = 1,  NOUNLOAD,  REPLACE,  STATS = 5"
```

## <a name="backup-and-restore-with-sql-server-management-studio-ssms"></a>備份及還原與 SQL Server Management Studio (SSMS)

您可以從 Windows 電腦使用 SSMS，連接到 Linux 資料庫並進行備份，以透過使用者介面。 

>[!NOTE] 
> 使用最新版本的 SSMS 連接到 SQL Server。 若要下載並安裝最新版本，請參閱[下載 SSMS](http://msdn.microsoft.com/library/mt238290.aspx)。 

備份使用 SSMS 逐步解說下列步驟。 

1. 啟動 SSMS 並連接到在 Linux 上的 SQL Server 2017 RC2 中的伺服器。

1. 在 物件總管 中，以滑鼠右鍵按一下您在資料庫上，按一下**工作**，然後按一下 **備份...**.

1. 在**資料庫備份**] 對話方塊中，確認參數和選項，然後按一下 [**確定**。
 
SQL Server 完成資料庫備份。

如需詳細資訊，請參閱[使用 SSMS 管理 SQL Server on Linux](sql-server-linux-manage-ssms.md)。

### <a name="restore-with-sql-server-management-studio-ssms"></a>Restore with SQL Server Management Studio (SSMS) 

下列步驟會引導您完成使用 SSMS 將資料庫還原。

1. 在 SSMS 中以滑鼠右鍵按一下**資料庫**按一下**還原資料庫...**. 

1. 在下**來源**按一下**裝置：**然後按一下省略符號 （...）。

1. 找出您的資料庫備份檔案並按一下**確定**。 

1. 在下**還原計劃**，確認備份檔案和設定。 按一下 **[確定]**。 

1. SQL Server 還原資料庫。 

## <a name="see-also"></a>另請參閱

* [建立完整資料庫備份 (SQL Server)](http://msdn.microsoft.com/library/ms187510.aspx)
* [備份交易記錄 (SQL Server)](http://msdn.microsoft.com/library/ms179478.aspx)
* [BACKUP (Transact-SQL)](http://msdn.microsoft.com/library/ms186865.aspx)
* [SQL Server 備份至 URL](http://msdn.microsoft.com/library/dn435916.aspx)

