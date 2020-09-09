---
description: sp_help_jobschedule (Transact-SQL)
title: sp_help_jobschedule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5d74890ab154700159fcf6ca086f88cd2ac57409
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538819"
---
# <a name="sp_help_jobschedule-transact-sql"></a>sp_help_jobschedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 用來執行自動化活動之工作排程的相關資訊。  
 
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_jobschedule { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @schedule_name = ] 'schedule_name' ]  
     [ , [ @schedule_id = ] schedule_id ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id` 作業識別碼。 *job_id*是 **uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'` 作業的名稱。 *job_name*是 **sysname**，預設值是 Null。  
  
> [!NOTE]
> 必須指定 *job_id* 或 *job_name* ，但不能同時指定兩者。

`[ @schedule_name = ] 'schedule_name'` 作業的排程專案名稱。 *schedule_name*是 **sysname**，預設值是 Null。  
  
`[ @schedule_id = ] schedule_id` 作業的排程專案識別碼。 *schedule_id*是 **int**，預設值是 Null。  
  
`[ @include_description = ] include_description` 指定是否要在結果集中包含排程的描述。 *include_description* 是 **bit**，預設值是 **0**。 當 *include_description* 是 **0**時，不會將排程的描述包含在結果集中。 當 *include_description* 為 **1**時，排程的描述會包含在結果集中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|排程識別碼。|  
|**schedule_name**|**sysname**|排程的名稱。|  
|**啟用**|**int**| (**1**) 或未啟用排程 (**0**) 。|  
|**freq_type**|**int**|指出作業執行時間的值。<br /><br /> **1** = 一次<br /><br /> **4** = 每日<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月，相對於 **freq_interval**<br /><br /> **64** = 啟動 **SQLServerAgent** 服務時執行。|  
|**freq_interval**|**int**|執行作業的天數。 值取決於 **freq_type**的值。 如需詳細資訊，請參閱 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_type**|**int**|**Freq_subday_interval**的單位。 如需詳細資訊，請參閱 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_interval**|**int**|每次執行作業之間發生的 **freq_subday_type** 期間數。 如需詳細資訊，請參閱 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_relative_interval**|**int**|每個月的排程工作發生 **freq_interval** 。 如需詳細資訊，請參閱 [sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_recurrence_factor**|**int**|排程執行作業的間隔月數。|  
|**active_start_date**|**int**|排程的開始日期。|  
|**active_end_date**|**int**|排程的結束日期。|  
|**active_start_time**|**int**|排程開始的日期時間。|  
|**active_end_time**|**int**|排程結束的日期時間。|  
|**date_created**|**datetime**|排程的建立日期。|  
|**schedule_description**|**nvarchar(4000)**|從 **msdb.dbo.sys**排程中的值衍生的排程的英文描述。 當 *include_description* 是 **0**時，此資料行會包含文字，指出未要求描述。|  
|**next_run_date**|**int**|排程下次執行作業的日期。|  
|**next_run_time**|**int**|排程下次執行作業的時間。|  
|**schedule_uid**|**uniqueidentifier**|排程的識別碼。|  
|**job_count**|**int**|傳回的作業計數。|  
  
> **注意： sp_help_jobschedule** 會從 **dbo.sysjobschedules** 傳回值，並 **dbo.sys** 排程 **msdb**中的系統資料表。 **sysjobschedules** 每隔20分鐘更新一次。 這可能會影響這個預存程序所傳回的值。  
  
## <a name="remarks"></a>備註  
 **Sp_help_jobschedule**的參數只能用於特定組合。 如果指定 *schedule_id* ，就不能同時指定 *job_id* 和 *job_name* 。 否則， *job_id* 或 *job_name* 參數可以搭配 *schedule_name*使用。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **SQLAgentUserRole**的成員只能看到他們所擁有之作業排程的屬性。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-job-schedule-for-a-specific-job"></a>A. 傳回特定作業的作業排程  
 下列範例會傳回名稱為 `BackupDatabase` 之作業的排程資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'BackupDatabase' ;  
GO  
```  
  
### <a name="b-returning-the-job-schedule-for-a-specific-schedule"></a>B. 傳回特定排程的作業排程  
 下列範例會傳回名稱為 `NightlyJobs` 的排程和名稱為 `RunReports` 之作業的資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule   
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="c-returning-the-job-schedule-and-schedule-description-for-a-specific-schedule"></a>C. 傳回特定排程的作業排程和排程描述  
 下列範例會傳回名稱為 `NightlyJobs` 的排程和名稱為 `RunReports` 之作業的資訊。 傳回的結果集包含排程的描述。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobschedule  
    @job_name = N'RunReports',  
    @schedule_name = N'NightlyJobs',  
    @include_description = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
