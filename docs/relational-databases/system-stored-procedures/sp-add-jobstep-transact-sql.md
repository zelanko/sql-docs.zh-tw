---
title: sp_add_jobstep (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobstep_TSQL
- sp_add_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 112afe8f7a8eaea87c860264c820c874788cbc7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66500362"
---
# <a name="spaddjobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

  將步驟 (操作) 加入作業中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```
sp_add_jobstep [ @job_id = ] job_id | [ @job_name = ] 'job_name'   
     [ , [ @step_id = ] step_id ]   
     { , [ @step_name = ] 'step_name' }   
     [ , [ @subsystem = ] 'subsystem' ]   
     [ , [ @command = ] 'command' ]   
     [ , [ @additional_parameters = ] 'parameters' ]   
          [ , [ @cmdexec_success_code = ] code ]   
     [ , [ @on_success_action = ] success_action ]   
          [ , [ @on_success_step_id = ] success_step_id ]   
          [ , [ @on_fail_action = ] fail_action ]   
          [ , [ @on_fail_step_id = ] fail_step_id ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @database_user_name = ] 'user' ]   
     [ , [ @retry_attempts = ] retry_attempts ]   
     [ , [ @retry_interval = ] retry_interval ]   
     [ , [ @os_run_priority = ] run_priority ]   
     [ , [ @output_file_name = ] 'file_name' ]   
     [ , [ @flags = ] flags ]   
     [ , { [ @proxy_id = ] proxy_id   
         | [ @proxy_name = ] 'proxy_name' } ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id` 要加入步驟之作業的識別碼。 *job_id*已**uniqueidentifier**，預設值是 NULL。  
  
`[ @job_name = ] 'job_name'` 要加入步驟之作業名稱。 *job_name*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
`[ @step_id = ] step_id` 作業步驟順序識別碼。 步驟識別碼數字開始**1**和沒有間距的遞增值。 如果在現有序列中插入步驟，序號會自動調整。 如果提供值，則*step_id*未指定。 *step_id*已**int**，預設值是 NULL。  
  
`[ @step_name = ] 'step_name'` 步驟的名稱。 *step_name*已**sysname**，沒有預設值。  
  
`[ @subsystem = ] 'subsystem'` 所使用的子系統[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式服務來執行*命令*。 *子系統*已**nvarchar(40)** ，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|'**ACTIVESCRIPTING**'|Active Script<br /><br /> **\*\* 重要事項 \*\*** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|'**CMDEXEC**'|作業系統命令或可執行的程式|  
|'**發佈**'|複寫散發代理程式作業|  
|'**快照集**'|複寫快照集代理程式作業|  
|'**LOGREADER**'|複寫記錄讀取器代理程式作業|  
|'**合併**'|複寫合併代理程式作業|  
|'**QueueReader**'|複寫佇列讀取器代理程式作業|  
|'**ANALYSISQUERY**'|Analysis Services 查詢 (MDX、DMX)。|  
|'**ANALYSISCOMMAND**'|Analysis Services 命令 (XMLA)。|  
|'**Dts**'|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝執行|  
|'**PowerShell**'|PowerShell 指令碼|  
|'**TSQL**' （預設值）|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式|  
  
`[ @command = ] 'command'` 要執行的命令**SQLServerAgent**服務透過*子系統*。 *命令*已**nvarchar （max)** ，預設值是 NULL。 SQL Server Agent 所提供的 Token 替代可在您撰寫軟體程式時，提供變數所提供的同等彈性。  
  
> [!IMPORTANT]  
>  逸出巨集現在必須伴隨著作業步驟中使用的所有 Token 一起執行，否則這些作業步驟將會失敗。 此外，您現在必須用括號括住 Token 名稱，並且在 Token 語法的開頭加上貨幣符號 (`$`)。 例如：  
>   
>  `$(ESCAPE_` *巨集名稱* `(DATE))`  
  
 如需有關這些 token 以及如何更新您的作業步驟，以利用新 token 語法的詳細資訊，請參閱 <<c0> [ 作業步驟中使用的語彙基元](../../ssms/agent/use-tokens-in-job-steps.md)。  
  
> [!IMPORTANT]  
>  對 Windows 事件記錄檔具有寫入權限的任何 Windows 使用者，都可以存取由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示或 WMI 警示啟動的作業步驟。 為了避免此安全性風險，依預設會停用在警示啟動的作業中可以使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Token。 這些 Token 包括：**A-DBN**、**A-SVR**、**A-ERR**、**A-SEV**、**A-MSG** 及 **WMI(** <屬性>  **)** 。 請注意在此版本中，Token 的使用擴充到所有警示。  
>   
>  如果需要使用這些 Token，請先確定只有受信任的 Windows 安全性群組的成員 (例如 Administrators 群組) 才對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在電腦的事件記錄檔具有寫入權限。 然後以滑鼠右鍵按一下物件總管中的 [SQL Server Agent]  、選取 [屬性]  ，然後在 [警示系統]  頁面上選取 [取代回應警示之所有作業的 Token]  ，以啟用這些 Token。  
  
`[ @additional_parameters = ] 'parameters'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *參數*已**ntext**，預設值是 NULL。  
  
`[ @cmdexec_success_code = ] code` 所傳回的值**CmdExec**子系統命令，以指出*命令*順利執行。 *程式碼*已**int**，預設值是**0**。  
  
`[ @on_success_action = ] success_action` 要執行步驟成功時的動作。 *success_action*已**tinyint**，而且可以是下列值之一。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**1** (預設值)|成功而結束|  
|**2**|失敗而結束|  
|**3**|移至下一步驟|  
|**4**|請移至步驟*on_success_step_id*|  
  
`[ @on_success_step_id = ] success_step_id` 此作業中步驟的識別碼，來執行步驟成功時， *success_action*是**4**。 *success_step_id*已**int**，預設值是**0**。  
  
`[ @on_fail_action = ] fail_action` 要在步驟失敗時所執行的動作。 *fail_action*已**tinyint**，而且可以是下列值之一。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**1**|成功而結束|  
|**2** (預設值)|失敗而結束|  
|**3**|移至下一步驟|  
|**4**|請移至步驟*on_fail_step_id*|  
  
`[ @on_fail_step_id = ] fail_step_id` 此作業中步驟的識別碼，來執行作業失敗時， *fail_action*是**4**。 *fail_step_id*已**int**，預設值是**0**。  
  
`[ @server = ] 'server'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *伺服器*已**nvarchar(30)** ，預設值是 NULL。  
  
`[ @database_name = ] 'database'` 在其中執行的資料庫名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]步驟。 *資料庫*已**sysname**，預設值是 NULL，在此情況下**主要**會使用資料庫。 不允許以括號 ([ ]) 括住的名稱。 ActiveX 作業步驟，如*資料庫*步驟會使用指令碼語言的名稱。  
  
`[ @database_user_name = ] 'user'` 若要在執行時使用的使用者帳戶名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]步驟。 *使用者*已**sysname**，預設值是 NULL。 當*使用者*是 NULL，在作業擁有者的使用者內容中的步驟執行上*資料庫*。  只有在作業擁有者為 SQL Server 系統管理員 (sysadmin) 時，SQL Server Agent 才會包含此參數。 在此情況下，指定的 Transact-SQL 步驟會在指定的 SQL Server 使用者名稱內容中執行。 如果作業擁有者不是 SQL Server 系統管理員，則一定會擁有此作業的登入的內容中執行的 TRANSACT-SQL 步驟和@database_user_name參數將會被忽略。  
  
`[ @retry_attempts = ] retry_attempts` 若要使用此步驟失敗時，嘗試重試次數。 *sp_update_jobstep*已**int**，預設值是**0**，表示無重試嘗試。  
  
`[ @retry_interval = ] retry_interval` 在重試嘗試之間的分鐘的時間量。 *retry_interval*已**int**，預設值是**0**，這表示**0**-分鐘的間隔。  
  
`[ @os_run_priority = ] run_priority` 保留。  
  
`[ @output_file_name = ] 'file_name'` 在其中儲存此步驟之輸出的檔案名稱。 *file_name*已**nvarchar(200**，預設值是 NULL。 *file_name*可包含一個或多個列在 token*命令*。 此參數才有效，只執行的命令[!INCLUDE[tsql](../../includes/tsql-md.md)]， **CmdExec**， **PowerShell**， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，或[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]子系統。  
  
`[ @flags = ] flags` 是一個控制行為的選項。 *旗標*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|覆寫輸出檔|  
|**2**|附加至輸出檔。|  
|**4**|將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟輸出寫入步驟記錄。|  
|**8**|將記錄寫入資料表 (覆寫現有的記錄)。|  
|**16**|將記錄寫入資料表 (附加至現有的記錄)。|  
|**32**|將所有輸出寫入作業記錄|  
|**64**|建立 Windows 事件以做為 CMD 工作步驟要中止的訊號|  
  
`[ @proxy_id = ] proxy_id` 執行作業步驟之 proxy 識別碼。 *proxy_id*是型別**int**，預設值是 NULL。 如果沒有*proxy_id*指定，則沒有*proxy_name*未指定，且不*user_name*指定，做為服務帳戶執行的作業步驟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。  
  
`[ @proxy_name = ] 'proxy_name'` 執行作業步驟的 proxy 名稱。 *proxy_name*是型別**sysname**，預設值是 NULL。 如果沒有*proxy_id*指定，則沒有*proxy_name*未指定，且不*user_name*指定，做為服務帳戶執行的作業步驟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_jobstep**必須從執行**msdb**資料庫。  
  
 SQL Server Management Studio 提供易用的作業管理圖形介面，是建立及管理作業基礎結構的建議方式。  
  
 作業步驟必須指定 proxy，除非作業步驟的建立者的成員，否則**sysadmin**固定的安全性角色。  
  
 Proxy 可能會識別所*proxy_name*或是*proxy_id*。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 作業步驟的建立者必須有權存取作業步驟的 Proxy。 成員**sysadmin**固定的伺服器角色有權存取所有 proxy。 其他使用者需要明確授與 Proxy 的存取權。  
  
## <a name="examples"></a>範例  
 下列範例會建立一個作業步驟，以便將 Sales 資料庫的資料庫存取變更成唯讀。 另外，這個範例還指定重試 5 次，每隔 5 分鐘重試一次。  
  
> [!NOTE]  
>  這個範例假設 `Weekly Sales Data Backup` 作業已在執行中。  
  
```sql
USE msdb;  
GO  
EXEC sp_add_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_name = N'Set database to read only',  
    @subsystem = N'TSQL',  
    @command = N'ALTER DATABASE SALES SET READ_ONLY',
    @retry_attempts = 5,  
    @retry_interval = 5 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [檢視或修改作業](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
