---
title: sp_help_schedule (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: f5a68160c8aee1bcb399513051e1f4cc35cea970
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085209"
---
# <a name="sphelpschedule-transact-sql"></a>sp_help_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @schedule_id = ] id` 要列出的排程識別碼。 *schedule_name&lt*已**int**，沒有預設值。 任一*schedule_id*或是*schedule_name&lt*可能指定。  
  
`[ @schedule_name = ] 'schedule_name'` 要列出的排程名稱。 *schedule_name&lt*已**sysname**，沒有預設值。 任一*schedule_id*或是*schedule_name&lt*可能指定。  
  
`[ @attached_schedules_only = ] attached_schedules_only ]` 指定是否只顯示排程作業所連接到。 *attached_schedules_only*已**位元**，預設值是**0**。 當*attached_schedules_only*是**0**，會顯示所有排程。 當*attached_schedules_only*是**1**，結果集包含附加至作業的排程。  
  
`[ @include_description = ] include_description` 指定是否要在結果集中併入說明。 *include_description*已**位元**，預設值是**0**。 當*include_description*是**0**，則*schedule_description*結果集的資料行包含預留位置。 當*include_description*是**1**，排程的描述包含在結果集中。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 這個程序會傳回下列結果集：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|排程識別碼。|  
|**schedule_uid**|**uniqueidentifier**|排程的識別碼。|  
|**schedule_name**|**sysname**|排程的名稱。|  
|**enabled**|**int**|是否要啟用排程 (**1**)，或未啟用 (**0**)。|  
|**freq_type**|**int**|指出作業執行時間的值。<br /><br /> **1** = 一次<br /><br /> **4** = 每天<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月，相對於**freq_interval**<br /><br /> **64** = 執行 SQLServerAgent 服務啟動時。|  
|**freq_interval**|**int**|執行作業的天數。 值的值需視**freq_type**。 如需詳細資訊，請參閱 < [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_type**|**int**|單位**freq_subday_interval**。 如需詳細資訊，請參閱 < [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_subday_interval**|**int**|數目**freq_subday_type**期間每次執行作業之間發生。 如需詳細資訊，請參閱 < [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_relative_interval**|**int**|排程作業的次數**freq_interval**中每個月。 如需詳細資訊，請參閱 < [sp_add_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)。|  
|**freq_recurrence_factor**|**int**|排程執行作業的間隔月數。|  
|**active_start_date**|**int**|排程的開始日期。|  
|**active_end_date**|**int**|排程的結束日期。|  
|**active_start_time**|**int**|排程開始的日期時間。|  
|**active_end_time**|**int**|排程結束的日期時間。|  
|**date_created**|**datetime**|排程的建立日期。|  
|**schedule_description**|**nvarchar(4000)**|排程的英文描述 (若要求的話)。|  
|**job_count**|**int**|傳回參考這個排程的工作數目。|  
  
## <a name="remarks"></a>備註  
 當未不提供任何參數時， **sp_help_schedule**列出執行個體中的所有排程的資訊。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 成員**SQLAgentUserRole**只能檢視他們自己的排程。  
  
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
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
