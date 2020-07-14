---
title: 復原到記錄序號 (SQL Server) | Microsoft Docs
description: 在 SQL Server 中，您可使用記錄序號 (LSN) 來復原到特定時間點。 這項功能適用於工具廠商。
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log sequence numbers [SQL Server]
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- LSNs
- database recovery [SQL Server]
- database restores [SQL Server], point in time
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 56f5262fe130d391bf152d0924df814e15ffc316
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85669839"
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>復原到記錄序號 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  本主題僅與使用完整或大量記錄復原模式的資料庫相關。  
  
 您可使用記錄序號 (LSN) 定義還原作業的復原點。 但是，這是為工具供應商所提供的特定功能，未必普遍適用。  
  
##  <a name="overview-of-log-sequence-numbers"></a><a name="LSNs"></a> 記錄序號概觀  
 執行 RESTORE 順序期間，在內部會使用 LSN 追蹤已還原之資料的時間點。 還原備份時，資料會還原到備份執行時間點所對應的 LSN； 差異與記錄備份則可將已還原的資料庫推往更後面的時間點，因為它們對應到較高的 LSN。 如需 LSN 的詳細資訊，請參閱 [SQL Server 交易記錄架構和管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。  
  
> [!NOTE]  
> LSN 是 **numeric(25,0)** 資料類型的值。 數學運算 (例如：加、減) 在此沒有意義，且絕不能搭配 LSN 使用。  
 
## <a name="viewing-lsns-used-by-backup-and-restore"></a>檢視備份與還原所使用的 LSN  
 特定備份與還原事件發生時的記錄 LSN，可透過下列一種或多種方式進行檢視：  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)； [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
-   [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
> [!NOTE]  
>  LSN 也會出現在錯誤記錄檔中的某些訊息內。  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>還原至 LSN 的 Transact-SQL 語法  
 使用 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式，您可以在 LSN 上或剛好就在它之前停止，如下所述：  
  
-   使用 WITH STOPATMARK **='** lsn: _<lsn_number>_ **'** 子句，其中 lsn: *\<lsnNumber>* 是會指定包含所指定的 LSN 的記錄檔記錄為復原點的字串。  
  
     STOPATMARK 會向前復原到 LSN，並且將該筆記錄納入向前復原中。  
  
-   使用 WITH STOPBEFOREMARK **='** lsn: _<lsn_number>_ **'** 子句，其中 lsn: *\<lsnNumber>* 是會指定緊接在包含指定的 LSN 號碼的記錄檔記錄之前的記錄檔記錄為復原點的字串。  
  
     STOPBEFOREMARK 會向前復原到 LSN，並且從向前復原中排除該筆記錄。  
  
 通常會選取要納入或排除的特定交易。 實際上雖不需要這麼做，但指定的記錄是交易認可記錄。  
  
## <a name="examples"></a>範例  
 下列範例假設 `AdventureWorks` 資料庫已變更為使用完整復原模式。  
  
```sql  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [還原資料庫至標示的交易 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [還原和復原概觀 (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)       
 [SQL Server 交易記錄架構與管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)      
  
