---
description: sp_add_job (Transact-SQL)
title: sp_add_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_job_TSQL
- sp_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_job
ms.assetid: 6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 89f90d460287fadc9cdda97c020ccef7a47ceccd
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753855"
---
# <a name="sp_add_job-transact-sql"></a>sp_add_job (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  加入 SQL Agent 服務所執行的新作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
 > [!IMPORTANT]  
 > [Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。
 
## <a name="syntax"></a>語法  
  
```  
  
sp_add_job [ @job_name = ] 'job_name'  
     [ , [ @enabled = ] enabled ]   
     [ , [ @description = ] 'description' ]   
     [ , [ @start_step_id = ] step_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @category_id = ] category_id ]   
     [ , [ @owner_login_name = ] 'login' ]   
     [ , [ @notify_level_eventlog = ] eventlog_level ]   
     [ , [ @notify_level_email = ] email_level ]   
     [ , [ @notify_level_netsend = ] netsend_level ]   
     [ , [ @notify_level_page = ] page_level ]   
     [ , [ @notify_email_operator_name = ] 'email_name' ]   
          [ , [ @notify_netsend_operator_name = ] 'netsend_name' ]   
     [ , [ @notify_page_operator_name = ] 'page_name' ]   
     [ , [ @delete_level = ] delete_level ]   
     [ , [ @job_id = ] job_id OUTPUT ]   
```  
  
## <a name="arguments"></a>引數  
`[ @job_name = ] 'job_name'` 作業的名稱。 名稱必須是唯一的，且不能包含百分比 (**%**) 字元。 *job_name*是 **Nvarchar (128) **，沒有預設值。  
  
`[ @enabled = ] enabled` 指出加入之作業的狀態。 *enabled*是 **Tinyint**，預設值是 1 (已啟用) 。 如果為 **0**，則不會啟用作業，而且不會根據其排程執行。不過，您可以手動執行它。  
  
`[ @description = ] 'description'` 作業的描述。 *描述* 是 **Nvarchar (512) **，預設值是 Null。 如果省略 *description* ，則會使用「沒有可用的描述」。  
  
`[ @start_step_id = ] step_id` 要為作業執行之第一個步驟的識別碼。 *step_id*是 **int**，預設值是1。  
  
`[ @category_name = ] 'category'` 作業的類別目錄。 *category*是 **sysname**，預設值是 Null。  
  
`[ @category_id = ] category_id` 用來指定作業類別目錄的與語言無關的機制。 *category_id*是 **int**，預設值是 Null。  
  
`[ @owner_login_name = ] 'login'` 擁有作業的登入名稱。 *login*是 **sysname**，預設值是 Null，這會被視為目前的登入名稱。 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才可以設定或變更** \@ owner_login_name**的值。 如果使用者不是**系統管理員（sysadmin** ）角色的成員，或變更** \@ owner_login_name**的值，則此預存程式的執行將會失敗，並傳回錯誤。  
  
`[ @notify_level_eventlog = ] eventlog_level` 值，指出何時要將專案放在 Microsoft Windows 應用程式記錄檔中，以進行這項作業。 *eventlog_level*是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|永不|  
|**1**|成功時|  
|**2** (預設值)|失敗時|  
|**3**|一律|  
  
`[ @notify_level_email = ] email_level` 值，指出此作業完成時，何時傳送電子郵件。 *email_level*是 **int**，預設值是 **0**，表示永不如此。 *email_level*使用與 *eventlog_level*相同的值。  
  
`[ @notify_level_netsend = ] netsend_level` 值，指出此作業完成時，何時傳送網路訊息。 *netsend_level*是 **int**，預設值是 **0**，表示永不如此。 *netsend_level* 使用與 *eventlog_level*相同的值。  
  
`[ @notify_level_page = ] page_level` 值，指出此作業完成時傳送頁面的時機。 *page_level*是 **int**，預設值是 **0**，表示永不如此。 *page_level*使用與 *eventlog_level*相同的值。  
  
`[ @notify_email_operator_name = ] 'email_name'` 當達到 *email_level* 時，要傳送電子郵件的寄件者電子郵件名稱。 *email_name* 是 **sysname**，預設值是 Null。  
  
`[ @notify_netsend_operator_name = ] 'netsend_name'` 此作業完成時，網路訊息所要傳送到的操作員名稱。 *netsend_name*是 **sysname**，預設值是 Null。  
  
`[ @notify_page_operator_name = ] 'page_name'` 完成此作業時所要分頁的人員名稱。 *page_name*是 **sysname**，預設值是 Null。  
  
`[ @delete_level = ] delete_level` 指出何時要刪除作業的值。 *delete_value*是 **int**，預設值是0，表示永不如此。 *delete_level*使用與 *eventlog_level*相同的值。  
  
> [!NOTE]  
>  當 *delete_level* 為 **3**時，作業只會執行一次，而不論作業是否定義任何排程。 此外，如果作業刪除作業本身，也會同時刪除作業的所有記錄。  
  
`[ @job_id = ] _job_idOUTPUT` 如果成功建立，指派給作業的作業識別碼。 *job_id*是 **uniqueidentifier**類型的輸出變數，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 ** \@ originating_server**存在於**sp_add_job 中，** 但未列于 [引數] 之下。 ** \@ originating_server**保留供內部使用。  
  
 執行 **sp_add_job** 以加入作業之後， **sp_add_jobstep** 可用來加入執行作業活動的步驟。 **sp_add_jobschedule** 可以用來建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式服務用來執行作業的排程。 使用 **sp_add_jobserver** 來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作執行所在的實例，並 **sp_delete_jobserver** 從實例中移除作業 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 如果工作將在多伺服器環境中的一或多個目標伺服器上執行，請使用 **sp_apply_job_to_targets** 設定作業的目標伺服器或目標伺服器群組。 若要從目標伺服器或目標伺服器群組中移除作業，請使用 **sp_remove_job_from_targets**。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
## <a name="permissions"></a>權限  
 若要執行這個預存程式，使用者必須是**系統管理員（sysadmin** ）固定伺服器角色的成員，或是被授與 msdb 資料庫的下列其中一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定**msdb**資料庫角色：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需與每個固定資料庫角色相關聯之特定許可權的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才可以設定或變更** \@ owner_login_name**的值。 如果使用者不是**系統管理員（sysadmin** ）角色的成員，或變更** \@ owner_login_name**的值，則此預存程式的執行將會失敗，並傳回錯誤。  
  
## <a name="examples"></a>範例  
  
### <a name="a-adding-a-job"></a>A. 加入作業  
 這個範例會加入名稱為 `NightlyBackups` 的新作業。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-adding-a-job-with-pager-e-mail-and-net-send-information"></a>B. 利用呼叫器、電子郵件和 net send 資訊來加入作業  
 這個範例會建立一項名稱為 `Ad hoc Sales Data Backup` 的作業，以便在作業失敗時通知 `François Ajenstat` (利用呼叫器、電子郵件或網路快顯訊息)，以及在順利完成刪除作業。  
  
> [!NOTE]  
>  這個範例假設名稱為 `François Ajenstat` 的操作員及名稱為 `françoisa` 的登入已經存在。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_job  
    @job_name = N'Ad hoc Sales Data Backup',   
    @enabled = 1,  
    @description = N'Ad hoc backup of sales data',  
    @owner_login_name = N'françoisa',  
    @notify_level_eventlog = 2,  
    @notify_level_email = 2,  
    @notify_level_netsend = 2,  
    @notify_level_page = 2,  
    @notify_email_operator_name = N'François Ajenstat',  
    @notify_netsend_operator_name = N'François Ajenstat',   
    @notify_page_operator_name = N'François Ajenstat',  
    @delete_level = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_add_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_apply_job_to_targets &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
