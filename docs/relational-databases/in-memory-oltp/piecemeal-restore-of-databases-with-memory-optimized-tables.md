---
title: 分次還原具有記憶體最佳化資料表的資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1305f3239f40fa6d699243e0512ce774da5109c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100225"
---
# <a name="piecemeal-restore-of-databases-with-memory-optimized-tables"></a>分次還原具有記憶體最佳化資料表的資料庫

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  具有記憶體最佳化資料表的資料庫支援分次還原，但受到下列一項限制。 如需分次備份和還原的詳細資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) 和[分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)。  
  
 記憶體最佳化的檔案群組必須與主要檔案群組同時備份和還原：  
  
-   如果您備份 (或還原) 主要檔案群組，您必須指定記憶體最佳化的檔案群組。  
  
-   若您備份 (或還原) 記憶體最佳化檔案群組，您必須指定主要檔案群組。  
  
 分次備份和還原的主要狀況包括：  
  
-   分次備份可縮小備份大小。 以下是一些範例：  
  
    -   設定在不同的時間或日期進行資料庫備份，可降低對工作負載的影響。 例如，非常大型的資料庫 (大於 1 TB) 無法在配置給資料庫維護的時間內完成完整資料庫備份。 在此情況下，您可以使用分次備份將整個資料庫分成多次備份。  
  
    -   如果檔案群組標示為唯讀，在標示為唯讀之後，便不需要交易記錄備份。 您可以選擇在標示為唯讀之後只備份檔案群組一次。  
  
-   分次還原。  
  
    -   分次還原的目標是要讓資料庫的重要部分恢復連線狀態，而不需要等候所有資料。 例如，如果資料庫具有分割資料，會很少使用這類舊的分割區。 您可以僅在必要時才進行還原。 類似的範例為包含歷程記錄資料的檔案群組。  
  
    -   透過頁面修復，您可以還原特定頁面來修正損毀的頁面。 如需詳細資訊，請參閱[還原頁面 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)。  
  
## <a name="samples"></a>範例  
 這些範例使用下列結構描述：  
  
```sql
CREATE DATABASE imoltp
    ON PRIMARY (
        name = imoltp_primary1,
        filename = 'c:\data\imoltp_data1.mdf')
    LOG ON (
        name = imoltp_log,
        filename = 'c:\data\imoltp_log.ldf');
    GO  
  
ALTER DATABASE imoltp
    ADD FILE (
        name = imoltp_primary2,
        filename = 'c:\data\imoltp_data2.ndf');
GO  
  
ALTER DATABASE imoltp
    ADD FILEGROUP imoltp_secondary;

ALTER DATABASE imoltp
    ADD FILE (
        name = imoltp_secondary,
        filename = 'c:\data\imoltp_secondary.ndf')
            TO FILEGROUP imoltp_secondary;
GO  
  
ALTER DATABASE imoltp
    ADD FILEGROUP imoltp_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE imoltp
    ADD FILE (
        name = 'imoltp_mod1',
        filename = 'c:\data\imoltp_mod1')
            TO FILEGROUP imoltp_mod;

ALTER DATABASE imoltp
    ADD FILE (
        name = 'imoltp_mod2',
        filename = 'c:\data\imoltp_mod2')
            TO FILEGROUP imoltp_mod;
GO  
```  
  
### <a name="backup"></a>Backup  
 此範例會示範如何備份主要檔案群組和記憶體最佳化的檔案群組。 您必須同時指定主要檔案群組和記憶體最佳化的檔案群組。  
  
```sql
BACKUP database imoltp
    filegroup = 'primary',
    filegroup = 'imoltp_mod'
    to disk = 'c:\data\imoltp.dmp'
    with init;
```
  
 下列範例顯示主要檔案群組和記憶體最佳化檔案群組之外的檔案群組備份，其運作方式與沒有記憶體最佳化資料表的資料庫相似。 下列命令會備份次要檔案群組  
  
```sql
BACKUP database imoltp
    filegroup = 'imoltp_secondary'
    to disk = 'c:\data\imoltp_secondary.dmp'
    with init;
```
  
### <a name="restore"></a>Restore  
 下列範例顯示如何同時還原主要檔案群組和記憶體最佳化的檔案群組。  

```sql
RESTORE database imoltp
    filegroup = 'primary',
    filegroup = 'imoltp_mod'
    from disk = 'c:\data\imoltp.dmp'
    with
        partial,
        norecovery;

-- Restore the transaction log.

RESTORE LOG [imoltp]
    FROM DISK = N'c:\data\imoltp_log.dmp'
    WITH
        FILE = 1,
        NOUNLOAD,
        STATS = 10;
GO
```
  
 下一個範例顯示還原主要檔案群組和記憶體最佳化的檔案群組之外的檔案群組，類似於還原不具有記憶體最佳化資料表的資料庫  
  
```sql
RESTORE DATABASE [imoltp]
    FILE = N'imoltp_secondary'
    FROM DISK = N'c:\data\imoltp_secondary.dmp'
    WITH
        FILE = 1,
        RECOVERY,
        NOUNLOAD,
        STATS = 10;
GO
```

## <a name="see-also"></a>另請參閱  
 [備份、還原及復原記憶體最佳化資料表](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  

