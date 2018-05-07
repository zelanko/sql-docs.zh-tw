---
title: sys.dm_exec_distributed_requests (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 395ddcb8b479da3b02aa5423544d0cc5c0c5e2bd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保存目前或最近使用 PolyBase 查詢中的所有要求的相關資訊。 它會列出每個要求/查詢的一個資料列。  
  
 根據工作階段，然後要求識別碼，使用者可以再擷取要執行 – 透過 sys.dm_exec_distributed_requests 產生實際的分散式的要求。 比方說，涉及一般 SQL 和外部的 SQL 資料表的查詢將會分解成各種陳述式/要求執行各種計算節點之間。 若要追蹤所有計算節點間的分散式的步驟，我們介紹可以用來追蹤所有作業分別與一個特定的要求和運算子，相關聯的計算節點上的 'global' 的執行識別碼。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|此檢視的索引鍵。 與要求相關聯的唯一數值識別碼。|在系統中的所有要求都是唯一的。|  
|execution_id|**nvarchar(32**|此查詢執行所在的工作階段相關聯的唯一數值識別碼。||  
|status|**nvarchar(32**|目前要求的狀態。|'暫止'、 '授權'，'AcquireSystemResources'，'Initializing'，'計劃'，'剖析'，'AquireResources'，'執行'、 '取消' 「 完成 」，「 失敗 」，'取消'。|  
|error_id|**nvarchar(36)**|如果有的話，與要求相關的錯誤的唯一識別碼。|如果沒有發生錯誤，請設為 NULL。|  
|start_time|**datetime**|開始在要求執行時間。|0 代表要求排入佇列。否則，便是有效的日期時間小於或等於目前的時間。|  
|end_time|**datetime**|引擎完成編譯要求的時間。|排入佇列，或使用中要求，則為 null否則，有效的日期時間小於或等於目前的時間。|  
|total_elapsed_time|**int**|自啟動要求，以毫秒為單位，在執行所經過時間。|介於 0 到的 start_time 和 end_time 之間的差異。如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 仍的最大值。 這種情況會產生警告的 「 已超過最大值 」。 以毫秒為單位的最大值就相當於 24.8 天。|  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase，疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
