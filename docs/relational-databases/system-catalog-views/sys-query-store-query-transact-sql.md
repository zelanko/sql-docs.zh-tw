---
title: sys.query_store_query (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_QUERY
- SYS.QUERY_STORE_QUERY_TSQL
- SYS.QUERY_STORE_QUERY
- QUERY_STORE_QUERY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_query catalog view
- sys.query_store_query catalog view
ms.assetid: bdee149e-7556-4fc3-8242-925dd4b7b6ac
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d9d53bc6cd0219502698ba8a02b6ba19eaf5f34f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37985184"
---
# <a name="sysquerystorequery-transact-sql"></a>sys.query_store_query & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含查詢和其相關聯的整體彙總執行階段執行統計資料的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|主索引鍵。|  
|**query_text_id**|**bigint**|外部索引鍵。 加入[sys.query_store_query_text &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**context_settings_id**|**bigint**|外部索引鍵。 加入[sys.query_context_settings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)。|  
|**object_id**|**bigint**|查詢是一部分的資料庫物件識別碼 (預存程序、 觸發程序、 CLR UDF/UDAgg，等等。)。 0，表示查詢不會執行一部分的資料庫物件 （臨機操作查詢）。|  
|**batch_sql_handle**|**varbinary(64)**|陳述式批次查詢的識別碼是的一部分。 查詢參考暫存資料表或資料表變數時，才填入。|  
|**query_hash**|**binary(8)**|個別的查詢，根據邏輯的查詢樹狀結構的 MD5 雜湊。 包括最佳化工具提示。|  
|**is_internal_query**|**bit**|查詢是在內部產生的。|  
|**query_parameterization_type**|**tinyint**|參數化的類型：<br /><br /> 0 – 無<br /><br /> 1-使用者<br /><br /> 2 – 簡單<br /><br /> 3 – 強制|  
|**query_parameterization_type_desc**|**nvarchar(60)**|參數化類型的文字描述。|  
|**initial_compile_start_time**|**datetimeoffset**|編譯開始時間。|  
|**last_compile_start_time**|**datetimeoffset**|編譯開始時間。|  
|**last_execution_time**|**datetimeoffset**|上次執行時間的最後一個參考查詢/計劃的結束的時間。|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|上次在其中查詢使用上一次的 SQL 批次的控制代碼。 它可以提供做為輸出[sys.dm_exec_sql_text &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)以取得完整的批次文字。|  
|**last_compile_batch_offset_start**|**bigint**|可以提供給 sys.dm_exec_sql_text () 以及 last_compile_batch_sql_handle 的資訊。|  
|**last_compile_batch_offset_end**|**bigint**|可以提供給 sys.dm_exec_sql_text () 以及 last_compile_batch_sql_handle 的資訊。|  
|**count_compiles**|**bigint**|編譯統計資料。|  
|**avg_compile_duration**|**float**|以百萬分之一秒的編譯統計資料。|  
|**last_compile_duration**|**bigint**|以百萬分之一秒的編譯統計資料。|  
|**avg_bind_duration**|**float**|繫結 （毫秒） 的統計資料。|  
|**last_bind_duration**|**bigint**|繫結的統計資料。|  
|**avg_bind_cpu_time**|**float**|繫結的統計資料。|  
|**last_bind_cpu_time**|**bigint**|繫結的統計資料。|  
|**avg_optimize_duration**|**float**|以微秒為單位的最佳化統計資料。|  
|**last_optimize_duration**|**bigint**|最佳化統計資料。|  
|**avg_optimize_cpu_time**|**float**|以微秒為單位的最佳化統計資料。|  
|**last_optimize_cpu_time**|**bigint**|最佳化統計資料。|  
|**avg_compile_memory_kb**|**float**|編譯記憶體統計資料。|  
|**last_compile_memory_kb**|**bigint**|編譯記憶體統計資料。|  
|**max_compile_memory_kb**|**bigint**|編譯記憶體統計資料。|  
|**is_clouddb_internal_query**|**bit**|永遠為 0 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在內部部署環境。|  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW DATABASE STATE**權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_query_store_options &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
