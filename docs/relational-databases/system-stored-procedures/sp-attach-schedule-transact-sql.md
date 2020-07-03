---
title: sp_attach_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_schedule_TSQL
- sp_attach_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_schedule
ms.assetid: 80c80eaf-cf23-4ed8-b8dd-65fe59830dd1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6bc01db6ae019694cbff4082c394fd8c736b9a5a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85874368"
---
# <a name="sp_attach_schedule-transact-sql"></a>sp_attach_schedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  設定作業的排程。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_attach_schedule  
     { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     { [ @schedule_id = ] schedule_id   
     | [ @schedule_name = ] 'schedule_name' }  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id`要加入排程之作業的作業識別碼。 *job_id*是**uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'`要加入排程的作業名稱。 *job_name*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定*job_id*或*job_name* ，但不能同時指定兩者。  
  
`[ @schedule_id = ] schedule_id`要為作業設定之排程的排程識別碼。 *schedule_id*是**int**，預設值是 Null。  
  
`[ @schedule_name = ] 'schedule_name'`要為作業設定的排程名稱。 *schedule_name*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定*schedule_id*或*schedule_name* ，但不能同時指定兩者。  
  
## <a name="remarks"></a>備註  
 排程和作業的擁有者必須相同。  
  
 多項作業可以設定同一份排程。 一項作業可以根據多份排程來執行。  
  
 這個預存程式必須從**msdb**資料庫中執行。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 請注意，作業擁有者不需要也是排程擁有者，就可以將作業附加到排程，也可以從排程卸離作業。 不過，如果卸離之後不會在排程中留下任何作業，除非呼叫端是排程擁有者，否則無法刪除該排程。  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會檢查使用者是否同時擁有作業和排程。  
  
## <a name="examples"></a>範例  
 下列範例會建立一份名稱為 `NightlyJobs` 的排程。 每天伺服器時間到了 `01:00` 時，就會開始執行使用這份排程的作業。 這個範例會將排程附加至 `BackupDatabase` 作業和 `RunReports` 作業上。  
  
> [!NOTE]  
>  這個範例假設 `BackupDatabase` 作業和 `RunReports` 作業都已經存在。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_add_schedule  
    @schedule_name = N'NightlyJobs' ,  
    @freq_type = 4,  
    @freq_interval = 1,  
    @active_start_time = 010000 ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'BackupDatabase',  
   @schedule_name = N'NightlyJobs' ;  
GO  
  
EXEC sp_attach_schedule  
   @job_name = N'RunReports',  
   @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)  
  
  
