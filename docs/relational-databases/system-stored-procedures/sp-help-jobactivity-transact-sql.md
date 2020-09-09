---
description: sp_help_jobactivity (Transact-SQL)
title: sp_help_jobactivity (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobactivity_TSQL
- sp_help_jobactivity
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobactivity
ms.assetid: d344864f-b4d3-46b1-8933-b81dec71f511
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e137d556413057b409d67c8ead14530d224241e0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549680"
---
# <a name="sp_help_jobactivity-transact-sql"></a>sp_help_jobactivity (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業之執行階段狀態的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_jobactivity { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @session_id = ] session_id ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id` 作業識別碼。 *job_id*是 **uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'` 作業的名稱。 *job_name*是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  必須指定 *job_id* 或 *job_name* ，但不能同時指定兩者。  
  
`[ @session_id = ] session_id` 要報告其相關資訊的會話識別碼。 *session_id* 是 **int**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 傳回下列結果集：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|代理程式工作階段識別碼。|  
|**job_id**|**uniqueidentifier**|作業的識別碼。|  
|**job_name**|**sysname**|作業的名稱。|  
|**run_requested_date**|**datetime**|要求執行作業的時間。|  
|**run_requested_source**|**sysname**|執行作業的要求來源。 值為下列其中之一：<br /><br /> **1** = 依排程執行<br /><br /> **2** = 為了回應警示而執行<br /><br /> **3** = 在啟動時執行<br /><br /> **4** = 由使用者執行<br /><br /> **6** = 在 CPU 閒置排程上執行|  
|**queued_date**|**datetime**|將要求放入佇列的時間。 如果是直接執行作業，便是 NULL。|  
|**start_execution_date**|**datetime**|將作業指派給可執行的執行緒之時間。|  
|**last_executed_step_id**|**int**|最近執行之作業步驟的步驟識別碼。|  
|**last_exectued_step_date**|**datetime**|最近執行的作業步驟開始執行的時間。|  
|**stop_execution_date**|**datetime**|作業停止執行的時間。|  
|**next_scheduled_run_date**|**datetime**|排程下次執行作業的時間。|  
|**job_history_id**|**int**|作業記錄資料表中之作業記錄的識別碼。|  
|**message**|**nvarchar(1024)**|上次執行作業期間所產生的訊息。|  
|**run_status**|**int**|上次執行作業所傳回的狀態：<br /><br /> **0** = 錯誤失敗<br /><br /> **1** = 成功<br /><br /> **3** = 已取消<br /><br /> **5** = 狀態不明|  
|**operator_id_emailed**|**int**|作業完成時，收到電子郵件通知的操作員識別碼。|  
|**operator_id_netsent**|**int**|作業完成時，透過 **net send** 通知的操作員識別碼。|  
|**operator_id_paged**|**int**|作業完成時，收到呼叫器通知的操作員識別碼。|  
  
## <a name="remarks"></a>備註  
 這個程序提供作業目前狀態的快照集。 傳回的結果代表處理要求時的資訊。  
  
 每當代理程式服務啟動時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 都會建立一個工作階段識別碼。 會話識別碼會儲存在 **msdb.dbo.sys會話**的資料表中。  
  
 未提供任何 *session_id* 時，會列出最近會話的相關資訊。  
  
 未提供 *job_name* 或 *job_id* 時，會列出所有作業的資訊。  
  
## <a name="permissions"></a>權限  
 依預設， **系統管理員（sysadmin** ）固定伺服器角色的成員可以執行此預存程式。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 只有 **系統管理員（sysadmin** ）的成員可以查看其他使用者所擁有之作業的活動。  
  
## <a name="examples"></a>範例  
 下列範例會列出目前使用者有權檢視的所有作業的活動。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobactivity ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的 SQL Server Agent 預存程式 ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)  
  
  
