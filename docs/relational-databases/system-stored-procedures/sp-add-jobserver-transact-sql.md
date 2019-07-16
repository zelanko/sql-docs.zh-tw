---
title: sp_add_jobserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobserver
- sp_add_jobserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobserver
ms.assetid: 485252cc-0081-490a-9bd1-cbbd68eea286
author: stevestein
ms.author: sstein
ms.openlocfilehash: fecd704d5f6b6f0384ecb17787bd8423852356ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078192"
---
# <a name="spaddjobserver-transact-sql"></a>sp_add_jobserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將指定作業的目標鎖定在指定的伺服器上。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_jobserver [ @job_id = ] job_id | [ @job_name = ] 'job_name'  
     [ , [ @server_name = ] 'server' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id` 作業識別碼。 *job_id*已**uniqueidentifier**，預設值是 NULL。  
  
`[ @job_name = ] 'job_name'` 作業名稱。 *job_name*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
`[ @server_name = ] 'server'` 要以工作為目標伺服器的名稱。 *伺服器*已**nvarchar(30)** ，預設值是 （local） '。 *伺服器*可以是 **(LOCAL)** 本機伺服器，或現有目標伺服器的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **@automatic_post** 存在於**sp_add_jobserver**，但並未列在引數。 **@automatic_post** 是保留供內部使用。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_add_jobserver**牽涉到多部伺服器的作業。  
  
## <a name="examples"></a>範例  
  
### <a name="a-assigning-a-job-to-the-local-server"></a>A. 將作業指派給本機伺服器  
 下列範例會指派 `NightlyBackups` 作業，讓它在本機伺服器中執行。  
  
> [!NOTE]  
>  這個範例假設 `NightlyBackups` 作業已在執行中。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-assigning-a-job-to-run-on-a-different-server"></a>B. 指派作業，使它在不同的伺服器中執行  
 下列範例會將多伺服器作業 `Weekly Sales Backups` 指派給 `SEATTLE2` 伺服器。  
  
> [!NOTE]  
>  這個範例假設 `Weekly Sales Backups` 作業已存在，且 `SEATTLE2` 已註冊為目前執行個體的目標伺服器。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',  
    @server_name = N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_apply_job_to_targets &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
