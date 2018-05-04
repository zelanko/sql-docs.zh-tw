---
title: sp_stop_job (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/01/2016
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
- sp_stop_job_TSQL
- sp_stop_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stop_job
ms.assetid: 64b4cc75-99a0-421e-b418-94e37595bbb0
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b90ea52e3a64f245633b19f23382b9a147fd1639
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spstopjob-transact-sql"></a>sp_stop_job (Transact-SQL)
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
 [ **@job_name =**] **'***job_name***'**  
 這是要停止的作業名稱。 *job_name*是**sysname**，預設值是 NULL。  
  
 [ **@job_id =**] *job_id*  
 這是要停止的作業識別碼。 *job_id*是**uniqueidentifier**，預設值是 NULL。  
  
 [ **@originating_server =**] **'***master_server***'**  
 主要伺服器的名稱。 如果指定的話，會停止所有多伺服器作業。 *master_server*是**nvarchar （128)**，預設值是 NULL。 只有當呼叫時，才指定這個參數**sp_stop_job**目標伺服器上。  
  
> [!NOTE]  
>  您只能指定前三個參數的其中一個。  
  
 [ **@server_name =**] **'***target_server***'**  
 這是要停止多伺服器作業之特定目標伺服器的名稱。 *target_server*是**nvarchar （128)**，預設值是 NULL。 只有當呼叫時，才指定這個參數**sp_stop_job**在多伺服器作業的主要伺服器。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 **sp_stop_job**停止訊號傳送至資料庫。 某些處理程序可以立即停止，某些必須達到一個穩定的點 （或程式碼路徑的起點） 它們可以停止之前。 某些長時間執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (如 BACKUP、RESTORE) 和某些 DBCC 命令可能需要一段很長的時間才能完成。 這些執行時，取消作業之前它可能需要一些時間。 停止作業會造成「作業取消」項目記錄在作業記錄中。  
  
 如果作業目前正在執行類型的步驟**CmdExec**或**PowerShell**，此程序正在執行 (例如 MyProgram.exe) 會強制提前結束。 提前結束可能造成無法預期的行為，例如，有保留開啟狀態的處理序在使用檔案。 因此， **sp_stop_job**應該只有在極端的情況下使用，如果作業包含類型的步驟**CmdExec**或**PowerShell**。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 成員**SQLAgentUserRole**和**SQLAgentReaderRole**只能停止他們所擁有的作業。 成員**SQLAgentOperatorRole**可以停止所有本機作業，包括其他使用者所擁有。 成員**sysadmin**可以停止所有本機作業和多伺服器作業。  
  
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
 [sp_delete_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_start_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_update_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
