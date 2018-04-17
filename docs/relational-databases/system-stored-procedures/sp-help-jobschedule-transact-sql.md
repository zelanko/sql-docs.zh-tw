---
title: sp_help_jobschedule (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_jobschedule
- sp_help_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobschedule
ms.assetid: 2cded902-9272-4667-ac4b-a4f95a9f008e
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 731857bc70bcda1c7817db6e2cdc7eed3ad68236
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpjobschedule-transact-sql"></a>sp_help_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@job_id=** ] *job_id*  
 作業識別碼。 *job_id*是**uniqueidentifier**，預設值是 NULL。  
  
 [ **@job_name=** ] **'***job_name***'**  
 作業的名稱。 *job_name*是**sysname**，預設值是 NULL。  
  
> **注意：**任一*job_id*或*job_name*必須指定，但不可同時指定兩者。  
  
 [  **@schedule_name=** ] **'***schedule_name***'**  
 作業的排程項目名稱。 *schedule_name*是**sysname**，預設值是 NULL。  
  
 [ **@schedule_id=** ] *schedule_id*  
 作業的排程項目識別碼。 *schedule_id*是**int**，預設值是 NULL。  
  
 [  **@include_description=** ] *include_description*  
 指定結果集中是否要包含排程的描述。 *include_description*是**元**，預設值是**0**。 當*include_description*是**0**，排程的描述不包含在結果集中。 當*include_description*是**1**，排程的描述包含在結果集中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|排程識別碼。|  
|**schedule_name**|**sysname**|排程的名稱。|  
|**enabled**|**int**|是否要啟用排程 (**1**) 或未啟用 (**0**)。|  
|**freq_type**|**int**|指出作業執行時間的值。<br /><br /> **1** = 一次<br /><br /> **4** = 每天<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月，相對於**freq_interval**<br /><br /> **64** = 時執行**SQLServerAgent**服務啟動。|  
|**freq_interval**|**int**|執行作業的天數。 值取決於值**freq_type**。 如需詳細資訊，請參閱[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_type**|**int**|單位**freq_subday_interval**。 如需詳細資訊，請參閱[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_interval**|**int**|數目**freq_subday_type**期間每次執行作業之間發生。 如需詳細資訊，請參閱[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_relative_interval**|**int**|排程作業的次數**freq_interval**中每個月。 如需詳細資訊，請參閱[sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_recurrence_factor**|**int**|排程執行作業的間隔月數。|  
|**active_start_date**|**int**|排程的開始日期。|  
|**active_end_date**|**int**|排程的結束日期。|  
|**active_start_time**|**int**|排程開始的日期時間。|  
|**active_end_time**|**int**|排程結束的日期時間。|  
|**date_created**|**datetime**|排程的建立日期。|  
|**schedule_description**|**nvarchar(4000)**|衍生自中值的排程的英文描述**msdb.dbo.sysschedules**。 當*include_description*是**0**，此資料行包含文字指出不要求描述。|  
|**next_run_date**|**int**|排程下次執行作業的日期。|  
|**next_run_time**|**int**|排程下次執行作業的時間。|  
|**schedule_uid**|**uniqueidentifier**|排程的識別碼。|  
|**job_count**|**int**|傳回的作業計數。|  
  
> **注意：****sp_help_jobschedule**傳回值，從**dbo.sysschedules**和**dbo.sysjobschedules**系統資料表的**msdb**.   **sysjobschedules**每 20 分鐘會更新。 這可能會影響這個預存程序所傳回的值。  
  
## <a name="remarks"></a>備註  
 參數的**sp_help_jobschedule**可以只能用在特定的組合。 如果*schedule_id*指定，則兩者都不*job_id*也*job_name*可以指定。 否則， *job_id*或*job_name*參數可以搭配*schedule_name*。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 成員**SQLAgentUserRole**只能檢視他們自己的作業排程的屬性。  
  
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
 [sp_add_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
