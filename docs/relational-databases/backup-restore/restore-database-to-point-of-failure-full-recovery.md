---
title: 還原資料庫：失敗點 - 完整復原
description: 本文說明如何使用完整或大量記錄復原模式，將 SQL Server 資料庫還原到資料庫的失敗點。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- point of failure [SQL Server]
- restoring databases [SQL Server], point of failure
- database restores [SQL Server], point of failure
ms.assetid: 04106e18-bbf7-4a5e-a2e1-3d65319814d5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1980c9911e9b8af8fc305c712be479af15926201
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "82180708"
---
# <a name="restore-database-to-point-of-failure---full-recovery"></a>將資料庫還原到失敗點 - 完整復原
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題說明如何還原到失敗點。 此主題只與使用完整或大量記錄復原模式的資料庫有關。  
  
### <a name="to-restore-to-the-point-of-failure"></a>還原到失敗點  
  
1.  執行下列基本的 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 陳述式，備份記錄的結尾：  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  執行下列基本的 [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式，還原完整的資料庫備份：  
  
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
  
1.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的預設復原模式是簡單復原模式。 由於此復原模式不支援還原至失敗點，請執行下列 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ALTER DATABASE [陳述式，設定](../../t-sql/statements/alter-database-transact-sql.md) 使用完整復原模式：  
  
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
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
