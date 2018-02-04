---
title: sys.dm_exec_distributed_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 348b78de034f252f5ea9561df53dc69c267d8257
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保留構成指定的 PolyBase 要求或查詢的所有步驟的相關資訊。 它會列出一個資料列，每個查詢步驟。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id 和 step_index 便會產生這份檢視的索引鍵。 與要求相關聯的唯一數值識別碼。|請參閱中的識別碼[sys.dm_exec_requests &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|這個步驟中的要求所組成的步驟順序的位置。|0 到 (n-1) 代表 n 的要求。|  
|operation_type|**nvarchar(128)**|此步驟中所代表的作業類型。|'MoveOperation','OnOperation','RandomIDOperation','RemoteOperation','ReturnOperation','ShuffleMoveOperation','TempTablePropertiesOperation','DropDiagnosticsNotifyOperation', ‘HadoopShuffleOperation', ‘HadoopBroadCastOperation', ‘HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|執行步驟的地方。|‘AllComputeNodes','AllDistributions','ComputeNode','Distribution','AllNodes','SubsetNodes','SubsetDistributions','Unspecified'.|  
|location_type|**nvarchar(32)**|執行步驟的地方。|'Compute'、 'Head' 或者 'DMS'。 所有的資料移動步驟顯示 'DMS'。|  
|status|**nvarchar(32)**|此步驟的狀態|' 取消暫停的'，'執行'，'完整'、 'Failed'、 'UndoFailed'、 'PendingCancel'，''，'復原'、 '中止'|  
|error_id|**nvarchar(36)**|如果有的話，這個步驟中，與相關的錯誤的唯一識別碼|請參閱識別碼[sys.dm_exec_compute_node_errors &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)，如果沒有發生錯誤則為 NULL。|  
|start_time|**datetime**|在步驟開始執行的時間|較小或等於目前的時間，大於或等於 end_compile_time 這個步驟所屬的查詢。|  
|end_time|**datetime**|在此步驟中完成執行、 已取消，或失敗的時間。|較小或等於目前的時間，大於或等於 start_time，針對目前在執行中的步驟設定為 NULL，或是排入佇列。|  
|total_elapsed_time|**int**|已執行的查詢步驟，以毫秒為單位的時間總數量|介於 0 到 end_time 和 start_time 之間的差異。 0 代表佇列的步驟。|  
|row_count|**bigint**|變更或這項要求所傳回的資料列的總數|0，表示沒有變更或傳回資料，否則受影響的資料列數目的步驟。 設定為-1 代表 DMS 步驟。|  
|command|nvarchar(4000)|保存這個步驟的命令的完整文字。|步驟的任何有效的要求字串。 如果超過 4000 個字元，截斷。|  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase，疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
