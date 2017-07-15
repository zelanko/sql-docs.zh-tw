---
title: "在不還原資料的情況下復原資料庫 (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restoring [SQL Server], recovery-only
- recovery-only scenario [SQL Server]
- restoring databases [SQL Server], recovery-only
- recovery [SQL Server], recovery-only
- database recovery [SQL Server]
- database restores [SQL Server], recovery-only
- recovery [SQL Server], without restoring data
ms.assetid: 7e8fa620-315d-4e10-a718-23fa5171c09e
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 06806d82a8075b0aa25bd66028eefee1a83ec2f9
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# 在不還原資料的情況下復原資料庫 (Transact-SQL)
<a id="recover-a-database-without-restoring-data-transact-sql" class="xliff"></a>
  通常會先還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的所有資料，再復原資料庫。 不過，還原作業可以復原資料庫，而不實際還原備份；例如，復原與資料庫一致的唯讀檔案時即是如此。 這稱為「僅復原的還原」。 如果離線資料已與資料庫一致，而且只需要回復為可用狀態，僅復原的還原作業就會完成資料庫的復原，並讓資料回到線上。  
  
 整個資料庫或一個或多個檔案或檔案群組，都可能發生僅復原的還原。  
  
## 僅復原的資料庫還原
<a id="recovery-only-database-restore" class="xliff"></a>  
 僅復原的資料庫還原在下列情況中會很有用：  
  
-   還原還原順序中最後一個備份時，您未復原資料庫，但是現在想要復原資料庫以使其回到線上。  
  
-   資料庫處於待命模式，而您想在不套用其他記錄備份的情況下使資料庫成為可更新的。  
  
 用於僅復原的資料庫還原的 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 語法如下：  
  
 RESTORE DATABASE *database_name* WITH RECOVERY  
  
> [!NOTE]  
>  FROM **=** \<*backup_device>* 子句未使用於僅復原的還原，因為沒有備份的必要。  
  
 **範例**  
  
 下列範例會在還原作業中復原 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫，而不還原資料。  
  
```  
-- Restore database using WITH RECOVERY.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY  
```  
  
## 僅復原的檔案還原
<a id="recovery-only-file-restore" class="xliff"></a>  
 僅復原的檔案還原在下列情況中會很有用：  
  
 分次還原資料庫。 主要檔案群組的還原完成之後，未還原的檔案中有一或多個檔案與新的資料庫狀態一致，或許是因為它已經有好一段時間是唯讀的。 這些檔案只需復原即可；不需要資料複製。  
  
 僅復原的還原作業會讓離線檔案群組中的資料回到線上；不會產生資料複製、重做或恢復階段。 如需還原階段的相關資訊，請參閱[還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
 用於僅復原之檔案還原的 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 語法為：  
  
 RESTORE DATABASE <資料庫名稱> { FILE **=***logical_file_name* | FILEGROUP **=<邏輯檔案群組名稱>** }[ **,**...*n* ] WITH RECOVERY  
  
 **範例**  
  
 下列範例說明如何針對 `SalesGroup2`資料庫中次要檔案群組 `Sales` 的檔案進行僅復原的檔案還原。 主要檔案群組已經在分次還原的初始步驟中還原，而且 `SalesGroup2` 與還原的主要檔案群組一致。 將此檔案群組復原並使其上線，只需要一個陳述式。  
  
```  
RESTORE DATABASE Sales FILEGROUP=SalesGroup2 WITH RECOVERY;  
```  
  
## 透過僅復原的還原完成分次還原狀況的範例
<a id="examples-of-completing-a-piecemeal-restore-scenario-with-a-recovery-only-restore" class="xliff"></a>  
 **簡單復原模式**  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
 **完整復原模式**  
  
-   [範例：分次還原資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
## 另請參閱
<a id="see-also" class="xliff"></a>  
 [線上還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [檔案還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [檔案還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
