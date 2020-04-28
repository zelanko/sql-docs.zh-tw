---
title: sys.databases dm_exec_distributed_requests （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 37fd17f17d8b6aa1a30f48d75258d27f4a45561a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097800"
---
# <a name="sysdm_exec_distributed_requests-transact-sql"></a>sys.databases dm_exec_distributed_requests （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保留 PolyBase 查詢中目前或最近作用中的所有要求的相關資訊。 它會針對每個要求/查詢列出一個資料列。  
  
 根據會話和要求識別碼，使用者可以接著取出產生要執行的實際分散式要求-透過 sys. dm_exec_distributed_requests。 例如，涉及一般 SQL 和外部 SQL 資料表的查詢，將會分解成各種不同計算節點上執行的各種語句/要求。 為了追蹤所有計算節點上的分散式步驟，我們引進了「全域」執行識別碼，可用來分別追蹤與某個特定要求和運算子相關聯之計算節點上的所有作業。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|此視圖的索引鍵。 與要求相關聯的唯一數值識別碼。|在系統的所有要求中都是唯一的。|  
|execution_id|**Nvarchar （32**|與執行此查詢的會話相關聯的唯一數值識別碼。||  
|status|**Nvarchar （32**|要求的目前狀態。|「擱置」、「授權」、「AcquireSystemResources」、「正在初始化」、「計畫」、「正在剖析」、「AquireResources」、「執行中」、「取消中」、「完成」、「失敗」、「已取消」。|  
|error_id|**Nvarchar （36）**|與要求相關聯之錯誤的唯一識別碼（如果有的話）。|如果未發生錯誤，則設為 Null。|  
|start_time|**datetime**|開始執行要求的時間。|0代表已佇列的要求;否則，有效的日期時間就會小於或等於目前的時間。|  
|end_time|**datetime**|引擎完成編譯要求的時間。|針對已佇列或作用中的要求，則為 Null;否則，有效的日期時間就會小於或等於目前的時間。|  
|total_elapsed_time|**int**|自要求開始後執行所經過的時間（以毫秒為單位）。|介於0和 start_time 與 end_time 之間的差異。如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 會繼續成為最大值。 此狀況會產生「已超過最大值」的警告。 最大值（以毫秒為單位）相當於24.8 天。|  
  
## <a name="see-also"></a>另請參閱  
 [使用動態管理檢視進行 PolyBase 疑難排解](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [資料庫相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
