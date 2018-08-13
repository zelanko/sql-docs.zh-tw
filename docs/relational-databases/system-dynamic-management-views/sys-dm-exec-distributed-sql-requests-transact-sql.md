---
title: sys.dm_exec_distributed_sql_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: ee6ce9ae453eb58bfa8dde2406c630b966287007
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540578"
---
# <a name="sysdmexecdistributedsqlrequests-transact-sql"></a>sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保留相關資訊的所有 SQL 查詢散發套件 SQL 步驟的一部分在查詢中。  此檢視會顯示的最近 1000 則要求; 的資料使用中要求一律會有此檢視中的資料。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|execution_id 和 step_index 組成此檢視的索引鍵。 與要求相關聯的唯一數值識別碼。|請參閱中的識別碼[sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|此分佈是一部分的查詢步驟的索引。|請參閱中的 step_index [sys.dm_exec_distributed_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)。|  
|compute_node_id|**int**|此步驟中所代表的作業類型。|請參閱中的 compute_node_id [sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|distribution_id|**int**|執行步驟的地方。|設定為-1 的執行在節點範圍內不發佈範圍的要求。|  
|status|**nvarchar(32)**|此步驟的狀態|作用中、 已取消、 已完成、 失敗、 已排入佇列|  
|error_id|**nvarchar(36)**|如果有的話，此步驟中，與相關的錯誤的唯一識別碼|請參閱識別碼[sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)，如果未不發生任何錯誤則為 NULL。|  
|start_time|**datetime**|步驟開始執行時間|較小或等於目前的時間和大於或等於 end_compile_time 屬於此步驟中的查詢。|  
|end_time|**datetime**|在此步驟中完成執行、 已取消，或失敗的時間。|較小或等於目前的時間和大於或等於 start_time，目前在執行中的步驟設定為 NULL 或已排入佇列。|  
|total_elapsed_time|**int**|已執行的查詢步驟，以毫秒為單位的時間總數量|介於 0 到 end_time 和 start_time 之間的差異。 0 代表已排入佇列的步驟。|  
|row_count|**bigint**|變更或這項要求所傳回的資料列的總數|0 表示未變更或傳回的資料，否則會受到影響的資料列數目的步驟。 設定為 DMS 步驟的-1。|  
|spid|**int**|執行查詢發佈在 SQL Server 執行個體上的工作階段識別碼||  
|command|nvarchar(4000)|保留此步驟的命令的完整文字。|步驟的任何有效的要求字串。 如果超過 4000 個字元，就會截斷。|  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase 疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
