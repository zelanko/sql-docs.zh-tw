---
title: 復原到記錄序號 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 835057cdef6b7d2a336b64480515a5046cfde070
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875761"
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>復原到記錄序號 (SQL Server)
  本主題僅與使用完整或大量記錄復原模式的資料庫相關。  
  
 您可使用記錄序號 (LSN) 定義還原作業的復原點。 但是，這是為工具供應商所提供的特定功能，未必普遍適用。  
  
##  <a name="LSNs"></a> 記錄序號概觀  
 執行 RESTORE 順序期間，在內部會使用 LSN 追蹤已還原之資料的時間點。 還原備份時，資料會還原到備份執行時間點所對應的 LSN； 差異與記錄備份則可將已還原的資料庫推往更後面的時間點，因為它們對應到較高的 LSN。  
  
 交易記錄中的每一筆記錄都由記錄序號 (LSN) 加以唯一識別。 LSN 是經過排序的，因此如果 LSN2 大於 LSN1，表示 LSN2 所參考記錄中描述的變更，發生在記錄 LSN1 所描述的變更之後。  
  
 發生重大事件時的記錄 LSN，有助於建構正確的還原順序。 因為 LSNs 經過排序，所以可以進行相等和不等比較 (亦即， **\<**、 **>**、 **=**、 **\<=**、 **>=**)。 要建構還原順序時，這種比較很有用。  
  
> [!NOTE]  
>  LSN 是資料類型 `numeric`(25,0) 的值。 數學運算 (例如：加、減) 在此沒有意義，且絕不能搭配 LSN 使用。  
  

  
## <a name="viewing-lsns-used-by-backup-and-restore"></a>檢視備份與還原所使用的 LSN  
 特定備份與還原事件發生時的記錄 LSN，可透過下列一種或多種方式進行檢視：  
  
-   [backupset](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
-   [backupfile](/sql/relational-databases/system-tables/backupfile-transact-sql)  
  
-   [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)； [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
-   [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
-   [RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)  
  
> [!NOTE]  
>  LSN 也會出現在某些訊息文字中。  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>還原至 LSN 所用的 Transact-SQL 語法  
 使用 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 陳述式，您可以在 LSN 上或剛好就在它之前停止，如下所述：  
  
-   使用 WITH STOPATMARK **='** lsn:_<lsn_number>_**'** 子句，其中 lsn:*\<lsnNumber>* 是會指定包含所指定的 LSN 的記錄檔記錄為復原點的字串。  
  
     STOPATMARK 會向前復原到 LSN，並且將該筆記錄納入向前復原中。  
  
-   使用 WITH STOPBEFOREMARK **='** lsn:_<lsn_number>_**'** 子句，其中 lsn:*\<lsnNumber>* 是會指定緊接在包含指定的 LSN 號碼的記錄檔記錄之前的記錄檔記錄為復原點的字串。  
  
     STOPBEFOREMARK 會向前復原到 LSN，並且從向前復原中排除該筆記錄。  
  
 通常會選取要納入或排除的特定交易。 實際上雖不需要這麼做，但指定的記錄是交易認可記錄。  
  
## <a name="examples"></a>範例  
 下列範例假設 `AdventureWorks` 資料庫已變更為使用完整復原模式。  
  
```  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [還原資料庫備份&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [備份交易記錄 &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [還原交易記錄備份 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
-   [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [還原資料庫至標示的交易 &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [套用交易記錄備份 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [交易記錄 &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
