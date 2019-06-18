---
title: 監視記錄傳送 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], status
- history tables [SQL Server]
- historical information [SQL Server], log shipping
- log shipping [SQL Server], monitoring
- alerts [SQL Server], log shipping
- status information [SQL Server], log shipping
- monitoring log shipping [SQL Server]
ms.assetid: acf3cd99-55f7-4287-8414-0892f830f423
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d480fe510b6d2e252faefaae13d7dd3776c8ec5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774882"
---
# <a name="monitor-log-shipping-transact-sql"></a>監視記錄傳送 (Transact-SQL)
  在您設定了記錄傳送之後，即可監視所有記錄傳送伺服器的狀態相關資訊。 記錄傳送作業的記錄和狀態一律是由記錄傳送作業儲存在本端。 備份作業的記錄和狀態會儲存在主要伺服器，而複製和還原作業的記錄和狀態會儲存在次要伺服器上。 若您已實作遠端監視伺服器，此資訊也會儲存在監視伺服器中。  
  
 您可以設定若記錄傳送作業無法依排程執行時將要引發的警示。 負責監視備份及還原作業狀態的警示作業會引發錯誤。 您可以定義當這些錯誤產生時，要用來通知操作員的警示。 若已設定監視伺服器，就會在監視伺服器上執行一項警示作業，針對記錄傳送組態中的所有作業來引發錯誤。 若未指定監視伺服器，就會在負責監視備份作業的主要伺服器執行個體上執行警示作業。 若未指定監視伺服器，警示作業也會在每個次要伺服器執行個體上執行，以監視本端的複製和還原作業。  
  
> [!IMPORTANT]  
>  若要監視記錄傳送組態，您必須在啟用記錄傳送時，加入監視伺服器。 如果您日後要加入監視伺服器，就必須移除記錄傳送組態，然後將它取代成包含監視伺服器的新組態。 如需詳細資訊，請參閱[設定記錄傳送 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)。 此外，在設定監視伺服器之後，如果未先移除記錄傳送，就無法進行變更。  
  
## <a name="history-tables-containing-monitoring-information"></a>包含監視資訊的記錄資料表  
 監視記錄資料表包含儲存在監視伺服器上的中繼資料。 給定之主要或次要伺服器的特定資訊副本也會儲存在本端。  
  
 您可以查詢這些資料表來監視記錄傳送工作階段的狀態。 例如，若要知道記錄傳送的狀態，請檢查備份作業、複製作業及還原作業的狀態和記錄。 您可以查詢下列監視資料表，以檢視特定的記錄傳送記錄和錯誤詳細資料。  
  
|資料表|描述|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|儲存警示作業識別碼。|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|儲存記錄傳送作業的錯誤明細。 您可以查詢此資料表來查看代理程式工作階段的錯誤。 您可以選擇依每個錯誤的記錄日期和時間來排序。 每個錯誤都會被記錄成一個例外狀況序列，而多重錯誤 (序列) 會依每項代理程式工作階段來記錄。|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|包含記錄傳送代理程式的記錄詳細資料。 您可以查詢此資料表來查看代理程式工作階段的記錄詳細資料。|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|在每個記錄傳送組態中儲存一筆主要資料庫的監視記錄，包括有助於監視作業的最後備份檔及最後還原檔的相關資訊。|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|為每個次要資料庫儲存一筆監視記錄，包括有助於監視作業的最後備份檔及最後還原檔的相關資訊。|  
  
## <a name="stored-procedures-for-monitoring-log-shipping"></a>用來監視記錄傳送的預存程序  
 監視和記錄資訊會儲存在 **msdb**的資料表中，可使用記錄傳送預存程序來存取。 在下表所指定的伺服器上執行這些預存程序。  
  
|預存程序|描述|執行此程序的伺服器|  
|----------------------|-----------------|---------------------------|  
|[sp_help_log_shipping_monitor_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)|從 **log_shipping_monitor_primary** 資料表傳回指定的主要資料庫的監視記錄。|監視伺服器或主要伺服器|  
|[sp_help_log_shipping_monitor_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)|從 **log_shipping_monitor_secondary** 資料表傳回指定的次要資料庫的監視記錄。|監視伺服器或次要伺服器|  
|[sp_help_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql)|傳回警示作業的作業識別碼。|監視伺服器，或主要或次要伺服器 (若未定義監視伺服器的話)|  
|[sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)|從 **log_shipping_primary_databases** 和 **log_shipping_monitor_primary** 資料表擷取主要資料庫設定然後顯示值。|主要伺服器|  
|[sp_help_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql)|擷取主要資料庫的次要資料庫名稱。|主要伺服器|  
|[sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)|從 **log_shipping_secondary**、 **log_shipping_secondary_databases** 和 **log_shipping_monitor_secondary** 資料表擷取次要資料庫的設定。|次要伺服器|  
|[sp_help_log_shipping_secondary_primary &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql)|這個預存程序會擷取次要伺服器上所指定主要資料庫的設定。|次要伺服器|  
  
## <a name="see-also"></a>另請參閱  
 [檢視記錄傳送報表 &#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)   
 [記錄傳送預存程序與資料表](log-shipping-tables-and-stored-procedures.md)  
  
  
