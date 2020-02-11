---
title: 結尾記錄備份 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6da8f9de22f1b3191d6fba1918e8c05a64d062f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62920675"
---
# <a name="tail-log-backups-sql-server"></a>結尾記錄備份 (SQL Server)
  本主題僅與使用完整或大量記錄復原模式備份和還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關。  
  
 「結尾記錄備份」**(tail-log backup) 可擷取任何尚未備份的記錄檔記錄 (「記錄結尾」**(tail of the log))，來防止工作遺失，並保持記錄鏈結完整。 將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫復原到最新時間點之前，必須備份其交易記錄的結尾。 結尾記錄備份會是資料庫之復原計畫中感興趣的最後一個備份。  
  
> [!NOTE]  
>  並不是所有的還原實例都需要結尾記錄備份。 如果復原點是包含在較早的記錄備份中，則不需要結尾記錄備份。 而且，如果您要移動或取代 (覆寫) 資料庫，而且不需要將它還原至最近備份之後的某個時間點，就不需要有結尾記錄備份。  
  
 
  
##  <a name="TailLogScenarios"></a>需要尾記錄備份的案例  
 建議您在下列實例中進行結尾記錄備份：  
  
-   如果資料庫在線上，而且您打算執行資料庫的還原作業，請從備份記錄結尾開始。 若要避免線上資料庫發生錯誤，您必須使用 .。。WITH [BACKUP](/sql/t-sql/statements/backup-transact-sql) [!INCLUDE[tsql](../../includes/tsql-md.md)]語句的 NORECOVERY 選項。  
  
-   如果資料庫離線且無法啟動，並且需要還原資料庫，請先備份記錄結尾。 因為這段時間不會發生交易，所以使用 WITH NORECOVERY 是選擇性的。  
  
-   如果資料庫損毀，請嘗試使用 BACKUP 陳述式的 WITH CONTINUE_AFTER_ERROR 選項來進行結尾記錄備份。  
  
     在損毀的資料庫上，只有在記錄檔未損壞、資料庫處於支援結尾記錄備份的狀態，以及資料庫未包含任何大量記錄的變更時，記錄結尾的備份才會成功。 如果無法建立結尾記錄備份，則會遺失在最新記錄備份之後確定的任何交易。  
  
 下表摘要說明 BACKUP NORECOVERY 和 CONTINUE_AFTER_ERROR 選項。  
  
|BACKUP LOG 選項|註解|  
|-----------------------|--------------|  
|NORECOVERY|每當您打算在資料庫上繼續還原作業時，請使用 NORECOVERY。 NORECOVERY 會讓資料庫進入還原狀態。 這樣可以保證資料庫不會在結尾記錄備份之後變更。  除非也指定了 NO_TRUNCATE 選項或 COPY_ONLY 選項，否則會截斷記錄。<br /><br /> ** \* \*重要\*事項**我們建議您避免使用 NO_TRUNCATE，除非資料庫損毀。|  
|CONTINUE_AFTER_ERROR|只有在您要備份受損資料庫的結尾時，才使用 CONTINUE_AFTER_ERROR。<br /><br /> 注意：當您在損毀的資料庫上使用備份記錄的結尾時，某些通常會在記錄備份中捕捉到的中繼資料可能無法使用。 如需詳細資訊，請參閱本節稍後的[具有不完整備份中繼資料的結尾記錄備份](#IncompleteMetadata)。|  
  
##  <a name="IncompleteMetadata"></a>具有不完整備份中繼資料的尾記錄備份  
 即使資料庫離線、損毀或遺漏資料檔案，結尾記錄備份還是會擷取記錄檔的結尾。 這可能會導致還原資訊命令和 **msdb**產生不完整的中繼資料。 不過，只有中繼資料不完整，所擷取的記錄仍然完整可用。  
  
 如果結尾記錄備份具有不完整的中繼資料， [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) 資料表中的 **has_incomplete_metadata** 會設為 **1**。 此外，在 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)的輸出中， **HasIncompleteMetadata** 也會設為 **1**。  
  
 如果結尾記錄備份的中繼資料不完整， [backupfilegroup](/sql/relational-databases/system-tables/backupfilegroup-transact-sql) 資料表將會遺失有關檔案群組在結尾記錄備份期間的大部分資訊。 大部分 **backupfilegroup** 資料表資料行為 NULL，只有下列資料行具有意義：  
  
-   **backup_set_id**  
  
-   **filegroup_id**  
  
-   **type**  
  
-   **type_desc**  
  
-   **is_readonly**  
  
##  <a name="RelatedTasks"></a> 相關工作  
 若要建立結尾記錄備份，請參閱[資料庫損毀時備份交易記錄 &#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)。  
  
 若要還原交易記錄備份，請參閱[還原交易記錄備份 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [SQL Server 資料庫的備份與還原](back-up-and-restore-of-sql-server-databases.md)   
 [只複製備份 &#40;SQL Server&#41;](copy-only-backups-sql-server.md)   
 [交易記錄備份 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)  
  
  
