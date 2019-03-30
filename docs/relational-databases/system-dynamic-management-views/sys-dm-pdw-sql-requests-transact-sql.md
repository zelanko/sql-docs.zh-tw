---
title: sys.dm_pdw_sql_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 24bcf44fe2e1e0d35610dba9fb40d64ac2c819bb
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658002"
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  在查詢中保留需所有 SQL Server 查詢分佈的詳細資訊，做為 SQL 步驟的一部分。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此 SQL 的查詢分佈所屬之查詢的唯一識別碼。<br /><br /> request_id、 step_index 和 distribution_id 形成這個檢視的索引鍵。|請參閱中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|此分佈是一部分的查詢步驟的索引。<br /><br /> request_id、 step_index 和 distribution_id 形成這個檢視的索引鍵。|請參閱中的 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|pdw_node_id|**int**|執行此查詢分佈之節點的唯一識別碼。|請參閱中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|distribution_id|**int**|執行此查詢分佈分布的唯一識別碼。<br /><br /> request_id、 step_index 和 distribution_id 形成這個檢視的索引鍵。|請參閱中的 distribution_id [sys.pdw_distributions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)。 設定為-1，在節點範圍內，未散發的範圍內執行的要求。|  
|status|**nvarchar(32)**|查詢發佈目前狀態。|暫止、 執行、 失敗、 已取消、 完成、 中止 CancelSubmitted|  
|error_id|**nvarchar(36)**|如果有的話，此查詢散發相關聯錯誤的唯一識別碼。|請參閱中的 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)。 如果沒有發生錯誤，請設為 NULL。|  
|start_time|**datetime**|查詢發佈開始時間執行。|此查詢發佈較小或等於目前的時間和大於或等於查詢步驟的 start_time 已屬於|  
|end_time|**datetime**|在此查詢散發完成執行、 已取消，或失敗的時間。|大於或等於開始時間，或進行中或已排入佇列的查詢分佈是否設為 NULL。|  
|total_elapsed_time|**int**|表示已執行的查詢分佈，以毫秒為單位的時間。|大於或等於 0。 差異的 start_time 和 end_time 完成、 失敗或已取消查詢散發套件。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 仍是最大值。 這種情況會產生警告 」 的最大值已超過 」。<br /><br /> 以毫秒為單位的最大值相當於 24.8 天。|  
|row_count|**bigint**|變更或讀取此查詢分佈的資料列數目。|不變更或不傳回資料，例如 CREATE TABLE 和 DROP TABLE 作業為-1。|  
|spid|**int**|執行查詢的散發套件的 SQL Server 執行個體上的工作階段識別碼。||  
|command|**nvarchar(4000)**|此查詢散發的命令的完整文字。|任何有效查詢或要求的字串。|  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱中的 [中繼資料] 區段[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
