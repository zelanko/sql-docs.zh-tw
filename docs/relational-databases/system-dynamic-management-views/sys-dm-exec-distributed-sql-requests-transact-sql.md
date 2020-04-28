---
title: sys.databases dm_exec_distributed_sql_requests （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a63d8a331163283598dd50a418f0dd32f9ac5edd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097793"
---
# <a name="sysdm_exec_distributed_sql_requests-transact-sql"></a>sys.databases dm_exec_distributed_sql_requests （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存所有 SQL 查詢散發套件的相關資訊，做為查詢中 SQL 步驟的一部分。  此視圖會顯示最後一個1000要求的資料;使用中要求的資料一律會出現在此視圖中。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|execution_id 和 step_index 組成此視圖的索引鍵。 與要求相關聯的唯一數值識別碼。|請參閱[dm_exec_requests &#40;transact-sql](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)中的識別碼&#41;|  
|step_index|**int**|此散發所屬之查詢步驟的索引。|請參閱[dm_exec_distributed_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)中的 step_index。|  
|compute_node_id|**int**|此步驟所表示的作業類型。|請參閱[dm_exec_compute_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)中的 compute_node_id。|  
|distribution_id|**int**|步驟執行所在的位置。|針對在節點範圍（而非散發範圍）執行的要求，設定為-1。|  
|status|**nvarchar(32)**|此步驟的狀態|作用中、已取消、已完成、失敗、已排入佇列|  
|error_id|**Nvarchar （36）**|與此步驟相關聯之錯誤的唯一識別碼（如果有的話）|請參閱[dm_exec_compute_node_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)的識別碼，如果未發生錯誤，則為 Null。|  
|start_time|**datetime**|步驟開始執行的時間|小於或等於目前的時間，或是大於或等於此步驟所屬查詢的 end_compile_time。|  
|end_time|**datetime**|此步驟完成執行、已取消或失敗的時間。|小於或等於目前時間且大於或等於 start_time，針對目前執行中或已排入佇列的步驟將設定為 Null。|  
|total_elapsed_time|**int**|查詢步驟已執行的總時間量（以毫秒為單位）|介於0和 end_time 與 start_time 之間的差異。 0表示已排入佇列的步驟。|  
|row_count|**bigint**|此要求變更或傳回的總數據列數|0適用于未變更或傳回資料的步驟，否則為受影響的資料列數目。 針對 DMS 步驟，設定為-1。|  
|spid|**int**|執行查詢散發之 SQL Server 實例上的會話識別碼||  
|命令|nvarchar(4000)|保存此步驟之命令的完整文字。|步驟的任何有效要求字串。 如果超過4000個字元，則會截斷。|  
  
## <a name="see-also"></a>另請參閱  
 [使用動態管理檢視進行 PolyBase 疑難排解](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
