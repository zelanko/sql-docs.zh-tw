---
title: sp_help_jobs_in_schedule （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobs_in_schedule_TSQL
- sp_help_jobs_in_schedule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobs_in_schedule
ms.assetid: 1168aa2c-136b-4ba3-b18e-9070d95a26fa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 55dbd9d513383fc4ed299dd56be5022b68f68bac
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893657"
---
# <a name="sp_help_jobs_in_schedule-transact-sql"></a>sp_help_jobs_in_schedule (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回附加了特定排程之作業的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_jobs_in_schedule   
     [ @schedule_name = ] 'schedule_name' ,  
     [ @schedule_id = ] schedule_id   
```  
  
## <a name="arguments"></a>引數  
`[ @schedule_id = ] schedule_id`要列出資訊的排程識別碼。 *schedule_id*是**int**，沒有預設值。 可以指定*schedule_id*或*schedule_name* 。  
  
`[ @schedule_name = ] 'schedule_name'`要列出資訊的排程名稱。 *schedule_name*是**sysname**，沒有預設值。 可以指定*schedule_id*或*schedule_name* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 傳回下列結果集：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|作業的唯一識別碼。|  
|**originating_server**|**nvarchar(30)**|作業的來源伺服器名稱。|  
|**name**|**sysname**|作業的名稱。|  
|**後**|**tinyint**|指出是否啟用作業，以便執行。|  
|**description**|**nvarchar(512)**|作業的描述。|  
|**start_step_id**|**int**|應該作為執行起點的作業步驟識別碼。|  
|**類別**|**sysname**|作業類別目錄。|  
|**主人**|**sysname**|作業擁有者。|  
|**notify_level_eventlog**|**int**|這是一個位元遮罩，指出在哪些情況之下，應該將通知事件記錄在 Microsoft Windows 應用程式記錄檔中。 它可以是下列值之一：<br /><br /> **0** = 永不<br /><br /> **1** = 當作業成功時<br /><br /> **2** = 當作業失敗時<br /><br /> **3** = 每次作業完成時（不論作業結果為何）|  
|**notify_level_email**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送通知電子郵件。 可能的值與**notify_level_eventlog**相同。|  
|**notify_level_netsend**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送網路訊息。 可能的值與**notify_level_eventlog**相同。|  
|**notify_level_page**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時傳送頁面。 可能的值與**notify_level_eventlog**相同。|  
|**notify_email_operator**|**sysname**|要通知的操作員電子郵件名稱。|  
|**notify_netsend_operator**|**sysname**|傳送網路訊息時所用的電腦或使用者名稱。|  
|**notify_page_operator**|**sysname**|傳送呼叫時所用的電腦或使用者名稱。|  
|**delete_level**|**int**|這是一個位元組遮罩，指出在哪些情況之下，應該在作業完成時刪除作業。 可能的值與**notify_level_eventlog**相同。|  
|**date_created**|**datetime**|作業的建立日期。|  
|**date_modified**|**datetime**|上次修改作業的日期。|  
|**version_number**|**int**|作業的版本 (每次修改作業時，都會自動更新)。|  
|**last_run_date**|**int**|上次開始執行作業的日期。|  
|**last_run_time**|**int**|上次開始執行作業的時間。|  
|**last_run_outcome**|**int**|上次執行作業的輸出：<br /><br /> **0** = 失敗<br /><br /> **1** = 成功<br /><br /> **3** = 已取消<br /><br /> **5** = 未知|  
|**next_run_date**|**int**|排程下一次執行作業的日期。|  
|**next_run_time**|**int**|排程下一次執行作業的時間。|  
|**next_run_schedule_id**|**int**|下次執行的排程識別碼。|  
|**current_execution_status**|**int**|目前的執行狀態。|  
|**current_execution_step**|**sysname**|作業中目前的執行步驟。|  
|**current_retry_attempt**|**int**|如果作業在執行中，且已重試這個步驟，這便是目前這次的重試。|  
|**has_step**|**int**|作業所擁有的作業步驟數目。|  
|**has_schedule**|**int**|作業所擁有的作業排程數目。|  
|**has_target**|**int**|作業所擁有的目標伺服器數目。|  
|**type**|**int**|作業類型：<br /><br /> **1** = 本機作業。<br /><br /> **2** = 多伺服器作業。<br /><br /> **0** = 作業沒有目標伺服器。|  
  
## <a name="remarks"></a>備註  
 這個程序會列出附加至指定排程之作業的相關資訊。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **SQLAgentUserRole**的成員只能查看他們所擁有之作業的狀態。  
  
## <a name="examples"></a>範例  
 下列範例會列出附加至 `NightlyJobs` 排程的作業。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_jobs_in_schedule  
    @schedule_name = N'NightlyJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_detach_schedule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
  
