---
title: "log_shipping_secondary (TRANSACT-SQL) |Microsoft 文件"
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
- log_shipping_secondary
- log_shipping_secondary_TSQL
dev_langs: TSQL
helpviewer_keywords: log_shipping_secondary system table
ms.assetid: 69723419-4544-49c6-a517-adb30ffa5741
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa03018420d1c5e23ff41981fd6190407a6a41bc
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="logshippingsecondary-transact-sql"></a>log_shipping_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個次要識別碼各儲存一項記錄。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**secondary_id**|**uniqueidentifier**|記錄傳送組態中之次要伺服器的識別碼。|  
|**primary_server**|**sysname**|記錄傳送組態中之 SQL Server Database Engine 主要執行個體的名稱。|  
|**primary_database**|**sysname**|記錄傳送組態中之主要資料庫的名稱。|  
|**backup_source_directory**|**nvarchar （500)**|用於儲存主要伺服器之交易記錄備份檔的目錄。|  
|**backup_destination_directory**|**nvarchar （500)**|備份檔要複製到其中的次要伺服器目錄。|  
|**file_retention_period**|**int**|在刪除備份檔之前，將它保留在次要伺服器中的時間長度 (以分鐘為單位)。|  
|**copy_job_id**|**uniqueidentifier**|次要伺服器中之複製作業的相關識別碼。|  
|**restore_job_id**|**uniqueidentifier**|次要伺服器中之還原作業的相關識別碼。|  
|**monitor_server**|**sysname**|執行個體名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]正做為監視伺服器，記錄傳送組態中。|  
|**monitor_server_security_mode**|**bit**|用於連接到監視伺服器的安全性模式。<br /><br /> 1 = Windows 驗證。<br /><br /> 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。|  
|**last_copied_file**|**nvarchar （500)**|前一個複製到次要伺服器的備份檔之檔案名稱。|  
|**last_copied_date**|**datetime**|在次要伺服器中，前一個複製作業的日期和時間。|  
  
## <a name="remarks"></a>備註  
 在給定主要資料庫位於相同次要伺服器上的多個次要資料庫會共用中的某些設定**log_shipping_secondary**資料表。 如果變更了其中一個次要資料庫的共用設定，也會改變所有次要資料庫的設定。  
  
## <a name="see-also"></a>請參閱＜  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_change_log_shipping_secondary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [系統資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
