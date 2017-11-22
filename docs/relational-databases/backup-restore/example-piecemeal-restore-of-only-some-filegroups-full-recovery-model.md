---
title: "範例：僅限於部分檔案群組的分次還原 (完整復原模式) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full recovery model [SQL Server], RESTORE example
- piecemeal restores [SQL Server], full recovery model
- restore sequences [SQL Server], piecemeal
ms.assetid: bced4b54-e819-472b-b784-c72e14e72a0b
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d469ef626a99270fd36bd50d8cbc861735391bb5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-full-recovery-model"></a>範例：僅限於部份檔案群組的分次還原 (完整復原模式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題是關於在完整復原模式下，包含多個檔案或檔案群組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
 分次還原順序會在檔案群組層級，分階段地還原與復原資料庫，先從主要檔案群組開始，然後才是所有的讀取/寫入次要檔案群組。  
  
 這個範例當中，使用完整復原模式，名為 `adb`的資料庫包含三個檔案群組。 檔案群組 `A` 可讀取/寫入，而檔案群組 `B` 和檔案群組 `C` 則是唯讀的。 所有的檔案群組一開始都是在線上。  
  
 資料庫 `B` 的主要檔案群組與檔案群組 `adb` 似乎已損毀。 主要檔案群組並不大，很快就可還原。 資料庫管理員決定使用分次還原順序來加以還原。 首先，還原主要檔案群組及後續的交易記錄檔，並復原資料庫。  
  
 完整未受損的檔案群組 `A` 和 `C` 中含有重要資料。 因此，下一步便是復原這兩個檔案群組，讓它們儘快恢復上線。 最後則是還原並復原已損毀的次要檔案群組 `B`。  
  
## <a name="restore-sequences"></a>還原順序：  
  
> [!NOTE]  
>  線上還原順序的語法和離線還原順序的語法相同。  
  
1.  為資料庫 `adb`建立結尾記錄備份。 您必須執行此步驟，才能讓完整的檔案群組 `A` 和 `C` 利用資料庫還原點保持在最新狀態。  
  
    ```  
    BACKUP LOG adb TO tailLogBackup WITH NORECOVERY  
    ```  
  
2.  主要檔案群組的部分還原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='Primary' FROM backup   
    WITH PARTIAL, NORECOVERY  
    RESTORE LOG adb FROM backup1 WITH NORECOVERY  
    RESTORE LOG adb FROM backup2 WITH NORECOVERY  
    RESTORE LOG adb FROM backup3 WITH NORECOVERY  
    RESTORE LOG adb FROM tailLogBackup WITH RECOVERY  
    ```  
  
     此時，主要檔案群組為線上狀態。 檔案群組 `A`、 `B`和 `C` 中的所有檔案皆為復原暫止狀態，且檔案群組已離線。  
  
3.  線上還原檔案群組 `A` 和 `C`。  
  
     由於這些檔案群組的資料並未損毀，因此它們不需要從備份還原，但必須進行復原才能回到線上。  
  
     資料庫管理員立即復原 `A` 和 `C` 。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A', FILEGROUP='C' WITH RECOVERY  
    ```  
  
     此時，主要與次要檔案群組 `A` 和 `C` 會在線上。 檔案群組 `B` 裡的檔案會保持復原暫止，而檔案群組為離線。  
  
4.  線上還原檔案群組 `B`。  
  
     檔案群組 `B` 中的檔案，可在此後的任何時間進行還原。  
  
    > [!NOTE]  
    >  檔案群組 `B` 的備份是在檔案群組變成唯讀之後進行的，因此這些檔案不需向前復原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY  
    ```  
  
     所有檔案群組現在都已在線上。  
  
## <a name="additional-examples"></a>其他範例  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [範例：分次還原資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [範例：線上還原讀寫檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [線上還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
