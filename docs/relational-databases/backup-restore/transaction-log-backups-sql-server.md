---
title: 交易記錄備份 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server]
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 491016d02dfdb890914633333e19a3138c01779d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68041349"
---
# <a name="transaction-log-backups-sql-server"></a>交易記錄備份 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題只與使用完整或大量記錄復原模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關。 本主題討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的交易記錄備份。  
  
 您至少要在建立任何記錄備份之前，必須建立一個完整備份。 之後，除非交易記錄已正在備份中，否則任何時候皆可以備份交易記錄。 
 
建議您時常進行記錄備份，以將工作損失風險降至最低，同時也讓記錄能夠截斷。 
 
一般而言，資料庫管理員有時會建立完整資料庫備份，例如每週一次；並且會選擇性地於較短的間隔建立一系列差異資料庫備份，例如每日一次。 除了資料庫備份之外，資料庫管理員會為交易記錄採取高頻率備份。 每種備份類型的最佳間隔取決於幾項因素，如資料的重要性、資料庫大小及伺服器負載。 如需實作良好策略的詳細資訊，請參閱本主題中的[建議](#Recommendations)。 
   
##  <a name="how-a-sequence-of-log-backups-works"></a><a name="LogBackupSequence"></a> 記錄備份順序的運作方式  
 交易記錄備份 *「記錄檔鏈結」* (Log chain) 的順序與資料備份無關。 例如，假設發生以下一連串事件：  
  
|Time|事件|  
|----------|-----------|  
|8:00 AM|備份資料庫。|  
|中午|備份交易記錄。|  
|4:00 PM|備份交易記錄。|  
|6:00 PM|備份資料庫。|  
|8:00 PM|備份交易記錄。|  
  
 在晚上 8:00 建立的交易記錄備份包含從下午 4:00 到晚上 8:00 的交易記錄，其跨越在下午 6:00 建立完整資料庫備份的時間。這一連串的交易記錄備份會從上午 8:00 時建立的初始完整資料庫備份開始，一直持續到晚上 8:00 時建立的最後一個交易記錄備份。 如需有關如何套用這些記錄備份的資訊，請參閱 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)中的範例。  
  
##  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   如果異動記錄損毀，則最近一次有效備份之後所執行的工作都會遺失。 因此，我們強烈建議您將記錄檔存放於容錯的儲存體中。  
  
-   若資料庫損毀或您準備還原資料庫時，建議您建立 [結尾記錄備份](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) ，使您可以將資料庫還原至目前的時間點。  
  
-   根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您經常備份記錄檔，這些成功訊息可能會快速累積，因而產生龐大的錯誤記錄檔，讓您難以尋找其他訊息。 在這類情況下，如果沒有任何指令碼相依於這些記錄項目，您就可以使用追蹤旗標 3226 來隱藏這些記錄項目。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。  

-   請經常進行充分的記錄備份來支援商務需求，特別是您對工作損失 (例如可能因損壞的記錄儲存體而引起) 的耐受性。 
   -   進行記錄備份的頻率如何才適當，視您在工作損失風險的耐受性，與儲存、管理及可能還原記錄備份的容量之間所做的取捨而定。 實作復原策略，以及特別是記錄備份頻率時，考慮使用必要的 [RTO](https://wikipedia.org/wiki/Recovery_time_objective) 和 [RPO](https://wikipedia.org/wiki/Recovery_point_objective)。
   -   每 15 到 30 分鐘進行一次記錄備份可能就足夠了。 如果您的業務需要將工作損失風險減至最低，請考慮更頻繁地進行記錄備份。 較頻繁的記錄備份還會帶來另一優點，就是增加記錄截斷的頻率，從而產生較小的記錄檔。  
  
> [!IMPORTANT]
> 若要限制您需要還原的記錄備份數目，定期備份資料是基本作業。 例如，您可能會排程每週的完整資料庫備份和每日的差異資料庫備份。  
> 同樣地，實作復原策略，以及特別是完整和差異資料庫備份頻率時，考慮使用必要的 [RTO](https://wikipedia.org/wiki/Recovery_time_objective) 和 [RPO](https://wikipedia.org/wiki/Recovery_point_objective)。
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
 **若要建立交易記錄備份**  
  
-   [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 若要排程備份作業，請參閱＜ [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)＞。  
  

## <a name="see-also"></a>另請參閱  
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [SQL Server 中的交易記錄備份交易記錄架構與管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)     
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
