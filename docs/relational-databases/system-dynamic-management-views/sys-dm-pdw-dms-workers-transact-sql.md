---
title: sys.dm_pdw_dms_workers (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7ee1f12501779910fe8a6c8c44da9d131bff967e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>sys.dm_pdw_dms_workers (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留所有背景工作完成 DMS 步驟的相關資訊。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|這個 DMS 工作者是一部分的查詢。<br /><br /> request_id、 step_index 和 dms_step_index 形成這個檢視的索引鍵。|請參閱中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|查詢此 DMS 工作者是一部分的步驟。<br /><br /> request_id、 step_index 和 dms_step_index 形成這個檢視的索引鍵。|請參閱在 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|dms_step_index|**int**|這個工作者執行的 DMS 計劃中的步驟。<br /><br /> request_id、 step_index 和 dms_step_index 形成這個檢視的索引鍵。||  
|pdw_node_id|**int**|背景工作執行的節點。|請參閱中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|distribution_id|**整數**|如果有任何背景工作執行所在的發佈。|請參閱在 distribution_id [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)。|  
|型別|**nvarchar(32)**|DMS 背景工作執行緒，這個項目所代表的類型。|'DIRECT_CONVERTER'、 'DIRECT_READER'、 'FILE_READER'、 'HASH_CONVERTER'、 'HASH_READER'、 'ROUNDROBIN_CONVERTER'、 'EXPORT_READER'、 'EXTERNAL_READER'、 'EXTERNAL_WRITER'、 'PARALLEL_COPY_READER'、 'REJECT_WRITER'、 '寫入器|  
|status|**nvarchar(32)**|DMS 背景工作的狀態。|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|在上一秒讀取或寫入輸送量。|大於或等於 0。 如果查詢已經取消或失敗之前可以執行背景工作，則為 NULL。|  
|bytes_processed|**bigint**|這個工作者所處理的位元組總數。|大於或等於 0。 如果查詢已經取消或失敗之前可以執行背景工作，則為 NULL。|  
|rows_processed|**bigint**|讀取或寫入此背景工作的資料列數目。|大於或等於 0。 如果查詢已經取消或失敗之前可以執行背景工作，則為 NULL。|  
|start_time|**datetime**|此工作者執行的開始時間。|大於或等於此背景工作所屬的查詢步驟的開始時間。 請參閱[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|在執行結束、 失敗或已取消的時間。|進行中或已佇列的背景工作為 NULL。 否則，大於 start_time。|  
|total_elapsed_time|**int**|花在執行中，以毫秒為單位的時間總計。|大於或等於 0。<br /><br /> 系統啟動或重新啟動後，就會經過的總時間。 如果 total_elapsed_time 超過整數 （以毫秒為單位的 24.8 天） 的最大值，它會導致具體化失敗，因為發生溢位。<br /><br /> 以毫秒為單位的最大值就相當於 24.8 天。|  
|cpu_time|**bigint**|這個背景工作，以毫秒為單位所耗用的 CPU 時間。|大於或等於 0。|  
|query_time|**int**|SQL 之前的時間週期開始傳回資料列至執行緒，以毫秒為單位。|大於或等於 0。|  
|buffers_available|**int**|未使用的緩衝區數目。| 如果查詢已經取消或失敗之前可以執行背景工作，則為 NULL。|  
|sql_spid|**int**|此 DMS 背景工作執行工作的 SQL Server 執行個體上的工作階段識別碼。||  
|dms_cpid|**int**|實際執行的執行緒處理序識別碼。||  
|error_id|**nvarchar(36)**|如果有的話，這個背景工作執行期間發生之錯誤的唯一識別碼。|請參閱在 error_id [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|source_info|**nvarchar(4000)**|讀取器、 來源資料表和資料行規格中。||  
|destination_info|**nvarchar(4000)**|寫入器，目的地資料表的規格。||  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱[系統檢視的最大值](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
