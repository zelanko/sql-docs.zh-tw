---
title: managed_backup. sp_backup_config_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 52df69439cecad5fddf3d38b8852a1ce86cc4dbd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942076"
---
# <a name="managed_backupsp_backup_config_schedule-transact-sql"></a>managed_backup. sp_backup_config_schedule （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  設定的[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]自動或自訂排程選項。  
    
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
  
##  <a name="Arguments"></a> 引數  
 @database_name  
 在特定資料庫上啟用受管理備份的資料庫名稱。 如果是 Null 或 *，則此受管理的備份會套用至伺服器上的所有資料庫。  
  
 @scheduling_option  
 針對系統控制的備份排程指定 [系統]。 針對其他參數所定義的自訂排程，指定「自訂」。  
  
 @full_backup_freq_type  
 受管理備份作業的頻率類型，可以設定為「每日」或「每週」。  
  
 @days_of_week  
 當設定為 [每週] 時@full_backup_freq_type ，備份的星期幾。 指定完整的字串名稱，例如「星期一」。  您也可以指定超過一天的名稱，並以分隔號分隔。 例如 N'Monday |星期三 |星期五 '。  
  
 @backup_begin_time  
 [備份] 視窗的開始時間。 備份不會在時間範圍外啟動，而是由@backup_begin_time和@backup_duration的組合所定義。  
  
 @backup_duration  
 備份時間範圍的持續時間。 請注意， @backup_begin_time並不保證備份會在和@backup_duration所定義的時間範圍內完成。 在此時間範圍內啟動但超過視窗持續時間的備份作業將不會取消。  
  
 @log_backup_freq  
 這會決定交易記錄備份的頻率。 這些備份會定期執行，而不是依照針對資料庫備份所指定的排程進行。 @log_backup_freq可以是分鐘或小時，0是有效的，表示沒有記錄備份。 停用記錄備份只適用于具有簡單復原模式的資料庫。  
  
> [!NOTE]  
>  如果復原模式從 [簡單] 變更為 [完整]，您必須將 log_backup_freq 從0重新設定為非零值。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要**db_backupoperator**資料庫角色中的成員資格、具有**ALTER ANY CREDENTIAL**許可權，以及**Sp_delete_backuphistory**預存程式的**EXECUTE**許可權。  
  
## <a name="see-also"></a>另請參閱  
 [managed_backup. sp_backup_config_basic （Transact-sql）](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup。 sp_backup_config_advanced &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
