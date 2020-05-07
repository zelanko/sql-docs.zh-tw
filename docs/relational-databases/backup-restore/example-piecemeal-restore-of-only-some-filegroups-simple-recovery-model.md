---
title: 分次還原：僅部分檔案群組 (簡單復原模式)
description: 此範例說明使用簡單復原模式來分次還原資料庫 SQL Server 中的某些檔案群組。
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
ms.assetid: d7ad026c-5355-4308-9560-0dc843940d4f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1673e3999b6a37ea6383b940bb5e7b66ac922984
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "82179094"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model"></a>範例：僅對部分檔案群組分次還原 (簡單復原模式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題是關於在簡單復原模式下，包含唯讀檔案群組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 分次還原順序會在檔案群組層級，分階段地還原與復原資料庫，先從主要檔案群組開始，然後才是所有的讀取/寫入次要檔案群組。  
  
 這個範例當中，使用簡單復原模式，名為 `adb`的資料庫包含三個檔案群組。 檔案群組 `A` 可讀取/寫入，而檔案群組 `B` 和檔案群組 `C` 則是唯讀的。 所有的檔案群組一開始都是在線上。  
  
 資料庫 `B` 的主要和檔案群組 `adb` 似乎已損毀，所以資料庫管理員決定使用分次還原順序來進行還原。 在簡單復原模式下，必須從相同的部分備份中還原所有的讀取/寫入檔案群組。 雖然檔案群組 `A` 完整無缺，但還是必須隨主要檔案群組一起還原，才能確定它們是一致的 (資料庫將會還原到最後一個部分備份結尾所定義的時間點)。 檔案群組 `C` 完整未受損，但仍然必須加以復原，才能回到線上。 檔案群組 `B`雖然受損，但是包含的資料不比檔案群組 `C`的資料來得重要，因此會在最後才還原 `B` 。  
  
## <a name="restore-sequences"></a>還原順序  
  
> [!NOTE]  
>  線上還原順序的語法和離線還原順序的語法相同。  
  
1.  從部分備份中部分還原主要檔案群組和檔案群組 `A` 。  
  
    ```  
    RESTORE DATABASE adb READ_WRITE_FILEGROUPS FROM partial_backup   
    WITH PARTIAL, RECOVERY  
    ```  
  
     此時，主要檔案群組和檔案群組 `A` 是在線上。 檔案群組 `B` 和 `C` 中的檔案皆為復原暫止狀態，且檔案群組已離線。  
  
2.  線上復原檔案群組 `C`。  
  
     檔案群組 `C` 會是一致的，因為以上所還原的部分備份是在檔案群 `C` 變成唯讀之後才建立的，即使資料庫被還原到了過去的時間點。 資料庫管理員只是復原檔案群組 `C`使其回到線上，並未加以還原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' WITH RECOVERY  
    ```  
  
     此時，主要與次要檔案群組 `A` 和 `C` 會在線上。 FilegroupB 裡的檔案會保持復原暫止，而檔案群組為離線。  
  
3.  線上還原檔案群組。 `B.`  
  
     檔案群組 `B` 中的檔案必須加以還原。 資料庫管理員所還原的檔案群組 `B` 備份，是在檔案群組 `B` 變成唯讀之後及部分備份之前所建立的。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup   
    WITH RECOVERY  
    ```  
  
     所有檔案群組現在都已在線上。  
  
## <a name="additional-examples"></a>其他範例  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
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
  
  
