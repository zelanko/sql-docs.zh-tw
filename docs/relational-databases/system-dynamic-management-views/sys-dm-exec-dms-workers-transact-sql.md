---
title: sys.databases dm_exec_dms_workers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4951954bb9f6336c2c984a8d74c2224eab4dfbb0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821087"
---
# <a name="sysdm_exec_dms_workers-transact-sql"></a>sys.databases dm_exec_dms_workers （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存所有工作人員完成 DMS 步驟的相關資訊。  
  
 此視圖會顯示最後一個1000要求和作用中要求的資料;使用中要求的資料一律會出現在此視圖中。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|查詢此 DMS 背景工作角色所屬的部分。 request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。||  
|step_index|`int`|此 DMS 背景工作角色所屬的查詢步驟。|請參閱[dm_exec_distributed_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)中的步驟索引。|  
|dms_step_index|`int`|此背景工作正在執行之 DMS 計畫中的步驟。|請參閱[sys.databases dm_exec_dms_workers （transact-sql）](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|`int`|正在執行背景工作的節點。|請參閱[dm_exec_compute_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|distribution_id|`int`|||  
|類型|`nvarcha(32)`|||  
|status|`nvarchar(32)`|此步驟的狀態|「擱置」、「執行中」、「完成」、「失敗」、「UndoFailed」、「PendingCancel」、「已取消」、「已復原」、「已中止」|  
|bytes_per_sec|`bigint`|||  
|bytes_processed|`bigint`|||  
|rows_processed|`bigint`|||  
|start_time|`datetime`|步驟開始執行的時間|小於或等於目前的時間，或是大於或等於此步驟所屬查詢的 end_compile_time。|  
|end_time|`datetime`|此步驟完成執行、已取消或失敗的時間。|小於或等於目前時間且大於或等於 start_time，針對目前執行中或已排入佇列的步驟將設定為 Null。|  
|total_elapsed_time|`int`|查詢步驟已執行的總時間量（以毫秒為單位）|介於0和 end_time 與 start_time 之間的差異。 0表示已排入佇列的步驟。|  
|cpu_time|`bigint`|||  
|query_time|`int`|||  
|buffers_available|`int`|||  
|dms_cpid|`int`|||  
|sql_spid|`int`|||  
|error_id|`nvarchar(36)`|||  
|source_info|`nvarchar(4000)`|||  
|destination_info|`nvarchar(4000)`|||  
|命令|`nvarchar(4000)`|||
|compute_pool_id|`int`|集區的唯一識別碼。|

## <a name="see-also"></a>另請參閱  
 [使用動態管理檢視進行 PolyBase 疑難排解](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
