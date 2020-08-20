---
description: sp_add_jobserver (Transact-SQL)
title: sp_add_jobserver (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 17759b079b8f2263d6cfe025d8550d35747ab080
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489670"
---
# <a name="sp_add_jobserver-transact-sql"></a>sp_add_jobserver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將指定作業的目標鎖定在指定的伺服器上。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_jobserver [ @job_id = ] job_id | [ @job_name = ] 'job_name'  
     [ , [ @server_name = ] 'server' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id` 作業的識別碼。 *job_id* 是 **uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'` 作業的名稱。 *job_name* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定 *job_id* 或 *job_name* ，但不能同時指定兩者。  
  
`[ @server_name = ] 'server'` 要做為作業目標的伺服器名稱。 *伺服器* 是 **Nvarchar (30) **，預設值是 N ' (LOCAL) '。 *伺服器* 可以 (本機伺服器的 ** 本機) ** ，也可以是現有目標伺服器的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 ** \@ automatic_post**存在於**sp_add_jobserver**中，但未列于 [引數] 之下。 ** \@ automatic_post**保留供內部使用。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠針對牽涉到多部伺服器的工作執行 **sp_add_jobserver** 。  
  
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
 [sp_apply_job_to_targets &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
