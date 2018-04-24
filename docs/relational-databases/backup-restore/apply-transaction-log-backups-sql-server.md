---
title: 套用異動記錄備份 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/13/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 878308631577ba9060e5a501f64d874594396733
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="apply-transaction-log-backups-sql-server"></a>套用異動記錄備份 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題僅與完整復原模式和大量記錄復原模式有關。  
  
 此主題描述如何在還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的過程中套用交易記錄備份。  
 
  
##  <a name="Requirements"></a> 還原交易記錄備份的需求  
 若要套用交易記錄備份，必須符合下列需求：  
  
-   **有足夠的記錄備份供還原順序使用：** 您必須備份了足夠的記錄，才能完成還原順序。 您必須先備妥必要的記錄備份，包括所需的 [結尾記錄備份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) ，才開始還原順序。  
  
-   **正確的還原順序：**  首先必須還原最新的完整資料庫備份或差異資料庫備份。 接著，必須依時間先後順序，還原在該完整或差異資料庫備份之後建立的所有交易記錄。 如果這個記錄鏈結中的某個交易記錄備份遺失或損毀，您只能還原該遺漏的交易記錄之前的交易記錄。  
  
-   **資料庫尚未復原：**  直到套用了最後一個交易記錄之後，才能復原資料庫。 如果您只還原了其中一個中繼交易記錄備份 (尚未到達記錄鏈結的尾端) 之後便復原資料庫，則您無法還原該時間點之後的資料庫，除非您以完整資料庫備份開始重新啟動整個還原順序。  
  
    > **提示！** 最佳做法就是還原所有的記錄備份 (RESTORE LOG *資料庫名稱* WITH NORECOVERY)。 然後，在還原最後一個記錄備份之後，以個別的作業來復原資料庫 (RESTORE DATABASE *資料庫名稱* WITH RECOVERY)。  
  
##  <a name="RecoveryAndTlogs"></a> 復原與交易記錄  
 當您完成還原作業並復原資料庫時，復原作業會回復所有未完成的交易。 此即稱為 *「恢復階段」*。 需要進行回復，才能還原資料庫的完整性。 回復之後，資料庫會上線，而且不再有交易記錄備份可以套用到資料庫。  
  
 例如，一系列交易記錄備份中包含長時間執行的交易。 該交易的開頭記錄在第一個交易記錄備份，但是交易的結尾記錄在第二個交易記錄備份。 那麼一個交易記錄備份中將沒有認可或回復作業的記錄。 如果在套用第一個交易記錄備份時執行復原作業，則會將長時間執行的交易視為未完成，並且回復在交易的第一個交易記錄備份中記錄的資料修改。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許在此時間點之後套用第二個交易記錄備份。  
  
> **注意：** 在某些狀況下，您可以在記錄還原期間明確加入檔案。  
  
##  <a name="PITrestore"></a> 使用記錄備份還原到失敗點  
 假設發生下列事件順序。  
  
|Time|事件|  
|----------|-----------|  
|上午 8:00|備份資料庫以建立完整資料庫備份。|  
|中午|備份交易記錄。|  
|下午 4:00|備份交易記錄。|  
|下午 6:00|備份資料庫以建立完整資料庫備份。|  
|下午 8:00|備份交易記錄。|  
|下午 9:45|發生故障。|  
  
> **注意：**如需這個備份順序範例的說明，請參閱[交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)。  
  
 若要將資料庫還原至下午 9:45 的狀態 (失敗點)，您可以使用下列任何一個替代程序：  
  
 **替代程序 1：使用最新的完整資料庫備份來還原資料庫**  
  
1.  將目前使用者中交易記錄的結尾記錄備份建立為失敗點。  
  
2.  不要還原上午 8:00 的 完整資料庫備份進行還原，這個程序需要更多的時間。 而是還原下午 6:00 的最新 完整資料庫備份，然後套用下午 8:00 的 記錄備份及結尾記錄備份。  
  
 **替代程序 2：使用較早的完整資料庫備份來還原資料庫**  
  
> **注意：** 如果發生問題，讓您無法使用下午 6:00 的 完整資料庫備份進行還原，這個程序需要更多的時間。 比起從下午 6:00 的 完整資料庫備份進行還原，這個程序需要更多的時間。  
  
1.  將目前使用者中交易記錄的結尾記錄備份建立為失敗點。  
  
2.  還原上午 8:00 的 完整資料庫備份，然後依序還原全部四個交易記錄備份。 如此即可將下午 9:45 前完成的所有交易都向前復原。  
  
     這個替代程序指出維護一系列完整資料庫備份的交易記錄備份鏈結可以提供的額外安全性。  
  
> **注意：** 在某些情況下，您也可以使用交易記錄，將資料庫還原到特定時間點。 如需詳細資訊，請參閱 [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **套用交易記錄備份**  
  
-   [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
 **還原到您的復原點**  
  
-   [在完整復原模式下將資料庫還原至失敗點 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [復原包含標記之異動的相關資料庫](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [復原到記錄序號 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
 **若要使用 WITH NORECOVERY，在還原備份之後復原資料庫**  
  
-   [在不還原資料的情況下復原資料庫 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
