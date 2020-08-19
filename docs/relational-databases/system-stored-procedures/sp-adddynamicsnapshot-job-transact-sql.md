---
description: sp_adddynamicsnapshot_job (Transact-SQL)
title: sp_adddynamicsnapshot_job (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 25bbf50a6732806c37eafeb3efedddd712dcba57
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447440"
---
# <a name="sp_adddynamicsnapshot_job-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

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
`[ @publication = ] 'publication'` 這是加入篩選資料快照集作業的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @suser_sname = ] 'suser_sname'` 這是為訂閱建立已篩選資料快照集時所用的值，該訂閱是由訂閱者端的 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 函數值所篩選。 *suser_sname* 是 **sysname**，沒有預設值。 如果不使用這個函數來動態篩選發行集， *suser_sname*應為 Null。  
  
`[ @host_name = ] 'host_name'` 這是為訂閱建立已篩選資料快照集時所用的值，該訂閱是由訂閱者端的 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 函數值所篩選。 *host_name* 是 **sysname**，沒有預設值。 如果不使用這個函數來動態篩選發行集， *host_name*應為 Null。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'` 這是已建立的已篩選資料快照集作業名稱。 *dynamic_snapshot_jobname* 是 **sysname**，預設值是 Null，而且是選擇性的輸出參數。 如果有指定， *dynamic_snapshot_jobname* 必須在散發者端解析為唯一的作業。 如果未指定，就會自動產生作業名稱，而且會在結果集中傳回作業名稱，名稱的建立方式如下：  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  產生動態快照集作業的名稱時，您可以截斷標準快照集作業的名稱。  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'` 這是已建立之已篩選資料快照集作業的識別碼。 *dynamic_snapshot_jobid* 是 **uniqueidentifier**，預設值是 Null，而且是選擇性的輸出參數。  
  
`[ @frequency_type = ] frequency_type` 這是已篩選資料快照集作業的排程頻率。 *frequency_type* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次性|  
|**2**|隨選|  
|**4** (預設) |每日|  
|**8**|每週|  
|**16**|每月|  
|**32**|每月相對|  
|**64**|自動啟動|  
|**128**|重複執行|  
  
`[ @frequency_interval = ] frequency_interval` 這是在執行已篩選資料快照集作業時， (以天為單位的期間) 。 *frequency_interval* 是 **int**，預設值為1，而且相依于 *frequency_type*的值。  
  
|*Frequency_type*的值|對*frequency_interval*的影響|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval* 未使用。|  
|**4** (預設) |每 *frequency_interval* 天，預設值為 [每日]。|  
|**8**|*frequency_interval* 是下列一或多個 (結合 [&#124; &#40;位或&#41; &#40;transact-sql&#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md) 邏輯運算子) ：<br /><br /> **1** = 星期日 &#124; **2** = 星期一 &#124; **4** = 星期二 &#124; **8** = 星期三 &#124; **16** = 星期四 &#124; **32** = 星期五 &#124; **64** = 星期六|  
|**16**|在當月的 *frequency_interval* 日。|  
|**32**|*frequency_interval* 是下列其中一項：<br /><br /> **1** = 星期日 &#124; **2** = 星期一 &#124; **3** = 星期二 &#124; **4** = 星期三 &#124; **5** = 星期四 &#124; **6** = 星期五 &#124; **7** = 星期六 &#124; **8** = 天 &#124; **9** = 工作日 &#124; **10** = 週末日|  
|**64**|*frequency_interval* 未使用。|  
|**128**|*frequency_interval* 未使用。|  
  
`[ @frequency_subday = ] frequency_subday` 指定 *frequency_subday_interval*的單位。 *frequency_subday* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|Second|  
|**4** (預設) |Minute|  
|**8**|小時|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 這是每次執行作業之間發生的 *frequency_subday* 期間數目。 *frequency_subday_interval* 是 **int**，預設值是5。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 這是每個月的已篩選資料快照集作業的出現次數。 當 *frequency_type* 設定為 **32** (每月相對) 時，就會使用這個參數。 *frequency_relative_interval* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|First|  
|**2**|Second|  
|**4**|Third|  
|**8**|第四個|  
|**16**|Last|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 這是 *frequency_type*所用的迴圈因數。 *frequency_recurrence_factor* 是 **int**，預設值是0。  
  
`[ @active_start_date = ] active_start_date` 這是第一次排程已篩選資料快照集作業的日期，格式為 YYYYMMDD。 *active_start_date* 是 **int**，預設值是 Null。  
  
`[ @active_end_date = ] active_end_date` 這是排程停止已篩選資料快照集作業的日期，格式為 YYYYMMDD。 *active_end_date* 是 **int**，預設值是 Null。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 這是第一次排程已篩選資料快照集作業的當日時間，格式為 HHMMSS。 *active_start_time_of_day* 是 **int**，預設值是 Null。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 這是排程停止已篩選資料快照集作業的當日時間，格式為 HHMMSS。 *active_end_time_of_day* 是 **int**，預設值是 Null。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別 [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) 系統資料表中的已篩選資料快照集作業。|  
|**dynamic_snapshot_jobname**|**sysname**|已篩選資料快照集作業的名稱。|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|唯一識別散發者端的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 在使用參數化篩選之發行集的合併式複寫中，會使用**sp_adddynamicsnapshot_job** 。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_adddynamicsnapshot_job**。  
  
## <a name="see-also"></a>另請參閱  
 [使用參數化篩選建立合併式發行集的快照集](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
