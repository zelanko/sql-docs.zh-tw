---
title: "sp_add_maintenance_plan_db (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
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
- sp_add_maintenance_plan_db_TSQL
- sp_add_maintenance_plan_db
dev_langs: TSQL
helpviewer_keywords: sp_add_maintenance_plan_db
ms.assetid: 76f4fefa-5b99-4deb-beed-e198987a45a9
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8dca1b116e4cea41332e581054403025f3d2d34f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="spaddmaintenanceplandb-transact-sql"></a>sp_add_maintenance_plan_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將資料庫關聯於維護計畫。  
  
> [!NOTE]  
>  這個預存程序需搭配資料庫維護計畫一起使用。 這項功能已被不使用這個預存程序的維護計畫所取代。 請使用這個程序來維護由舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級之安裝的資料庫維護計畫。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_maintenance_plan_db [ @plan_id = ] 'plan_id' ,   
     [ @db_name = ] 'database_name'  
```  
  
## <a name="arguments"></a>引數  
 [  **@plan_id =**] **'***plan_id***'**  
 指定維護計畫的計畫識別碼。 *plan_id*是**uniqueidentifier**，而且必須是有效的識別碼。  
  
 [  **@db_name =**] **'***database_name***'**  
 指定要加入維護計畫的資料庫名稱。 資料庫必須先建立好或已存在，才能加入計畫中。 *database_name*是**sysname**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_add_maintenance_plan_db**必須從執行**msdb**資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_add_maintenance_plan_db**。  
  
## <a name="examples"></a>範例  
 這個範例會將**AdventureWorks2012**資料庫中建立的維護計畫**sp_add_maintenance_plan**。  
  
```  
EXECUTE   sp_add_maintenance_plan_db N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC',N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>請參閱＜  
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [資料庫維護計畫預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
