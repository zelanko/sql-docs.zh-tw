---
title: sys.databases query_store_query （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 676c7a8c20c6374d9ceff521622f030c8f8fb983
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396377"
---
# <a name="sysquery_store_query-transact-sql"></a>sys.databases query_store_query （Transact-sql）
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  包含有關查詢的資訊，以及其相關聯的整體匯總執行時間執行統計資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**query_id**|**bigint**|主索引鍵。|  
|**query_text_id**|**bigint**|外鍵。 Query_store_query_text 的聯結[&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|  
|**coNtext_settings_id**|**bigint**|外鍵。 [Query_coNtext_settings &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)的聯結。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|object_id|**bigint**|查詢所屬之資料庫物件的識別碼（預存程式、觸發程式、CLR UDF/UDAgg 等等）。 如果查詢不是當做資料庫物件（臨機操作查詢）的一部分來執行，則為0。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**batch_sql_handle**|**varbinary(64)**|查詢所屬之語句批次的識別碼。 只有在查詢參考臨時表或資料表變數時，才會填入。<br/>**注意：** Azure SQL 資料倉儲一律會傳回*Null*。|  
|**query_hash**|**binary （8）**|個別查詢的 MD5 雜湊，以邏輯查詢樹狀結構為基礎。 包含優化工具提示。|  
|**is_internal_query**|**bit**|查詢是在內部產生。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**query_parameterization_type**|**tinyint**|參數化的種類：<br /><br /> 0 - 無<br /><br /> 1-使用者<br /><br /> 2-簡單<br /><br /> 3-強制<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**query_parameterization_type_desc**|**nvarchar(60)**|參數化型別的文字描述。<br/>**注意：** Azure SQL 資料倉儲一律會傳回*None*。|  
|**initial_compile_start_time**|**datetimeoffset**|編譯開始時間。|  
|**last_compile_start_time**|**datetimeoffset**|編譯開始時間。|  
|**last_execution_time**|**datetimeoffset**|上次執行時間指的是查詢/計畫的最後結束時間。|  
|**last_compile_batch_sql_handle**|**varbinary(64)**|上次使用查詢之 SQL 批次的控制碼。 可以提供它做為 sys 的輸入[。 dm_exec_sql_text &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)取得批次的全文檢索。<br/>**注意：** Azure SQL 資料倉儲一律會傳回*Null*。|  
|**last_compile_batch_offset_start**|**bigint**|可以提供給 sys.databases 的資訊，以及 last_compile_batch_sql_handle 的 dm_exec_sql_text。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_compile_batch_offset_end**|**bigint**|可以提供給 sys.databases 的資訊，以及 last_compile_batch_sql_handle 的 dm_exec_sql_text。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**count_compiles**|**bigint**|編譯統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回一（1）。|  
|**avg_compile_duration**|**float**|編譯統計資料（以毫秒為單位）。|  
|**last_compile_duration**|**bigint**|編譯統計資料（以毫秒為單位）。|  
|**avg_bind_duration**|**float**|以毫秒為單位的系結統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**last_bind_duration**|**bigint**|系結統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**avg_bind_cpu_time**|**float**|系結統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**last_bind_cpu_time**|**bigint**|系結統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**avg_optimize_duration**|**float**|優化統計資料（以毫秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_optimize_duration**|**bigint**|優化統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_optimize_cpu_time**|**float**|優化統計資料（以毫秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_optimize_cpu_time**|**bigint**|優化統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_compile_memory_kb**|**float**|編譯記憶體統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_compile_memory_kb**|**bigint**|編譯記憶體統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_compile_memory_kb**|**bigint**|編譯記憶體統計資料。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**is_clouddb_internal_query**|**bit**|在內部部署中一律為 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
  
## <a name="permissions"></a>權限  
 需要**VIEW DATABASE STATE**許可權。  
  
## <a name="see-also"></a>另請參閱  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_coNtext_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
