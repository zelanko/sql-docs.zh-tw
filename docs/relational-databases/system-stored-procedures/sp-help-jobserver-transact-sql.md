---
title: sp_help_jobserver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobserver
- sp_help_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobserver
ms.assetid: 57971787-f9f5-4199-9f64-c2b61a308906
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6a1a2ce1208dcf359bb0586c3de1fe294644e3a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054885"
---
# <a name="sphelpjobserver-transact-sql"></a>sp_help_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回給定作業之伺服器的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_jobserver  
     { [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name' }  
     [ , [ @show_last_run_details = ] show_last_run_details ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id` 作業識別碼為其傳回的資訊。 *job_id*已**uniqueidentifier**，預設值是 NULL。  
  
`[ @job_name = ] 'job_name'` 要傳回資訊的作業名稱。 *job_name*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
`[ @show_last_run_details = ] show_last_run_details` 這是上次執行的執行資訊是否結果集的一部分。 *show_last_run_details*已**tinyint**，預設值是**0**。 **0**不包含上次執行的詳細資訊，並**1**沒有。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|目標伺服器的識別碼。|  
|**server_name**|**nvarchar(30)**|目標伺服器的電腦名稱。|  
|**enlist_date**|**datetime**|將目標伺服器編列到主要伺服器的日期。|  
|**last_poll_date**|**datetime**|目標伺服器前次輪詢主要伺服器的日期。|  
  
 如果**sp_help_jobserver**內含*show_last_run_details*設定為**1**，結果集具有下列額外的資料行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**last_run_date**|**int**|在這部目標伺服器中上次開始執行作業的日期。|  
|**last_run_time**|**int**|在這部伺服器中上次開始執行作業的時間。|  
|**last_run_duration**|**int**|前次在這部目標伺服器執行作業的持續時間 (以秒為單位)。|  
|**last_outcome_message**|**nvarchar(1024)**|描述作業前次的結果。|  
|**last_run_outcome**|**int**|前次在這部伺服器執行作業的結果：<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **3** = 取消<br /><br /> **5** = 未知|  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 成員**SQLAgentUserRole**只能檢視他們擁有之作業的資訊。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `NightlyBackups` 作業的相關資訊，其中包括上次執行的資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobserver  
    @job_name = N'NightlyBackups',  
    @show_last_run_details = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
