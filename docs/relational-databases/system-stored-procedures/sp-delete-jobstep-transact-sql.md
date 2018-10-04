---
title: sp_delete_jobstep (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_jobstep
- sp_delete_jobstep_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_jobstep
ms.assetid: 421ede8e-ad57-474a-9fb9-92f70a3e77e3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9408fe7939b5a34a18ecde2b1a98f68ac19e49a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628537"
---
# <a name="spdeletejobstep-transact-sql"></a>sp_delete_jobstep (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從作業中移除作業步驟。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_delete_jobstep { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ,   
     [ @step_id = ] step_id   
```  
  
## <a name="arguments"></a>引數  
 [ **@job_id=** ] *job_id*  
 將從中移除步驟之作業的識別碼。 *job_id*已**uniqueidentifier**，預設值是 NULL。  
  
 [ **@job_name=** ] **'***job_name***'**  
 將從中移除步驟之作業的名稱。 *job_name*已**sysname**，預設值是 NULL。  
  
> **注意：** 任一*job_id*或是*job_name*必須指定; 不可同時指定兩者。  
  
 [ **@step_id=** ] *step_id*  
 這是要移除的步驟識別碼。 *step_id*已**int**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 移除作業步驟會自動更新參考已刪除步驟的其他作業步驟。  
  
 如需有關相關聯的特定作業步驟的詳細資訊，請執行**sp_help_jobstep**。  
  
> **注意︰** 呼叫**sp_delete_jobstep**具有*step_id*值為零會刪除作業的所有作業步驟。  
  
 Microsoft SQL Server Management Studio 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
## <a name="permissions"></a>Permissions  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有成員**sysadmin**可以刪除其他使用者所擁有的作業步驟。  
  
## <a name="examples"></a>範例  
 下列範例會從 `1` 作業中，移除作業步驟 `Weekly Sales Data Backup`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_jobstep  
    @job_name = N'Weekly Sales Data Backup',  
    @step_id = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [檢視或修改作業](../../ssms/agent/view-or-modify-jobs.md)   
 [sp_add_jobstep &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)   
 [sp_update_jobstep &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)   
 [sp_help_jobstep &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
