---
title: sp_adddynamicsnapshot_job (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2a4967dd959be15f8f9bb1ef4654486b6fee6ace
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立一項代理程式作業，利用參數化資料列篩選器，產生發行集篩選資料快照集。 這個預存程序執行於發行集資料庫的發行者端。 管理員利用這個預存程序，手動建立訂閱者的已篩選資料快照集作業。  
  
> [!NOTE]  
>  若要建立已篩選資料快照集，發行集的標準快照集作業必須已經存在。  
  
 如需詳細資訊，請參閱＜ [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)＞。  
  
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
 [ **@publication=**] **'***publication***'**  
 這是加入篩選之資料快照集作業的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [ **@suser_sname**=] **'***suser_sname***'**  
 建立已篩選的資料快照集的訂用帳戶篩選的值時所用的值[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)函式在 「 訂閱者 」。 *suser_sname*是**sysname**，沒有預設值。 *suser_sname*應該是 NULL，如果不利用這個函數來動態篩選發行集。  
  
 [ **@host_name**=] **'***host_name***'**  
 建立已篩選的資料快照集的訂用帳戶篩選的值時所用的值[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函式在 「 訂閱者 」。 *host_name*是**sysname**，沒有預設值。 *host_name*應該是 NULL，如果不利用這個函數來動態篩選發行集。  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname***'**  
 這是建立的已篩選資料快照集作業名稱。 *dynamic_snapshot_jobname*是**sysname**，預設值是 NULL，而且是選擇性輸出參數。 如果指定， *dynamic_snapshot_jobname*必須解析為散發者端的唯一作業。 如果未指定，就會自動產生作業名稱，而且會在結果集中傳回作業名稱，名稱的建立方式如下：  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  產生動態快照集作業的名稱時，您可以截斷標準快照集作業的名稱。  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid***'**  
 這是建立的已篩選資料快照集作業識別碼。 *dynamic_snapshot_jobid*是**uniqueidentifier**，預設值是 NULL，而且是選擇性輸出參數。  
  
 [  **@frequency_type=**] *frequency_type*  
 這是已篩選資料快照集作業的排程頻率。 *frequency_type*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|視需要|  
|**4** （預設值）|每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 這是執行已篩選資料快照集作業的週期 (以天為單位)。 *frequency_interval*是**int**，預設值為 1，而定的值*frequency_type*。  
  
|值*frequency_type*|在影響*frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval*未使用。|  
|**4** （預設值）|每個*frequency_interval*天，預設值是每日。|  
|**8**|*frequency_interval*是下列一或多個項目 (結合[ &#124; &#40;位元 OR&#41; &#40;TRANSACT-SQL&#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md)邏輯運算子):<br /><br /> **1** = 星期日&#124; **2** = 星期一&#124; **4** = 星期二&#124; **8** = 星期三&#124; **16** =星期四&#124; **32** = 星期五&#124; **64** = 星期六|  
|**16**|在*frequency_interval*月份的日期。|  
|**32**|*frequency_interval*是下列其中之一：<br /><br /> **1** = 星期日&#124; **2** = 星期一&#124; **3** = 星期二&#124; **4** = 星期三&#124; **5** =星期四&#124; **6** = 星期五&#124; **7** = 星期六&#124; **8** = 日&#124; **9** = 工作日&#124; **10** = 週末|  
|**64**|*frequency_interval*未使用。|  
|**128**|*frequency_interval*未使用。|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 指定的單位*frequency_subday_interval*。 *frequency_subday*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4** （預設值）|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 是的數目*frequency_subday*每次執行作業之間發生的期間。 *frequency_subday_interval*是**int**，預設值是 5。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 這是每個月已篩選資料快照集作業的出現頻率。 使用這個參數時*frequency_type*設**32** （每月相對）。 *frequency_relative_interval*是**int**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**1** (預設值)|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*是**int**，預設值是 0。  
  
 [  **@active_start_date=**] *active_start_date*  
 這是第一次排程已篩選資料快照集作業的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 NULL。  
  
 [  **@active_end_date=**] *active_end_date*  
 這是排程停止已篩選資料快照集作業的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 NULL。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 這是第一次排程已篩選資料快照集作業的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是 NULL。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 這是排程停止已篩選資料快照集作業的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 NULL。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別已篩選的資料快照集作業中[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)系統資料表。|  
|**dynamic_snapshot_jobname**|**sysname**|已篩選資料快照集作業的名稱。|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|可唯一識別[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在散發者代理程式作業。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_adddynamicsnapshot_job**用於合併式複寫中使用參數化的篩選之發行集。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_adddynamicsnapshot_job**。  
  
## <a name="see-also"></a>另請參閱  
 [建立合併式發行集使用參數化篩選的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [參數化資料列篩選器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
