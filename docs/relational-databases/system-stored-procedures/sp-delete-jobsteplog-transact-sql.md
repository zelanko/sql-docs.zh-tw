---
title: sp_delete_jobsteplog (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 719038f8ce72bdb05ad9dbf3c3585c377abb3a75
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526229"
---
# <a name="spdeletejobsteplog-transact-sql"></a>sp_delete_jobsteplog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除引數所指定的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟記錄。 使用此預存程序來維護**sysjobstepslogs**資料表中**msdb**資料庫。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_jobsteplog { [ @job_id = ] 'job_id' | [ @job_name = ] 'job_name' }  
       [ , [ @step_id = ] step_id | [ @step_name = ] 'step_name' ]  
       [ , [ @older_than = ] 'date' ]  
       [ , [ @larger_than = ] 'size_in_bytes' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@job_id =**] **'**_job_id_**'**  
 包含將移除的作業步驟記錄之作業的作業識別碼。 *job_id*已**int**，預設值是 NULL。  
  
 [  **@job_name =**] **'**_job_name_**'**  
 作業的名稱。 *job_name*已**sysname**，預設值是 NULL。  
  
> **注意：** 任一*job_id*或是*job_name*必須指定，但不可同時指定兩者。  
  
 [ **@step_id =**] *step_id*  
 這是作業中將刪除作業步驟記錄之步驟的識別碼。 如果未包含，會刪除作業中的所有作業步驟記錄，除非**@older_than**或是**@larger_than**所指定。 *step_id*已**int**，預設值是 NULL。  
  
 [  **@step_name =**] **'**_step_name_**'**  
 這是作業中將刪除作業步驟記錄之步驟名稱。 *step_name*已**sysname**，預設值是 NULL。  
  
> **注意：** 任一*step_id*或是*step_name*可以指定，但不可同時指定兩者。  
  
 [  **@older_than =**] **'**_日期_**'**  
 您要保留的最舊作業步驟記錄的日期和時間。 在這個日期和時間之前的所有作業步驟記錄都會被移除。 *日期*已**datetime**，預設值是 NULL。 兩者**@older_than**並**@larger_than**可以指定。  
  
 [  **@larger_than =**] **'**_size_in_bytes_**'**  
 您要保留的最大作業步驟記錄的大小 (以位元組為單位)。 所有超出這個大小的作業步驟記錄都會被移除。 兩者**@larger_than**並**@older_than**可以指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_delete_jobsteplog**處於**msdb**資料庫。  
  
 如果任何引數，除了**@job_id**或是**@job_name**指定，會刪除指定工作的所有作業步驟記錄。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有成員**sysadmin**可以刪除其他使用者所擁有的作業步驟記錄。  
  
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
 [sp_help_jobsteplog &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [SQL Server Agent 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
