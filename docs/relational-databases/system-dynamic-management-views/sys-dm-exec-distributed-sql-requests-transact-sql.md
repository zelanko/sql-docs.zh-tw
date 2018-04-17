---
title: sys.dm_exec_distributed_sql_requests (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_distributed_requests management view
- dm_exec_distributed_requests management view
ms.assetid: d065dc01-35d4-472f-9554-53ac41e7d104
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 860418a7184fd22e4f8828fc4a5572786ef81502
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecdistributedsqlrequests-transact-sql"></a>sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  查詢中保存 SQL 步驟的 SQL 查詢的所有分佈的相關資訊。  此檢視會顯示要求的最近 1000 則; 的資料使用中要求一定會出現在此檢視中的資料。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|execution_id 和 step_index 便會產生這份檢視的索引鍵。 與要求相關聯的唯一數值識別碼。|請參閱中的識別碼[sys.dm_exec_requests &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|此分佈是一部分的查詢步驟索引。|請參閱在 step_index [sys.dm_exec_distributed_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)。|  
|compute_node_id|**int**|此步驟中所代表的作業類型。|請參閱在 compute_node_id [sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|distribution_id|**int**|執行步驟的地方。|設定為-1 可執行在節點範圍散發範圍的要求。|  
|status|**nvarchar(32)**|此步驟的狀態|作用中、 已取消、 已完成、 失敗、 排入佇列|  
|error_id|**nvarchar(36)**|如果有的話，這個步驟中，與相關的錯誤的唯一識別碼|請參閱識別碼[sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)，如果沒有發生錯誤則為 NULL。|  
|start_time|**datetime**|在步驟開始執行的時間|較小或等於目前的時間，大於或等於 end_compile_time 這個步驟所屬的查詢。|  
|end_time|**datetime**|在此步驟中完成執行、 已取消，或失敗的時間。|較小或等於目前的時間，大於或等於 start_time，針對目前在執行中的步驟設定為 NULL，或是排入佇列。|  
|total_elapsed_time|**int**|已執行的查詢步驟，以毫秒為單位的時間總數量|介於 0 到 end_time 和 start_time 之間的差異。 0 代表佇列的步驟。|  
|row_count|**bigint**|變更或這項要求所傳回的資料列的總數|0，表示沒有變更或傳回資料，否則受影響的資料列數目的步驟。 設定為-1 代表 DMS 步驟。|  
|spid|**int**|執行查詢發佈在 SQL Server 執行個體上的工作階段識別碼||  
|command|nvarchar(4000)|保存這個步驟的命令的完整文字。|步驟的任何有效的要求字串。 如果超過 4000 個字元，截斷。|  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase，疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
