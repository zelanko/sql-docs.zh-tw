---
title: "檔案還原 (完整復原模式) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- file restores [SQL Server]
- full recovery model [SQL Server], performing restores
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- file restores [SQL Server], full recovery model
- restoring files [SQL Server], full recovery model
- Transact-SQL restore sequence
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: d2236a2a-4cf1-4c3f-b542-f73f6096e15c
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d5feafb861d0c0a9cb65f6c8a27d2bfa49d1465
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="file-restores-full-recovery-model"></a>檔案還原 (完整復原模式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  這個主題僅與在完整或大量載入復原模式下，包含多個檔案或檔案群組的資料庫有關。  
  
 檔案還原的目的是還原一個或多個損毀的檔案，而不還原整個資料庫。 檔案還原實例包含複製、向前復原及復原適當資料的單一還原順序。  
  
 如果正在還原的檔案群組為可讀寫，則必須在還原最後一個資料或差異備份之後，套用無間斷的記錄備份鏈結。 這會將檔案群組向前復原到位於記錄檔內目前使用中記錄檔記錄上的記錄檔記錄。 復原點通常接近記錄的結尾，但不一定如此。  
  
 如果正在還原的檔案群組為唯讀，通常沒有必要套用記錄備份，所以會略過。 如果是在檔案變成唯讀之後進行的備份，此備份就是要還原的最後一個備份。 向前復原會在目標點停止。  
  
 這些檔案還原實例如下：  
  
-   離線檔案還原  
  
     在 *「離線檔案還原」*(Offline File Restore) 中，還原損毀的檔案或檔案群組時，資料庫處於離線狀態。 在還原順序結束後，資料庫會恢復上線。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的所有版本都支援離線檔案還原。  
  
-   線上檔案還原  
  
     在 *「線上檔案還原」*(Online File Restore) 中，如果資料庫在還原期間處於線上，則在檔案還原期間也會處於線上。 不過，在還原作業期間，包含正在還原之檔案的每個檔案群組都會離線。 離線檔案群組中的所有檔案都復原後，檔案群組就會自動回到線上。  
  
     如需線上頁面和檔案還原支援的資訊，請參閱 [SQL Server 2016 版本支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。 如需線上還原的詳細資訊，請參閱[線上還原 (SQL Server)](../../relational-databases/backup-restore/online-restore-sql-server.md)。
  
    > [!TIP]  
    >  若您要讓資料庫離線以進行檔案還原，請在啟動還原順序之前，執行下列 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) 陳述式：ALTER DATABASE *database_name* SET OFFLINE。  
  
  
##  <a name="Overview"></a> 從檔案備份還原損壞的檔案  
  
1.  在還原一個或多個損壞的檔案之前，請嘗試建立 [結尾記錄備份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
     如果記錄已經損壞，就無法建立結尾記錄備份，而且您必須還原整個資料庫。  
  
     如需如何備份交易記錄的相關資訊，請參閱[交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)。  
  
    > [!IMPORTANT]  
    >  如果是離線檔案還原，一定要在檔案還原之前進行結尾記錄備份。 如果是線上檔案還原，一定要在檔案還原之後進行記錄備份。 為了讓檔案可以復原到與資料庫其餘部分一致的狀態，進行這個記錄備份有其必要。  
  
2.  從每個損毀檔案的最近一次檔案備份還原該檔案。  
  
3.  還原每個已還原檔案的最新差異檔案備份 (如果有的話)。  
  
4.  依序還原交易記錄備份，從包含最舊還原檔案的備份開始，到步驟 1 所建立的結尾記錄備份結束。  
  
     您必須還原在檔案備份之後建立的交易記錄備份，才能讓資料庫恢復一致的狀態。 交易記錄備份可以快速地向前復原，因為只需套用適用於還原檔案的變更。 還原個別檔案比還原整個資料庫更為理想，因為不需複製未受損的檔案，便可接著向前復原。 不過，仍然需要讀取記錄備份的整個鏈結。  
  
5.  復原資料庫。  
  
> [!NOTE]  
>  檔案備份可以用來將資料庫還原至較早的時間點。 若要這樣做，您必須還原整個檔案備份組，然後依序還原交易記錄備份，以回到上一次還原的檔案備份結尾之後的目標時間點。 如需時間點還原的詳細資訊，請參閱[將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
## <a name="transact-sql-restore-sequence-for-an-offline-file-restore-full-recovery-model"></a>離線檔案還原的 Transact-SQL 還原順序 (完整復原模式)  
 檔案還原實例包含複製、向前復原及復原適當資料的單一還原順序。  
  
 本節說明檔案還原順序的基本 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 選項。 會省略與這個檔案還原無關的語法和詳細資料。  
  
 下列範例還原順序顯示如何使用 WITH NORECOVERY 來離線還原兩個次要檔案 ( `A` 和 `B`)。 接下來，此範例會以 NORECOVERY 套用這兩個記錄備份，然後再使用 WITH RECOVERY 套用結尾記錄備份以進行還原。  
  
> [!NOTE]  
>  下列範例還原順序是透過讓檔案離線來啟動，然後建立結尾記錄備份。  
  
```  
--Take the file offline.  
ALTER DATABASE database_name MODIFY FILE SET OFFLINE;  
-- Back up the currently active transaction log.  
BACKUP LOG database_name  
   TO <tail_log_backup>  
   WITH NORECOVERY;  
GO   
-- Restore the files.  
RESTORE DATABASE database_name FILE=name   
   FROM <file_backup_of_file_A>   
   WITH NORECOVERY;  
RESTORE DATABASE database_name FILE=<name> ......  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
-- Restore the log backups.  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <tail_log_backup>   
   WITH RECOVERY;  
```  
  
## <a name="examples"></a>範例  
  
-   [範例：線上還原讀寫檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
-   [範例：離線還原主要檔案群組與另一個檔案群組 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **還原檔案和檔案群組**  
  
-   [將檔案還原到新位置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [還原檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
  
## <a name="see-also"></a>另請參閱  
 [備份與還原：互通性與共存性 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [完整檔案備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
