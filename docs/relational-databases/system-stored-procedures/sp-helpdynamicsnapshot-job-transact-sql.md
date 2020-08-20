---
description: sp_helpdynamicsnapshot_job (Transact-SQL)
title: sp_helpdynamicsnapshot_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords:
- sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 61e72b03e3bc6adff3a9e3d0858a8a2bdb4b5805
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469290"
---
# <a name="sp_helpdynamicsnapshot_job-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  傳回產生已篩選資料快照集之代理程式作業的資訊。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，預設值是 **%** ，它會傳回符合所有發行集之指定 *dynamic_snapshot_jobid*和 *dynamic_snapshot_jobname*的所有已篩選資料快照集作業的相關資訊。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'` 這是已篩選資料快照集作業的名稱。 *dynamic_snapshot_jobname*是 **sysname**，預設值是 **%** '，它會傳回具有指定 *dynamic_snapshot_jobid*之發行集的所有動態作業。 如果在建立作業時，沒有明確指定作業名稱，則作業名稱格式如下：  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'` 這是已篩選資料快照集作業的識別碼。 *dynamic_snapshot_jobid*是 **uniqueidentifier**，預設值是 Null，會傳回符合指定之 *dynamic_snapshot_jobname*的所有快照集作業。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別已篩選資料快照集作業。|  
|**job_name**|**sysname**|已篩選資料快照集作業的名稱。|  
|**job_id**|**uniqueidentifier**|識別散發者端的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業。|  
|**dynamic_filter_login**|**sysname**|值，用於評估為發行集所定義之參數化資料列篩選器中的 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 函數。|  
|**dynamic_filter_hostname**|**sysname**|值，用於評估為發行集所定義之參數化資料列篩選器中的 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 函數。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|如果使用參數化資料列篩選器的話，便是要讀取之快照集檔案的資料夾路徑。|  
|**frequency_type**|**int**|這是排程執行代理程式的頻率，它可以是下列值之一。<br /><br /> **1** = 一次<br /><br /> **2** = 隨選<br /><br /> **4** = 每日<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月相對<br /><br /> **64** = 自動啟動<br /><br /> **128** = 週期性|  
|**frequency_interval**|**int**|代理程式執行的天數，它可以是下列值之一。<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 天<br /><br /> **9** = 工作日<br /><br /> **10** = 週末日|  
|**frequency_subday_type**|**int**|這種類型會定義 *frequency_type* 為 **4** (每日) 時，代理程式的執行頻率，而且可以是下列值之一。<br /><br /> **1** = 指定時間<br /><br /> **2** = 秒<br /><br /> **4** = 分鐘<br /><br /> **8** = 小時|  
|**frequency_subday_interval**|**int**|代理程式排程執行之間發生的 *frequency_subday_type* 間隔數目。|  
|**frequency_relative_interval**|**int**|當 *frequency_type* 為 **32** (每月相對) ，且可以是下列其中一個值時，代理程式會在指定的月份內執行。<br /><br /> **1** = First<br /><br /> **2** = 秒<br /><br /> **4** = 第三<br /><br /> **8** = 第四個<br /><br /> **16** = Last|  
|**frequency_recurrence_factor**|**int**|排程執行代理程式的間隔週數或月數。|  
|**active_start_date**|**int**|這是第一次排程執行代理程式的日期，格式為 YYYYMMDD。|  
|**active_end_date**|**int**|這是最後一次排程執行代理程式的日期，格式為 YYYYMMDD。|  
|**active_start_time**|**int**|這是第一次排程執行代理程式的時間，格式為 HHMMSS。|  
|**active_end_time**|**int**|這是最後一次排程執行代理程式的時間，格式為 HHMMSS。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helpdynamicsnapshot_job** 用於合併式複寫中。  
  
 如果所有的預設參數值都要使用，則會傳回整個發行集資料庫所有分割資料快照集作業的資訊。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員、 **db_owner** 固定資料庫角色，以及發行集的發行集存取清單才能執行 **sp_helpdynamicsnapshot_job**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
