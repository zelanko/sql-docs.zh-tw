---
title: sp_add_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_schedule_TSQL
- sp_add_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_schedule
ms.assetid: 9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 21fe2a05c87caf5270967381e9ebeefc1069729f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "70810391"
---
# <a name="sp_add_schedule-transact-sql"></a>sp_add_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  建立可供任意數量的作業使用的排程。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_schedule [ @schedule_name = ] 'schedule_name'   
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
    [ , [ @schedule_uid = ] schedule_uid OUTPUT ]  
    [ , [ @schedule_id = ] schedule_id OUTPUT ]  
    [ , [ @originating_server = ] server_name ] /* internal */  
```  
  
## <a name="arguments"></a>引數  
`[ @schedule_name = ] 'schedule_name'`排程的名稱。 *schedule_name*是**sysname**，沒有預設值。  
  
`[ @enabled = ] enabled`指出排程的目前狀態。 [*已啟用*] 是**Tinyint**，預設值是**1** （已啟用）。 如果為**0**，則不會啟用排程。 當未啟用排程時，不會依據這份排程來執行任何作業。  
  
`[ @freq_type = ] freq_type`值，表示要執行作業的時間。 *freq_type*是**int**，預設值是**0**，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**4**|每日|  
|**8**|每週|  
|**1600**|每月|  
|**32**|每月，相對於*freq_interval*|  
|**64**|當 SQL 代理程式服務啟動時執行|  
|**128**|在電腦閒置時執行（ [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)不支援） |  
  
`[ @freq_interval = ] freq_interval`執行作業的天數。 *freq_interval*是**int**，預設值是**1**，且取決於*freq_type*的值。  
  
|*Freq_type*的值|對*freq_interval*的影響|  
|---------------------------|--------------------------------|  
|**1** （一次）|未使用*freq_interval* 。|  
|**4** （每日）|每*freq_interval*天。|  
|**8** （每週）|*freq_interval*是下列一或多個（與 or 邏輯運算子結合）：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **4** = 星期二<br /><br /> **8** = 星期三<br /><br /> **16** = 星期四<br /><br /> **32** = 星期五<br /><br /> **64** = 星期六|  
|**16** （每月）|在當月的*freq_interval*天。|  
|**32** （每月相對）|*freq_interval*為下列其中一項：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 日<br /><br /> **9** = 工作日<br /><br /> **10** = 週末|  
|**64** （當 SQLServerAgent 服務啟動時）|未使用*freq_interval* 。|  
|**128**|未使用*freq_interval* 。|  
  
`[ @freq_subday_type = ] freq_subday_type`指定*freq_subday_interval*的單位。 *freq_subday_type*是**int**，預設值是**0**，它可以是下列值之一。  
  
|值|描述 (單位)|  
|-----------|--------------------------|  
|**0x1**|在指定的時間|  
|**0x2**|秒|  
|**0x4**|分鐘|  
|**0x8**|小時|  
  
`[ @freq_subday_interval = ] freq_subday_interval`每次執行作業之間所發生的*freq_subday_type*週期數。 *freq_subday_interval*是**int**，預設值是**0**。 附註：間隔長度不應大於 10 秒。 在*freq_subday_type*等於**1**的情況下，會忽略*freq_subday_interval* 。  
  
`[ @freq_relative_interval = ] freq_relative_interval`如果*freq_interval*為32（每月相對），則會在每個月的*freq_interval*作業發生。 *freq_relative_interval*是**int**，預設值是**0**，它可以是下列值之一。 在*freq_type*不等於32的情況下，會忽略*freq_relative_interval* 。  
  
|值|描述 (單位)|  
|-----------|--------------------------|  
|**1**|First|  
|**2**|Second|  
|**4**|第三個|  
|**8**|第四個|  
|**1600**|Last|  
  
`[ @freq_recurrence_factor = ] freq_recurrence_factor`作業的排程執行之間的周數或月數。 只有在*freq_type*是**8**、 **16**或**32**時，才會使用*freq_recurrence_factor* 。 *freq_recurrence_factor*是**int**，預設值是**0**。  
  
`[ @active_start_date = ] active_start_date`可以開始執行作業的日期。 *active_start_date*是**int**，預設值是 Null，表示今天的日期。 日期格式為 YYYYMMDD。 如果*active_start_date*不是 Null，則日期必須大於或等於19900101。  
  
 建立排程之後，檢閱開始日期，並確認該日期正確。 如需詳細資訊，請參閱[建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)中的「排程開始日期」一節。  
  
 若為每週或每月排程，代理程式會對 active_start_date 已是過去日期予以忽略，而將改為使用目前的日期。 使用 sp_add_schedule 建立 SQL 代理程式排程時，有一個選項可指定 active_start_date 參數，表示將要開始執行作業的日期。 如果排程類型是每週或每月，而且 active_start_date 參數設定為過去的日期，便會忽略 active_start_date 參數，並使用目前的日期做為 active_start_date。  
  
`[ @active_end_date = ] active_end_date`作業執行可以停止的日期。 *active_end_date*是**int**，預設值是**99991231**，表示9999年12月31日。 格式為 YYYYMMDD。  
  
`[ @active_start_time = ] active_start_time`*Active_start_date*和*active_end_date*之間的任何一天開始執行作業的時間。 *active_start_time*是**int**，預設值是**000000**，表示 12:00:00 A.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @active_end_time = ] active_end_time`*Active_start_date*和*active_end_date*之間的任何一天結束執行作業的時間。 *active_end_time*是**int**，預設值是**235959**，表示 11:59:59 P.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @owner_login_name = ] 'owner_login_name'`擁有排程之伺服器主體的名稱。 *owner_login_name*是**sysname**，預設值是 Null，表示排程是建立者所擁有。  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT`排程的唯一識別碼。 *schedule_uid*是**uniqueidentifier**類型的變數。  
  
`[ @schedule_id = ] _schedule_idOUTPUT`排程的識別碼。 *schedule_id*是**int**類型的變數。  
  
`[ @originating_server = ] server_name` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-schedule"></a>A. 建立排程  
 下列範例會建立一份名稱為 `RunOnce` 的排程。 這份排程會在建立排程當日的 `23:30` 執行一次。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_schedule  
    @schedule_name = N'RunOnce',  
    @freq_type = 1,  
    @active_start_time = 233000 ;  
  
GO  
```  
  
### <a name="b-creating-a-schedule-attaching-the-schedule-to-multiple-jobs"></a>B. 建立一份排程，將排程附加至多項作業  
 下列範例會建立一份名稱為 `NightlyJobs` 的排程。 每天伺服器時間到了 `01:00` 時，就會開始執行使用這份排程的作業。 這個範例會將排程附加至 `BackupDatabase` 作業和 `RunReports` 作業上。  
  
> [!NOTE]  
>  這個範例假設 `BackupDatabase` 作業和 `RunReports` 作業都已經存在。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立排程並將其附加至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [排程作業](../../ssms/agent/schedule-a-job.md)   
 [建立排程](../../ssms/agent/create-a-schedule.md)   
 [SQL Server Agent 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_jobschedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
