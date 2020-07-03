---
title: sp_start_job （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_start_job
- sp_start_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_start_job
ms.assetid: 8a91df6a-eb84-4512-9a17-4a6e32a9538a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 506fde9c77a0a78ef36bc4a89933ccdbe6a5f45d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893011"
---
# <a name="sp_start_job-transact-sql"></a>sp_start_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @job_name = ] 'job_name'`要啟動之作業的名稱。 必須指定*job_id*或*job_name* ，但不能同時指定兩者。 *job_name*是**sysname**，預設值是 Null。  
  
`[ @job_id = ] job_id`要啟動之作業的識別碼。 必須指定*job_id*或*job_name* ，但不能同時指定兩者。 *job_id*是**uniqueidentifier**，預設值是 Null。  
  
`[ @error_flag = ] error_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @server_name = ] 'server_name'`要在其上啟動作業的目標伺服器。 *server_name*是**Nvarchar （128）**，預設值是 Null。 *server_name*必須是作業目前設為目標的其中一個目標伺服器。  
  
`[ @step_name = ] 'step_name'`開始執行作業的步驟名稱。 只適用於本機作業。 *step_name*是**sysname**，預設值是 Null  
  
`[ @output_flag = ] output_flag` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 這個預存程式是在**msdb**資料庫中。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **SQLAgentUserRole**和**SQLAgentReaderRole**的成員只能啟動他們所擁有的作業。 **SQLAgentOperatorRole**的成員可以啟動所有本機作業，包括其他使用者所擁有的工作。 **系統管理員（sysadmin** ）的成員可以啟動所有本機和多伺服器作業。  
  
## <a name="examples"></a>範例  
 下列範例會啟動名稱為 `Weekly Sales Data Backup` 的作業。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
