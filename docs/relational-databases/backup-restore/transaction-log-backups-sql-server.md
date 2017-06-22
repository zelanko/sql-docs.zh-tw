---
title: "交易記錄備份 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server[
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
caps.latest.revision: 52
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b7bad833291d3ad6b61cb4fac99334284404b97f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="transaction-log-backups-sql-server"></a>交易記錄備份 (SQL Server)
  本主題只與使用完整或大量記錄復原模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關。 本主題討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的交易記錄備份。  
  
 您至少要在建立任何記錄備份之前，必須建立一個完整備份。 之後，除非交易記錄已正在備份中，否則任何時候皆可以備份交易記錄。 
 
建議您時常進行記錄備份，以將工作損失風險降至最低，同時也讓記錄能夠截斷。 
 
一般而言，資料庫管理員有時會建立完整資料庫備份，例如每週一次；並且會選擇性地於較短的間隔建立一系列差異資料庫備份，例如每日一次。 除了資料庫備份之外，資料庫管理員會為交易記錄採取高頻率備份，例如每 10 分鐘一次。 每種備份類型的最佳間隔取決於幾項因素，如資料的重要性、資料庫大小及伺服器負載。  
   
##  <a name="LogBackupSequence"></a> 記錄備份順序的運作方式  
 交易記錄備份 *「記錄檔鏈結」* (Log chain) 的順序與資料備份無關。 例如，假設發生以下一連串事件：  
  
|Time|事件|  
|----------|-----------|  
|上午 8:00|備份資料庫。|  
|中午|備份交易記錄。|  
|下午 4:00|備份交易記錄。|  
|下午 6:00|備份資料庫。|  
|下午 8:00|備份交易記錄。|  
  
 此交易記錄備份建立於下午 8:00。 其交易記錄自下午 4:00 起 至下午 8:00 止，涵蓋整個建立於下午 6:00 之資料庫備份的時間。 異動記錄備份的順序是連續的，從建立於上午 8:00 的初始完整資料庫備份開始， 至最後一份建立於下午 8:00 的異動記錄備份為止。 如需有關如何套用這些記錄備份的資訊，請參閱 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)中的範例。  
  
##  <a name="Recommendations"></a> 建議  
  
-   如果異動記錄損毀，則最近一次有效備份之後所執行的工作都會遺失。 因此，我們強烈建議您將記錄檔存放於容錯的儲存體中。  
  
-   若資料庫損毀或您準備還原資料庫時，建議您建立 [結尾記錄備份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) ，使您可以將資料庫還原至目前的時間點。  
  
-   根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您經常備份記錄檔，這些成功訊息可能會快速累積，因而產生龐大的錯誤記錄檔，讓您難以尋找其他訊息。 在這類情況下，如果沒有任何指令碼相依於這些記錄項目，您就可以使用追蹤旗標 3226 來隱藏這些記錄項目。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要建立交易記錄備份**  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 若要排程備份作業，請參閱＜ [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)＞。  
  

## <a name="see-also"></a>另請參閱  
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  

