---
title: log_shipping_secondary_databases (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- log_shipping_secondary_databases_TSQL
- log_shipping_secondary_databases
dev_langs:
- TSQL
helpviewer_keywords:
- log_shipping_secondary_databases system table
ms.assetid: ba2374af-86b8-480c-a10c-51e7c4e3ae23
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 206ed601e845fb4eceddcbca7146e4ca6974f71f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="logshippingsecondarydatabases-transact-sql"></a>log_shipping_secondary_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在記錄傳送組態中，儲存每個次要資料庫各一項記錄。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**secondary_database**|**sysname**|記錄傳送組態中之次要資料庫的名稱。|  
|**secondary_id**|**uniqueidentifier**|記錄傳送組態中之次要伺服器的識別碼。|  
|**restore_delay**|**int**|在還原給定的備份檔之前，次要伺服器等待的時間 (以分鐘為單位)。 預設值是 0 分鐘。|  
|**restore_all**|**bit**|如果設為 1，當執行還原作業時，次要伺服器會還原所有可用的交易記錄備份。 否則，它會在還原一個檔案之後停止。|  
|**restore_mode**|**bit**|次要資料庫的還原模式。<br /><br /> 0 = 以 NORECOVERY 來還原記錄。<br /><br /> 1 = 以 STANDBY 來還原記錄。|  
|**disconnect_users**|**bit**|如果設為 1，當執行還原作業時，會從次要資料庫中斷使用者的連接。 預設值 = 0。|  
|**block_size**|**int**|用來做為備份裝置區塊大小的大小 (以位元組為單位)。|  
|**buffer_count**|**int**|備份或還原作業所用的緩衝區總數。|  
|**max_transfer_size**|**int**|大小，以位元組為單位的最大輸入或輸出要求發出的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份裝置。|  
|**last_restored_file**|**nvarchar(500)**|前一個還原到次要資料庫的備份檔之檔案名稱。|  
|**last_restored_date**|**datetime**|在次要資料庫中，前一個還原作業的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 & #40;SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [sp_add_log_shipping_secondary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)   
 [sp_delete_log_shipping_secondary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [log_shipping_secondary &#40;Transact SQL&#41;](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [系統資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
