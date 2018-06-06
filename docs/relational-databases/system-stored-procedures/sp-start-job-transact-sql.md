---
title: sp_start_job (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 58fb415b74bf26880c1000e1f3122b5f6b86f2e4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spstartjob-transact-sql"></a>sp_start_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 立即執行作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## <a name="arguments"></a>引數  
 [ **@job_name=** ] **'***job_name***'**  
 要啟動的作業名稱。 任一*job_id*或*job_name*必須指定，但不可同時指定兩者。 *job_name*是**sysname**，預設值是 NULL。  
  
 [ **@job_id=** ] *job_id*  
 要啟動的作業識別碼。 任一*job_id*或*job_name*必須指定，但不可同時指定兩者。 *job_id*是**uniqueidentifier**，預設值是 NULL。  
  
 [ **@error_flag=** ] *error_flag*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@server_name=** ] **'***server_name***'**  
 這是要在其中啟動作業的目標伺服器。 *server_name*是**nvarchar （128)**，預設值是 NULL。 *server_name*必須是其中一項作業目前針對目標伺服器。  
  
 [ **@step_name=** ] **'***step_name***'**  
 作業開始執行的步驟名稱。 只適用於本機作業。 *step_name*是**sysname**，預設值是 NULL  
  
 [ **@output_flag=** ] *output_flag*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 這個預存程序處於**msdb**資料庫。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
 成員**SQLAgentUserRole**和**SQLAgentReaderRole**只能啟動他們所擁有的作業。 成員**SQLAgentOperatorRole**可以啟動所有本機作業，包括其他使用者所擁有。 成員**sysadmin**可以啟動所有本機作業和多伺服器作業。  
  
## <a name="examples"></a>範例  
 下列範例會啟動名稱為 `Weekly Sales Data Backup` 的作業。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
