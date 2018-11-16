---
title: 檔案還原 (簡單復原模式) | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server]
- simple recovery model [SQL Server]
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- Transact-SQL restore sequence
- restoring files [SQL Server], simple recovery model
- file restores [SQL Server], simple recovery model
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: b6d07386-7c6f-4cc6-be32-93289adbd3d6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7b68a59129df88c1ea40736ec90a73d0b7e1c5ae
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673617"
---
# <a name="file-restores-simple-recovery-model"></a>檔案還原 (簡單復原模式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  這個主題僅與至少包含一個唯讀次要檔案群組的簡單模式資料庫有關。  
  
 檔案還原的目的是還原一個或多個損毀的檔案，而不還原整個資料庫。 在簡單復原模式下，僅支援唯讀檔案的檔案備份。 透過還原資料庫或部分備份，永遠一併還原主要檔案群組和讀取/寫入次要檔案群組。  
  
 這些檔案還原實例如下：  
  
-   離線檔案還原  
  
     在 *「離線檔案還原」*(Offline File Restore) 中，還原損毀的檔案或檔案群組時，資料庫處於離線狀態。 在還原順序結束後，資料庫會恢復上線。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的所有版本都支援離線檔案還原。  
  
-   線上檔案還原  
  
     在 *「線上檔案還原」*(Online File Restore) 中，如果資料庫在還原期間處於線上，則在檔案還原期間也會處於線上。 不過，在還原作業期間，包含正在還原之檔案的每個檔案群組都會離線。 離線檔案群組中的所有檔案都復原後，檔案群組就會自動回到線上。  
  
     如需線上頁面和檔案還原支援的資訊，請參閱 [Database Engine 功能及工作](https://msdn.microsoft.com/library/d9efe145-3306-4d61-bd77-e2af43e19c34)。 如需線上還原的詳細資訊，請參閱[線上還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)。  
  
    > [!TIP]  
    >  若您要讓資料庫離線以進行檔案還原，請在啟動還原順序之前，執行下列 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) 陳述式：ALTER DATABASE *database_name* SET OFFLINE。  
  
 **本主題內容：**  
  
-   [簡單復原模式下的檔案和檔案群組還原概觀](#Overview)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="Overview"></a> 簡單復原模式下的檔案和檔案群組還原概觀  
 檔案還原案例是單一還原順序，涵蓋複製、向前復原及復原適當資料等動作，如下所示：  
  
1.  從最新的檔案備份來還原每一個損毀的檔案。  
  
2.  針對每個已還原的檔案，還原其最新的差異檔案備份，並復原資料庫。  
  
### <a name="transact-sql-steps-for-file-restore-sequence-simple-recovery-model"></a>檔案還原順序的 Transact-SQL 步驟 (簡單復原模式)  
 本節顯示簡單檔案還原順序的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)][RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 選項。 會省略與這個檔案還原無關的語法和詳細資料。  
  
 還原順序只包含兩個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 第一個陳述式會還原次要檔案 (即 `A`檔案)，而此檔案是使用 WITH NORECOVERY 進行還原。 第二項作業還原其他兩個檔案 ( `B` 和 `C` )，而這些檔案是使用 WITH RECOVERY 從不同的備份裝置進行還原。  
  
1.  RESTORE DATABASE *database* FILE **=***name_of_file_A*  
  
     FROM *file_backup_of_file_A*  
  
     WITH NORECOVERY **;**  
  
2.  RESTORE DATABASE *database* FILE **=***name_of_file_B***,***name_of_file_C*  
  
     FROM *file_backup_of_files_B_and_C*  
  
     WITH RECOVERY **;**  
  
### <a name="examples"></a>範例  
  
-   [範例：線上還原唯讀檔案 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [範例：離線還原主要檔案群組與另一個檔案群組 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **還原檔案和檔案群組**  
  
-   [以覆蓋現有檔案的方式還原檔案與檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [還原檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [還原檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restore.SqlRestore 方法 (伺服器) (SMO)](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.restore.sqlrestore.aspx)   
  
## <a name="see-also"></a>另請參閱  
 [備份與還原：互通性與共存性 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [完整檔案備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
