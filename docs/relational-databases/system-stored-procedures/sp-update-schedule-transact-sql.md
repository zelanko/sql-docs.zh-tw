---
description: sp_update_schedule (Transact-SQL)
title: sp_update_schedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_schedule
- sp_update_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_schedule
ms.assetid: 97b3119b-e43e-447a-bbfb-0b5499e2fefe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5aead8188bbdaac714bb68e44be0c54cce12fce6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541575"
---
# <a name="sp_update_schedule-transact-sql"></a>sp_update_schedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 排程的設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_update_schedule   
    {   [ @schedule_id = ] schedule_id   
      | [ @name = ] 'schedule_name' }  
    [ , [ @new_name = ] new_name ]  
    [ , [ @enabled = ] enabled ]  
    [ , [ @freq_type = ] freq_type ]  
    [ , [ @freq_interval = ] freq_interval ]   
    [ , [ @freq_subday_type = ] freq_subday_type ]   
    [ , [ @freq_subday_interval = ] freq_subday_interval ]   
    [ , [ @freq_relative_interval = ] freq_relative_interval ]   
    [ , [ @freq_recurrence_factor = ] freq_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time = ] active_start_time ]   
    [ , [ @active_end_time = ] active_end_time ]   
    [ , [ @owner_login_name = ] 'owner_login_name' ]  
    [ , [ @automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>引數  
`[ @schedule_id = ] schedule_id` 要修改之排程的識別碼。 *schedule_id* 是 **int**，沒有預設值。 必須指定 *schedule_id* 或 *schedule_name* 。  
  
`[ @name = ] 'schedule_name'` 要修改的排程名稱。 *schedule_name*是 **sysname**，沒有預設值。 必須指定 *schedule_id* 或 *schedule_name* 。  
  
`[ @new_name = ] new_name` 排程的新名稱。 *new_name* 是 **sysname**，預設值是 Null。 當 *new_name* 為 Null 時，就不會變更排程的名稱。  
  
`[ @enabled = ] enabled` 指出排程的目前狀態。 *enabled*是 **Tinyint**，預設值是 **1** (已啟用) 。 如果是 **0**，則不會啟用排程。 當未啟用排程時，不會依據這份排程來執行任何作業。  
  
`[ @freq_type = ] freq_type` 指出何時要執行作業的值。 *freq_type*是 **int**，預設值是 **0**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月，相對於 *頻率間隔*|  
|**64**|在 SQLServerAgent 服務啟動之時執行|  
|**128**|在電腦閒置之時執行|  
  
`[ @freq_interval = ] freq_interval` 執行作業的天數。 *freq_interval* 是 **int**，預設值是 **0**，而且相依于 *freq_type*的值。  
  
|*Freq_type*的值|對*freq_interval*的影響|  
|---------------------------|--------------------------------|  
|**1** (一次) |*freq_interval* 未使用。|  
|每日) **4** (|每 *freq_interval* 天。|  
|每週) **8** (|*freq_interval* 是下列一或多個 (與 **或** 邏輯運算子) 結合：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **4** = 星期二<br /><br /> **8** = 星期三<br /><br /> **16** = 星期四<br /><br /> **32** = 星期五<br /><br /> **64** = 星期六|  
|每月**16** () |在當月的 *freq_interval* 日。|  
|**32** (每月相對) |*freq_interval* 是下列其中一項：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 天<br /><br /> **9** = 工作日<br /><br /> **10** = 週末日|  
|**64** (SQLServerAgent 服務啟動時) |*freq_interval* 未使用。|  
|**128**|*freq_interval* 未使用。|  
  
`[ @freq_subday_type = ] freq_subday_type`指定*freq_subday_interval * ** 的單位。 *freq_subday_type*是 **int**，預設值是 **0**，而且可以是下列值之一。  
  
|值|描述 (單位)|  
|-----------|--------------------------|  
|**0x1**|在指定的時間|  
|**0x2**|秒|  
|**0x4**|分鐘|  
|**0x8**|小時|  
  
`[ @freq_subday_interval = ] freq_subday_interval` 每次執行作業之間發生的 *freq_subday_type* 期間數。 *freq_subday_interval*是 **int**，預設值是 **0**。  
  
`[ @freq_relative_interval = ] freq_relative_interval`在每個月中，如果*freq_interval*為**32** (每月相對) ，就會發生*freq_interval*的作業。 *freq_relative_interval*是 **int**，預設值是 **0**，而且可以是下列值之一。  
  
|值|描述 (單位)|  
|-----------|--------------------------|  
|**1**|First|  
|**2**|Second|  
|**4**|Third|  
|**8**|第四個|  
|**16**|Last|  
  
`[ @freq_recurrence_factor = ] freq_recurrence_factor` 作業排程執行之間的周數或月數。 只有當*freq_type*是**8**、 **16**或**32**時，才會使用*freq_recurrence_factor* 。 *freq_recurrence_factor*是 **int**，預設值是 **0**。  
  
`[ @active_start_date = ] active_start_date` 可以開始執行作業的日期。 *active_start_date*是 **int**，預設值是 Null，表示今天的日期。 日期格式為 YYYYMMDD。 如果 *active_start_date* 不是 Null，則日期必須大於或等於19900101。  
  
 建立排程之後，檢閱開始日期，並確認該日期正確。 如需詳細資訊，請參閱 [建立和附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)中的「排程開始日期」一節。  
  
`[ @active_end_date = ] active_end_date` 作業的執行時間可以停止的日期。 *active_end_date*是 **int**，預設值是 **99991231**，表示9999年12月31日。 格式為 YYYYMMDD。  
  
`[ @active_start_time = ] active_start_time` 在 *active_start_date* 和 *active_end_date* 之間的任何一天開始執行作業的時間。 *active_start_time*是 **int**，預設值為000000，表示上午12:00:00 必須用 HHMMSS 格式來輸入。  
  
`[ @active_end_time = ] active_end_time` 在 *active_start_date* 和 *active_end_date* 之間的任何一天，結束執行作業的時間。 *active_end_time*是 **int**，預設值是 **235959**，表示 11:59:59 P.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @owner_login_name = ] 'owner_login_name']` 擁有排程之伺服器主體的名稱。 *owner_login_name* 是 **sysname**，預設值是 Null，表示排程是建立者所擁有。  
  
`[ @automatic_post = ] automatic_post` 保留。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 所有使用排程的作業都會立即使用新設定。 不過，變更排程並不會停止目前在執行中的作業。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有 **系統管理員（sysadmin** ）的成員可以修改另一位使用者所擁有的排程。  
  
## <a name="examples"></a>範例  
 下列範例會將 `NightlyJobs` 排程的啟用狀態改成 `0`，並將擁有者設為 `terrid`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_schedule  
    @name = 'NightlyJobs',  
    @enabled = 0,  
    @owner_login_name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立排程並將其附加至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [排程作業](../../ssms/agent/schedule-a-job.md)   
 [建立排程](../../ssms/agent/create-a-schedule.md)   
 [&#40;Transact-sql&#41;的 SQL Server Agent 預存程式 ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
