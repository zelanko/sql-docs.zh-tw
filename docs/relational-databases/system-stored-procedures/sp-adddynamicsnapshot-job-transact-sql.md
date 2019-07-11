---
title: sp_adddynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a86fd3d8abcee391852c8528d3fbe054b7bcc525
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716720"
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立一項代理程式作業，利用參數化資料列篩選器，產生發行集篩選資料快照集。 這個預存程序執行於發行集資料庫的發行者端。 管理員利用這個預存程序，手動建立訂閱者的已篩選資料快照集作業。  
  
> [!NOTE]  
>  若要建立已篩選資料快照集，發行集的標準快照集作業必須已經存在。  
  
 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_adddynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]   
    [ , [ @host_name = ] 'host_name' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' OUTPUT ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' OUTPUT ]   
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是要加的已篩選的資料快照集作業的發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @suser_sname = ] 'suser_sname'` 建立訂用帳戶的已篩選的資料快照集，篩選的值時所用的值[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)函式，在訂閱者。 *suser_sname*已**sysname**，沒有預設值。 *suser_sname*應該是 NULL，如果此函式不用來動態篩選發行集。  
  
`[ @host_name = ] 'host_name'` 建立訂用帳戶的已篩選的資料快照集，篩選的值時所用的值[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函式，在訂閱者。 *host_name*已**sysname**，沒有預設值。 *host_name*應該是 NULL，如果此函式不用來動態篩選發行集。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'` 是建立已篩選的資料快照集作業名稱。 *dynamic_snapshot_jobname*已**sysname**，預設值是 NULL，而且是選擇性的 OUTPUT 參數。 如果指定， *dynamic_snapshot_jobname*必須解析為在散發者的唯一作業。 如果未指定，就會自動產生作業名稱，而且會在結果集中傳回作業名稱，名稱的建立方式如下：  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  產生動態快照集作業的名稱時，您可以截斷標準快照集作業的名稱。  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'` 是建立已篩選的資料快照集作業的識別碼。 *dynamic_snapshot_jobid*已**uniqueidentifier**，預設值是 NULL，而且是選擇性的 OUTPUT 參數。  
  
`[ @frequency_type = ] frequency_type` 是的排程已篩選的資料快照集作業的頻率。 *frequency_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4** （預設值）|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
  
`[ @frequency_interval = ] frequency_interval` 是已篩選的資料快照集作業執行時的間隔 （以天為單位）。 *frequency_interval*已**int**，預設值為 1，而定的值*frequency_type*。  
  
|值*frequency_type*|在影響*frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval*未使用。|  
|**4** （預設值）|每隔*frequency_interval*天，預設值是每日。|  
|**8**|*frequency_interval*是一或多個項目 (結合[ &#124; &#40;位元 OR&#41; &#40;-&#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md)邏輯運算子):<br /><br /> **1** = 星期日&#124; **2** = 星期一&#124; **4** = 星期二&#124; **8** = 星期三&#124; **16** =星期四&#124; **32** = 星期五&#124; **64** = 星期六|  
|**16**|在  *frequency_interval*天的月份。|  
|**32**|*frequency_interval*是下列其中之一：<br /><br /> **1** = 星期日&#124; **2** = 星期一&#124; **3** = 星期二&#124; **4** = 星期三&#124; **5** =星期四&#124; **6** = 星期五&#124; **7** = 星期六&#124; **8** = 日&#124; **9** = 工作日&#124; **10** = 週末|  
|**64**|*frequency_interval*未使用。|  
|**128**|*frequency_interval*未使用。|  
  
`[ @frequency_subday = ] frequency_subday` 指定的單位*frequency_subday_interval*。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4** （預設值）|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 是的數目*frequency_subday*每次執行作業之間發生的期間。 *frequency_subday_interval*已**int**，預設值是 5。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 是已篩選的資料快照集作業的每個月一次。 使用這個參數時*frequency_type*設為**32** （每月相對）。 *frequency_relative_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是 0。  
  
`[ @active_start_date = ] active_start_date` 排程的日期篩選的資料快照集作業時第一，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是 NULL。  
  
`[ @active_end_date = ] active_end_date` 是已篩選的資料快照集作業停止的日期在排程，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 是第一次排程已篩選的資料快照集作業時的時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 已篩選的資料快照集的當日作業停止正在排程時間，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 NULL。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別中的已篩選的資料快照集作業[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)系統資料表。|  
|**dynamic_snapshot_jobname**|**sysname**|已篩選資料快照集作業的名稱。|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|可唯一識別[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在散發者的代理程式作業。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adddynamicsnapshot_job**用於合併式複寫中使用參數化的篩選之發行集。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_adddynamicsnapshot_job**。  
  
## <a name="see-also"></a>另請參閱  
 [使用參數化篩選的合併式發行集建立快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
