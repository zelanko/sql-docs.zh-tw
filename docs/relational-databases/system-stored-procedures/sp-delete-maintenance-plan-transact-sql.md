---
description: sp_delete_maintenance_plan (Transact-SQL)
title: sp_delete_maintenance_plan (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_maintenance_plan
- sp_delete_maintenance_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan
ms.assetid: 6f36b63f-3d18-4d42-9469-2febb6926530
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8ba3e8e3529ab47b7789bc19334f973ae0879deb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469664"
---
# <a name="sp_delete_maintenance_plan-transact-sql"></a>sp_delete_maintenance_plan (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  刪除指定的維護計畫。  
  
> [!NOTE]  
>  這個預存程序需搭配資料庫維護計畫一起使用。 這項功能已被不使用這個預存程序的維護計畫所取代。 請使用這個程序來維護由舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級之安裝的資料庫維護計畫。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_maintenance_plan [ @plan_id = ] 'plan_id'   
```  
  
## <a name="arguments"></a>引數  
`[ @plan_id = ] 'plan\_id'` 指定要刪除之維護計畫的識別碼。 *plan_id* 是 **uniqueidentifier**，必須是有效的識別碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_delete_maintenance_plan** 必須從 **msdb** 資料庫執行。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_delete_maintenance_plan**。  
  
## <a name="examples"></a>範例  
 刪除使用 **sp_add_maintenance_plan**所建立的維護計畫。  
  
```  
EXECUTE sp_delete_maintenance_plan 'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>另請參閱  
 [維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [&#40;Transact-sql&#41;的資料庫維護計畫預存程式 ](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
