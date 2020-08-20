---
description: sp_remove_job_from_targets (Transact-SQL)
title: sp_remove_job_from_targets (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_remove_job_from_targets_TSQL
- sp_remove_job_from_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sp_remove_job_from_targets
ms.assetid: b8171fb1-c11d-4244-8618-a12e28a150ce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d40f7d8812fe83648871bedbb3538202f5c519a1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489141"
---
# <a name="sp_remove_job_from_targets-transact-sql"></a>sp_remove_job_from_targets (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @job_id = ] job_id` 要從中移除指定目標伺服器或目標伺服器群組之作業的作業識別碼。 必須指定 *job_id* 或 *job_name* ，但不能同時指定兩者。 *job_id* 是 **uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'` 要從中移除指定目標伺服器或目標伺服器群組的作業名稱。 必須指定 *job_id* 或 *job_name* ，但不能同時指定兩者。 *job_name* 是 **sysname**，預設值是 Null。  
  
`[ @target_server_groups = ] 'target_server_groups'` 要從指定作業中移除的目標伺服器群組清單（以逗號分隔）。 *target_server_groups* 是 **Nvarchar (1024) **，預設值是 Null。  
  
`[ @target_servers = ] 'target_servers'` 要從指定作業中移除的目標伺服器清單（以逗號分隔）。 *target_servers* 是 **Nvarchar (1024) **，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="permissions"></a>權限  
 執行此程式的許可權預設為 **系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [sp_apply_job_to_targets &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-apply-job-to-targets-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
