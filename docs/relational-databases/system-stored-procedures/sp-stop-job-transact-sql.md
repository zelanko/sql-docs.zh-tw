---
title: sp_stop_job （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a0549d247078634feadced301570e00746d5ba7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68032717"
---
# <a name="sp_stop_job-transact-sql"></a>sp_stop_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 停止執行作業。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_stop_job   
      [@job_name =] 'job_name'  
    | [@job_id =] job_id   
    | [@originating_server =] 'master_server'  
    | [@server_name =] 'target_server'  
```  
  
## <a name="arguments"></a>引數  
`[ @job_name = ] 'job_name'`要停止之作業的名稱。 *job_name*是**sysname**，預設值是 Null。  
  
`[ @job_id = ] job_id`要停止之作業的識別碼。 *job_id*是**uniqueidentifier**，預設值是 Null。  
  
`[ @originating_server = ] 'master_server'`主伺服器的名稱。 如果指定的話，會停止所有多伺服器作業。 *master_server*是**Nvarchar （128）**，預設值是 Null。 只有在呼叫目標伺服器上的**sp_stop_job**時，才指定此參數。  
  
> [!NOTE]  
>  您只能指定前三個參數的其中一個。  
  
`[ @server_name = ] 'target_server'`要停止多伺服器作業之特定目標伺服器的名稱。 *target_server*是**Nvarchar （128）**，預設值是 Null。 只有在針對多伺服器作業呼叫主伺服器的**sp_stop_job**時，才指定此參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_stop_job**將停止信號傳送到資料庫。 有些進程可以立即停止，有些則必須達到穩定的點（或程式碼路徑的進入點），才會停止。 某些長時間執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (如 BACKUP、RESTORE) 和某些 DBCC 命令可能需要一段很長的時間才能完成。 當這些執行時，可能需要一段時間才會取消工作。 停止作業會造成「作業取消」項目記錄在作業記錄中。  
  
 如果作業目前正在執行**CmdExec**或**PowerShell**類型的步驟，執行中的進程（例如 myprogram.exe）會強制提前結束。 提前結束可能造成無法預期的行為，例如，有保留開啟狀態的處理序在使用檔案。 因此，如果作業包含**CmdExec**或**PowerShell**類型的步驟，應該只在極端情況下使用**sp_stop_job** 。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **SQLAgentUserRole**和**SQLAgentReaderRole**的成員只能停止他們所擁有的作業。 **SQLAgentOperatorRole**的成員可以停止所有的本機作業，包括其他使用者所擁有的工作。 **系統管理員（sysadmin** ）的成員可以停止所有本機和多伺服器作業。  
  
## <a name="examples"></a>範例  
 下列範例會停止名稱為 `Weekly Sales Data Backup` 的作業。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_stop_job  
    N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
