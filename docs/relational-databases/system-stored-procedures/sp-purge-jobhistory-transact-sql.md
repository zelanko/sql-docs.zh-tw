---
description: sp_purge_jobhistory (Transact-SQL)
title: sp_purge_jobhistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 771d053b8e775ee59266aa5ff53180f2ee739327
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469264"
---
# <a name="sp_purge_jobhistory-transact-sql"></a>sp_purge_jobhistory (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  移除作業的記錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_name = ] 'job_name'` 要刪除歷程記錄的作業名稱。 *job_name*是 **sysname**，預設值是 Null。 必須指定 *job_id* 或 *job_name* ，但不能同時指定兩者。  
  
> [!NOTE]  
>  **系統管理員（sysadmin** ）固定伺服器角色的成員或**SQLAgentOperatorRole**固定資料庫角色的成員，不需要指定*job_name*或*job_id*，就可以執行**sp_purge_jobhistory** 。 當 **系統管理員（sysadmin** ）使用者未指定這些引數時，會在 *oldest_date*指定的時間內刪除所有本機和多伺服器作業的作業歷程記錄。 當 **SQLAgentOperatorRole** 使用者未指定這些引數時，會在 *oldest_date*指定的時間內刪除所有本機作業的作業歷程記錄。  
  
`[ @job_id = ] job_id` 要刪除記錄之作業的作業識別碼。 *job_id* 是 **uniqueidentifier**，預設值是 Null。 必須指定 *job_id* 或 *job_name* ，但不能同時指定兩者。 如需**系統管理員（sysadmin** ）或**SQLAgentOperatorRole**使用者可以如何使用此引數的詳細資訊，請參閱** \@ job_name**描述中的附注。  
  
`[ @oldest_date = ] oldest_date` 要保留在歷程記錄中的最舊記錄。 *oldest_date* 是 **datetime**，預設值是 Null。 當指定 *oldest_date* 時， **sp_purge_jobhistory** 只會移除比指定值還舊的記錄。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 當 **sp_purge_jobhistory** 成功完成時，就會傳回訊息。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員（sysadmin** ）固定伺服器角色或 **SQLAgentOperatorRole** 固定資料庫角色的成員，才能夠執行這個預存程式。 **系統管理員（sysadmin** ）的成員可以清除所有本機和多伺服器作業的作業歷程記錄。 **SQLAgentOperatorRole**的成員只能清除所有本機作業的作業歷程記錄。  
  
 其他使用者，包括 **SQLAgentUserRole** 和 **SQLAgentReaderRole**成員的成員，必須明確地授與 **sp_purge_jobhistory**的 EXECUTE 許可權。 被授與此預存程序的 EXECUTE 權限之後，這些使用只能清除他們自己的作業記錄。  
  
 **SQLAgentUserRole**、 **SQLAgentReaderRole**和**SQLAgentOperatorRole**固定資料庫角色位於**msdb**資料庫中。 如需其許可權的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-remove-history-for-a-specific-job"></a>A. 移除特定作業的記錄  
 下列範例會移除名稱為 `NightlyBackups` 之作業的記錄。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-remove-history-for-all-jobs"></a>B. 移除所有作業的記錄  
  
> [!NOTE]  
>  只有 **系統管理員（sysadmin** ）固定伺服器角色的成員和 **SQLAgentOperatorRole** 的成員，才能夠移除所有作業的歷程記錄。 當 **系統管理員（sysadmin** ）使用者執行不含任何參數的此預存程式時，會清除所有本機和多伺服器作業的作業歷程記錄。 當 **SQLAgentOperatorRole** 使用者不使用參數執行此預存程式時，只會清除所有本機作業的作業歷程記錄。  
  
 下列範例會執行不含任何參數的程序來移除所有記錄。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_help_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
