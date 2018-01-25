---
title: "在備份和還原期間可能的媒體錯誤 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
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
- media errors [SQL Server]
- CONTINUE_AFTER_ERROR option
- errors [SQL Server], backups
- backups [SQL Server], errors
- RESTORE VERIFYONLY statement
- backup media [SQL Server], error management
- page checksums [SQL Server]
- backup checksums [SQL Server]
- backing up [SQL Server], media errors
- RESTORE statement, media errors
- NO_CHECKSUM option
- checksums [SQL Server]
ms.assetid: 83a27b29-1191-4f8d-9648-6e6be73a9b7c
caps.latest.revision: "37"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7422aabdffd7985332c669964f0eb518a210ec07
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="possible-media-errors-during-backup-and-restore-sql-server"></a>在備份和還原期間可能的媒體錯誤 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 可讓您選擇復原資料庫，而不理會偵測到的錯誤。 有一項重要的新錯誤偵測機制，就是可以選擇建立備份總和檢查碼，這是由備份作業所建立，並可使用還原作業來加以驗證。 您可以控制作業是否要檢查錯誤，以及在發生錯誤時，是要停止作業，還是要繼續進行。 如果備份包含備份總和檢查碼，RESTORE 和 RESTORE VERIFYONLY 陳述式就可以檢查錯誤。  
  
> [!NOTE]  
>  鏡像備份提供高達四個媒體集複本 (鏡像)，可在因為媒體損壞而導致錯誤時，提供其他的複本來復原。 如需詳細資訊，請參閱本主題稍後的 [鏡像備份媒體集 &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)的使用者閱讀。  
  
  
##  <a name="BckChecksums"></a> 備份總和檢查碼  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援三種類型的總和檢查碼：分頁上的總和檢查碼、記錄區塊中的總和檢查碼，以及備份總和檢查碼。 產生備份總和檢查碼時，BACKUP (備份) 會驗證從資料庫讀取的資料，是否與資料庫中的任何總和檢查碼或損毀頁指示一致。  
  
 BACKUP 陳述式可選擇性地計算備份資料流的備份總和檢查碼；如果分頁總和檢查碼或損毀頁資訊顯示在特定的分頁上，備份該分頁時，BACKUP 也會驗證該分頁的總和檢查碼、損毀頁狀態及分頁識別碼。 建立備份總和檢查碼時，備份作業不會新增任何總和檢查碼至分頁。 分頁會依照其存在於資料庫中的樣子來備份，而且備份不會修改分頁。  
  
 因為驗證及產生備份總和檢查碼會造成額外負擔，使用備份總和檢查碼可能會影響效能。 工作負載及備份的輸送量可能都會受到影響。 因此，您可以選擇是否要使用備份總和檢查碼。 決定要在備份期間產生總和檢查碼時，請小心監視對 CPU 造成的額外負擔，以及對系統上任何並行工作負載所造成的影響。  
  
 BACKUP 絕不會修改磁碟上的來源分頁或是分頁的內容。  
  
 已啟用備份總和檢查碼時，備份作業會執行下列步驟：  
  
1.  在將分頁寫入備份媒體之前，備份作業會先驗證分頁層級的資訊 (分頁總和檢查碼或損毀頁偵測，若其中一項存在的話)。 如果兩者都不存在，則備份無法驗證分頁。 而是直接包含未驗證的分頁，並且將其內容加入整體的備份總和檢查碼。  
  
     如果備份作業在驗證期間發生分頁錯誤，則備份失敗。  
  
    > [!NOTE]  
    >  如需分頁總和檢查碼及損毀頁偵測的詳細資訊，請參閱 ALTER DATABASE 陳述式的 PAGE_VERIFY 選項。 如需詳細資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
2.  不論頁面總和檢查碼是否存在，BACKUP 都會產生備份資料流的個別備份總和檢查碼。 還原作業可以選擇性地利用備份總和檢查碼來驗證備份是否損毀。 備份總和檢查碼儲存在備份媒體中，而不是儲存在資料庫頁面中。 在還原時，您可以選擇性地使用備份總和檢查碼。  
  
3.  備份組會以旗標標示為包含備份總和檢查碼 (在 **msdb..backupset** 的 **has_backup_checksums**資料行中)。 如需詳細資訊，請參閱 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)。  
  
 在還原作業期間，如果備份媒體上有備份總和檢查碼，依預設 RESTORE 和 RESTORE VERIFYONLY 陳述式都會驗證備份總和檢查碼及分頁總和檢查碼。 如果沒有備份總和檢查碼，這二種還原作業仍會繼續進行，但不會執行任何驗證；這是因為沒有備份總和檢查碼，還原作業就不能確實地驗證分頁總和檢查碼。  
  
## <a name="response-to-page-checksum-errors-during-a-backup-or-restore-operation"></a>在備份或還原作業期間對分頁總和檢查碼錯誤的回應  
 根據預設，在發生分頁總和檢查碼錯誤之後，BACKUP 或 RESTORE 作業會失敗，而 RESTORE VERIFYONLY 作業會繼續。 但是，您可以控制給定的作業在發生錯誤時是失敗還是盡其所能地繼續。  
  
 如果 BACKUP 作業在發生錯誤後繼續，該作業會執行下列步驟：  
  
1.  將備份媒體上的備份組標註為包含錯誤，並且在 **msdb** 資料庫的 **suspect_pages** 資料表中追蹤該分頁。 如需詳細資訊，請參閱 [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)。  
  
2.  將錯誤記錄在 SQL Server 錯誤記錄檔中。  
  
3.  將備份組標示為包含該類型的錯誤 (在 **msdb.backupset** 的 **is_damaged**資料行中)。 如需詳細資訊，請參閱 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)。  
  
4.  發出訊息指出已順利產生備份，但包含分頁錯誤。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要啟用或停用備份總和檢查碼**  
  
-   [在備份或還原期間啟用或停用備份總和檢查碼 &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
 **若要在備份作業期間控制錯誤的回應方式**  
  
-   [指定在發生錯誤後備份或還原作業應該繼續還是停止 &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [鏡像備份媒體集 &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
  
