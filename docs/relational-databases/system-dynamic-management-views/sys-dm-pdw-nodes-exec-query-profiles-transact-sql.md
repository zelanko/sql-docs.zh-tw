---
title: sys.databases dm_pdw_nodes_exec_query_profiles （Transact-sql） |Microsoft Docs
description: 動態管理檢視，可在執行查詢時用來監視即時資料倉儲查詢進度。
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7237e7f7b49916e09f4a8c5cab0d7d49486cb971
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73145653"
---
# <a name="sysdm_pdw_nodes_exec_query_profiles-transact-sql"></a>sys.databases dm_pdw_nodes_exec_query_profiles （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

監視執行查詢時的即時資料倉儲查詢進度。   
  
## <a name="table-returned"></a>傳回的資料表  
傳回的計數器是以每個執行緒的每個運算子為基礎。 結果是動態的，而且不符合現有選項的結果，例如`SET STATISTICS XML ON` ，當查詢完成時，只會建立輸出。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。|
|session_id|**smallint**|識別此查詢執行所在的工作階段。 參考 dm_exec_sessions.session_id。|  
|request_id|**int**|識別目標要求。 參考 dm_exec_sessions.request_id。|  
|sql_handle|**Varbinary （64）**|這是一個標記，可唯一識別查詢所屬的批次或預存程式。 參考 dm_exec_query_stats.sql_handle。|  
|plan_handle|**Varbinary （64）**|這是一個標記，可唯一識別已執行之批次的查詢執行計畫，且其計畫位於計畫快取中，或目前正在執行。 參考 dm_exec_query_stats. plan_handle。|  
|physical_operator_name|**nvarchar(256)**|實體運算子名稱。|  
|node_id|**int**|識別查詢樹狀結構中的運算子節點。|  
|thread_id|**int**|區分屬於相同查詢運算子節點的執行緒 (針對平行查詢)。|  
|task_address|**varbinary(8)**|識別此執行緒使用的 SQLOS 工作。 參考 dm_os_tasks.task_address。|  
|row_count|**Bigint**|目前為止運算子傳回的資料列數目。|  
|rewind_count|**Bigint**|目前為止的倒轉數目。|  
|rebind_count|**Bigint**|目前為止的重新繫結數目。|  
|end_of_scan_count|**Bigint**|目前為止結束的掃描數目。|  
|estimate_row_count|**Bigint**|估計的資料列數目。 將 estimated_row_count 與實際的 row_count 比較可能會很實用。|  
|first_active_time|**Bigint**|初次呼叫運算子的時間 (以毫秒為單位)。|  
|last_active_time|**Bigint**|最後呼叫運算子的時間 (以毫秒為單位)。|  
|open_time|**Bigint**|開啟的時間戳記 (以毫秒為單位)。|  
|first_row_time|**Bigint**|開啟第一個資料列的時間戳記 (以毫秒為單位)。|  
|last_row_time|**Bigint**|開啟最後一個資料列的時間戳記 (以毫秒為單位)。|  
|close_time|**Bigint**|關閉的時間戳記 (以毫秒為單位)。|  
|elapsed_time_ms|**Bigint**|目前為止，目標節點的作業所用的總時間（以毫秒為單位）。|  
|cpu_time_ms|**Bigint**|目前為止目標節點的作業所使用的總 CPU 時間（以毫秒為單位）。|  
|database_id|**smallint**|包含在上面執行讀取和寫入之物件的資料庫識別碼。|  
|object_id|**int**|正在上面執行讀取和寫入之物件的識別碼。 參考 sys.objects.object_id。|  
|index_id|**int**|資料列集開啟所依據的索引 (如果有的話)。|  
|scan_count|**Bigint**|目前為止的資料表/索引掃描數目。|  
|logical_read_count|**Bigint**|目前為止的邏輯讀取數目。|  
|physical_read_count|**Bigint**|目前為止的實體讀取數目。|  
|read_ahead_count|**Bigint**|目前為止的預先讀取數目。|  
|write_page_count|**Bigint**|目前為止因為溢出的頁面寫入數目。|  
|lob_logical_read_count|**Bigint**|目前為止的 LOB 邏輯讀取數目。|  
|lob_physical_read_count|**Bigint**|目前為止的 LOB 實體讀取數目。|  
|lob_read_ahead_count|**Bigint**|目前為止的 LOB 預先讀取數目。|  
|segment_read_count|**int**|目前為止的區段預先讀取數目。|  
|segment_skip_count|**int**|目前為止略過的區段數目。| 
|actual_read_row_count|**Bigint**|套用剩餘述詞之前，由運算子讀取的資料列數目。| 
|estimated_read_row_count|**Bigint**|**適用物件：** 從[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 開始。 <br/>在套用剩餘述詞之前，由運算子讀取的估計資料列數目。|  
  
## <a name="remarks"></a>備註  
[Dm_exec_query_profiles](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql?view=sql-server-ver15)適用相同的備註。  

## <a name="permissions"></a>權限  
 需要伺服器的 `VIEW SERVER STATE` 權限。  

## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
   

 ## <a name="next-steps"></a>後續步驟
 如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop)。
