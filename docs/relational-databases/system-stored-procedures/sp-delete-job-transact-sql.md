---
title: sp_delete_job (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e56bfe08d9279408cc7bdbc4b57a9719a04946fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47857050"
---
# <a name="spdeletejob-transact-sql"></a>sp_delete_job (Transact-SQL)
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
 [ **@job_id=** ] *job_id*  
 這是要刪除的作業識別碼。 *job_id*已**uniqueidentifier**，預設值是 NULL。  
  
 [ **@job_name=** ] **'***job_name***'**  
 這是要刪除的作業名稱。 *job_name*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  任一*job_id*或是*job_name*必須指定; 不能同時指定這兩者。  
  
 [ **@originating_server=** ] **'***server***'**  
 供內部使用。  
  
 [  **@delete_history=** ] *delete_history*  
 指定是否刪除作業的記錄。 *delete_history*已**位元**，預設值是**1**。 當*delete_history*是**1**，刪除作業的作業記錄。 當*delete_history*是**0**，不會刪除作業記錄。  
  
 請注意，當刪除作業並不會刪除歷程記錄時，作業的歷程記錄資訊不會顯示於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式圖形化使用者介面工作歷程記錄，但資訊仍存留在**sysjobhistory**資料表中**msdb**資料庫。  
  
 [  **@delete_unused_schedule=** ] *delete_unused_schedule*  
 指定當附加至這項作業的排程並未附加至任何其他作業時，是否刪除這些排程。 *delete_unused_schedule*已**位元**，預設值是**1**。 當*delete_unused_schedule*是**1**，如果沒有其他作業參考排程，會刪除附加至這項作業的排程。 當*delete_unused_schedule*是**0**，不會刪除排程。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **@originating_server**引數保留供內部使用。  
  
 **@delete_unused_schedule**引數會提供回溯相容性的先前版本的 SQL Server 會自動移除未附加至任何作業的排程。 請注意，這個參數預設相容於舊版的行為。 若要保留未附加至作業的排程，您必須提供值**0**作為**@delete_unused_schedule**引數。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
 這個預存程序無法刪除維護計畫，也無法刪除在維護計畫中的作業。 請改用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來刪除維護計畫。  
  
## <a name="permissions"></a>Permissions  
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
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [sp_help_job &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_update_job &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
