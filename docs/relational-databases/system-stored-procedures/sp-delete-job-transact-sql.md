---
title: sp_delete_job （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_job
- sp_delete_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_job
ms.assetid: b85db6e4-623c-41f1-9643-07e5ea38db09
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 53bb2daacf55bf86693f2e083262083d7cbff22b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831240"
---
# <a name="sp_delete_job-transact-sql"></a>sp_delete_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  刪除作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_job { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,  
     [ , [ @originating_server = ] 'server' ]   
     [ , [ @delete_history = ] delete_history ]  
     [ , [ @delete_unused_schedule = ] delete_unused_schedule ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id`這是要刪除之作業的識別碼。 *job_id*是**uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'`這是要刪除的作業名稱。 *job_name*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定*job_id*或*job_name*;兩者都無法指定。  
  
`[ @originating_server = ] 'server'`供內部使用。  
  
`[ @delete_history = ] delete_history`指定是否要刪除作業的歷程記錄。 *delete_history*是**bit**，預設值是**1**。 當*delete_history*為**1**時，就會刪除作業的作業歷程記錄。 當*delete_history*為**0**時，不會刪除作業歷程記錄。  
  
 請注意，刪除作業並不刪除記錄時，該作業的歷程記錄資訊不會顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式圖形化使用者介面作業歷程記錄中，但是資訊仍然會位於**msdb**資料庫的**sysjobhistory**資料表中。  
  
`[ @delete_unused_schedule = ] delete_unused_schedule`指定是否要刪除附加至此作業的排程（如果未附加至任何其他工作）。 *delete_unused_schedule*是**bit**，預設值是**1**。 當*delete_unused_schedule*為**1**時，如果沒有其他作業參考排程，則會刪除附加至此作業的排程。 當*delete_unused_schedule*為**0**時，不會刪除排程。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 ** \@ Originating_server**引數保留供內部使用。  
  
 ** \@ Delete_unused_schedule**引數會自動移除未附加至任何作業的排程，以提供與舊版 SQL Server 的回溯相容性。 請注意，這個參數預設相容於舊版的行為。 若要保留未附加至作業的排程，您必須提供值**0**做為** \@ delete_unused_schedule**引數。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
 這個預存程序無法刪除維護計畫，也無法刪除在維護計畫中的作業。 請改用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來刪除維護計畫。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 **sp_delete_job** 來刪除任何作業。 本身不是 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者只能刪除其本身所擁有的作業。  
  
## <a name="examples"></a>範例  
 下列範例會刪除 `NightlyBackups` 作業。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_job  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
