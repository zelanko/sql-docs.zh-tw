---
title: sp_delete_schedule (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_schedule
- sp_delete_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_schedule
ms.assetid: 18b2c985-47b8-49c8-82d1-8a4af3d7d33a
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14fd520f5447092e5f82dc786696148f3dbe3bd3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spdeleteschedule-transact-sql"></a>sp_delete_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  刪除排程。  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_schedule { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @force_delete = ] force_delete  
```  
  
## <a name="arguments"></a>引數  
 [ **@schedule_id=** ] *schedule_id*  
 這是要刪除之排程的排程識別碼。 *schedule_id*是**int**，預設值是 NULL。  
  
> **注意：**任一*schedule_id*或*schedule_name*必須指定，但不可同時指定兩者。  
  
 [  **@schedule_name=** ] **'***schedule_name***'**  
 這是要刪除的排程名稱。 *schedule_name*是**sysname**，預設值是 NULL。  
  
> **注意：**任一*schedule_id*或*schedule_name*必須指定，但不可同時指定兩者。  
  
 [ **@force_delete** = ] *force_delete*  
 指定如果排程附加至作業，程序是否會失敗。 *Force_delete* bit，預設值是**0**。 當*force_delete*是**0**，如果排程附加至作業的預存程序會失敗。 當*force_delete*是**1**，不論排程是否附加至作業刪除此排程。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 依預設，如果排程附加至作業中，並無法刪除排程。 若要刪除附加至作業的排程，指定其值為**1**如*force_delete*。 刪除排程，並不會停止目前在執行中的作業。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 請注意，作業擁有者不需要也是排程擁有者，就可以將作業附加到排程，也可以從排程卸離作業。 不過，如果卸離之後不會在排程中留下任何作業，除非呼叫端是排程擁有者，否則無法刪除該排程。  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 只有成員**sysadmin**角色可以刪除另一位使用者所擁有的作業排程。  
  
## <a name="examples"></a>範例  
  
### <a name="a-deleting-a-schedule"></a>A. 刪除排程  
 下列範例會刪除 `NightlyJobs` 排程。 如果這份排程附加至任何作業中，這個範例便不會刪除這份排程。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
### <a name="b-deleting-a-schedule-attached-to-a-job"></a>B. 刪除附加至作業的排程  
 下列範例會刪除 `RunOnce` 排程，不論排程是否附加至作業中都是如此。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_schedule  
    @schedule_name = 'RunOnce',  
    @force_delete = 1;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [實作作業](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
  
