---
title: 復原模式 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- bulk-logged recovery model [SQL Server]
- recovery [SQL Server], recovery model
- restoring transaction logs [SQL Server], recovery models
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], about
- transaction log backups [SQL Server]
- simple recovery model [SQL Server]
- backups [SQL Server], recovery models
- recovery models [SQL Server]
- recovery models [SQL Server], transaction log management
- database restores [SQL Server], recovery models
- transaction log restores [SQL Server]
- logs [SQL Server], recovery models
- restoring databases [SQL Server], recovery models
- full recovery model [SQL Server]
- backing up transaction logs [SQL Server], recovery models
ms.assetid: 8cfea566-8f89-4581-b30d-c53f1f2c79eb
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6c5b85e316c859e0b6d44fb83e3df6da2edd72ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921763"
---
# <a name="recovery-models-sql-server"></a>復原模式 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份和還原作業是在資料庫之復原模式的內容中進行。 復原模式的設計目的是要控制交易記錄維護。 「復原模式」  是一項資料庫屬性，可控制交易的記錄方式、是否需要 (及允許) 備份交易記錄，以及可用的還原作業類型。 復原模式共有三種：簡單、完整和大量記錄。 一般而言，資料庫會使用完整復原模式或簡單復原模式。 資料庫可以隨時切換到另一個復原模式。  
  
 **本主題內容：**  
  
-   [復原模式概觀](#RMov)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="RMov"></a> 復原模式概觀  
 下表摘要說明三種復原模式。  
  
|復原模式|描述|工作損失風險|復原至時間點？|  
|--------------------|-----------------|------------------------|-------------------------------|  
|**Simple**|無記錄備份。<br /><br /> 自動收回記錄空間，使空間需求保持在最低，實際消弭管理交易記錄空間的需求。 如需簡單復原模式下之資料庫備份的相關資訊，請參閱[完整資料庫備份 &#40;SQL Server&#41;](full-database-backups-sql-server.md)。<br /><br /> 簡單復原模式不支援需要交易記錄備份的作業。 在簡單復原模式中，不能使用下列功能：<br /><br /> 記錄傳送<br /><br /> AlwaysOn 或資料庫鏡像<br /><br /> 無資料遺失的媒體復原<br /><br /> 時間點還原|最近一次備份之後所做的變更並未受到保護。 如果發生損毀事件，則必須重做這些變更。|只能復原至備份結束時。 如需詳細資訊，請參閱[完整資料庫還原 &#40;簡單復原模式&#41;](complete-database-restores-simple-recovery-model.md)。|  
|**Full**|需要記錄備份。<br /><br /> 不因損失或損毀資料檔案而失去任何工作。<br /><br /> 可復原至任意時間點 (例如，應用程式或使用者錯誤前)。 如需完整復原模式下之資料庫備份的相關資訊，請參閱[完整資料庫備份 &#40;SQL Server&#41;](full-database-backups-sql-server.md) 和[完整資料庫還原 &#40;完整復原模式&#41;](complete-database-restores-full-recovery-model.md)。|通常沒有。<br /><br /> 如果記錄結尾損毀，必須重做最近一次記錄備份後的變更。|可以復原至特定時間點 (假設您已完成至該時間點的備份)。 如需使用記錄備份還原至失敗點的相關資訊，請參閱[將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。<br /><br /> 注意:如果您有必須在邏輯上一致的兩個或多個完整復原模式資料庫，您可能必須實作特殊的程序，以確定這些資料庫能夠復原。 如需詳細資訊，請參閱 [復原包含標示之交易的相關資料庫](recovery-of-related-databases-that-contain-marked-transaction.md)。|  
|**大量記錄**|需要記錄備份。<br /><br /> 完整復原模式的輔助，允許執行高效能的大量複製作業。<br /><br /> 針對大多數的大量作業使用最少記錄，以減少記錄空間的使用量。 如需只記錄基本資訊之作業的相關資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)。<br /><br /> 如需大量記錄復原模式下之資料庫備份的相關資訊，請參閱[完整資料庫備份 &#40;SQL Server&#41;](full-database-backups-sql-server.md) 和[完整資料庫還原 &#40;完整復原模式&#41;](complete-database-restores-full-recovery-model.md)。|如果記錄損毀，或在最近一次記錄備份後進行過大量記錄作業的話，必須重做最近一次備份後的變更。<br /><br /> 否則不會損失任何工作。|可復原至任何備份結束時。 不支援時間點復原。|  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [寫滿交易記錄疑難排解 &#40;SQL Server 錯誤 9002&#41;](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
## <a name="see-also"></a>另請參閱  
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [SQL Server 資料庫的備份與還原](back-up-and-restore-of-sql-server-databases.md)   
 [交易記錄 &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [自動化管理工作 &#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
  
  
