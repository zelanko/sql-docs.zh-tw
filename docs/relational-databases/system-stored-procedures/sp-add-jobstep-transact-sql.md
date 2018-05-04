---
title: sp_add_jobstep (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
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
- sp_add_jobstep_TSQL
- sp_add_jobstep
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
caps.latest.revision: 80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eea1729d2f33cffb37ffdd803739f9b65d77fc83
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spaddjobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@job_id =** ] *job_id*  
 這是加入步驟之作業的識別碼。 *job_id*是**uniqueidentifier**，預設值是 NULL。  
  
 [ **@job_name =** ] **'***job_name***'**  
 這是加入步驟的作業名稱。 *job_name*是**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  任一*job_id*或*job_name*必須指定，但不可同時指定兩者。  
  
 [ **@step_id =** ] *step_id*  
 作業步驟的順序識別碼。 步驟識別碼數字開始**1**和沒有間距的遞增值。 如果在現有序列中插入步驟，序號會自動調整。 如果提供值，則*step_id*未指定。 *step_id*是**int**，預設值是 NULL。  
  
 [ **@step_name =** ] **'***step_name***'**  
 步驟的名稱。 *step_name*是**sysname**，沒有預設值。  
  
 [ **@subsystem =** ] **'***subsystem***'**  
 所用的子系統[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式服務來執行*命令*。 *子系統*是**nvarchar （40)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|'**ACTIVESCRIPTING**'|Active Script<br /><br /> **\*\* 重要 \*\*** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|'**CMDEXEC**'|作業系統命令或可執行的程式|  
|'**發佈**'|複寫散發代理程式作業|  
|'**快照**'|複寫快照集代理程式作業|  
|'**LOGREADER**'|複寫記錄讀取器代理程式作業|  
|'**合併**'|複寫合併代理程式作業|  
|'**QueueReader**'|複寫佇列讀取器代理程式作業|  
|'**ANALYSISQUERY**'|Analysis Services 查詢 (MDX、DMX)。|  
|'**ANALYSISCOMMAND**'|Analysis Services 命令 (XMLA)。|  
|'**Dts**'|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝執行|  
|'**PowerShell**'|PowerShell 指令碼|  
|'**TSQL**' （預設值）|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式|  
  
 [  **@command=** ] **'***命令***'**  
 要執行之命令**SQLServerAgent**服務透過*子系統*。 *命令*是**nvarchar （max)**，預設值是 NULL。 SQL Server Agent 所提供的 Token 替代可在您撰寫軟體程式時，提供變數所提供的同等彈性。  
  
> [!IMPORTANT]  
>  逸出巨集現在必須伴隨著作業步驟中使用的所有 Token 一起執行，否則這些作業步驟將會失敗。 此外，您現在必須用括號括住 Token 名稱，並且在 Token 語法的開頭加上貨幣符號 (`$`)。 例如：  
>   
>  `$(ESCAPE_`*巨集名稱*`(DATE))`  
  
 如需有關這些語彙基元和更新作業步驟以使用新的 token 語法的詳細資訊，請參閱[作業步驟中使用的語彙基元](http://msdn.microsoft.com/library/105bbb66-0ade-4b46-b8e4-f849e5fc4d43)。  
  
> [!IMPORTANT]  
>  對 Windows 事件記錄檔具有寫入權限的任何 Windows 使用者，都可以存取由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示或 WMI 警示啟動的作業步驟。 為了避免此安全性風險，依預設會停用在警示啟動的作業中可以使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Token。 這些 Token 包括：**A-DBN**、**A-SVR**、**A-ERR**、**A-SEV**、**A-MSG** 及 **WMI(<屬性>)**。 請注意在此版本中，Token 的使用擴充到所有警示。  
>   
>  如果需要使用這些 Token，請先確定只有受信任的 Windows 安全性群組的成員 (例如 Administrators 群組) 才對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在電腦的事件記錄檔具有寫入權限。 然後以滑鼠右鍵按一下物件總管中的 [SQL Server Agent]、選取 [屬性]，然後在 [警示系統] 頁面上選取 [取代回應警示之所有作業的 Token]，以啟用這些 Token。  
  
 [  **@additional_parameters=** ] **'***參數***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *參數*是**ntext**，預設值是 NULL。  
  
 [ **@cmdexec_success_code =** ] *code*  
 所傳回的值**CmdExec**子系統命令，以表示*命令*執行成功。 *程式碼*是**int**，預設值是**0**。  
  
 [ **@on_success_action=** ] *success_action*  
 步驟成功時所要執行的動作。 *success_action*是**tinyint**，而且可以是下列值之一。  
  
|Value|描述 (動作)|  
|-----------|----------------------------|  
|**1** (預設值)|成功而結束|  
|**2**|失敗而結束|  
|**3**|移至下一步驟|  
|**4**|請移至步驟*on_success_step_id*|  
  
 [ **@on_success_step_id =** ] *success_step_id*  
 如果步驟成功執行此作業中的步驟的識別碼和*success_action*是**4**。 *success_step_id*是**int**，預設值是**0**。  
  
 [ **@on_fail_action=** ] *fail_action*  
 步驟失敗時所要執行的動作。 *fail_action*是**tinyint**，而且可以是下列值之一。  
  
|Value|描述 (動作)|  
|-----------|----------------------------|  
|**1**|成功而結束|  
|**2** (預設值)|失敗而結束|  
|**3**|移至下一步驟|  
|**4**|請移至步驟*on_fail_step_id*|  
  
 [ **@on_fail_step_id=** ] *fail_step_id*  
 要執行步驟失敗時的這項工作中的步驟識別碼和*fail_action*是**4**。 *fail_step_id*是**int**，預設值是**0**。  
  
 [ **@server =**] **'***server***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *伺服器*是**nvarchar （30)**，預設值是 NULL。  
  
 [  **@database_name=** ] **'***資料庫***'**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 步驟執行所在的資料庫名稱。 *資料庫*是**sysname**，預設值是 NULL，在此情況下**主要**會使用資料庫。 不允許以括號 ([ ]) 括住的名稱。 ActiveX 作業步驟，如*資料庫*步驟會使用的指令碼語言的名稱。  
  
 [ **@database_user_name=** ] **'***user***'**  
 執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 步驟時所用的使用者帳戶名稱。 *使用者*是**sysname**，預設值是 NULL。 當*使用者*上是 NULL，在作業擁有者的使用者內容中執行此步驟*資料庫*。  只有在作業擁有者為 SQL Server 系統管理員 (sysadmin) 時，SQL Server Agent 才會包含此參數。 在此情況下，指定的 Transact-SQL 步驟會在指定的 SQL Server 使用者名稱內容中執行。 如果作業擁有者不是 SQL Server 系統管理員，則一定會擁有這項作業的登入的內容中執行的 TRANSACT-SQL 步驟和@database_user_name參數將會被忽略。  
  
 [  **@retry_attempts=** ] *retry_attempts*  
 此步驟失敗時的重試次數。 *retry_attempts*是**int**，預設值是**0**，表示無重試嘗試。  
  
 [  **@retry_interval=** ] *retry_interval*  
 重試的間隔時間 (以分鐘為單位)。 *retry_interval*是**int**，預設值是**0**，表示**0**-分鐘的間隔。  
  
 [ **@os_run_priority =** ] *run_priority*  
 已保留。  
  
 [ **@output_file_name=** ] **'***file_name***'**  
 儲存此步驟之輸出的檔案名稱。 *file_name*是**nvarchar(200)**，預設值是 NULL。 *file_name*可以包含一個或多個列在 token*命令*。 只執行的命令，此參數才有效[!INCLUDE[tsql](../../includes/tsql-md.md)]， **CmdExec**， **PowerShell**， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，或[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]子系統。  
  
 [  **@flags=** ]*旗標*  
 這是控制行為的選項。 *旗標*是**int**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**0** (預設)|覆寫輸出檔|  
|**2**|附加至輸出檔。|  
|**4**|將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟輸出寫入步驟記錄。|  
|**8**|將記錄寫入資料表 (覆寫現有的記錄)。|  
|**16**|將記錄寫入資料表 (附加至現有的記錄)。|  
|**32**|將所有輸出寫入作業記錄|  
|**64**|建立 Windows 事件以做為 CMD 工作步驟要中止的訊號|  
  
 [ **@proxy_id** = ] *proxy_id*  
 用於執行作業步驟之 Proxy 的識別碼。 *proxy_id*是型別**int**，預設值是 NULL。 如果沒有*proxy_id*指定，則沒有*proxy_name*指定時，並沒有*user_name*指定，則作業步驟執行的服務帳戶為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。  
  
 [ **@proxy_name** = ] **'***proxy_name***'**  
 用於執行作業步驟的 Proxy 名稱。 *proxy_name*是型別**sysname**，預設值是 NULL。 如果沒有*proxy_id*指定，則沒有*proxy_name*指定時，並沒有*user_name*指定，則作業步驟執行的服務帳戶為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 **sp_add_jobstep**必須從執行**msdb**資料庫。  
  
 SQL Server Management Studio 提供易用的作業管理圖形介面，是建立及管理作業基礎結構的建議方式。  
  
 除非作業步驟的建立者所屬的作業步驟必須指定 proxy **sysadmin**固定的安全性角色。  
  
 Proxy 可能會由*proxy_name*或*proxy_id*。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 作業步驟的建立者必須有權存取作業步驟的 Proxy。 成員**sysadmin**固定的伺服器角色有權存取所有 proxy。 其他使用者需要明確授與 Proxy 的存取權。  
  
## <a name="examples"></a>範例  
 下列範例會建立一個作業步驟，以便將 Sales 資料庫的資料庫存取變更成唯讀。 另外，這個範例還指定重試 5 次，每隔 5 分鐘重試一次。  
  
> [!NOTE]  
>  這個範例假設 `Weekly Sales Data Backup` 作業已在執行中。  
  
```  
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
 [檢視或修改作業](http://msdn.microsoft.com/library/57f649b8-190c-4304-abd7-7ca5297deab7)   
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_add_schedule &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
