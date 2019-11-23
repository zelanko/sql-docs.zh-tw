---
title: sys.databases dm_exec_external_work （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5afdfd4f9a5f66845ae6d3798910fc2c4bf5ab8a
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532946"
---
# <a name="sysdm_exec_external_work-transact-sql"></a>sys.databases dm_exec_external_work （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  傳回每個計算節點上每個背景工作負載的相關資訊。  
  
 查詢 dm_exec_external_work sys.databases，以識別要與外部資料源（例如 Hadoop 或外部 SQL Server）進行通訊的工作。  
  
|Column Name|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|相關聯的 PolyBase 查詢的唯一識別碼。|請參閱 sys.databases 中的*request_ID* [dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|step_index|`int`|此工作者正在執行的要求。|請參閱 sys.databases 中的*step_index* [dm_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|dms_step_index|`int`|此工作者正在執行之 DMS 計畫中的步驟。|請參閱[sys.databases dm_exec_dms_workers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)。|  
|compute_node_id|`int`|正在執行背景工作的節點。|請參閱[sys.databases dm_exec_compute_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|類型|`nvarchar(60)`|外部工作的類型。|「檔案分割」|  
|work_id|`int`|實際分割的識別碼。|大於或等於0。|  
|input_name|`nvarchar(4000)`|要讀取的輸入名稱|使用 Hadoop 時的檔案名。|  
|read_location|`bigint`|位移或讀取位置。|要讀取之檔案的位移。|  
|bytes_processed|`bigint`|此背景工作所處理的位元組總數。|大於或等於0。|  
|length|`bigint`|Hadoop 時的分割或 HDFS 區塊長度|使用者可定義。 預設值為 Ed-64m|  
|status|`nvarchar(32)`|背景工作角色的狀態|擱置中、處理中、完成、失敗、已中止|  
|start_time|`datetime`|工作開始||  
|end_time|`datetime`|工作結束||  
|total_elapsed_time|`int`|總時間（以毫秒為單位）||
|compute_pool_id|`int`|集區的唯一識別碼。|

## <a name="see-also"></a>另請參閱  
 [使用動態管理檢視進行 PolyBase 疑難排解](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關的動態管理&#40;Views transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
