---
title: sp_help_jobsteplog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobsteplog_TSQL
- sp_help_jobsteplog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobsteplog
ms.assetid: 1a0be7b1-8f31-4b4c-aadb-586c0e00ed04
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b6480c498914c4ec0bc02ba21552615bbdd28f6e
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535690"
---
# <a name="sphelpjobsteplog-transact-sql"></a>sp_help_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關特定中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式作業步驟記錄。 **sp_help_jobsteplog**不會傳回實際的記錄檔。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
     [ , [ @step_id = ] step_id ]  
     [ , [ @step_name = ] 'step_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] 'job_id'` 作業識別碼為其傳回作業步驟記錄資訊。 *job_id*已**int**，預設值是 NULL。  
  
`[ @job_name = ] 'job_name'` 作業名稱。 *job_name*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
`[ @step_id = ] step_id` 在 作業步驟的識別碼。 如果沒有包含這個識別碼，便會包含作業中的所有步驟。 *step_id*已**int**，預設值是 NULL。  
  
`[ @step_name = ] 'step_name'` 在 作業步驟的名稱。 *step_name*已**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作業的唯一識別碼。|  
|**job_name**|**sysname**|作業名稱。|  
|**step_id**|**int**|作業內的步驟識別碼。 例如，如果此步驟是第一個步驟，在作業中，其*step_id*為 1。|  
|**step_name**|**sysname**|作業中的步驟名稱。|  
|**step_uid**|**uniqueidentifier**|作業中的 (系統產生) 步驟的唯一識別碼。|  
|**date_created**|**datetime**|步驟的建立日期。|  
|**date_modified**|**datetime**|上次修改步驟的日期。|  
|**log_size**|**float**|作業步驟記錄的大小 (以 MB 為單位)。|  
|**log**|**nvarchar(max)**|作業步驟記錄輸出。|  
  
## <a name="remarks"></a>備註  
 **sp_help_jobsteplog**處於**msdb**資料庫。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 成員**SQLAgentUserRole**只能檢視他們擁有的作業步驟的作業步驟記錄中繼資料。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returns-job-step-log-information-for-all-steps-in-a-specific-job"></a>A. 傳回特定作業中所有步驟的作業步驟記錄資訊  
 下列範例會傳回名稱為 `Weekly Sales Data Backup` 之作業的所有作業步驟記錄資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup' ;  
GO  
```  
  
### <a name="b-return-job-step-log-information-about-a-specific-job-step"></a>B. 傳回特定作業步驟的作業步驟記錄資訊  
 下列範例會傳回名稱為 `Weekly Sales Data Backup` 之作業的第一個作業步驟的作業步驟記錄資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_delete_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)   
 [SQL Server Agent 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
