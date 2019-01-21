---
title: 在不還原資料的情況下復原資料庫 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], recovery-only
- recovery-only scenario [SQL Server]
- restoring databases [SQL Server], recovery-only
- recovery [SQL Server], recovery-only
- database recovery [SQL Server]
- database restores [SQL Server], recovery-only
- recovery [SQL Server], without restoring data
ms.assetid: 7e8fa620-315d-4e10-a718-23fa5171c09e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55e6800063ba308fca51f60e253500f147e2acb1
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2019
ms.locfileid: "54242109"
---
# <a name="recover-a-database-without-restoring-data-transact-sql"></a>在不還原資料的情況下復原資料庫 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  通常會先還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的所有資料，再復原資料庫。 不過，還原作業可以復原資料庫，而不實際還原備份；例如，復原與資料庫一致的唯讀檔案時即是如此。 這稱為「僅復原的還原」。 如果離線資料已與資料庫一致，而且只需要回復為可用狀態，僅復原的還原作業就會完成資料庫的復原，並讓資料回到線上。  
  
 整個資料庫或一個或多個檔案或檔案群組，都可能發生僅復原的還原。  
  
## <a name="recovery-only-database-restore"></a>僅復原的資料庫還原  
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
  
## <a name="recovery-only-file-restore"></a>僅復原的檔案還原  
 僅復原的檔案還原在下列情況中會很有用：  
  
 分次還原資料庫。 主要檔案群組的還原完成之後，未還原的檔案中有一或多個檔案與新的資料庫狀態一致，或許是因為它已經有好一段時間是唯讀的。 這些檔案只需復原即可；不需要資料複製。  
  
 僅復原的還原作業會讓離線檔案群組中的資料回到線上；不會產生資料複製、重做或恢復階段。 如需還原階段的相關資訊，請參閱[還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
 用於僅復原之檔案還原的 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 語法為：  
  
 RESTORE DATABASE *database_name* { FILE **=**_logical_file_name_ | FILEGROUP **=**_logical_filegroup_name_ }[ **,**...*n* ] WITH RECOVERY  
  
 **範例**  
  
 下列範例說明如何針對 `SalesGroup2`資料庫中次要檔案群組 `Sales` 的檔案進行僅復原的檔案還原。 主要檔案群組已經在分次還原的初始步驟中還原，而且 `SalesGroup2` 與還原的主要檔案群組一致。 將此檔案群組復原並使其上線，只需要一個陳述式。  
  
```  
RESTORE DATABASE Sales FILEGROUP=SalesGroup2 WITH RECOVERY;  
```  
  
## <a name="examples-of-completing-a-piecemeal-restore-scenario-with-a-recovery-only-restore"></a>透過僅復原的還原完成分次還原狀況的範例  
 **簡單復原模式**  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
 **完整復原模式**  
  
-   [範例：分次還原資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
## <a name="see-also"></a>另請參閱  
 [線上還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [檔案還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [檔案還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
