---
description: 'managed_backup sp_backup_config_schedule (Transact-sql) '
title: managed_backup sp_backup_config_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/20/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_schedule_TSQL
- managed_backup.sp_backup_config_schedule
- managed_backup.sp_backup_config_schedule_TSQL
- sp_backup_config_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_schedule
- sp_backup_config_schedule
ms.assetid: 82541160-d1df-4061-91a5-6868dd85743a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 23f1f96ff6d41412e8606e67aacfdc42d9afabc4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486301"
---
# <a name="managed_backupsp_backup_config_schedule-transact-sql"></a>managed_backup sp_backup_config_schedule (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  設定的自動化或自訂排程選項 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。  
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```vb  
EXEC managed_backup.sp_backup_config_schedule   
    [@database_name = ] 'database_name'
    ,[@scheduling_option = ] {'Custom' | 'System'}  
    ,[@full_backup_freq_type = ] {'Daily' | 'Weekly'}  
    ,[@days_of_week = ] 'days_of_the_week'  
    ,[@backup_begin_time = ] 'begin time of the backup window'  
    ,[@backup_duration = ] 'backup window length'  
    ,[@log_backup_freq = ] 'frequency of log backup'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引數  
 @database_name  
 在特定資料庫上啟用 managed 備份的資料庫名稱。 如果是 Null 或 *，則此 managed 備份會套用至伺服器上的所有資料庫。  
  
 @scheduling_option  
 指定「系統」以進行系統控制的備份排程。 針對其他參數所定義的自訂排程指定 [自訂]。  
  
 @full_backup_freq_type  
 受管理備份作業的頻率類型，可以設定為「每日」或「每週」。  
  
 @days_of_week  
 當設定為 [每週] 時，備份的星期幾 @full_backup_freq_type 。 請指定完整的字串名稱，例如 ' Monday '。  您也可以指定超過一天的名稱（以管道分隔）。 例如 N'Monday |星期三 |星期五。  
  
 @backup_begin_time  
 備份時間範圍的開始時間。 備份不會在時間範圍之外啟動，而是由和組合定義 @backup_begin_time @backup_duration 。  
  
 @backup_duration  
 備份時間範圍的持續時間。 請注意，並不保證會在和定義的時間範圍內完成備份 @backup_begin_time @backup_duration 。 在此時間範圍內啟動但超過視窗持續時間的備份作業將不會取消。  
  
 @log_backup_freq  
 這會決定交易記錄備份的頻率。 這些備份會定期執行，而不是依照針對資料庫備份所指定的排程進行。 @log_backup_freq 可以是幾分鐘或幾小時，而且 `0:00` 是有效的，這表示沒有任何記錄備份。 停用記錄備份只適用于具有簡單復原模式的資料庫。  
  
> [!NOTE]  
>  如果復原模式從 simple 變更為 full，您需要將 log_backup_freq 重新設定 `0:00` 為非零值。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要**db_backupoperator**資料庫角色中的成員資格、具有**ALTER ANY CREDENTIAL**許可權，以及**Sp_delete_backuphistory**預存程式的**EXECUTE**許可權。  
  
## <a name="see-also"></a>另請參閱  
 [managed_backup sp_backup_config_basic (Transact-sql) ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
