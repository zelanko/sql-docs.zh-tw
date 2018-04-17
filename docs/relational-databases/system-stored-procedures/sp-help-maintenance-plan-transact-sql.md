---
title: sp_help_maintenance_plan (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a949b24851a4cb5a2a7bcfec8fb9ad4730f3efe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpmaintenanceplan-transact-sql"></a>sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定維護計畫的相關資訊。 如果未指定計畫，這個預存程序會傳回所有維護計畫的相關資訊。  
  
> **注意：**這個預存程序搭配資料庫維護計畫。 這項功能已被不使用這個預存程序的維護計畫所取代。 請使用這個程序來維護由舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級之安裝的資料庫維護計畫。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@plan_id =**] **'***plan_id***'**  
 指定維護計畫的計畫識別碼。 *plan_id*是**UNIQUEIDENTIFIER**。 預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
 如果*plan_id*指定，則**sp_help_maintenance_plan**會傳回三個資料表： 計劃、 資料庫和作業。  
  
### <a name="plan-table"></a>計畫資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|維護計畫識別碼。|  
|**plan_name**|**sysname**|維護計畫名稱。|  
|**date_created**|**datetime**|維護計畫的建立日期。|  
|**擁有者**|**sysname**|維護計畫的擁有者。|  
|**max_history_rows**|**int**|用來將維護計畫的記錄記載到系統資料表中，所配置的最大資料列數。|  
|**remote_history_server**|**int**|可以寫入記錄報表之遠端伺服器的名稱。|  
|**max_remote_history_rows**|**int**|在遠端伺服器系統資料表中，可寫入記錄報表的資料列最大配置列數。|  
|**user_defined_1**|**int**|預設值是 NULL。|  
|**user_defined_2**|**nvarchar(100)**|預設值是 NULL。|  
|**user_defined_3**|**datetime**|預設值是 NULL。|  
|**user_defined_4**|**uniqueidentifier**|預設值是 NULL。|  
  
### <a name="database-table"></a>資料庫資料表  
  
|資料行名稱|Description|  
|-----------------|-----------------|  
|**database_name**|維護計畫所有相關資料庫的名稱。 *database_name* 為 **sysname**。|  
  
### <a name="job-table"></a>作業資料表  
  
|資料行名稱|Description|  
|-----------------|-----------------|  
|**job_id**|與維護計畫相關聯之所有作業的識別碼。 *job_id*是**uniqueidentifier**。|  
  
## <a name="remarks"></a>備註  
 **sp_help_maintenance_plan**處於**msdb**資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_help_maintenance_plan**。  
  
## <a name="examples"></a>範例  
 這個範例說明 FAD6F2AB-3571-11D3-9D4A-00C04FB925FC 維護計畫的相關資訊。  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>另請參閱  
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [資料庫維護計畫預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
