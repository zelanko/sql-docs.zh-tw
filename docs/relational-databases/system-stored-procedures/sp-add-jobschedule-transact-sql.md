---
title: "sp_add_jobschedule (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3b2680a591628811fb9617077700d05981ece2a2
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="spaddjobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立作業的排程。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
```  
  
## <a name="arguments"></a>引數  
 [  **@job_id=** ] *job_id*  
 要加入排程的作業識別碼。 *job_id*是**uniqueidentifier**，沒有預設值。  
  
 [  **@job_name=** ] **'***job_name***'**  
 要加入排程的作業名稱。 *job_name*是**nvarchar （128)**，沒有預設值。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必須指定，但不可同時指定兩者。  
  
 [  **@name=** ] **'***名稱***'**  
 排程的名稱。 *名稱*是**nvarchar （128)**，沒有預設值。  
  
 [  **@enabled=** ] *enabled_flag*  
 指出排程的目前狀態。 *enabled_flag*是**tinyint**，預設值是**1** （啟用）。 如果**0**，未啟用排程。 停用排程時，就不會執行作業。  
  
 [  **@freq_type=** ] *frequency_type*  
 指出作業執行時間的值。 *frequency_type*是**int**，預設值是**0**，而且可以是下列值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月，相對於*frequency_interval。*|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務啟動時執行。|  
|**128**|在電腦閒置時執行。|  
  
 [  **@freq_interval=** ] *frequency_interval*  
 執行作業的天數。 *frequency_interval*是**int**，預設值是 0，而定的值*frequency_type*下表所示：  
  
|ReplTest1|效果|  
|-----------|------------|  
|**1** （一次）|*frequency_interval*未使用。|  
|**4** （每天）|每個*frequency_interval*天。|  
|**8** （每週）|*frequency_interval*是下列一或多個項目 （使用 OR 邏輯運算子結合）：<br /><br /> 1 = 星期日<br /><br /> 2 = 星期一<br /><br /> 4 = 星期二<br /><br /> 8 = 星期三<br /><br /> 16 = 星期四<br /><br /> 32 = 星期五<br /><br /> 64 = 星期六|  
|**16** （每月）|在*frequency_interval*月份的日期。|  
|**32** （每月相對）|*frequency_interval*是下列其中之一：<br /><br /> 1 = 星期日<br /><br /> 2 = 星期一<br /><br /> 3 = 星期二<br /><br /> 4 = 星期三<br /><br /> 5 = 星期四<br /><br /> 6 = 星期五<br /><br /> 7 = 星期六<br /><br /> 8 = 日<br /><br /> 9 = 工作日<br /><br /> 10 = 週末|  
|**64** (當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 服務啟動)|*frequency_interval*未使用。|  
|**128**|*frequency_interval*未使用。|  
  
 [  **@freq_subday_type=** ] *frequency_subday_type*  
 指定的單位*frequency_subday_interval*。 *frequency_subday_type*是**int**，沒有預設值，它可以是下列值之一：  
  
|ReplTest1|描述 (單位)|  
|-----------|--------------------------|  
|**0x1**|在指定的時間|  
|**0x4**|Minutes|  
|**0x8**|小時|  
  
 [  **@freq_subday_interval=** ] *frequency_subday_interval*  
 數目*frequency_subday_type*期間每次執行作業之間發生。 *frequency_subday_interval*是**int**，預設值是 0。  
  
 [  **@freq_relative_interval=** ] *frequency_relative_interval*  
 進一步定義*frequency_interval*時*frequency_type*設**32** （每月相對）。  
  
 *frequency_relative_interval*是**int**，沒有預設值，它可以是下列值之一：  
  
|ReplTest1|描述 (單位)|  
|-----------|--------------------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
 *frequency_relative_interval*表示的間隔發生。 例如，如果*frequency_relative_interval*設**2**， *frequency_type*設為**32**，和*frequency_間隔*設**3**，排程的工作就會在每個月的第二個星期二發佈。  
  
 [  **@freq_recurrence_factor=** ] *frequency_recurrence_factor*  
 作業的各排程執行之間的週數或月數。 *frequency_recurrence_factor*才會使用*frequency_type*設**8**， **16**，或**32**。 *frequency_recurrence_factor*是**int**，預設值是 0。  
  
 [  **@active_start_date=** ] *active_start_date*  
 作業執行可以開始的日期。 *active_start_date*是**int**，沒有預設值。 日期格式為 YYYYMMDD。 如果*active_start_date*設定日期必須大於或等於 19900101。  
  
 建立排程之後，檢閱開始日期，並確認該日期正確。 如需詳細資訊，請參閱 「 排程開始日期 」 一節中[建立及附加排程至作業](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)。  
  
 [  **@active_end_date=** ] *active_end_date*  
 作業執行可以停止的日期。 *active_end_date*是**int**，沒有預設值。 日期格式為 YYYYMMDD。  
  
 [  **@active_start_time=** ] *active_start_time*  
 之間任何一天時間*active_start_date*和*active_end_date*開始執行作業。 *active_start_time*是**int**，沒有預設值。 時間格式為使用 24 小時制的 HHMMSS。  
  
 [  **@active_end_time=***active_end_time*  
 之間任何一天時間*active_start_date*和*active_end_date*結束執行作業。 *active_end_time*是**int**，沒有預設值。 時間格式為使用 24 小時制的 HHMMSS。  
  
 [  **@schedule_id=***schedule_id***輸出**  
 成功建立排程時，指派給這個排程的排程識別碼。 *schedule_id*是 output 變數的型別**int**，沒有預設值。  
  
 [  **@schedule_uid** =] *schedule_uid***輸出**  
 排程的唯一識別碼。 *schedule_uid*這類型的變數**uniqueidentifier**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 現在，您可以在作業之外，獨立管理作業排程。 若要加入至作業的排程，使用**sp_add_schedule**建立排程及**sp_attach_schedule**將排程附加至作業。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
 
 ## <a name="example"></a>範例
 下列範例會指定作業排程`SaturdayReports`會同時執行每個星期六的上午 2:00。
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>請參閱  
 [建立並附加排程至作業](http://msdn.microsoft.com/library/079c2984-0052-4a37-a2b8-4ece56e6b6b5)   
 [排程的作業](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)   
 [建立排程](http://msdn.microsoft.com/library/8c7ef3b3-c06d-4a27-802d-ed329dc86ef3)   
 [SQL Server Agent 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
