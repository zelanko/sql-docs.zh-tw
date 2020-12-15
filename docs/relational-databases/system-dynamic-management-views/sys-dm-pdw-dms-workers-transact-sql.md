---
description: 'sys.dm_pdw_dms_workers (Transact-sql) '
title: sys.dm_pdw_dms_workers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 2c81bb5c02b11753fa98024cfd4d3861b2768d24
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482589"
---
# <a name="sysdm_pdw_dms_workers-transact-sql"></a>sys.dm_pdw_dms_workers (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存所有工作者完成 DMS 步驟的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|查詢此 DMS 背景工作角色所屬的。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。|請參閱 [sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id。|  
|step_index|**int**|此 DMS 背景工作角色所屬的查詢步驟。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。|請參閱 [sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)中的 step_index。|  
|dms_step_index|**int**|此背景工作正在執行之 DMS 計畫中的步驟。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。||  
|pdw_node_id|**int**|正在執行背景工作的節點。|請參閱 [sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 node_id。|  
|distribution_id|**整數**|背景工作執行所在的散發（如果有的話）。|請參閱 [sys.pdw_distributions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)中的 distribution_id。|  
|類型|**nvarchar(32)**|此專案代表的 DMS 工作者執行緒類型。|「DIRECT_CONVERTER」、「DIRECT_READER」、「FILE_READER」、「HASH_CONVERTER」、「HASH_READER」、「ROUNDROBIN_CONVERTER」、「EXPORT_READER」、「EXTERNAL_READER」、「EXTERNAL_WRITER」、「PARALLEL_COPY_READER」、「REJECT_WRITER」、「寫入器」|  
|status|**nvarchar(32)**|DMS 背景工作角色的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|最後一秒的讀取或寫入輸送量。|大於或等於0。 如果查詢在背景工作角色可以執行之前取消或失敗，則為 Null。|  
|bytes_processed|**bigint**|此背景工作所處理的總位元組數。|大於或等於0。 如果查詢在背景工作角色可以執行之前取消或失敗，則為 Null。|  
|rows_processed|**bigint**|此背景工作所讀取或寫入的資料列數目。|大於或等於0。 如果查詢在背景工作角色可以執行之前取消或失敗，則為 Null。|  
|start_time|**datetime**|此背景工作開始執行的時間。|大於或等於此背景工作所屬查詢步驟的開始時間。 請參閱 [sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|執行結束、失敗或已取消的時間。|針對進行中或佇列的背景工作角色為 Null。 否則，大於 start_time。|  
|total_elapsed_time|**int**|花費在執行的總時間（以毫秒為單位）。|大於或等於0。<br /><br /> 自系統啟動或重新開機以來經過的總時間。 如果 total_elapsed_time 超過整數 (24.8 天（以毫秒為單位）的最大值) ，則會造成具體化失敗，因為溢位。<br /><br /> 以毫秒為單位的最大值相當於24.8 天。|  
|cpu_time|**bigint**|此背景工作所耗用的 CPU 時間（以毫秒為單位）。|大於或等於0。|  
|query_time|**int**|SQL 開始將資料列傳回執行緒之前的時間長度（以毫秒為單位）。|大於或等於0。|  
|buffers_available|**int**|未使用的緩衝區數目。| 如果查詢在背景工作角色可以執行之前取消或失敗，則為 Null。|  
|sql_spid|**int**|SQL Server 實例上執行此 DMS 工作者工作的會話識別碼。||  
|dms_cpid|**int**|實際執行之執行緒的處理序識別碼。||  
|error_id|**Nvarchar (36)**|在此背景工作執行期間發生之錯誤的唯一識別碼（如果有的話）。|請參閱 [sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)中的 error_id。|  
|source_info|**nvarchar(4000)**|針對讀取器，指定來源資料表和資料行的規格。||  
|destination_info|**nvarchar(4000)**|若為寫入器，則為目的地資料表的規格。||  
  
 如需此視圖所保留之最大資料列的相關資訊，請參閱「 [容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」主題中的「中繼資料」一節。  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
