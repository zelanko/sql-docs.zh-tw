---
title: sys.dm_exec_distributed_request_steps (TRANSACT-SQL) |Microsoft Docs
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
- SYS.DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_distributed_request_steps
- sys.dm_exec_distributed_request_steps management view
ms.assetid: 1954541d-b716-4e03-8fcc-7022f428e01d
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f226ff8c5f18a0e812c6a457fe3382cb8f7b8d84
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982590"
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保留構成指定的 PolyBase 要求或查詢的所有步驟的相關資訊。 它會列出每個查詢步驟的一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id 和 step_index 組成此檢視的索引鍵。 與要求相關聯的唯一數值識別碼。|請參閱中的識別碼[sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|step_index|**int**|此步驟中的要求，以進行的步驟順序的位置。|0 到 (n-1) 代表 n 的要求。|  
|operation_type|**nvarchar(128)**|此步驟中所代表的作業類型。|'MoveOperation','OnOperation','RandomIDOperation','RemoteOperation','ReturnOperation','ShuffleMoveOperation','TempTablePropertiesOperation','DropDiagnosticsNotifyOperation', ‘HadoopShuffleOperation', ‘HadoopBroadCastOperation', ‘HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|執行步驟的地方。|' AllComputeNodes '、' AllDistributions'、 'ComputeNode'、 'Distribution'、 'AllNodes'、 'SubsetNodes'、 'SubsetDistributions'，' 未指定 '。|  
|location_type|**nvarchar(32)**|執行步驟的地方。|'Compute'、 'Head' 或者 'DMS'。 所有的資料移動步驟示範 'DMS'。|  
|status|**nvarchar(32)**|此步驟的狀態|'暫止'、 'Running'，'Complete'、 'Failed'、 'UndoFailed'、 'PendingCancel'，' 已取消 '，'復原'、 '中止'|  
|error_id|**nvarchar(36)**|如果有的話，此步驟中，與相關的錯誤的唯一識別碼|請參閱識別碼[sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)，如果未不發生任何錯誤則為 NULL。|  
|start_time|**datetime**|步驟開始執行時間|較小或等於目前的時間和大於或等於 end_compile_time 屬於此步驟中的查詢。|  
|end_time|**datetime**|在此步驟中完成執行、 已取消，或失敗的時間。|較小或等於目前的時間和大於或等於 start_time，目前在執行中的步驟設定為 NULL 或已排入佇列。|  
|total_elapsed_time|**int**|已執行的查詢步驟，以毫秒為單位的時間總數量|介於 0 到 end_time 和 start_time 之間的差異。 0 代表已排入佇列的步驟。|  
|row_count|**bigint**|變更或這項要求所傳回的資料列的總數|0 表示未變更或傳回的資料，否則會受到影響的資料列數目的步驟。 設定為 DMS 步驟的-1。|  
|command|nvarchar(4000)|保留此步驟的命令的完整文字。|步驟的任何有效的要求字串。 如果超過 4000 個字元，就會截斷。|  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase 疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
