---
title: "復原到記錄序號 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "記錄序號 [SQL Server]"
  - "STOPBEFOREMARK 選項 [RESTORE 陳述式]"
  - "STOPATMARK 選項 [RESTORE 陳述式]"
  - "時間點復原 [SQL Server]"
  - "還原資料庫 [SQL Server], 時間點"
  - "復原 [SQL Server], 資料庫"
  - "還原 [SQL Server], 時間點"
  - "LSN"
  - "資料庫復原 [SQL Server]"
  - "資料庫還原 [SQL Server], 時間點"
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
caps.latest.revision: 38
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 37
---
# 復原到記錄序號 (SQL Server)
  本主題僅與使用完整或大量記錄復原模式的資料庫相關。  
  
 您可使用記錄序號 (LSN) 定義還原作業的復原點。 但是，這是為工具供應商所提供的特定功能，未必普遍適用。  
  
##  <a name="LSNs"></a> 記錄序號概觀  
 執行 RESTORE 順序期間，在內部會使用 LSN 追蹤已還原之資料的時間點。 還原備份時，資料會還原到備份執行時間點所對應的 LSN； 差異與記錄備份則可將已還原的資料庫推往更後面的時間點，因為它們對應到較高的 LSN。  
  
 交易記錄中的每一筆記錄都由記錄序號 (LSN) 加以唯一識別。 LSN 是經過排序的，因此如果 LSN2 大於 LSN1，表示 LSN2 所參考記錄中描述的變更，發生在記錄 LSN1 所描述的變更之後。  
  
 發生重大事件時的記錄 LSN，有助於建構正確的還原順序。 因為 LSNs 經過排序，所以可以進行相等和不等比較 (亦即，**\<**、**>**、**=**、**\<=**、**>=**)。 要建構還原順序時，這種比較很有用。  
  
> [!NOTE]  
>  LSN 是資料類型 **numeric** (25,0) 的值。 數學運算 (例如：加、減) 在此沒有意義，且絕不能搭配 LSN 使用。  
  
 [[頁首]](#Top)  
  
## 檢視備份與還原所使用的 LSN  
 特定備份與還原事件發生時的記錄 LSN，可透過下列一種或多種方式進行檢視：  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)；[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
-   [RESTORE HEADERONLY](../Topic/RESTORE%20HEADERONLY%20\(Transact-SQL\).md)  
  
-   [RESTORE FILELISTONLY](../Topic/RESTORE%20FILELISTONLY%20\(Transact-SQL\).md)  
  
> [!NOTE]  
>  LSN 也會出現在某些訊息文字中。  
  
## 還原至 LSN 所用的 Transact-SQL 語法  
 使用 [RESTORE](../Topic/RESTORE%20\(Transact-SQL\).md) 陳述式，您可以在 LSN 上或剛好就在它之前停止，如下所述：  
  
-   使用 WITH STOPATMARK **='**lsn:*<lsn_number>***'** 子句，其中 lsn:*\<lsnNumber>* 是會指定包含所指定的 LSN 的記錄檔記錄為復原點的字串。  
  
     STOPATMARK 會向前復原到 LSN，並且將該筆記錄納入向前復原中。  
  
-   使用 WITH STOPBEFOREMARK **='**lsn:*<lsn_number>***'** 子句，其中 lsn:*\<lsnNumber>*會指定緊接在包含指定的 LSN 號碼的記錄檔記錄之前的記錄檔記錄為復原點的字串。  
  
     STOPBEFOREMARK 會向前復原到 LSN，並且從向前復原中排除該筆記錄。  
  
 通常會選取要納入或排除的特定交易。 實際上雖不需要這麼做，但指定的記錄是交易認可記錄。  
  
## 範例  
 下列範例假設 `AdventureWorks` 資料庫已變更為使用完整復原模式。  
  
```  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore database to point of failure - full recovery.md)  
  
-   [還原資料庫至標示的交易 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## 另請參閱  
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  