---
title: 結尾記錄備份 (SQL Server) | Microsoft Docs
description: 在 SQL Server 中，結尾記錄備份會擷取任何尚未備份的記錄檔記錄，以避免資料遺失，並保持記錄鏈結完整。
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], tail of log
- transaction log backups [SQL Server], tail-log backups
- NO_TRUNCATE clause
- backups [SQL Server], log backups
- tail-log backups
- backups [SQL Server], tail-log backups
ms.assetid: 313ddaf6-ec54-4a81-a104-7ffa9533ca58
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b719e284c56a1b2a83c4be2dd6db14fa431cc242
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829778"
---
# <a name="tail-log-backups-sql-server"></a>結尾記錄備份 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題僅與使用完整或大量記錄復原模式備份和還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關。  
  
 「結尾記錄備份」  (tail-log backup) 可擷取任何尚未備份的記錄檔記錄 (「記錄結尾」  (tail of the log))，來防止工作遺失，並保持記錄鏈結完整。 將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫復原到最新時間點之前，必須備份其交易記錄的結尾。 結尾記錄備份會是資料庫之復原計畫中感興趣的最後一個備份。  
  
> **注意：** 並不是所有的還原實例都需要結尾記錄備份。 如果復原點是包含在較早的記錄備份中，則不需要結尾記錄備份。 而且，如果您要移動或取代 (覆寫) 資料庫，而且不需要將它還原至最近備份之後的某個時間點，就不需要有結尾記錄備份。  
  
   ##  <a name="scenarios-that-require-a-tail-log-backup"></a><a name="TailLogScenarios"></a> 需要結尾記錄備份的實例  
 建議您在下列實例中進行結尾記錄備份：  
  
-   如果資料庫在線上，而且您打算執行資料庫的還原作業，請從備份記錄結尾開始。 若要避免線上資料庫的錯誤，則必須使用...[BACKUP](../../t-sql/statements/backup-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的 WITH NORECOVERY 選項。  
  
-   如果資料庫離線且無法啟動，並且需要還原資料庫，請先備份記錄結尾。 因為這段時間不會發生交易，所以使用 WITH NORECOVERY 是選擇性的。  
  
-   如果資料庫損毀，請嘗試使用 BACKUP 陳述式的 WITH CONTINUE_AFTER_ERROR 選項來進行結尾記錄備份。  
  
     在損毀的資料庫上，只有在記錄檔未損壞、資料庫處於支援結尾記錄備份的狀態，以及資料庫未包含任何大量記錄的變更時，記錄結尾的備份才會成功。 如果無法建立結尾記錄備份，則會遺失在最新記錄備份之後確定的任何交易。  
  
 下表摘要說明 BACKUP NORECOVERY 和 CONTINUE_AFTER_ERROR 選項。  
  
|BACKUP LOG 選項|註解|  
|-----------------------|--------------|  
|NORECOVERY|每當您打算在資料庫上繼續還原作業時，請使用 NORECOVERY。 NORECOVERY 會讓資料庫進入還原狀態。 這樣可以保證資料庫不會在結尾記錄備份之後變更。 除非也指定了 NO_TRUNCATE 選項或 COPY_ONLY 選項，否則將會截斷記錄。<br /><br /> **重要：** 除非資料庫受損，否則請避免使用 NO_TRUNCATE。 您可能需要在使用 NORECOVERY 執行還原之前，將資料庫置於[單一使用者模式](../../relational-databases/databases/set-a-database-to-single-user-mode.md)以取得獨佔存取權。 還原之後，請將資料庫設回多使用者模式。 |  
|CONTINUE_AFTER_ERROR|只有在您要備份受損資料庫的結尾時，才使用 CONTINUE_AFTER_ERROR。<br /><br /> 當您在受損資料庫上使用結尾記錄備份時，一般可在記錄備份中擷取到的某些中繼資料可能無法使用。 如需詳細資訊，請參閱本主題中的 [具有不完整備份中繼資料的結尾記錄備份](#IncompleteMetadata)。|  
  
##  <a name="tail-log-backups-that-have-incomplete-backup-metadata"></a><a name="IncompleteMetadata"></a> 具有不完整備份中繼資料的結尾記錄備份  
 即使資料庫離線、損毀或遺漏資料檔案，結尾記錄備份還是會擷取記錄檔的結尾。 這可能會導致還原資訊命令和 **msdb**產生不完整的中繼資料。 不過，只有中繼資料不完整，所擷取的記錄仍然完整可用。  
  
 如果結尾記錄備份具有不完整的中繼資料， [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) 資料表中的 **has_incomplete_metadata** 會設為 **1**。 此外，在 [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)的輸出中， **HasIncompleteMetadata** 也會設為 **1**。  
  
 如果結尾記錄備份的中繼資料不完整， [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md) 資料表將會遺失有關檔案群組在結尾記錄備份期間的大部分資訊。 大部分 **backupfilegroup** 資料表資料行為 NULL，只有下列資料行具有意義：  
  
-   **backup_set_id**  
-   **filegroup_id**  
-   **type**  
-   **type_desc**  
-   **is_readonly**  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
 若要建立結尾記錄備份，請參閱[資料庫損毀時備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)。  
  
 若要還原交易記錄備份，請參閱[還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)。  
    
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [只複製備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)    
 [SQL Server 交易記錄架構與管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)
  
