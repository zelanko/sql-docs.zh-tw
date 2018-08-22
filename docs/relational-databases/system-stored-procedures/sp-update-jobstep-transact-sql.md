---
title: sp_update_jobstep (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43dfe2a04a6c4f12fad0df12c3cf520d7d08d7a7
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394028"
---
# <a name="spupdatejobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更用來執行自動化活動之作業步驟的設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_update_jobstep   
     {   [@job_id =] job_id   
       | [@job_name =] 'job_name' } ,  
     [@step_id =] step_id  
     [ , [@step_name =] 'step_name' ]  
     [ , [@subsystem =] 'subsystem' ]   
     [ , [@command =] 'command' ]  
     [ , [@additional_parameters =] 'parameters' ]  
     [ , [@cmdexec_success_code =] success_code ]  
     [ , [@on_success_action =] success_action ]   
     [ , [@on_success_step_id =] success_step_id ]  
     [ , [@on_fail_action =] fail_action ]   
     [ , [@on_fail_step_id =] fail_step_id ]  
     [ , [@server =] 'server' ]   
     [ , [@database_name =] 'database' ]  
     [ , [@database_user_name =] 'user' ]   
     [ , [@retry_attempts =] retry_attempts ]  
     [ , [@retry_interval =] retry_interval ]   
     [ , [@os_run_priority =] run_priority ]  
     [ , [@output_file_name =] 'file_name' ]   
     [ , [@flags =] flags ]  
     [ ,  {   [ @proxy_id = ] proxy_id   
            | [ @proxy_name = ] 'proxy_name' }   
```  
  
## <a name="arguments"></a>引數  
 [ **@job_id =**] *job_id*  
 這是步驟所屬之作業的識別碼。 *job_id*已**uniqueidentifier**，預設值是 NULL。 任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
 [ **@job_name =**] **'***job_name***'**  
 這是步驟所屬的作業名稱。 *job_name*已**sysname**，預設值是 NULL。 任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
 [ **@step_id =**] *step_id*  
 要修改的作業步驟的識別碼。 無法變更這個識別碼。 *step_id*已**int**，沒有預設值。  
  
 [ **@step_name =**] **'***step_name***'**  
 這是步驟的新名稱。 *step_name*已**sysname**，預設值是 NULL。  
  
 [ **@subsystem =**] **'***subsystem***'**  
 Microsoft SQL Server Agent 執行子系統*命令*。 *子系統*已**nvarchar(40)**，預設值是 NULL。  
  
 [  **@command =**] **'***命令***'**  
 若要透過執行命令*子系統*。 *命令*已**nvarchar （max)**，預設值是 NULL。  
  
 [ **@additional_parameters =**] **'***parameters***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@cmdexec_success_code =**] *success_code*  
 所傳回的值**CmdExec**子系統命令，以指出*命令*順利執行。 *success_code*已**int**，預設值是 NULL。  
  
 [ **@on_success_action =**] *success_action*  
 要執行步驟成功時的動作。*success_action*是**tinyint**，預設值是 NULL，而且可以是下列值之一。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**1**|成功而結束。|  
|**2**|失敗而結束。|  
|**3**|移至下一步驟。|  
|**4**|請移至步驟*success_step_id。*|  
  
 [ **@on_success_step_id =**] *success_step_id*  
 如果步驟成功執行此作業中步驟的識別碼和*success_action*是**4**。 *success_step_id*已**int**，預設值是 NULL。  
  
 [ **@on_fail_action =**] *fail_action*  
 步驟失敗時所要執行的動作。 *fail_action*已**tinyint**，預設值是 NULL，而且可以有下列值之一。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**1**|成功而結束。|  
|**2**|失敗而結束。|  
|**3**|移至下一步驟。|  
|**4**|請移至步驟*fail_step_id * *。*|  
  
 [ **@on_fail_step_id =**] *fail_step_id*  
 步驟失敗時執行此作業中步驟的識別碼和*fail_action*是**4**。 *fail_step_id*已**int**，預設值是 NULL。  
  
 [ **@server =**] **'***server***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *伺服器*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>**，預設值是 NULL。  
  
 [ **@database_name =**] **'***database***'**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 步驟執行所在的資料庫名稱。 *資料庫*已**sysname**。 不允許以括號 ([ ]) 括住的名稱。 預設值是 NULL。  
  
 [ **@database_user_name =**] **'***user***'**  
 執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 步驟時所用的使用者帳戶名稱。 *使用者*已**sysname**，預設值是 NULL。  
  
 [ **@retry_attempts =**] *retry_attempts*  
 此步驟失敗時的重試次數。 *sp_update_jobstep*已**int**，預設值是 NULL。  
  
 [ **@retry_interval =**] *retry_interval*  
 重試的間隔時間 (以分鐘為單位)。 *retry_interval*已**int**，預設值是 NULL。  
  
 [ **@os_run_priority =**] *run_priority*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@output_file_name =**] **'***file_name***'**  
 儲存此步驟之輸出的檔案名稱。 *file_name*已**nvarchar(200**，預設值是 NULL。 這個參數只對在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 CmdExec 子系統中執行的命令有效。  
  
 若要將 output_file_name 設為 NULL，您必須設定*output_file_name*為空字串 (' ') 或字串空白的字元，但您無法使用**CHAR(32)** 函式。 例如，依照下列方式，將這個引數設為空字串：  
  
 **@output_file_name = ' '**  
  
 [ **@flags =**] *flags*  
 控制行為的選項。 *旗標*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|覆寫輸出檔。|  
|**2**|附加至輸出檔。|  
|**4**|將 Transact-SQL 作業步驟輸出寫入步驟記錄。|  
|**8**|將記錄寫入資料表 (覆寫現有的記錄)。|  
|**16**|將記錄寫入資料表 (附加至現有的記錄)。|  
  
 [ **@proxy_id**= ] *proxy_id*  
 用於執行作業步驟之 Proxy 的識別碼。 *proxy_id*是型別**int**，預設值是 NULL。 如果沒有*proxy_id*指定，則沒有*proxy_name*未指定，且不*user_name*指定，做為服務帳戶執行的作業步驟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。  
  
 [ **@proxy_name**= ] **'***proxy_name***'**  
 用於執行作業步驟的 Proxy 名稱。 *proxy_name*是型別**sysname**，預設值是 NULL。 如果沒有*proxy_id*指定，則沒有*proxy_name*未指定，且不*user_name*指定，做為服務帳戶執行的作業步驟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_update_jobstep**必須從執行**msdb**資料庫。  
  
 更新作業步驟會累加作業版本號碼。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有成員**sysadmin**可以更新另一位使用者所擁有的作業步驟。  
  
 如果作業步驟需要存取 Proxy，作業步驟的建立者必須有權存取作業步驟的 Proxy。 除了 Transact-SQL，所有子系統都需要 Proxy 帳戶。 成員**sysadmin**有權存取所有 proxy，而且可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]proxy 代理程式服務帳戶。  
  
## <a name="examples"></a>範例  
 下列範例會變更 `Weekly Sales Data Backup` 作業之第一個步驟的重試次數。 執行這個範例之後，重試次數是 `10`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1,  
    @retry_attempts = 10 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [檢視或修改作業](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_delete_jobstep &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
