---
title: sp_add_jobstep （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: c312f8798ba4ad42eed327123c9adc5feacba8a8
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412852"
---
# <a name="sp_add_jobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  將步驟（作業）新增至 SQL 代理程式作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [transact-sql 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > 在[Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)上，大部分（但不是全部） SQL Server Agent 作業類型都受到支援。 如需詳細資訊，請參閱[Azure SQL Database 受控執行個體與 SQL Server 的 t-sql 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。
  
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
`[ @job_id = ] job_id`要加入步驟之作業的識別碼。 *job_id*是**uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'`要加入步驟之作業的名稱。 *job_name*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定*job_id*或*job_name* ，但不能同時指定兩者。  
  
`[ @step_id = ] step_id`作業步驟的序列識別碼。 步驟識別碼從**1**開始，並遞增而不會有間距。 如果在現有序列中插入步驟，序號會自動調整。 如果未指定*step_id* ，就會提供值。 *step_id*是**int**，預設值是 Null。  
  
`[ @step_name = ] 'step_name'`步驟的名稱。 *step_name*是**sysname**，沒有預設值。  
  
`[ @subsystem = ] 'subsystem'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務用來執行*命令*的子系統。 *子系統*是**Nvarchar （40）**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|'**ACTIVESCRIPTING**'|Active Script<br /><br /> ** \* \*重要\*事項**[!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|'**CMDEXEC**'|作業系統命令或可執行的程式|  
|'**散發**'|複寫散發代理程式作業|  
|「**快照**集」|複寫快照集代理程式作業|  
|'**日誌**'|複寫記錄讀取器代理程式作業|  
|「**合併**」|複寫合併代理程式作業|  
|'**QueueReader**'|複寫佇列讀取器代理程式作業|  
|'**ANALYSISQUERY**'|Analysis Services 查詢 (MDX、DMX)。|  
|'**ANALYSISCOMMAND**'|Analysis Services 命令 (XMLA)。|  
|'**Dts**'|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]封裝執行|  
|'**PowerShell**'|PowerShell 指令碼|  
|'**TSQL**' （預設值）|[!INCLUDE[tsql](../../includes/tsql-md.md)]句|  
  
`[ @command = ] 'command'`由**SQLServerAgent**服務透過*子系統*執行的命令。 *command*是**Nvarchar （max）**，預設值是 Null。 SQL Server Agent 所提供的 Token 替代可在您撰寫軟體程式時，提供變數所提供的同等彈性。  
  
> [!IMPORTANT]  
>  逸出巨集現在必須伴隨著作業步驟中使用的所有 Token 一起執行，否則這些作業步驟將會失敗。 此外，您現在必須用括號括住 Token 名稱，並且在 Token 語法的開頭加上貨幣符號 (`$`)。 例如：  
>   
>  `$(ESCAPE_`*宏名稱*`(DATE))`  
  
 如需這些權杖的詳細資訊，以及如何將作業步驟更新為使用新的權杖語法，請參閱[在作業步驟中使用權杖](../../ssms/agent/use-tokens-in-job-steps.md)。  
  
> [!IMPORTANT]  
>  對 Windows 事件記錄檔具有寫入權限的任何 Windows 使用者，都可以存取由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示或 WMI 警示啟動的作業步驟。 為了避免此安全性風險，依預設會停用在警示啟動的作業中可以使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Token。 這些權杖包括： **DBN**、 **SVR**、 **a-ERR**、**嚴重性**、 **a-MSG**和**WMI （**_屬性_**）**。 請注意在此版本中，Token 的使用擴充到所有警示。  
>   
>  如果需要使用這些 Token，請先確定只有受信任的 Windows 安全性群組的成員 (例如 Administrators 群組) 才對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在電腦的事件記錄檔具有寫入權限。 然後以滑鼠右鍵按一下物件總管中的 [SQL Server Agent]****、選取 [屬性]****，然後在 [警示系統]**** 頁面上選取 [取代回應警示之所有作業的 Token]****，以啟用這些 Token。  
  
`[ @additional_parameters = ] 'parameters'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *參數*是**Ntext**，預設值是 Null。  
  
`[ @cmdexec_success_code = ] code`**CmdExec**子系統命令傳回的值，表示已成功執行*命令*。 *code*是**int**，預設值是**0**。  
  
`[ @on_success_action = ] success_action`步驟成功時要執行的動作。 *success_action*是**Tinyint**，而且可以是下列其中一個值。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**1** （預設值）|成功而結束|  
|**2**|失敗而結束|  
|**第**|移至下一步驟|  
|**4gb**|移至步驟*on_success_step_id*|  
  
`[ @on_success_step_id = ] success_step_id`當步驟成功且*success_action*為**4**時，此作業中要執行之步驟的識別碼。 *success_step_id*是**int**，預設值是**0**。  
  
`[ @on_fail_action = ] fail_action`步驟失敗時所要執行的動作。 *fail_action*是**Tinyint**，而且可以是下列其中一個值。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**sha-1**|成功而結束|  
|**2** （預設值）|失敗而結束|  
|**第**|移至下一步驟|  
|**4gb**|移至步驟*on_fail_step_id*|  
  
`[ @on_fail_step_id = ] fail_step_id`如果步驟失敗且*fail_action*為**4**時，此作業中要執行之步驟的識別碼。 *fail_step_id*是**int**，預設值是**0**。  
  
`[ @server = ] 'server'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] *伺服器*是**Nvarchar （30）**，預設值是 Null。  
  
`[ @database_name = ] 'database'`要在其中執行[!INCLUDE[tsql](../../includes/tsql-md.md)]步驟的資料庫名稱。 *資料庫*是**sysname**，預設值是 Null，在此情況下會使用**master**資料庫。 不允許以括號 ([ ]) 括住的名稱。 若為 ActiveX 作業步驟，*資料庫*就是步驟所使用的指令碼語言名稱。  
  
`[ @database_user_name = ] 'user'`執行[!INCLUDE[tsql](../../includes/tsql-md.md)]步驟時要使用的使用者帳戶名稱。 *user*是**sysname**，預設值是 Null。 當*user*為 Null 時，此步驟會在工作擁有者在*資料庫*上的使用者內容中執行。  只有在作業擁有者為 SQL Server 系統管理員 (sysadmin) 時，SQL Server Agent 才會包含此參數。 在此情況下，指定的 Transact-SQL 步驟會在指定的 SQL Server 使用者名稱內容中執行。 如果作業擁有者不是 SQL Server 系統管理員（sysadmin），則 Transact-sql 步驟一律會在擁有此作業的登入內容中執行，且會忽略@database_user_name參數。  
  
`[ @retry_attempts = ] retry_attempts`此步驟失敗時所要使用的重試次數。 *retry_attempts*是**int**，預設值是**0**，表示不會嘗試重試。  
  
`[ @retry_interval = ] retry_interval`重試嘗試之間的時間量（以分鐘為單位）。 *retry_interval*是**int**，預設值是**0**，表示**0**分鐘的間隔。  
  
`[ @os_run_priority = ] run_priority`留.  
  
`[ @output_file_name = ] 'file_name'`儲存此步驟之輸出的檔案名。 *file_name*是**Nvarchar （200）**，預設值是 Null。 *file_name*可以包含 [*命令*] 底下所列的一或多個權杖。 此參數只[!INCLUDE[tsql](../../includes/tsql-md.md)]適用于在、 **CmdExec**、 **PowerShell**、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]或[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]子系統上執行的命令。  
  
`[ @flags = ] flags`是控制行為的選項。 *旗標*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0** （預設值）|覆寫輸出檔|  
|**2**|附加至輸出檔。|  
|**4gb**|將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟輸出寫入步驟記錄。|  
|**8**|將記錄寫入資料表 (覆寫現有的記錄)。|  
|**1600**|將記錄寫入資料表 (附加至現有的記錄)。|  
|**32**|將所有輸出寫入作業記錄|  
|**64**|建立 Windows 事件以做為 CMD 工作步驟要中止的訊號|  
  
`[ @proxy_id = ] proxy_id`執行作業步驟之 proxy 的 id 編號。 *proxy_id*的類型為**int**，預設值為 Null。 如果未指定任何*proxy_id* 、未指定任何*proxy_name* ，而且未指定任何*user_name* ，則作業步驟會以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的服務帳戶執行。  
  
`[ @proxy_name = ] 'proxy_name'`執行作業步驟的 proxy 名稱。 *proxy_name*的類型為**sysname**，預設值為 Null。 如果未指定任何*proxy_id* 、未指定任何*proxy_name* ，而且未指定任何*user_name* ，則作業步驟會以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的服務帳戶執行。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 **sp_add_jobstep**必須從**msdb**資料庫中執行。  
  
 SQL Server Management Studio 提供易用的作業管理圖形介面，是建立及管理作業基礎結構的建議方式。  
  
 根據預設，除非指定另一個 proxy，否則作業步驟會[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當做 Agent 的服務帳戶執行。 此帳戶的需求是**系統管理員（sysadmin** ）固定安全性角色的成員。
  
 Proxy 可透過*proxy_name*或*proxy_id*來識別。  
  
## <a name="permissions"></a>權限  
 根據預設，**系統管理員（sysadmin** ）固定伺服器角色的成員可以執行此預存程式。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 作業步驟的建立者必須有權存取作業步驟的 Proxy。 **系統管理員（sysadmin** ）固定伺服器角色的成員具有所有 proxy 的存取權。 其他使用者需要明確授與 Proxy 的存取權。  
  
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
 [查看或修改作業](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_delete_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
