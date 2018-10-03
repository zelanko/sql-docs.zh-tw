---
title: sys.dm_exec_distributed_requests (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 87fa42aa2603a3a25e5a53ca5abb3a140299dd6c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743236"
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>sys.dm_exec_distributed_requests & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保留目前或最近使用 PolyBase 查詢中的所有要求的相關資訊。 它會列出每個要求/查詢的一個資料列。  
  
 根據工作階段和要求識別碼，使用者便可以擷取要執行 – 透過 sys.dm_exec_distributed_requests 產生實際的分散式的要求。 比方說，關於一般的 SQL 和外部的 SQL 資料表的查詢將會分解成各種陳述式/要求跨各種不同的計算節點執行。 若要追蹤所有計算節點的分散式的步驟，我們將介紹可用來都追蹤相關聯一個特定的要求和運算子，分別在計算節點上的所有作業的 'global' 的執行識別碼。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary(64)**|此檢視的索引鍵。 與要求相關聯的唯一數值識別碼。|在系統中的所有要求間是唯一的。|  
|execution_id|**nvarchar(32**|此查詢執行所在的工作階段相關聯的唯一數值識別碼。||  
|status|**nvarchar(32**|目前要求的狀態。|'擱置'、 '授權'，'AcquireSystemResources'，'Initializing'，'計劃'，'剖析'，'AquireResources'，'Running'、 '取消'，'Complete'，' 失敗 '，'已取消'。|  
|error_id|**nvarchar(36)**|如果有的話，與要求相關的錯誤的唯一識別碼。|如果沒有發生錯誤，請設為 NULL。|  
|start_time|**datetime**|開始要求執行時間。|0 代表已排入佇列的要求;否則，有效的日期時間小於或等於目前的時間。|  
|end_time|**datetime**|引擎完成編譯要求的時間。|已排入佇列或作用中的要求; 是 null否則，有效的日期時間小於或等於目前的時間。|  
|total_elapsed_time|**int**|在執行中的事件，是因為啟動要求，以毫秒為單位經過的時間。|介於 0 到 start_time 和 end_time 之間的差異。如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 仍是最大值。 這種情況會產生警告 」 的最大值已超過 」。 以毫秒為單位的最大值相當於 24.8 天。|  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase 疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
