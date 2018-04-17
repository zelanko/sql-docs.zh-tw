---
title: sys.dm_pdw_sql_requests (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b42317f45eeb74533f713e256ee6340d0187e030
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  在查詢中會保存 SQL 步驟的所有 SQL Server 查詢發佈的相關資訊。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此 SQL 的查詢分佈所屬之查詢的唯一識別碼。<br /><br /> request_id、 step_index 和 distribution_id 形成這個檢視的索引鍵。|請參閱中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|此分佈是一部分的查詢步驟索引。<br /><br /> request_id、 step_index 和 distribution_id 形成這個檢視的索引鍵。|請參閱在 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|pdw_node_id|**int**|執行此查詢發佈節點唯一識別碼。|請參閱中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|distribution_id|**int**|執行此查詢發佈的發佈唯一識別碼。<br /><br /> request_id、 step_index 和 distribution_id 形成這個檢視的索引鍵。|請參閱在 distribution_id [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)。 設定為-1 可執行在節點範圍內，未散發範圍的要求。|  
|status|**nvarchar(32)**|查詢分佈的目前狀態。|暫止狀態，執行失敗，已取消，完成，已中止 CancelSubmitted|  
|error_id|**nvarchar(36)**|如果有任何與此查詢發佈，相關聯錯誤的唯一識別碼。|請參閱在 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)。 如果沒有發生錯誤，請設為 NULL。|  
|start_time|**datetime**|哪一個查詢發佈開始時間執行。|此查詢發佈較小或等於目前的時間，大於或等於查詢步驟的 start_time 隸屬於|  
|end_time|**datetime**|在此查詢散發完成執行、 已取消，或失敗的時間。|大於或等於開始時間，或如果查詢分佈是進行中或已佇列設為 NULL。|  
|total_elapsed_time|**int**|表示已執行的查詢分佈，以毫秒為單位的時間。|大於或等於 0。 等於差異的 start_time 和 end_time 已完成、 失敗或取消的查詢分佈。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 仍的最大值。 這種情況會產生警告的 「 已超過最大值 」。<br /><br /> 以毫秒為單位的最大值就相當於 24.8 天。|  
|row_count|**bigint**|讀取這個查詢發佈或變更的資料列數目。|-1 代表不會變更或傳回資料，例如 CREATE TABLE 和 DROP TABLE 的作業。|  
|spid|**int**|在執行查詢散發的 SQL Server 執行個體上的工作階段識別碼。||  
|command|**nvarchar(4000)**|此查詢散發的命令的完整文字。|任何有效查詢或要求的字串。|  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱中的系統檢視的最大值 」 一節[最小和最大值 (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)主題。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
