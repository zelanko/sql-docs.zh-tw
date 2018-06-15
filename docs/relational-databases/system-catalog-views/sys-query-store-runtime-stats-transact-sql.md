---
title: sys.query_store_runtime_stats (TRANSACT-SQL) |Microsoft 文件
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
- SYS.QUERY_STORE_RUNTIME_STATS_TSQL
- QUERY_STORE_RUNTIME_STATS_TSQL
- SYS.QUERY_STORE_RUNTIME_STATS
- QUERY_STORE_RUNTIME_STATS
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_runtime_stats catalog view
- sys.query_store_runtime_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 85bb7aa5bf91f8d357556adac9e58fb6ab83df24
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33182354"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含查詢的執行階段執行統計資料資訊的相關資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|代表執行階段執行統計資料的資料列的識別項**plan_id**， **execution_type**和**runtime_stats_interval_id**。 它是唯一的只會針對過去的執行階段統計資料間隔。 對於目前有效間隔可能代表執行階段統計資料所參考的計劃的多個資料列**plan_id**，與所代表的執行類型**execution_type**。 一般而言，一個資料列都代表執行階段統計資料會排清至磁碟，而其他 (s) 代表記憶體中狀態。 因此，若要取得每個間隔中的實際狀態您要彙總的度量資訊分組所依據**plan_id**， **execution_type**和**runtime_stats_interval_id**。 |  
|**plan_id**|**bigint**|外部索引鍵。 加入[sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。|  
|**runtime_stats_interval_id**|**bigint**|外部索引鍵。 加入[sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)。|  
|**execution_type**|**tinyint**|判斷執行查詢的類型：<br /><br /> 0 – 正常執行 （成功完成）<br /><br /> 3 – 由用戶端起始已中止執行<br /><br /> 4-例外狀況已中止執行|  
|**execution_type_desc**|**nvarchar(128)**|執行類型欄位的文字描述：<br /><br /> 0 – 一般<br /><br /> 3 – 中止<br /><br /> 4-例外狀況|  
|**first_execution_time**|**datetimeoffset**|查詢計劃的彙總間隔內的第一個執行時間。|  
|**last_execution_time**|**datetimeoffset**|上次執行時間的查詢計劃的彙總間隔內。|  
|**count_executions**|**bigint**|執行查詢計畫的彙總間隔內的總計數。|  
|**avg_duration**|**float**|平均持續時間 （以毫秒為單位來報告） 的彙總間隔內的查詢計畫。|  
|**last_duration**|**bigint**|最後一個持續時間的查詢計劃內彙總間隔 （以毫秒為單位來報告）。|  
|**min_duration**|**bigint**|最小持續期間 （以毫秒為單位來報告） 的彙總間隔內的查詢計畫。|  
|**max_duration**|**bigint**|（以毫秒為單位來報告） 的彙總間隔內的查詢計畫的最大持續期間。|  
|**stdev_duration**|**float**|持續時間 （以毫秒為單位來報告） 的彙總間隔內的查詢計劃的標準差。|  
|**avg_cpu_time**|**float**|平均 CPU 時間 （以毫秒為單位來報告） 的彙總間隔內的查詢計畫。|  
|**last_cpu_time**|**bigint**|最後一個 CPU 時間的查詢計劃內彙總間隔 （以毫秒為單位來報告）。|  
|**min_cpu_time**|**bigint**|（以毫秒為單位來報告） 的彙總間隔內的查詢計畫的最小 CPU 時間。|  
|**max_cpu_time**|**bigint**|（以毫秒為單位來報告） 的彙總間隔內的查詢計畫的最大 CPU 時間。|  
|**stdev_cpu_time**|**float**|CPU 時間 （以毫秒為單位來報告） 的彙總間隔內的查詢計劃的標準差。|  
|**avg_logical_io_reads**|**float**|查詢計畫的彙總間隔內讀取邏輯 IO 的平均數目。 （以 8 KB 頁面讀取數目表示）。|  
|**last_logical_io_reads**|**bigint**|最後一個的邏輯 IO 讀取數彙總間隔內的查詢計畫。 （以 8 KB 頁面讀取數目表示）。|  
|**min_logical_io_reads**|**bigint**|查詢計畫的彙總間隔內讀取邏輯 IO 的最小數目。 （以 8 KB 頁面讀取數目表示）。|  
|**max_logical_io_reads**|**bigint**|彙總間隔內查詢計劃讀取邏輯 IO 的最大數目。（以 8 KB 頁面讀取數目表示）。 |  
|**stdev_logical_io_reads**|**float**|標準差的查詢計劃的彙總間隔內讀取邏輯 IO 的數目。 （以 8 KB 頁面讀取數目表示）。|  
|**avg_logical_io_writes**|**float**|彙總間隔內查詢計劃寫入邏輯 IO 的平均數目。|  
|**last_logical_io_writes**|**bigint**|寫入查詢計畫的彙總間隔內的邏輯 IO 的最後一個數目。|  
|**min_logical_io_writes**|**bigint**|查詢計畫的彙總間隔內，寫入邏輯 IO 的最小數目。|  
|**max_logical_io_writes**|**bigint**|彙總間隔內查詢計劃寫入邏輯 IO 的最大數目。|  
|**stdev_logical_io_writes**|**float**|寫入查詢計劃的彙總間隔內的標準差的邏輯 IO 數目。|  
|**avg_physical_io_reads**|**float**|查詢計劃 （以 8 KB 頁面讀取數目表示） 的彙總間隔內讀取平均實體 IO 數。|  
|**last_physical_io_reads**|**bigint**|最後一個的實體 IO 讀取數目 （以 8 KB 頁面讀取數目表示） 的彙總間隔內的查詢計畫。|  
|**min_physical_io_reads**|**bigint**|最小的實體 IO 讀取數目 （以 8 KB 頁面讀取數目表示） 的彙總間隔內查詢計劃。|  
|**max_physical_io_reads**|**bigint**|查詢計劃 （以 8 KB 頁面讀取數目表示） 的彙總間隔內讀取最大實體 IO 數。|  
|**stdev_physical_io_reads**|**float**|實體 IO 讀取數目 （以 8 KB 頁面讀取數目表示） 的彙總間隔內的查詢計劃的標準差。|  
|**avg_clr_time**|**float**|CLR 的平均時間 （以毫秒為單位來報告） 的彙總間隔內的查詢計畫。|  
|**last_clr_time**|**bigint**|最後一個 CLR 時間查詢計劃內彙總間隔 （以毫秒為單位來報告）。|  
|**min_clr_time**|**bigint**|（以毫秒為單位來報告） 的彙總間隔內的查詢計畫的最小 CLR 時間。|  
|**max_clr_time**|**bigint**|CLR 時間上限 （以毫秒為單位來報告） 的彙總間隔內的查詢計畫。|  
|**stdev_clr_time**|**float**|CLR 時間 （以毫秒為單位來報告） 的彙總間隔內的查詢計劃的標準差。|  
|**avg_dop**|**float**|彙總間隔內的查詢計畫的平均 DOP （平行處理原則的程度）。|  
|**last_dop**|**bigint**|查詢計畫的彙總間隔內，最後一個 DOP （平行處理原則的程度）。|  
|**min_dop**|**bigint**|查詢計畫的彙總間隔內的最小 DOP （平行處理原則的程度）。|  
|**max_dop**|**bigint**|查詢計畫的彙總間隔內的最大 DOP （平行處理原則的程度）。|  
|**stdev_dop**|**float**|DOP （平行處理原則的程度） 彙總間隔內的查詢計劃的標準差。|  
|**avg_query_max_used_memory**|**float**|平均記憶體授權 （報告為 8 KB 頁數） 彙總間隔內的查詢計畫。 一律 0 的查詢使用原生編譯記憶體最佳化程序。|  
|**last_query_max_used_memory**|**bigint**|最後一個記憶體授權 （報告為 8 KB 頁數） 彙總間隔內的查詢計畫。 一律 0 的查詢使用原生編譯記憶體最佳化程序。|  
|**min_query_max_used_memory**|**bigint**|最小記憶體授與 （報告為 8 KB 頁數） 彙總間隔內的查詢計畫。 一律 0 的查詢使用原生編譯記憶體最佳化程序。|  
|**max_query_max_used_memory**|**bigint**|最大記憶體授與 （報告為 8 KB 頁數） 彙總間隔內的查詢計畫。 一律 0 的查詢使用原生編譯記憶體最佳化程序。|  
|**stdev_query_max_used_memory**|**float**|記憶體授與彙總間隔內的查詢計畫 （報告為 8 KB 頁數） 的標準差。 一律 0 的查詢使用原生編譯記憶體最佳化程序。|  
|**avg_rowcount**|**float**|傳回的資料列彙總間隔內的查詢計畫的平均數目。|  
|**last_rowcount**|**bigint**|彙總間隔內的查詢計畫上次執行所傳回的資料列數目。|  
|**min_rowcount**|**bigint**|查詢傳回的資料列的最小數目的計劃的彙總間隔內。|  
|**max_rowcount**|**bigint**|彙總間隔內，規劃查詢傳回的資料列的數目上限。|  
|**stdev_rowcount**|**float**|傳回的資料列彙總間隔內的查詢計劃的標準差數目。|
|**avg_log_bytes_used**|**float**|平均彙總間隔內的查詢計畫所使用的資料庫記錄檔中的位元組數目。 適用於**只到 Azure SQL Database**。|    
|**last_log_bytes_used**|**bigint**|彙總間隔內的查詢計畫上次執行所使用的資料庫記錄檔中的位元組數目。 適用於**只到 Azure SQL Database**。|  
|**min_log_bytes_used**|**bigint**|最小的查詢計畫，彙總間隔內所使用的資料庫記錄檔中的位元組數。  適用於**只到 Azure SQL Database**。|  
|**max_log_bytes_used**|**bigint**|彙總間隔內的查詢計畫所使用的資料庫記錄檔中的位元組數目上限。  適用於**只到 Azure SQL Database**。| 
|**stdev_log_bytes_used**|**float**|標準差的查詢計劃，彙總間隔內所使用的資料庫記錄檔中的位元組數目。  適用於**只到 Azure SQL Database**。|
  
## <a name="permissions"></a>Permissions  
 需要**VIEW DATABASE STATE**權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
