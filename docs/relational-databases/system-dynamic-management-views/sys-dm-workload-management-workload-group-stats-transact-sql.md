---
description: 'sys. dm_workload_management_workload_groups_stats (Transact-sql) '
title: sys. dm_workload_management_workload_groups_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/02/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: a439ebecacd29c2ca412e5ba90fac6b6b5af2b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498306"
---
# <a name="sysdm_workload_management_workload_groups_stats-transact-sql"></a>sys. dm_workload_management_workload_groups_stats (Transact-sql) 
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

傳回工作負載群組統計資料和工作負載群組在中的有效值 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|group_id|**int**|工作負載群組的唯一識別碼。||
|NAME|**sysname**|工作負載群組的名稱。||
|statistics_start_time|**datetime**|針對工作負載群組開始統計資料收集的時間。  此值為建立工作負載群組的時間，或是實例暫停或調整時。||
|total_request_count|**bigint**|已在工作負載群組中完成之要求的累計計數。||
|total_shared_resource_reqeusts|**bigint**|使用共用集區資源的工作負載群組中已完成要求的累計計數。||
|total_queued_request_count|**bigint**|達到 max_concurrency 限制之後，佇列的累計要求計數。||
|total_request_execution_timeouts|**bigint**|在工作負載群組中，根據 query_execution_timeout_sec 設定在完成前完成的要求累計計數。||
|effective_min_percentage_resource|**tinyint**|有效的 min_percentage_resource 設定，可考慮服務層級和工作負載群組設定。 有效的 min_percentage_resource 可以在較低的服務層級上調整。  例如，在 DW100c 上，允許的最低 min_percentage_resource 為25%。  如果無法在服務層級授與值，min_percentage_resource 會調整為0%。  例如 min_percentage_resource，在 DW6000c 設定為10% 時，在相應縮小為 DW100c 時，會有0% 的 effective_min_percentage_resource。||
|effective_cap_percentage_resource|**tinyint**|工作負載群組的有效 cap_percentage_resource。  如果有其他工作負載群組的 min_percentage_resource > 0，則會按比例減少 effective_cap_percentage_resource。||
|effective_request_min_resource_grant_percent|**decimal (5，2) **|工作負載群組 request_min_resource_grant_percent 的有效運行時間值。 考慮服務層級的有效值，以及工作負載群組的設定方式。  如果因為服務層級而調整 min_percentage_resource，effective_request_min_resource_grant_percent 會據以調整。||
|effective_request_max_resource_grant_percent|**decimal (5，2) **|工作負載群組 request_max_resource_grant_percent 的有效運行時間值（考慮所有工作負載群組的設定）。||
|||||

## <a name="see-also"></a>另請參閱

 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
