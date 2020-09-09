---
description: sp_delete_maintenance_plan_job (Transact-SQL)
title: sp_delete_maintenance_plan_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_maintenance_plan_job
- sp_delete_maintenance_plan_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan_job
ms.assetid: 1c2148c3-2928-4d9b-b1c8-3512cfbd6a63
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b06c9c385d85c1b1a4cb4df79ebb22f70d5abee
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536578"
---
# <a name="sp_delete_maintenance_plan_job-transact-sql"></a>sp_delete_maintenance_plan_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  解除指定維護計畫與指定工作之間的關聯。  
  
> [!NOTE]  
>  這個預存程序需搭配資料庫維護計畫一起使用。 這項功能已被不使用這個預存程序的維護計畫所取代。 請使用這個程序來維護由舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級之安裝的資料庫維護計畫。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_maintenance_plan_job [ @plan_id = ] 'plan_id' ,   
   [ @job_id = ] 'job_id'   
```  
  
## <a name="arguments"></a>引數  
`[ @plan_id = ] 'plan\_id'` 指定維護計畫的識別碼。 *plan_id* 是 **uniqueidentifier**，必須是有效的識別碼。  
  
`[ @job_id = ] 'job\_id'` 指定與維護計畫相關聯之作業的識別碼。 *job_id* 是 **uniqueidentifier**，必須是有效的識別碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_delete_maintenance_plan_job** 必須從 **msdb** 資料庫執行。  
  
 當所有作業都已從維護計畫中移除之後，我們建議使用者執行 **sp_delete_maintenance_plan_db** ，以從方案中移除剩餘的資料庫。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_delete_maintenance_plan_job**。  
  
## <a name="examples"></a>範例  
 這個範例會從維護計畫中移除 "B8FCECB1-E22C-11D2-AA64-00C04F688EAE" 作業。  
  
```  
EXECUTE   sp_delete_maintenance_plan_job N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'B8FCECB1-E22C-11D2-AA64-00C04F688EAE';  
```  
  
## <a name="see-also"></a>另請參閱  
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [&#40;Transact-sql&#41;的資料庫維護計畫預存程式 ](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
