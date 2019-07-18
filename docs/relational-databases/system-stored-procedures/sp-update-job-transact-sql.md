---
title: sp_update_job (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_job
- sp_update_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_job
ms.assetid: cbdfea38-9e42-47f3-8fc8-5978b82e2623
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5428ae9130646db662c6c960f777c6a7dfe25000
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084889"
---
# <a name="spupdatejob-transact-sql"></a>sp_update_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更作業的屬性。  
  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_update_job [ @job_id =] job_id | [@job_name =] 'job_name'  
     [, [@new_name =] 'new_name' ]   
     [, [@enabled =] enabled ]  
     [, [@description =] 'description' ]   
     [, [@start_step_id =] step_id ]  
     [, [@category_name =] 'category' ]   
     [, [@owner_login_name =] 'login' ]  
     [, [@notify_level_eventlog =] eventlog_level ]  
     [, [@notify_level_email =] email_level ]  
     [, [@notify_level_netsend =] netsend_level ]  
     [, [@notify_level_page =] page_level ]  
     [, [@notify_email_operator_name =] 'operator_name' ]  
     [, [@notify_netsend_operator_name =] 'netsend_operator' ]  
     [, [@notify_page_operator_name =] 'page_operator' ]  
     [, [@delete_level =] delete_level ]   
     [, [@automatic_post =] automatic_post ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id` 要更新的作業識別碼。 *job_id*已**uniqueidentifier**。  
  
`[ @job_name = ] 'job_name'` 作業名稱。 *job_name*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** 。  
  
> **注意：** 任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
`[ @new_name = ] 'new_name'` 作業的新名稱。 *new_name*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** 。  
  
`[ @enabled = ] enabled` 指定是否啟用作業 (**1**)，或未啟用 (**0**)。 *已啟用*已**tinyint**。  
  
`[ @description = ] 'description'` 作業描述。 *描述*已**nvarchar(512)** 。  
  
`[ @start_step_id = ] step_id` 執行作業的第一個步驟的識別碼。 *step_id*已**int**。  
  
`[ @category_name = ] 'category'` 作業類別目錄。 *類別目錄*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** 。  
  
`[ @owner_login_name = ] 'login'` 擁有作業的登入名稱。 *登入*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** 只有成員**sysadmin**固定的伺服器角色可以變更作業擁有權。  
  
`[ @notify_level_eventlog = ] eventlog_level` 指定當項目放在這個工作的 Microsoft Windows 應用程式記錄檔中。 *eventlog_level*已**int**，而且可以是下列值之一。  
  
|值|描述 (動作)|  
|-----------|----------------------------|  
|**0**|永不|  
|**1**|成功時|  
|**2**|失敗時|  
|**3**|永遠|  
  
`[ @notify_level_email = ] email_level` 指定何時傳送電子郵件的這項作業完成時。 *email_level*已**int**。*email_level*使用相同的值為*eventlog_level*。  
  
`[ @notify_level_netsend = ] netsend_level` 指定何時傳送網路訊息的這項作業完成時。 *netsend_level*已**int**。*netsend_level*使用相同的值為*eventlog_level*。  
  
`[ @notify_level_page = ] page_level` 指定在傳送這項作業完成時的頁面。 *page_level*已**int**。*page_level*使用相同的值為*eventlog_level*。  
  
`[ @notify_email_operator_name = ] 'operator_name'` 電子郵件時要送往的操作員名稱*email_level*為止。 *email_name*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** 。  
  
`[ @notify_netsend_operator_name = ] 'netsend_operator'` 網路訊息所要送往之操作員名稱。 *netsend_operator*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** 。  
  
`[ @notify_page_operator_name = ] 'page_operator'` 頁面所要送往之操作員名稱。 *page_operator*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** 。  
  
`[ @delete_level = ] delete_level` 指定何時刪除作業。 *delete_value*已**int**。*delete_level*使用相同的值為*eventlog_level*。  
  
`[ @automatic_post = ] automatic_post` 保留。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_update_job**必須從執行**msdb**資料庫。  
  
 **sp_update_job**只變更這些設定的參數提供值。 如果省略某個參數，就會保留目前的設定。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有成員**sysadmin**可以使用這個預存程序，來編輯的其他使用者所擁有的作業屬性。  
  
## <a name="examples"></a>範例  
 下列範例會變更 `NightlyBackups` 作業的名稱、描述和啟用狀態。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_job  
    @job_name = N'NightlyBackups',  
    @new_name = N'NightlyBackups -- Disabled',  
    @description = N'Nightly backups disabled during server migration.',  
    @enabled = 0 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
