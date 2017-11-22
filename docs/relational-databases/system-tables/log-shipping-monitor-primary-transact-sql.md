---
title: "log_shipping_monitor_primary (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- log_shipping_monitor_primary
- log_shipping_monitor_primary_TSQL
dev_langs: TSQL
helpviewer_keywords: log_shipping_monitor_primary system table
ms.assetid: 5f629a29-1a62-40e6-ae33-6f6b7dd09a36
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4386b5cade983a01c33dae27393dccad667c0842
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="logshippingmonitorprimary-transact-sql"></a>log_shipping_monitor_primary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在每個記錄傳送組態中，儲存每個主要資料庫各一項監視記錄。 這份資料表儲存在**msdb**資料庫。  
  
 主要伺服器和次要伺服器也會使用記錄和監視的相關資料表。   
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**primary_id**|**uniqueidentifier**|記錄傳送組態之主要資料庫的識別碼。|  
|**primary_server**|**sysname**|主要執行個體的名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]記錄傳送組態中。|  
|**primary_database**|**sysname**|記錄傳送組態中之主要資料庫的名稱。|  
|**backup_threshold**|**int**|在產生警示之前，備份作業之間所能經歷的時間 (以分鐘為單位)。|  
|**threshold_alert**|**int**|當超出備份臨界值時，所產生的警示。|  
|**threshold_alert_enabled**|**bit**|決定是否啟用備份臨界值警示。 1 = 已啟用。<br /><br /> 0 = 已停用。|  
|**last_backup_file**|**nvarchar （500)**|最近之交易記錄備份的絕對路徑。|  
|**last_backup_date**|**datetime**|在主要資料庫中，前一個交易記錄備份作業的日期和時間。|  
|**last_backup_date_utc**|**datetime**|在主要資料庫中，前一個交易記錄備份作業的日期和時間 (以國際標準時間 (UTC) 為單位)。|  
|**history_retention_period**|**int**|給定主要資料庫的記錄傳送記錄，在刪除之前所保留的時間 (以分鐘為單位)。|  
  
## <a name="remarks"></a>備註  
 除了儲存在遠端監視伺服器，主要伺服器的相關資訊會儲存在主要伺服器上其**log_shipping_monitor_primary**資料表。  
  
## <a name="see-also"></a>請參閱＜  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_primary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md)   
 [sp_change_log_shipping_primary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql.md)   
 [sp_delete_log_shipping_primary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_primary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_refresh_log_shipping_monitor &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql.md)   
 [sp_help_log_shipping_monitor_primary &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql.md)   
 [sp_delete_log_shipping_alert_job &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql.md)   
 [系統資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
