---
title: sp_help_log_shipping_monitor_secondary (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_secondary
- sp_help_log_shipping_monitor_secondary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor_secondary
ms.assetid: 3ac091ea-c9a8-4c05-a0b6-1ccf4e001339
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 598f988483e3bef6ffe784f7be18145ebf1a89e5
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028002"
---
# <a name="sphelplogshippingmonitorsecondary-transact-sql"></a>sp_help_log_shipping_monitor_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從監視資料表傳回次要資料庫的相關資訊。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_log_shipping_monitor_secondary  
[ @secondary_server = ] 'secondary_server',  
[ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>引數  
 [ **@secondary_server =** ] '*secondary_server*'  
 這是次要伺服器的名稱。 *secondary_server*已**sysname**，沒有預設值。  
  
 [  **@secondary_database =** ] '*secondary_database*'  
 這是次要資料庫的名稱。 *secondary_database*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|「資料行」|描述|  
|------------|-----------------|  
|**secondary_server**|第二個執行個體名稱[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]記錄傳送組態中。|  
|**secondary_database**|記錄傳送組態中之次要資料庫的名稱。|  
|**secondary_id**|記錄傳送組態中之次要伺服器的識別碼。|  
|**primary_server**|記錄傳送組態中之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 主要執行個體的名稱。|  
|**primary_database**|記錄傳送組態中之主要資料庫的名稱。|  
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
  
## <a name="remarks"></a>備註  
 **sp_help_log_shipping_monitor_secondary**必須從執行**主要**監視伺服器上的資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行此程序。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
