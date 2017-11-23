---
title: "sys.dm_resource_governor_workload_groups (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/30/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups
- sys.dm_resource_governor_workload_groups_TSQL
- dm_resource_governor_workload_groups
- dm_resource_governor_workload_groups_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_resource_governor_workload_groups dynamic management view
ms.assetid: f63c4914-1272-43ef-b135-fe1aabd953e0
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc999091f302ee61c12e6eeb7bd2aa6b3bac58d0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmresourcegovernorworkloadgroups-transact-sql"></a>sys.dm_resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  傳回工作負載群組統計資料以及工作負載群組的目前記憶體中組態。 這個檢視可以使用 sys.dm_resource_governor_resource_pools 加入，以取得資源集區名稱。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_resource_governor_workload_groups**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|group_id|**int**|工作負載群組的識別碼。 不可為 Null。|  
|name|**sysname**|工作負載群組的名稱。 不可為 Null。|  
|pool_id|**int**|資源集區的識別碼。 不可為 Null。|  
|external_pool_id|**int**|**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 外部資源集區的識別碼。 不可為 Null。|  
|statistics_start_time|**datetime**|針對工作負載群組重設之統計資料集合的時間。 不可為 Null。|  
|total_request_count|**bigint**|已在工作負載群組中完成之要求的累計計數。 不可為 Null。|  
|total_queued_request_count|**bigint**|到達 GROUP_MAX_REQUESTS 限制後所佇列之要求的累計計數。 不可為 Null。|  
|active_request_count|**int**|目前的要求計數。 不可為 Null。|  
|queued_request_count|**int**|目前佇列的要求計數。 不可為 Null。|  
|total_cpu_limit_violation_count|**bigint**|超過 CPU 限制之要求的累計計數。 不可為 Null。|  
|total_cpu_usage_ms|**bigint**|此工作負載群組的累計 CPU 使用量 (以毫秒為單位)。 不可為 Null。|  
|max_request_cpu_time_ms|**bigint**|單一要求的最大 CPU 使用量 (以毫秒為單位)。 不可為 Null。<br /><br /> **注意：**這是一個測量的值，不像 request_max_cpu_time_sec，後者是可設定的值。 如需詳細資訊，請參閱[CPU Threshold Exceeded Event Class<](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)。|  
|blocked_task_count|**int**|封鎖之工作的目前計數。 不可為 Null。|  
|total_lock_wait_count|**bigint**|發生之鎖定等候的累計計數。 不可為 Null。|  
|total_lock_wait_time_ms|**bigint**|保留鎖定之經過時間的累計總和 (以毫秒為單位)。 不可為 Null。|  
|total_query_optimization_count|**bigint**|查詢最佳化在此工作負載群組中的累計計數。 不可為 Null。|  
|total_suboptimal_plan_generation_count|**bigint**|由於記憶體不足的壓力，在此工作負載群組中產生之次佳計畫的累計計數。 不可為 Null。|  
|total_reduced_memgrant_count|**bigint**|到達最大查詢大小限制之記憶體授與的累計計數。 不可為 Null。|  
|max_request_grant_memory_kb|**bigint**|自重設統計資料以來，單一要求的最大記憶體授與大小 (以 KB 為單位)。 不可為 Null。|  
|active_parallel_thread_count|**bigint**|平行執行緒使用量的目前計數。 不可為 Null。|  
|importance|**sysname**|要求在此工作負載群組中之相對重要性的目前組態值。 重要性為下列其中之一，「 中 」 的預設值： 低、 中或高。<br /><br /> 不可為 Null。|  
|request_max_memory_grant_percent|**int**|單一要求之最大記憶體授與的目前設定 (以百分比為單位)。 不可為 Null。|  
|request_max_cpu_time_sec|**int**|單一要求之最大 CPU 使用限制的目前設定 (以秒為單位)。 不可為 Null。|  
|request_memory_grant_timeout_sec|**int**|單一要求記憶體授與逾時的目前設定 (以秒為單位)。 不可為 Null。|  
|group_max_requests|**int**|並行要求之最大數目的目前設定。 不可為 Null。|  
|max_dop|**int**|工作負載群組之平行處理原則的最大程度。 預設值為 0 時，使用全域設定。 不可為 Null。|  
|pdw_node_id|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="remarks"></a>備註  
 這個動態管理檢視會顯示記憶體中組態。 若要查看儲存的組態中繼資料，請使用 sys.resource_governor_workload_groups 目錄檢視。  
  
 當 ALTER RESOURCE GOVERNOR RESET STATISTICS 成功執行時，下列計數器會重設： statistics_start_time，total_request_count，total_queued_request_count，total_cpu_limit_violation_count，total_cpu_usage_ms max_request_cpu_time_ms、 total_lock_wait_count，total_lock_wait_time_ms，total_query_optimization_count，total_suboptimal_plan_generation_count，total_reduced_memgrant_count 和 max_request_grant_memory_kb。 statistics_start_time 會設為目前的系統日期和時間，其他的計數器則設定為零 (0)。  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>請參閱＜  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_resource_pools &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [sys.resource_governor_workload_groups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  



