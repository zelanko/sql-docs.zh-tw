---
title: sp_help_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_schedule
- sp_help_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_schedule
ms.assetid: b2fc4ce1-0a8e-44d2-b206-7dc7b258d8c9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2b14900e32c32a5de50998580a8d0de9ed7eacfb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720303"
---
# <a name="sp_help_schedule-transact-sql"></a>sp_help_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  列出排程的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_schedule   
     [ @schedule_id = ] id ,  
     [ @schedule_name = ] 'schedule_name'   
     [ , [ @attached_schedules_only = ] attached_schedules_only ]  
     [ , [ @include_description = ] include_description ]  
```  
  
## <a name="arguments"></a>引數  
`[ @schedule_id = ] id`要列出的排程識別碼。 *schedule_name*是**int**，沒有預設值。 可以指定*schedule_id*或*schedule_name* 。  
  
`[ @schedule_name = ] 'schedule_name'`要列出的排程名稱。 *schedule_name*是**sysname**，沒有預設值。 可以指定*schedule_id*或*schedule_name* 。  
  
`[ @attached_schedules_only = ] attached_schedules_only ]`指定是否只顯示作業所附加的排程。 *attached_schedules_only*是**bit**，預設值是**0**。 當*attached_schedules_only*為**0**時，會顯示所有排程。 當*attached_schedules_only*為**1**時，結果集只會包含附加至作業的排程。  
  
`[ @include_description = ] include_description`指定是否要在結果集中包含描述。 *include_description*是**bit**，預設值是**0**。 當*include_description*是**0**時，結果集的*schedule_description*資料行就會包含預留位置。 當*include_description*為**1**時，排程的描述就會包含在結果集中。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 這個程序會傳回下列結果集：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|排程識別碼。|  
|**schedule_uid**|**uniqueidentifier**|排程的識別碼。|  
|**schedule_name**|**sysname**|排程的名稱。|  
|**後**|**int**|排程是否已啟用（**1**）或未啟用（**0**）。|  
|**freq_type**|**int**|指出作業執行時間的值。<br /><br /> **1** = 一次<br /><br /> **4** = 每天<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月，相對於**freq_interval**<br /><br /> **64** = 在 SQLServerAgent 服務啟動時執行。|  
|**freq_interval**|**int**|執行作業的天數。 此值取決於**freq_type**的值。 如需詳細資訊，請參閱[sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_type**|**int**|**Freq_subday_interval**的單位。 如需詳細資訊，請參閱[sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_interval**|**int**|每次執行作業之間所發生的**freq_subday_type**週期數。 如需詳細資訊，請參閱[sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_relative_interval**|**int**|排程作業在每個月的**freq_interval**發生次數。 如需詳細資訊，請參閱[sp_add_schedule &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_recurrence_factor**|**int**|排程執行作業的間隔月數。|  
|**active_start_date**|**int**|排程的開始日期。|  
|**active_end_date**|**int**|排程的結束日期。|  
|**active_start_time**|**int**|排程開始的日期時間。|  
|**active_end_time**|**int**|排程結束的日期時間。|  
|**date_created**|**datetime**|排程的建立日期。|  
|**schedule_description**|**nvarchar(4000)**|排程的英文描述 (若要求的話)。|  
|**job_count**|**int**|傳回參考這個排程的工作數目。|  
  
## <a name="remarks"></a>備註  
 未提供任何參數時， **sp_help_schedule**會列出實例中所有排程的資訊。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **SQLAgentUserRole**的成員只能查看他們所擁有的排程。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-information-for-all-schedules-in-the-instance"></a>A. 列出執行個體中所有排程的資訊  
 下列範例會列出執行個體中所有排程的資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-schedule"></a>B. 列出特定排程的資訊  
 下列範例會列出名稱為 `NightlyJobs` 之排程的資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
