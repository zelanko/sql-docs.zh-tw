---
title: 備份已啟用延展功能的資料庫(Stretch Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.technology: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, backing up
- backups (Stretch Database)
ms.assetid: 18f0dff0-d8ce-4bee-a935-76ed6dfb3208
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 72c41239ba6b5f843ae28b8337fb7de4c4d50ebd
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2018
ms.locfileid: "36925839"
---
# <a name="backup-stretch-enabled-databases-stretch-database"></a>備份已啟用延展功能的資料庫(Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 資料庫備份可協助您從許多失敗、錯誤和損毀類型中復原。  
  
 -   您必須備份已啟用 Stretch 的 SQL Server 資料庫。  
      
 -   Microsoft Azure 會自動備份 Stretch Database 從 SQL Server 遷移到 Azure 的遠端資料。  

> [!TIP]
> 備份只是完整高可用性和商務持續性解決方案的一部分。 如需高可用性的詳細資訊，請參閱 [高可用性解決方案](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)。
   
## <a name="back-up-your-sql-server-data"></a>備份 SQL Server 資料  
  
若要備份已啟用 Stretch 的 SQL Server 資料庫，您可以繼續使用目前所使用的 SQL Server 備份方法。 如需詳細資訊，請參閱 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。
  
 已啟用 Stretch 之 SQL Server 資料庫的備份只包含本機資料及適合在執行備份的時間點進行移轉的資料。 (合格資料是尚未遷移，但會視資料表的移轉設定而遷移到 Azure 的資料。)這稱為**淺層**備份，而且不包含已遷移到 Azure 的資料。  
  
## <a name="back-up-your-remote-azure-data"></a>備份遠端 Azure 資料   
  
Microsoft Azure 會自動備份 Stretch Database 從 SQL Server 遷移到 Azure 的遠端資料。    
### <a name="azure-reduces-the-risk-of-data-loss-with-automatic-backup"></a>Azure 可降低自動備份的資料遺失風險  
Azure 上的 SQL Server Stretch Database 服務會至少每隔 8 小時使用自動儲存快照集來保護您的遠端資料庫。 它會保留每個快照集 7 天，為您提供各種可能的還原點。  
  
### <a name="azure-reduces-the-risk-of-data-loss-with-geo-redundancy"></a>Azure 可降低異地備援的資料遺失風險  
Azure 資料庫備份儲存在異地備援的 Azure 儲存體 (RA-GRS) 中，因此預設會啟用異地備援。 異地備援的儲存體會將您的資料複寫到與主要區域相距甚遠的次要區域。 在主要和次要區域中，您的資料會在不同的容錯網域和升級網域之間各複寫三次。 這可確保即使在發生全面性地區中斷或損毀而造成其中一個 Azure 區域無法使用的情況下，也能持續使用您的資料。

### <a name="stretchRPO"></a>Stretch Database 透過暫時保留已移轉的資料列，來降低 Azure 資料的資料遺失風險
在 Stretch Database 將合格的資料列從 SQL Server 移轉到 Azure 之後，它會在暫存表格中保留這些資料列至少 8 小時。 如果您還原 Azure 資料庫的備份，Stretch Database 會使用儲存在暫存表格中的資料列，來協調 SQL Server 和 Azure 資料庫。

還原 Azure 資料的備份之後，您必須執行預存程序 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) ，將已啟用 Stretch 的 SQL Server 資料庫重新連接到遠端 Azure 資料庫。 當您執行 **sys.sp_rda_reauthorize_db**時，Stretch Database 會自動協調 SQL Server 和 Azure 資料庫。

若要增加 Stretch Database 在暫存表格中暫時保留已移轉之資料的時數，請執行預存程序 [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) 並指定大於 8 的時數。 若要決定所要保留的資料量，請考慮下列因素：
-   自動 Azure 備份的頻率 (至少每隔 8 小時)。
-   發生問題後到辨識問題及決定將備份還原所需的時間。
-   Azure 還原作業的持續時間。

> [!NOTE]
> 增加 Stretch Database 在暫存表格中暫時保留的資料量，可增加 SQL Server 上所需的空間量。

若要檢查 Stretch Database 目前在暫存表格中暫時保留資料的時數，請執行預存程序 [sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)。

## <a name="see-also"></a>另請參閱  
[還原已啟用 Stretch 的資料庫](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
 [管理 Stretch Database 並對其進行疑難排解](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
   
  
  
