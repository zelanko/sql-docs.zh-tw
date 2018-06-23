---
title: 將資料庫還原至失敗點 (TRANSACT-SQL) 完整復原模式下 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- point of failure [SQL Server]
- restoring databases [SQL Server], point of failure
- database restores [SQL Server], point of failure
ms.assetid: 04106e18-bbf7-4a5e-a2e1-3d65319814d5
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 743408c4cafccedf6648834fbdcb0be459857768
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144741"
---
# <a name="restore-a-database-to-the-point-of-failure-under-the-full-recovery-model-transact-sql"></a>在完整復原模式下將資料庫還原至失敗點 (Transact-SQL)
  此主題說明如何還原到失敗點。 此主題只與使用完整或大量記錄復原模式的資料庫有關。  
  
### <a name="to-restore-to-the-point-of-failure"></a>還原到失敗點  
  
1.  執行下列基本的 [BACKUP](/sql/t-sql/statements/backup-transact-sql) 陳述式，備份記錄的結尾：  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  執行下列基本的 [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql) 陳述式，還原完整的資料庫備份：  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
3.  也可以選擇，執行下列基本的 RESTORE DATABASE 陳述式，還原差異資料庫備份：  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
4.  套用每個交易記錄，包括您在步驟 1，透過在 RESTORE LOG 陳述式中指定 WITH NORECOVERY 所建立的結尾記錄備份：  
  
    ```  
    RESTORE LOG <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
5.  執行下列 RESTORE DATABASE 陳述式，復原資料庫：  
  
    ```  
    RESTORE DATABASE <database_name>   
       WITH RECOVERY;  
    ```  
  
## <a name="example"></a>範例  
 在執行範例之前，必須先完成下列準備工作：  
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的預設復原模式是簡單復原模式。 由於此復原模式不支援還原至失敗點，請執行下列 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ALTER DATABASE [陳述式，設定](/sql/t-sql/statements/alter-database-transact-sql) 使用完整復原模式：  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
    ```  
  
2.  使用下列 BACKUP 陳述式，建立資料庫的完整資料庫備份：  
  
    ```  
    BACKUP DATABASE AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Data.bck';  
    ```  
  
3.  建立例行的記錄備份：  
  
    ```  
    BACKUP LOG AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Log.bck';  
    ```  
  
 下列範例會在建立 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的結尾記錄備份之後，還原先前建立的備份 (此步驟假定可以取得記錄磁碟)。  
  
 首先，範例建立資料庫的結尾記錄備份，擷取使用中的記錄，並讓資料庫保留為「還原」狀態。 然後，範例還原資料庫備份，套用先前建立的例行記錄備份，然後套用結尾記錄備份。 最後，範例用另外一個步驟復原資料庫。  
  
> [!NOTE]  
>  預設行為是復原資料庫，作為還原最後備份的陳述式一部分。  
  
```  
/* Example of restoring a to the point of failure */  
-- Step 1: Create a tail-log backup by using WITH NORECOVERY.  
BACKUP LOG AdventureWorks2012  
   TO DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 2: Restore the full database backup.  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Data.bck'  
   WITH NORECOVERY;  
GO  
-- Step 3: Restore the first transaction log backup.  
RESTORE LOG AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 4: Restore the tail-log backup.  
RESTORE LOG AdventureWorks2012  
   FROM  DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 5: Recover the database.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
