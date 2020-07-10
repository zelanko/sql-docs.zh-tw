---
title: dm_pdw_sql_requests (Transact-sql) |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 455ccc47d4150211001b0cf715d67827c04376bc
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196806"
---
# <a name="sysdm_pdw_sql_requests-transact-sql"></a>dm_pdw_sql_requests (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存所有 SQL Server 查詢散發的相關資訊，做為查詢中 SQL 步驟的一部分。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此 SQL 查詢散發所屬之查詢的唯一識別碼。<br /><br /> request_id、step_index 和 distribution_id 會形成此視圖的索引鍵。|請參閱[dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id。|  
|step_index|**int**|此散發所屬之查詢步驟的索引。<br /><br /> request_id、step_index 和 distribution_id 會形成此視圖的索引鍵。|請參閱[dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)中的 step_index。|  
|pdw_node_id|**int**|執行此查詢散發所在節點的唯一識別碼。|請參閱[dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 node_id。|  
|distribution_id|**int**|執行此查詢散發之散發的唯一識別碼。<br /><br /> request_id、step_index 和 distribution_id 會形成此視圖的索引鍵。|請參閱[pdw_distributions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)中的 distribution_id。 針對在節點範圍（而不是散發範圍）執行的要求，設定為-1。|  
|status|**nvarchar(32)**|查詢散發的目前狀態。|暫止，執行中，失敗，已取消，完成，已中止，CancelSubmitted|  
|error_id|**Nvarchar (36) **|與此查詢散發相關聯之錯誤的唯一識別碼（如果有的話）。|請參閱[dm_pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)中的 error_id。 如果未發生錯誤，則設為 Null。|  
|start_time|**datetime**|查詢散發開始執行的時間。|小於或等於目前的時間，且大於或等於此查詢散發所屬之查詢步驟的 start_time|  
|end_time|**datetime**|此查詢散發完成執行、已取消或失敗的時間。|大於或等於開始時間，如果查詢散發正在進行中或已排入佇列，則設為 Null。|  
|total_elapsed_time|**int**|代表查詢散發的執行時間（以毫秒為單位）。|大於或等於0。 等於 [已完成]、[失敗] 或 [已取消] 查詢散發的 start_time 和 end_time 差異。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 會繼續成為最大值。 此狀況會產生「已超過最大值」的警告。<br /><br /> 最大值（以毫秒為單位）相當於24.8 天。|  
|row_count|**bigint**|此查詢散發變更或讀取的資料列數目。|-1 適用于不會變更或傳回資料的作業，例如 CREATE TABLE 和 DROP TABLE。|  
|spid|**int**|執行查詢散發之 SQL Server 實例上的會話識別碼。||  
|命令|**nvarchar(4000)**|此查詢散發的完整命令文字。|任何有效的查詢或要求字串。|  
  
 如需此視圖所保留之最大資料列的詳細資訊，請參閱[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題中的 Metadata 一節。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
