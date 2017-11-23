---
title: "sys.dm_exec_dms_workers (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
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
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs: TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b5677eb04a9a5809c2caf25d37edd288e4b1efbc
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecdmsworkers-transact-sql"></a>sys.dm_exec_dms_workers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保留所有背景工作完成 DMS 步驟的相關資訊。  
  
 此檢視會顯示最近 1000 則要求和作用中要求的資料使用中要求一定會出現在此檢視中的資料。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar （32)**|查詢此 DMS 工作者是部分 of.request_id，step_index，，和 dms_step_index 形成這個檢視的索引鍵。||  
|step_index|**int**|查詢此 DMS 工作者是一部分的步驟。|請參閱中的步驟索引[sys.dm_exec_distributed_request_steps &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|dms_step_index|**int**|這個工作者執行的 DMS 計劃中的步驟。|請參閱[sys.dm_exec_dms_workers (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|**int**|背景工作執行的節點。|請參閱[sys.dm_exec_compute_nodes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|||  
|型別|**nvarcha(32)**|||  
|status|**nvarchar （32)**|此步驟的狀態|' 取消暫停的'，'執行'，'完整'、 'Failed'、 'UndoFailed'、 'PendingCancel'，''，'復原'、 '中止'|  
|bytes_per_sec|**bigint**|||  
|bytes_processed|**bigint**|||  
|rows_processed|**bigint**|||  
|start_time|**datetime**|在步驟開始執行的時間|較小或等於目前的時間，大於或等於 end_compile_time 這個步驟所屬的查詢。|  
|end_time|**datetime**|在此步驟中完成執行、 已取消，或失敗的時間。|較小或等於目前的時間，大於或等於 start_time，針對目前在執行中的步驟設定為 NULL，或是排入佇列。|  
|total_elapsed_time|**int**|已執行的查詢步驟，以毫秒為單位的時間總數量|介於 0 到 end_time 和 start_time 之間的差異。 0 代表佇列的步驟。|  
|cpu_time|**bigint**|||  
|query_time|**int**|||  
|buffers_available|**int**|||  
|dms_cpid|**int**|||  
|sql_spid|**int**|||  
|error_id|**nvarchar(36)**|||  
|source_info|**nvarchar(4000)**|||  
|destination_info|**nvarchar(4000)**|||  
|command|**nvarchar(4000)**|||  
  
## <a name="see-also"></a>請參閱＜  
 [PolyBase，疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
