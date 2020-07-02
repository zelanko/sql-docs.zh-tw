---
title: sp_update_jobstep （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_jobstep
- sp_update_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_jobstep
ms.assetid: e158802c-c347-4a5d-bf75-c03e5ae56e6b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 02697937d5a0402edbaf959ed52731010eab1ce6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723067"
---
# <a name="sp_update_jobstep-transact-sql"></a>sp_update_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

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
`[ @job_id = ] job_id`步驟所屬之作業的識別碼。 *job_id*是**uniqueidentifier**，預設值是 Null。 必須指定*job_id*或*job_name* ，但不能同時指定兩者。  
  
`[ @job_name = ] 'job_name'`步驟所屬的作業名稱。 *job_name*是**sysname**，預設值是 Null。 必須指定*job_id*或*job_name* ，但不能同時指定兩者。  
  
`[ @step_id = ] step_id`要修改之作業步驟的識別碼。 無法變更這個識別碼。 *step_id*是**int**，沒有預設值。  
  
`[ @step_name = ] 'step_name'`這是步驟的新名稱。 *step_name*是**sysname**，預設值是 Null。  
  
`[ @subsystem = ] 'subsystem'`Microsoft SQL Server Agent 用來執行*命令*的子系統。 *子系統*是**Nvarchar （40）**，預設值是 Null。  
  
`[ @command = ] 'command'`要透過*子系統*執行的命令。 *command*是**Nvarchar （max）**，預設值是 Null。  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @cmdexec_success_code = ] success_code`**CmdExec**子系統命令傳回的值，表示已成功執行*命令*。 *success_code*是**int**，預設值是 Null。  
  
`[ @on_success_action = ] success_action`步驟成功時要執行的動作。*success_action*是**Tinyint**，預設值是 Null，它可以是下列值之一。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**1**|成功而結束。|  
|**2**|失敗而結束。|  
|**3**|移至下一步驟。|  
|**4**|移至步驟*success_step_id。*|  
  
`[ @on_success_step_id = ] success_step_id`如果步驟成功且*success_action*為**4**時，此作業中要執行之步驟的識別碼。 *success_step_id*是**int**，預設值是 Null。  
  
`[ @on_fail_action = ] fail_action`步驟失敗時所要執行的動作。 *fail_action*是**Tinyint**，預設值是 Null，而且可以有下列其中一個值。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**1**|成功而結束。|  
|**2**|失敗而結束。|  
|**3**|移至下一步驟。|  
|**4**|移至步驟*fail_step_id * *。*|  
  
`[ @on_fail_step_id = ] fail_step_id`如果步驟失敗且*fail_action*為**4**時，此作業中要執行之步驟的識別碼。 *fail_step_id*是**int**，預設值是 Null。  
  
`[ @server = ] 'server'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*伺服器*是**Nvarchar （128）**，預設值是 Null。  
  
`[ @database_name = ] 'database'`要在其中執行步驟的資料庫名稱 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *資料庫*為**sysname**。 不允許以括號 ([ ]) 括住的名稱。 預設值是 NULL。  
  
`[ @database_user_name = ] 'user'`執行步驟時要使用的使用者帳戶名稱 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *user*是**sysname**，預設值是 Null。  
  
`[ @retry_attempts = ] retry_attempts`此步驟失敗時所要使用的重試次數。 *retry_attempts*是**int**，預設值是 Null。  
  
`[ @retry_interval = ] retry_interval`重試嘗試之間的時間量（以分鐘為單位）。 *retry_interval*是**int**，預設值是 Null。  
  
`[ @os_run_priority = ] run_priority` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @output_file_name = ] 'file_name'`儲存此步驟之輸出的檔案名。 *file_name*是**Nvarchar （200）**，預設值是 Null。 這個參數只對在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 CmdExec 子系統中執行的命令有效。  
  
 若要將 output_file_name 設回 Null，您必須將*output_file_name*設定為空字串（' '）或空白字元字串，但不能使用**CHAR （32）** 函數。 例如，依照下列方式，將這個引數設為空字串：  
  
 **@output_file_name= ' '**  
  
`[ @flags = ] flags`控制行為的選項。 *旗標*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|覆寫輸出檔。|  
|**2**|附加至輸出檔。|  
|**4**|將 Transact-SQL 作業步驟輸出寫入步驟記錄。|  
|**8**|將記錄寫入資料表 (覆寫現有的記錄)。|  
|**16**|將記錄寫入資料表 (附加至現有的記錄)。|  
  
`[ @proxy_id = ] proxy_id`執行作業步驟之 proxy 的 ID 編號。 *proxy_id*的類型為**int**，預設值為 Null。 如果未指定任何*proxy_id* 、未指定任何*proxy_name* ，而且未指定任何*user_name* ，則作業步驟會以 Agent 的服務帳戶執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @proxy_name = ] 'proxy_name'`執行作業步驟的 proxy 名稱。 *proxy_name*的類型為**sysname**，預設值為 Null。 如果未指定任何*proxy_id* 、未指定任何*proxy_name* ，而且未指定任何*user_name* ，則作業步驟會以 Agent 的服務帳戶執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_update_jobstep**必須從**msdb**資料庫中執行。  
  
 更新作業步驟會累加作業版本號碼。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有**系統管理員（sysadmin** ）的成員可以更新另一位使用者所擁有的作業步驟。  
  
 如果作業步驟需要存取 Proxy，作業步驟的建立者必須有權存取作業步驟的 Proxy。 除了 Transact-SQL，所有子系統都需要 Proxy 帳戶。 **系統管理員（sysadmin** ）的成員具有所有 proxy 的存取權，而且可以使用代理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式服務帳戶來取得 proxy。  
  
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
 [查看或修改作業](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_delete_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
