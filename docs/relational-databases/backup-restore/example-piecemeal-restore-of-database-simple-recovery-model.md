---
title: 分次還原：簡單復原模式
description: 此範例說明如何使用簡單復原模式，將資料庫 SQL Server 分次還原至新電腦。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
author: cawrites
ms.author: chadam
ms.openlocfilehash: b9114f8c2318b7b17692a6c522b6c87f019886a3
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96126949"
---
# <a name="example-piecemeal-restore-of-database-simple-recovery-model"></a>範例：分次還原資料庫 (簡單復原模式)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  分次還原順序會在檔案群組層級，分階段地還原與復原資料庫，先從主要檔案群組開始，然後才是所有的讀取/寫入次要檔案群組。  
  
 在此範例中，資料庫 `adb` 是在損毀之後還原至新的電腦。 此資料庫使用的是簡單復原模式。 在損毀之前，所有檔案群組都在線上。 檔案群組 `A` 和 `C` 可讀取/寫入，而檔案群組 `B` 則是唯讀的。 檔案群組 `B` 在最近一次部分備份之前變成唯讀，該部分備份包含主要檔案群組以及讀取/寫入次要檔案群組 `A` 和 `C`。 在檔案群組 `B` 變成唯讀之後，對檔案群組 `B` 進行了個別的檔案備份。  
  
## <a name="restore-sequences"></a>還原順序  
  
1.  主要檔案群組和檔案群組 `A` 和 `C`的部分還原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A',FILEGROUP='C'   
       FROM partial_backup   
       WITH PARTIAL, RECOVERY;  
  
    ```  
  
     此時，主要檔案群組和檔案群組 `A` 和 `C` 在線上。 檔案群組 `B` 中的所有檔案皆為復原暫止狀態，且檔案群組已離線。  
  
2.  線上還原檔案群組 `B`。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY;  
  
    ```  
  
     所有檔案群組現在都已在線上。  
  
## <a name="additional-examples"></a>其他範例  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [範例：分次還原資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [範例：線上還原讀取/寫入檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [線上還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
