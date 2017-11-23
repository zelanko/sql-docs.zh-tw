---
title: "sp_helpdynamicsnapshot_job (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords: sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f9accc8ae7ffb64d82fa10c3b60a2f8fec44b8a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回產生已篩選資料快照集之代理程式作業的資訊。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication =** ] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，預設值是 **%** ，傳回所有符合指定的已篩選的資料快照集作業的資訊*dynamic_snapshot_jobid*和*dynamic_snapshot_jobname*針對所有發行集。  
  
 [  **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 這是篩選資料快照集作業的名稱。 *dynamic_snapshot_jobname*是**sysname**，預設值是 **%** '，它會傳回使用指定的發行集的所有動態作業*dynamic_snapshot_jobid*。 如果在建立作業時，沒有明確指定作業名稱，則作業名稱格式如下：  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
 [  **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 這是已篩選資料快照集作業的識別碼。 *dynamic_snapshot_jobid*是**uniqueidentifier**，預設值是 NULL，它會傳回所有符合指定的快照集作業*dynamic_snapshot_jobname*。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別已篩選資料快照集作業。|  
|**job_name**|**sysname**|已篩選資料快照集作業的名稱。|  
|**job_id**|**uniqueidentifier**|識別[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在散發者代理程式作業。|  
|**dynamic_filter_login**|**sysname**|值用來評估[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)針對發行集定義參數化資料列篩選器中的函式。|  
|**dynamic_filter_hostname**|**sysname**|值用來評估[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)針對發行集定義參數化資料列篩選器中的函式。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|如果使用參數化資料列篩選器的話，便是要讀取之快照集檔案的資料夾路徑。|  
|**frequency_type**|**int**|這是排程執行代理程式的頻率，它可以是下列值之一。<br /><br /> **1** = 一次<br /><br /> **2** = 視需要<br /><br /> **4** = 每天<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月相對<br /><br /> **64** = 自動啟動<br /><br /> **128** = 重複執行|  
|**frequency_interval**|**int**|代理程式執行的天數，它可以是下列值之一。<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 日<br /><br /> **9** = 工作日<br /><br /> **10** = 週末|  
|**frequency_subday_type**|**int**|會定義代理程式執行的頻率時的型別*frequency_type*是**4** （每天），而且可以是下列值之一。<br /><br /> **1** = 在指定的時間<br /><br /> **2** = 秒數<br /><br /> **4** = 分鐘<br /><br /> **8** = 小時|  
|**frequency_subday_interval**|**int**|間隔的數*frequency_subday_type*所發生的代理程式排程執行之間。|  
|**frequency_relative_interval**|**int**|是一週中，給定月份的代理程式執行時*frequency_type*是**32** （每月相對），而且可以是下列值之一。<br /><br /> **1** = 第一個<br /><br /> **2** = 第二個<br /><br /> **4** = 第三個<br /><br /> **8** = 第四個<br /><br /> **16** = 最後一個|  
|**frequency_recurrence_factor**|**int**|排程執行代理程式的間隔週數或月數。|  
|**active_start_date**|**int**|這是第一次排程執行代理程式的日期，格式為 YYYYMMDD。|  
|**active_end_date**|**int**|這是最後一次排程執行代理程式的日期，格式為 YYYYMMDD。|  
|**active_start_time**|**int**|這是第一次排程執行代理程式的時間，格式為 HHMMSS。|  
|**active_end_time**|**int**|這是最後一次排程執行代理程式的時間，格式為 HHMMSS。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpdynamicsnapshot_job**用於合併式複寫中。  
  
 如果所有的預設參數值都要使用，則會傳回整個發行集資料庫所有分割資料快照集作業的資訊。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色、 **db_owner**固定資料庫角色，且發行集存取清單的發行集可以執行**sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>請參閱＜  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
