---
title: sp_add_jobschedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7c7f644b94c405fa4072ecd7d7c448f6ea865404
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85879974"
---
# <a name="sp_add_jobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  建立 SQL 代理程式作業的排程。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

## <a name="syntax"></a>語法  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]
     [ , [ @schedule_uid = ] _schedule_uid OUTPUT ]
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id`要加入排程之作業的作業識別碼。 *job_id*是**uniqueidentifier**，沒有預設值。  
  
`[ @job_name = ] 'job_name'`要加入排程的作業名稱。 *job_name*是**Nvarchar （128）**，沒有預設值。  
  
> [!NOTE]  
>  必須指定*job_id*或*job_name* ，但不能同時指定兩者。  
  
`[ @name = ] 'name'`排程的名稱。 *名稱*為**Nvarchar （128）**，沒有預設值。  
  
`[ @enabled = ] enabled_flag`指出排程的目前狀態。 *enabled_flag*是**Tinyint**，預設值是**1** （已啟用）。 如果為**0**，則不會啟用排程。 停用排程時，就不會執行作業。  
  
`[ @freq_type = ] frequency_type`指出作業執行時間的值。 *frequency_type*是**int**，預設值是**0**，它可以是下列其中一個值：  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月，相對於*frequency_interval。*|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務啟動時執行。|  
|**128**|在電腦閒置時執行。|  
  
`[ @freq_interval = ] frequency_interval`執行作業的日期。 *frequency_interval*是**int**，預設值是0，而且取決於下表所示的*frequency_type*值：  
  
|值|效果|  
|-----------|------------|  
|**1** （一次）|未使用*frequency_interval* 。|  
|**4** （每日）|每*frequency_interval*天。|  
|**8** （每週）|*frequency_interval*是下列一或多個（與 or 邏輯運算子結合）：<br /><br /> 1 = 星期日<br /><br /> 2 = 星期一<br /><br /> 4 = 星期二<br /><br /> 8 = 星期三<br /><br /> 16 = 星期四<br /><br /> 32 = 星期五<br /><br /> 64 = 星期六|  
|**16** （每月）|在當月的*frequency_interval*天。|  
|**32** （每月相對）|*frequency_interval*為下列其中一項：<br /><br /> 1 = 星期日<br /><br /> 2 = 星期一<br /><br /> 3 = 星期二<br /><br /> 4 = 星期三<br /><br /> 5 = 星期四<br /><br /> 6 = 星期五<br /><br /> 7 = 星期六<br /><br /> 8 = 日<br /><br /> 9 = 工作日<br /><br /> 10 = 週末|  
|**64** （當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務啟動時）|未使用*frequency_interval* 。|  
|**128**|未使用*frequency_interval* 。|  
  
`[ @freq_subday_type = ] frequency_subday_type`指定*frequency_subday_interval*的單位。 *frequency_subday_type*是**int**，沒有預設值，而且可以是下列其中一個值：  
  
|值|描述 (單位)|  
|-----------|--------------------------|  
|**0x1**|在指定的時間|  
|**0x4**|分鐘|  
|**0x8**|小時|  
  
`[ @freq_subday_interval = ] frequency_subday_interval`每次執行作業之間所發生的*frequency_subday_type*週期數。 *frequency_subday_interval*是**int**，預設值是0。  
  
`[ @freq_relative_interval = ] frequency_relative_interval`當*frequency_type*設定為**32** （每月相對）時，進一步定義*frequency_interval* 。  
  
 *frequency_relative_interval*是**int**，沒有預設值，而且可以是下列其中一個值：  
  
|值|描述 (單位)|  
|-----------|--------------------------|  
|**1**|First|  
|**2**|Second|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|Last|  
  
 *frequency_relative_interval*指出間隔的出現次數。 例如，如果*frequency_relative_interval*設定為**2**， *frequency_type*設定為**32**，而*frequency_interval*設定為**3**，則排程工作會在每個月的第二個星期二發生。  
  
`[ @freq_recurrence_factor = ] frequency_recurrence_factor`作業的排程執行之間的周數或月數。 只有在*frequency_type*設定為**8**、 **16**或**32**時，才會使用*frequency_recurrence_factor* 。 *frequency_recurrence_factor*是**int**，預設值是0。  
  
`[ @active_start_date = ] active_start_date`可以開始執行作業的日期。 *active_start_date*是**int**，沒有預設值。 日期格式為 YYYYMMDD。 如果已設定*active_start_date* ，則日期必須大於或等於19900101。  
  
 建立排程之後，檢閱開始日期，並確認該日期正確。 如需詳細資訊，請參閱[建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)中的「排程開始日期」一節。  
  
`[ @active_end_date = ] active_end_date`作業執行可以停止的日期。 *active_end_date*是**int**，沒有預設值。 日期格式為 YYYYMMDD。  
  
`[ @active_start_time = ] active_start_time`在*active_start_date*和*active_end_date*之間的任何一天開始執行作業的時間。 *active_start_time*是**int**，沒有預設值。 時間格式為使用 24 小時制的 HHMMSS。  
  
`[ @active_end_time = active_end_time_`*Active_start_date*和*active_end_date*之間任何一天的時間，以結束作業執行。 *active_end_time*是**int**，沒有預設值。 時間格式為使用 24 小時制的 HHMMSS。  
  
`[ @schedule_id = schedule_idOUTPUT`已成功建立排程的排程識別碼。 *schedule_id*是**int**類型的輸出變數，沒有預設值。  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT`排程的唯一識別碼。 *schedule_uid*是**uniqueidentifier**類型的變數。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 現在，您可以在作業之外，獨立管理作業排程。 若要將排程加入作業，請使用**sp_add_schedule**來建立排程，並**sp_attach_schedule**將排程附加至作業。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
 
 ## <a name="example"></a>範例
 下列範例會將作業排程指派給 `SaturdayReports` 每個星期六的上午2:00 執行。
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>另請參閱  
 [建立排程並將其附加至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [排程作業](../../ssms/agent/schedule-a-job.md)   
 [建立排程](../../ssms/agent/create-a-schedule.md)   
 [SQL Server Agent 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
