---
title: managed_backup.sp_backup_config_schedule & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8ebeca4b0a1c9079f8786303207bcbae4dfe74c3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38035276"
---
# <a name="managedbackupspbackupconfigschedule-transact-sql"></a>managed_backup.sp_backup_config_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  設定自動或自訂排程選項[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。  
    
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
 啟用特定資料庫上的受管理的備份的資料庫名稱。 如果是 NULL 或 *，則此受管理的備份套用至伺服器上的所有資料庫。  
  
 @scheduling_option  
 系統控制備份排程中指定 'System'。 其他參數所定義的自訂排程，請指定 'Custom'。  
  
 @full_backup_freq_type  
 受管理的備份作業，可以設定為 'Daily' 或 '每週' 頻率類型。  
  
 @days_of_week  
 每週備份天數時@full_backup_freq_type設為每週。 指定完整的字串名稱，例如 「 星期一 」。  您也可以指定 超過一天名稱，並以管道分隔。 比方說 N'Monday |星期三 |星期五 '。  
  
 @backup_begin_time  
 備份時間範圍開始時間。 備份將不會啟動時間視窗中，由組合所定義的外部@backup_begin_time和@backup_duration。  
  
 @backup_duration  
 備份時間範圍持續時間。 請注意，則備份將會完成所定義的時間間隔不能保證@backup_begin_time和@backup_duration。 在此時間範圍內啟動，但超過視窗的持續時間的備份作業將不會取消。  
  
 @log_backup_freq  
 這會決定交易記錄備份的頻率。 這些備份會在定期間隔中，而不是在指定的資料庫備份的排程。 @log_backup_freq 可以是分鐘或小時，0 是有效的這表示沒有記錄備份。 停用記錄檔備份只會適用於使用簡單復原模式的資料庫。  
  
> [!NOTE]  
>  如果設為 full，從簡單變更復原模式，您需要重新設定從 0 log_backup_freq，設為非零值。  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要的成員資格**db_backupoperator**資料庫角色，使用**ALTER ANY CREDENTIAL**權限，並**EXECUTE**的權限**sp_delete_backuphistory**預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)  
  
  
