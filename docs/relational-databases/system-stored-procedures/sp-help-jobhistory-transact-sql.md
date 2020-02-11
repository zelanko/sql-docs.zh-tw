---
title: sp_help_jobhistory （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobhistory_TSQL
- sp_help_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobhistory
ms.assetid: a944d44e-411b-4735-8ce4-73888d4262d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 10033b2525ba28e79bd31a73bd9e71a7cca15e42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054935"
---
# <a name="sp_help_jobhistory-transact-sql"></a>sp_help_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供多伺服器管理網域中之伺服器的作業相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_jobhistory [ [ @job_id = ] job_id ]   
     [ , [ @job_name = ] 'job_name' ]   
     [ , [ @step_id = ] step_id ]   
     [ , [ @sql_message_id = ] sql_message_id ]   
     [ , [ @sql_severity = ] sql_severity ]   
     [ , [ @start_run_date = ] start_run_date ]   
     [ , [ @end_run_date = ] end_run_date ]   
     [ , [ @start_run_time = ] start_run_time ]   
     [ , [ @end_run_time = ] end_run_time ]   
     [ , [ @minimum_run_duration = ] minimum_run_duration ]   
     [ , [ @run_status = ] run_status ]   
     [ , [ @minimum_retries = ] minimum_retries ]   
     [ , [ @oldest_first = ] oldest_first ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @mode = ] 'mode' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_id = ] job_id`作業識別碼。 *job_id*是**uniqueidentifier**，預設值是 Null。  
  
`[ @job_name = ] 'job_name'`作業的名稱。 *job_name*是**sysname**，預設值是 Null。  
  
`[ @step_id = ] step_id`步驟識別碼。 *step_id*是**int**，預設值是 Null。  
  
`[ @sql_message_id = ] sql_message_id`執行作業時，Microsoft SQL Server 所傳回之錯誤訊息的識別碼。 *sql_message_id*是**int**，預設值是 Null。  
  
`[ @sql_severity = ] sql_severity`執行作業時 SQL Server 所傳回之錯誤訊息的嚴重性層級。 *sql_severity*是**int**，預設值是 Null。  
  
`[ @start_run_date = ] start_run_date`作業的啟動日期。 *start_run_date*是**int**，預設值是 Null。 *start_run_date*必須以 YYYYMMDD 格式輸入，其中 YYYY 是四字元的年份，MM 是兩個字元的月份名稱，而 DD 是兩字元的日期名稱。  
  
`[ @end_run_date = ] end_run_date`作業的完成日期。 *end_run_date*是**int**，預設值是 Null。 *end_run_date*必須以 YYYYMMDD 格式輸入，其中 YYYY 是四位數的年份，MM 是兩個字元的月份名稱，而 DD 是兩字元的日期名稱。  
  
`[ @start_run_time = ] start_run_time`作業的啟動時間。 *start_run_time*是**int**，預設值是 Null。 *start_run_time*必須以 HHMMSS 的形式輸入，其中 HH 是一天的兩個字元的小時，MM 是一天中的兩個字元的分鐘，而 SS 則是一天中的兩個字元。  
  
`[ @end_run_time = ] end_run_time`作業完成執行的時間。 *end_run_time*是**int**，預設值是 Null。 *end_run_time*必須以 HHMMSS 的形式輸入，其中 HH 是一天的兩個字元的小時，MM 是一天中的兩個字元的分鐘，而 SS 則是一天中的兩個字元。  
  
`[ @minimum_run_duration = ] minimum_run_duration`作業完成的最短時間長度。 *minimum_run_duration*是**int**，預設值是 Null。 *minimum_run_duration*必須以 HHMMSS 的形式輸入，其中 HH 是一天的兩個字元的小時，MM 是一天中的兩個字元的分鐘，而 SS 則是一天中的兩個字元。  
  
`[ @run_status = ] run_status`作業的執行狀態。 *run_status*是**int**，預設值是 Null，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|Failed|  
|**1**|Succeeded|  
|**2**|重試 (僅限步驟)|  
|**第**|已取消|  
|**4**|進行中訊息|  
|**第**|Unknown|  
  
`[ @minimum_retries = ] minimum_retries`作業應該重試執行的最小次數。 *minimum_retries*是**int**，預設值是 Null。  
  
`[ @oldest_first = ] oldest_first`這是指是否要先呈現具有最舊作業的輸出。 *oldest_first*是**int**，預設值是**0**，它會先顯示最新的作業。 **1**會先提供最舊的作業。  
  
`[ @server = ] 'server'`執行作業所在的伺服器名稱。 *伺服器*是**Nvarchar （30）**，預設值是 Null。  
  
`[ @mode = ] 'mode'`這是指 SQL Server 是否會列印結果集中的所有資料行（**FULL**）或資料行的摘要。 *mode*是**Varchar （7）**，預設值是**SUMMARY**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 實際的資料行清單取決於*模式*的值。 最完整的一組資料行如下所示，當*模式*為 FULL 時，會傳回。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|記錄項目識別碼。|  
|**job_id**|**uniqueidentifier**|作業識別碼。|  
|**job_name**|**sysname**|作業名稱。|  
|**step_id**|**int**|步驟識別碼（作業歷程記錄將會是**0** ）。|  
|**step_name**|**sysname**|步驟名稱 (作業記錄的這個項目是 NULL)。|  
|**sql_message_id**|**int**|這是執行命令時，[!INCLUDE[tsql](../../includes/tsql-md.md)] 步驟所遇到的最新 [!INCLUDE[tsql](../../includes/tsql-md.md)] 錯誤號碼。|  
|**sql_severity**|**int**|這是執行命令時，[!INCLUDE[tsql](../../includes/tsql-md.md)] 步驟所遇到的最高 [!INCLUDE[tsql](../../includes/tsql-md.md)] 錯誤嚴重性。|  
|**消息**|**nvarchar(1024)**|作業或步驟歷程記錄訊息。|  
|**run_status**|**int**|作業或步驟的結果。|  
|**run_date**|**int**|作業或步驟開始執行的日期。|  
|**run_time**|**int**|作業或步驟開始執行的時間。|  
|**run_duration**|**int**|執行作業或步驟所經歷的時間 (以 HHMMSS 格式表示)。|  
|**operator_emailed**|**Nvarchar （20）**|這項作業的相關電子郵件所送往的操作員 (步驟記錄的這個項目是 NULL)。|  
|**operator_netsent**|**Nvarchar （20）**|這項作業的相關網路訊息所送往的操作員 (步驟記錄的這個項目是 NULL)。|  
|**operator_paged**|**Nvarchar （20）**|這項作業的相關呼叫所送往的操作員 (步驟記錄的這個項目是 NULL)。|  
|**retries_attempted**|**int**|步驟重試的次數 (作業記錄的這個項目一律是 0)。|  
|**伺服器**|**Nvarchar （30）**|執行步驟或作業的伺服器。 一律為（**local**）。|  
  
## <a name="remarks"></a>備註  
 **sp_help_jobhistory**會傳回具有指定之排程工作歷程記錄的報表。 如果未指定任何參數，報表會包含所有已排程作業的記錄。  
  
## <a name="permissions"></a>權限  
 根據預設，**系統管理員（sysadmin** ）固定伺服器角色的成員可以執行此預存程式。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
 **SQLAgentUserRole**資料庫角色的成員只能查看他們所擁有之作業的歷程記錄。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-job-information-for-a-job"></a>A. 列出作業的所有作業資訊  
 下列範例會列出 `NightlyBackups` 作業的所有作業資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobhistory   
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-that-match-certain-conditions"></a>B. 列出符合特定準則之作業的資訊  
 下列範例會列印錯誤訊息為 `50100` (使用者自訂的錯誤訊息)，且嚴重性為 `20` 之任何失敗作業或失敗作業步驟的所有資料行和作業資訊。  
  
```  
USE msdb  
GO  
  
EXEC dbo.sp_help_jobhistory  
    @sql_message_id = 50100,  
    @sql_severity = 20,  
    @run_status = 0,  
    @mode = N'FULL' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_purge_jobhistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
