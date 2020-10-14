---
description: 'sys.dm_pdw_sql_requests (Transact-sql) '
title: sys.dm_pdw_sql_requests (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 3bbf99db3971ecb9979c1ef234d1f57c1761afa9
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035201"
---
# <a name="sysdm_pdw_sql_requests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存所有 SQL Server 查詢散發套件的相關資訊，作為查詢中 SQL 步驟的一部分。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此 SQL 查詢散發所屬查詢的唯一識別碼。<br /><br /> request_id、step_index 和 distribution_id 會形成此視圖的索引鍵。|請參閱 [sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id。|  
|step_index|**int**|此散發所屬之查詢步驟的索引。<br /><br /> request_id、step_index 和 distribution_id 會形成此視圖的索引鍵。|請參閱 [sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)中的 step_index。|  
|pdw_node_id|**int**|執行此查詢散發之節點的唯一識別碼。|請參閱 [sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 node_id。|  
|distribution_id|**int**|執行此查詢散發的散發之唯一識別碼。<br /><br /> request_id、step_index 和 distribution_id 會形成此視圖的索引鍵。|請參閱 [sys.pdw_distributions &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)中的 distribution_id。 針對在節點範圍執行的要求，將設定為-1，而不是在散發範圍中。|  
|status|**nvarchar(32)**|查詢散發的目前狀態。|擱置中、執行中、失敗、已取消、完成、已中止、CancelSubmitted|  
|error_id|**Nvarchar (36) **|與此查詢散發相關聯之錯誤的唯一識別碼（如果有的話）。|請參閱 [sys.dm_pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)中的 error_id。 如果未發生任何錯誤，則設定為 Null。|  
|start_time|**datetime**|查詢散發開始執行的時間。|小於或等於目前的時間，且大於或等於此查詢散發所屬的查詢步驟 start_time|  
|end_time|**datetime**|此查詢散發完成執行、已取消或失敗的時間。|大於或等於開始時間，如果查詢散發正在進行中或已排入佇列，則設定為 Null。|  
|total_elapsed_time|**int**|代表執行查詢散發的時間（以毫秒為單位）。|大於或等於0。 等於 [已完成]、[失敗] 或 [已取消] 的查詢散發的 start_time 和 end_time 差異。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 將會繼續成為最大值。 這種狀況會產生「已超過最大值」的警告。<br /><br /> 以毫秒為單位的最大值相當於24.8 天。|  
|row_count|**bigint**|此查詢散發變更或讀取的資料列數目。|-1 用於不變更或傳回資料的作業，例如 CREATE TABLE 和 DROP TABLE。|  
|spid|**int**|執行查詢散發的 SQL Server 實例上的會話識別碼。||  
|命令|**nvarchar(4000)**|此查詢散發的完整命令文字。|任何有效的查詢或要求字串。|  
  
 如需此視圖所保留之最大資料列的相關資訊，請參閱「 [容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」主題中的「中繼資料」一節。  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
