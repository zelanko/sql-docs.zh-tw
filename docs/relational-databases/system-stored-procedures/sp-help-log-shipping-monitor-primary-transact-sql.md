---
title: sp_help_log_shipping_monitor_primary （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_primary
- sp_help_log_shipping_monitor_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor_primary
ms.assetid: d9dfcb8f-1da6-49ca-a2c8-411574915434
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c133218f7714bd7611e76c2dd202e81041cfa725
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891774"
---
# <a name="sp_help_log_shipping_monitor_primary-transact-sql"></a>sp_help_log_shipping_monitor_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從監視資料表傳回主要資料庫的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_log_shipping_monitor_primary  
[ @primary_server = ] 'primary_server',   
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>引數  
`[ @primary_server = ] 'primary_server'`記錄傳送設定中之主要實例的名稱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 。 *primary_server*是**sysname** ，不能是 Null。  
  
`[ @primary_database = ] 'primary_database'`這是主伺服器上的資料庫名稱。 *primary_database*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**primary_id**|記錄傳送組態之主要資料庫的識別碼。|  
|**primary_server**|記錄傳送組態中之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 主要執行個體的名稱。|  
|**primary_database**|記錄傳送組態中之主要資料庫的名稱。|  
|**backup_threshold**|在產生警示之前，備份作業之間所能經歷的時間 (以分鐘為單位)。|  
|**threshold_alert**|當超出備份臨界值時，所產生的警示。|  
|**threshold_alert_enabled**|決定是否啟用備份臨界值警示。 1 = 已啟用；0 = 已停用。|  
|**last_backup_file**|最近之交易記錄備份的絕對路徑。|  
|**last_backup_date**|在主要資料庫中，前一個交易記錄備份作業的日期和時間。|  
|**last_backup_date_utc**|在主要資料庫中，前一個交易記錄備份作業的日期和時間 (以國際標準時間 (UTC) 為單位)。|  
|**history_retention_period**|給定主要資料庫的記錄傳送記錄，在刪除之前所保留的時間 (以分鐘為單位)。|  
  
## <a name="remarks"></a>備註  
 **sp_help_log_shipping_monitor_primary**必須從監視伺服器上的**master**資料庫中執行。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行此程式。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
