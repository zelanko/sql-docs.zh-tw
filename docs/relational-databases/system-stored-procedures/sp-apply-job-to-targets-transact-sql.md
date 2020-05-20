---
title: sp_apply_job_to_targets （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 64da8efb8018748a6fe114d5ee719d71f9940e92
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833548"
---
# <a name="sp_apply_job_to_targets-transact-sql"></a>sp_apply_job_to_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將作業套用在一或多部目標伺服器上，或套用在屬於一或多個目標伺服器群組的目標伺服器上。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id`要套用至指定目標伺服器或目標伺服器群組之作業的作業識別碼。 *job_id*是**uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'`要套用至指定之相關聯目標伺服器或目標伺服器群組的作業名稱。 *job_name*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定*job_id*或*job_name* ，但不能同時指定兩者。  
  
`[ @target_server_groups = ] 'target_server_groups'`要套用指定作業的目標伺服器群組清單（以逗號分隔）。 *target_server_groups*是**Nvarchar （2048）**，預設值是 Null。  
  
`[ @target_servers = ] 'target_servers'`要套用指定作業的目標伺服器清單（以逗號分隔）。 *target_servers*是**Nvarchar （2048）**，預設值是 Null。  
  
`[ @operation = ] 'operation'`這是指應該將指定的作業套用至指定的目標伺服器或目標伺服器群組，或從中移除。 *operation*是**Varchar （7）**，預設值是 APPLY。 有效的作業為**APPLY**和**REMOVE**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_apply_job_to_targets**提供一種簡單的方式，從多個目標伺服器套用（或移除）作業，而這是針對每個所需的目標伺服器呼叫**sp_add_jobserver** （或**sp_delete_jobserver**）的替代方法。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行此程式。  
  
## <a name="examples"></a>範例  
 下列範例會將先前建立的 `Backup Customer Information` 作業套用在 `Servers Maintaining Customer Information` 群組中的所有目標伺服器上。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_apply_job_to_targets  
    @job_name = N'Backup Customer Information',  
    @target_server_groups = N'Servers Maintaining Customer Information',   
    @operation = N'APPLY' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
