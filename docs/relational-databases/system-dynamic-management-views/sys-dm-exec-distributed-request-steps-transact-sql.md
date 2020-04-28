---
title: sys.databases dm_exec_distributed_request_steps （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5c40ce6d1c7b7ef85f24fc8032559e000d89be1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097826"
---
# <a name="sysdm_exec_distributed_request_steps-transact-sql"></a>sys.databases dm_exec_distributed_request_steps （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存組成指定的 PolyBase 要求或查詢之所有步驟的相關資訊。 它會針對每個查詢步驟列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id 和 step_index 組成此視圖的索引鍵。 與要求相關聯的唯一數值識別碼。|請參閱[dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)中的識別碼。|  
|step_index|**int**|此步驟在組成要求的步驟順序中的位置。|0到（n-1），代表具有 n 個步驟的要求。|  
|operation_type|**nvarchar(128)**|此步驟所表示的作業類型。|' MoveOperation '、' OnOperation '、' RandomIDOperation '、' RemoteOperation '、' ReturnOperation '、' ShuffleMoveOperation '、' TempTablePropertiesOperation '、' DropDiagnosticsNotifyOperation '、' HadoopShuffleOperation '、' HadoopBroadCastOperation '、' HadoopRoundRobinOperation '|  
|distribution_type|**nvarchar(32)**|步驟執行所在的位置。|' AllComputeNodes '、' AllDistributions '、' ComputeNode '、' 散發 '、' AllNodes '、' SubsetNodes '、' SubsetDistributions '、' 未指定 '。|  
|location_type|**nvarchar(32)**|步驟執行所在的位置。|「計算」、「標頭」或「DMS」。 所有資料移動步驟都會顯示「DMS」。|  
|status|**nvarchar(32)**|此步驟的狀態|「擱置」、「執行中」、「完成」、「失敗」、「UndoFailed」、「PendingCancel」、「已取消」、「已復原」、「已中止」|  
|error_id|**Nvarchar （36）**|與此步驟相關聯之錯誤的唯一識別碼（如果有的話）|請參閱[dm_exec_compute_node_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)的識別碼，如果未發生錯誤，則為 Null。|  
|start_time|**datetime**|步驟開始執行的時間|小於或等於目前的時間，或是大於或等於此步驟所屬查詢的 end_compile_time。|  
|end_time|**datetime**|此步驟完成執行、已取消或失敗的時間。|小於或等於目前時間且大於或等於 start_time，針對目前執行中或已排入佇列的步驟將設定為 Null。|  
|total_elapsed_time|**int**|查詢步驟已執行的總時間量（以毫秒為單位）|介於0和 end_time 與 start_time 之間的差異。 0表示已排入佇列的步驟。|  
|row_count|**bigint**|此要求變更或傳回的總數據列數|0適用于未變更或傳回資料的步驟，否則為受影響的資料列數目。 針對 DMS 步驟，設定為-1。|  
|命令|nvarchar(4000)|保存此步驟之命令的完整文字。|步驟的任何有效要求字串。 如果超過4000個字元，則會截斷。|  
  
## <a name="see-also"></a>另請參閱  
 [使用動態管理檢視進行 PolyBase 疑難排解](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
