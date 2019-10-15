---
title: sp_delete_jobsteplog （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobsteplog
- sp_delete_jobsteplog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobsteplog
ms.assetid: e9ef4c99-abde-4038-b6a3-a25dcbaf0958
author: stevestein
ms.author: sstein
ms.openlocfilehash: 66b353c7fc79b49cb9cd3fb9fe228075f3a0d473
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305095"
---
# <a name="sp_delete_jobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除引數所指定的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟記錄。 使用此預存程式來維護**msdb**資料庫中的**sysjobstepslogs**資料表。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] 'job_id'` 包含要移除之作業步驟記錄之作業的作業識別碼。 *job_id*是**int**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'`，這是作業的名稱。 *job_name*是**sysname**，預設值是 Null。  
  
> **注意：** 必須指定*job_id*或*job_name* ，但不能同時指定兩者。  
  
`[ @step_id = ] step_id` 作業中要刪除作業步驟記錄之步驟的識別碼。 如果未包含，則會刪除作業中的所有作業步驟記錄檔，除非指定了 **@no__t 1older_than**或 **@no__t 3larger_than** 。 *step_id*是**int**，預設值是 Null。  
  
`[ @step_name = ] 'step_name'` 作業中要刪除作業步驟記錄之步驟的名稱。 *step_name*是**sysname**，預設值是 Null。  
  
> **注意：** 可以指定*step_id*或*step_name* ，但不能同時指定兩者。  
  
`[ @older_than = ] 'date'` 您要保留的最舊作業步驟記錄的日期和時間。 在這個日期和時間之前的所有作業步驟記錄都會被移除。 *date*是**datetime**，預設值是 Null。 可以同時指定 **@no__t 1older_than**和 **@no__t 3larger_than** 。  
  
`[ @larger_than = ] 'size_in_bytes'`，這是您想要保留的最大作業步驟記錄檔的大小（以位元組為單位）。 所有超出這個大小的作業步驟記錄都會被移除。 可以同時指定 **@no__t 1larger_than**和 **@no__t 3older_than** 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_delete_jobsteplog**在**msdb**資料庫中。  
  
 如果未指定 **\@job_id**或 **\@job_name**以外的任何引數，則會刪除指定之作業的所有作業步驟記錄。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有**系統管理員（sysadmin** ）的成員可以刪除其他使用者所擁有的作業步驟記錄。  
  
## <a name="examples"></a>範例  
  
### <a name="a-removing-all-job-step-logs-from-a-job"></a>A. 從作業中移除所有作業步驟記錄  
 下列範例會移除 `Weekly Sales Data Backup` 作業的所有作業步驟記錄。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup';  
GO  
```  
  
### <a name="b-removing-the-job-step-log-for-a-particular-job-step"></a>B. 移除特定作業步驟的作業步驟記錄  
 下列範例會移除 `Weekly Sales Data Backup` 作業中第 2 步驟的作業步驟記錄。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 2;  
GO  
```  
  
### <a name="c-removing-all-job-step-logs-based-on-age-and-size"></a>C. 根據存在時間和大小來移除所有作業步驟記錄  
 下列範例會從 `Weekly Sales Data Backup` 作業中，移除在 2005 年 10 月 25 日中午之前的所有作業步驟記錄，以及超出 100 MB 的作業步驟記錄。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobsteplog  
    @job_name = N'Weekly Sales Data Backup',  
    @older_than = '10/25/2005 12:00:00',  
    @larger_than = 104857600;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_help_jobsteplog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [SQL Server Agent 預存&#40;程式 transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
