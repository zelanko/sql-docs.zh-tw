---
title: sp_delete_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_schedule
- sp_delete_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_schedule
ms.assetid: 18b2c985-47b8-49c8-82d1-8a4af3d7d33a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2fcc7830a9efaae7e4fa7027d196e9a1df0e40b4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757947"
---
# <a name="sp_delete_schedule-transact-sql"></a>sp_delete_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  刪除排程。  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_schedule { [ @schedule_id = ] schedule_id | [ @schedule_name = ] 'schedule_name' } ,  
     [ @force_delete = ] force_delete  
```  
  
## <a name="arguments"></a>引數  
`[ @schedule_id = ] schedule_id`要刪除之排程的排程識別碼。 *schedule_id*是**int**，預設值是 Null。  
  
> **注意：** 必須指定*schedule_id*或*schedule_name* ，但不能同時指定兩者。  
  
`[ @schedule_name = ] 'schedule_name'`要刪除的排程名稱。 *schedule_name*是**sysname**，預設值是 Null。  
  
> **注意：** 必須指定*schedule_id*或*schedule_name* ，但不能同時指定兩者。  
  
`[ @force_delete = ] force_delete`指定如果排程附加至作業，程式是否應該失敗。 *Force_delete*是 bit，預設值是**0**。 當*force_delete*為**0**時，如果排程附加至作業，則預存程式會失敗。 當*force_delete*為**1**時，不論排程是否附加至作業，都會刪除排程。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 依預設，如果排程附加至作業中，並無法刪除排程。 若要刪除附加至作業的排程，請為*force_delete*指定**1**的值。 刪除排程，並不會停止目前在執行中的作業。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 請注意，作業擁有者不需要也是排程擁有者，就可以將作業附加到排程，也可以從排程卸離作業。 不過，如果卸離之後不會在排程中留下任何作業，除非呼叫端是排程擁有者，否則無法刪除該排程。  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有**系統管理員（sysadmin** ）角色的成員，才能夠刪除另一位使用者所擁有的作業排程。  
  
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
 [執行作業](../../ssms/agent/implement-jobs.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
  
