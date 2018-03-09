---
title: "sp_help_log_shipping_secondary_database (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_secondary_database
- sp_help_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_secondary_database
ms.assetid: 11ce42ca-d3f1-44c8-9cac-214ca8896b9a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8bb243bd5d35293df828be305dba20cb405ad926
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sphelplogshippingsecondarydatabase-transact-sql"></a>sp_help_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個預存程序會擷取一或多個次要資料庫的設定。  
  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database' OR  
[ @secondary_id = ] 'secondary_id'  
```  
  
## <a name="arguments"></a>引數  
 [ **@secondary_database =** ] '*secondary_database*'  
 這是次要資料庫的名稱。 *secondary_database*是**sysname**，沒有預設值。  
  
 [ **@secondary_id =** ] '*secondary_id*'  
 記錄傳送組態中之次要伺服器的識別碼。 *secondary_id*是**uniqueidentifier**不能是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|Description|  
|-----------------|-----------------|  
|**secondary_id**|記錄傳送組態中之次要伺服器的識別碼。|  
|**primary_server**|主要執行個體的名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]記錄傳送組態中。|  
|**primary_database**|記錄傳送組態中之主要資料庫的名稱。|  
|**backup_source_directory**|用於儲存主要伺服器之交易記錄備份檔的目錄。|  
|**backup_destination_directory**|備份檔要複製到其中的次要伺服器目錄。|  
|**file_retention_period**|在刪除備份檔之前，將它保留在次要伺服器中的時間長度 (以分鐘為單位)。|  
|**copy_job_id**|次要伺服器中之複製作業的相關識別碼。|  
|**restore_job_id**|次要伺服器中之還原作業的相關識別碼。|  
|**monitor_server**|在記錄傳送組態中，用於做為監視伺服器之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體的名稱。|  
|**monitor_server_security_mode**|用於連接到監視伺服器的安全性模式。<br /><br /> 1 = [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證。<br /><br /> 0 =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。|  
|**secondary_database**|記錄傳送組態中之次要資料庫的名稱。|  
|**restore_delay**|在還原給定的備份檔之前，次要伺服器等待的時間 (以分鐘為單位)。 預設值是 0 分鐘。|  
|**restore_all**|如果設為 1，當執行還原作業時，次要伺服器會還原所有可用的交易記錄備份。 否則，它會在還原一個檔案之後停止。|  
|**restore_mode**|次要資料庫的還原模式。<br /><br /> 0 = 以 NORECOVERY 來還原記錄。<br /><br /> 1 = 以 STANDBY 來還原記錄。|  
|**disconnect_users**|如果設為 1，當執行還原作業時，會從次要資料庫中斷使用者的連接。 預設值 = 0。|  
|**block_size**|用來做為備份裝置區塊大小的大小 (以位元組為單位)。|  
|**buffer_count**|備份或還原作業所用的緩衝區總數。|  
|**max_transfer_size**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向備份裝置發出的最大輸入或輸出要求大小 (以位元組為單位)。|  
|**restore_threshold**|在產生警示之前，還原作業之間所能經歷的時間 (以分鐘為單位)。|  
|**threshold_alert**|當超出還原臨界值時所產生的警示。|  
|**threshold_alert_enabled**|決定是否啟用還原臨界值警示。<br /><br /> 1 = 已啟用。<br /><br /> 0 = 已停用。|  
|**last_copied_file**|前一個複製到次要伺服器的備份檔之檔案名稱。|  
|**last_copied_date**|在次要伺服器中，前一個複製作業的日期和時間。|  
|**last_copied_date_utc**|在次要伺服器中，前一個複製作業的日期和時間 (以國際標準時間 (UTC) 為單位)。|  
|**last_restored_file**|前一個還原到次要資料庫的備份檔之檔案名稱。|  
|**last_restored_date**|在次要資料庫中，前一個還原作業的日期和時間。|  
|**last_restored_date_utc**|在次要資料庫中，前一個還原作業的日期和時間 (以國際標準時間 (UTC) 為單位)。|  
|**history_retention_period**|給定次要資料庫的記錄傳送記錄，在刪除之前所保留的時間 (以分鐘為單位)。|  
|**last_restored_latency**|在主要資料庫中建立記錄備份和在次要資料庫中還原這個記錄備份，其間所經歷的時間 (以分鐘為單位)。<br /><br /> 初始值是 NULL。|  
  
## <a name="remarks"></a>備註  
 如果您包含*secondary_database*參數，結果集包含的相關資訊的次要資料庫; 如果您包含*secondary_id*結果集將包含參數，具有該次要識別碼相關聯的所有次要資料庫的相關資訊  
  
 **sp_help_log_shipping_secondary_database**必須從執行**主要**次要伺服器上的資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="see-also"></a>另請參閱  
 [sp_help_log_shipping_secondary_primary &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql.md)   
 [關於記錄傳送 &#40;SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
