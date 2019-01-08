---
title: sp_changedynamicsnapshot_job & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedynamicsnapshot_job
- sp_changedynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_changedynamicsnapshot_job
ms.assetid: ea0dacd2-a5fd-42f4-88dd-7d289b0ae017
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b3f2d65811e856bfec95fcd5ffa1749f62c58c3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822472"
---
# <a name="spchangedynamicsnapshotjob-transact-sql"></a>sp_changedynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改利用參數化資料列篩選器來產生發行集訂閱快照集的代理程式作業。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changedynamicsnapshot_job [ @publication = ] 'publication'  
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
```  
  
## <a name="arguments"></a>引數  
 [ **@publication =** ] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [ **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 這是要變更的快照集作業名稱。 *dynamic_snapshot_jobname*已**sysname**，預設值是 N '%'。 如果*dynamic_snapshot_jobid*指定時，您必須使用的預設值*dynamic_snapshot_jobname*。  
  
 [ **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 這是要變更的快照集作業識別碼。 *dynamic_snapshot_jobid*已**uniqueidentifier**，預設值是 NULL。 如果*dynamic_snapshot_jobname*指定時，您必須使用的預設值*dynamic_snapshot_jobid*。  
  
 [  **@frequency_type =** ] *frequency_type*  
 這是代理程式的排程頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4**|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
|NULL (預設值)||  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 代理程式的執行天數。 *frequency_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**3**|星期二|  
|**4**|星期三|  
|**5**|星期四|  
|**6**|星期五|  
|**7**|星期六|  
|**8**|Day|  
|**9**|工作日|  
|**10**|週末|  
|NULL (預設值)||  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 這是在定義的期間內，重新排程的頻率。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (預設值)||  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是 NULL。  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 這是合併代理程式的執行日期。 使用這個參數時*frequency_type*設為**32** （每月相對）。 *frequency_relative_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
|NULL (預設值)||  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor&lt*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是 NULL。  
  
 [ **@active_start_date =** ] *active_start_date*  
 這是第一次排程合併代理程式的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是 NULL。  
  
 [ **@active_end_date =** ] *active_end_date*  
 這是排程停止合併代理程式的日期，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 NULL。  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 這是第一次排程合併代理程式的當日時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是 NULL。  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 這是排程停止合併代理程式的當日時間，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 NULL。  
  
 [  **@job_login=** ] **'***job_login***'**  
 這是利用參數化資料列篩選器來產生訂閱的快照集時，用來執行快照集代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 *job_login*已**nvarchar(257)**，預設值是 NULL。  
  
 [  **@job_password=** ] **'***job_password***'**  
 這是利用參數化資料列篩選器來產生訂閱的快照集時，用來執行快照集代理程式的 Windows 帳戶密碼。 *job_password*已**nvarchar(257)**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changedynamicsnapshot_job**用於合併式複寫中發行集使用參數化資料列篩選器。  
  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_changedynamicsnapshot_job**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
