---
title: "sp_remove_job_from_targets (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs: TSQL
helpviewer_keywords: sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8748e6968197faeb3809cf8adef59bc9b2452d57
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="spremovejobfromtargets-transact-sql"></a>sp_remove_job_from_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從給定的目標伺服器或目標伺服器群組中移除指定的作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_remove_job_from_targets [ @job_id = ] job_id   
     | [ @job_name = ] 'job_name'   
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@job_id =**] *job_id*  
 要從中移除指定目標伺服器或目標伺服器群組的作業之作業識別碼。 任一*job_id*或*job_name*必須指定，但不可同時指定兩者。 *job_id*是**uniqueidentifier**，預設值是 NULL。  
  
 [  **@job_name =**] **'***job_name***'**  
 要從中移除指定目標伺服器或目標伺服器群組的作業名稱。 任一*job_id*或*job_name*必須指定，但不可同時指定兩者。 *job_name*是**sysname**，預設值是 NULL。  
  
 [  **@target_server_groups =**] **'***target_server_groups***'**  
 要從指定作業中移除的目標伺服器群組清單 (以逗號分隔)。 *target_server_groups*是**nvarchar （1024)**，預設值是 NULL。  
  
 [  **@target_servers =**] **'***target_servers***'**  
 要從指定作業中移除的目標伺服器清單 (以逗號分隔)。 *target_servers*是**nvarchar （1024)**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="permissions"></a>Permissions  
 這個程序的執行權限預設會授與 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會從 `Weekly Sales Backups` 目標伺服器群組及 `Servers Processing Customer Orders` 和 `SEATTLE1` 伺服器中，移除先前建立的 `SEATTLE2` 作業。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_remove_job_from_targets  
    @job_name = N'Weekly Sales Backups',  
    @target_server_groups = N'Servers Processing Customer Orders',   
    @target_servers = N'SEATTLE2,SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [sp_apply_job_to_targets &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
