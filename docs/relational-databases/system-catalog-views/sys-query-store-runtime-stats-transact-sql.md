---
title: sys.query_store_runtime_stats & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 41916bbd0efabca03cc25e0c087a8c1a7a3d4070
ms.sourcegitcommit: 3d50caa30681bf384f5628b1dd3e06e24fc910cd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2019
ms.locfileid: "54838118"
---
# <a name="sysquerystoreruntimestats-transact-sql"></a>sys.query_store_runtime_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含查詢的執行階段執行統計資料資訊的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|代表執行階段執行統計資料的資料列的識別項**plan_id**， **execution_type**並**runtime_stats_interval_id**。 它是唯一的僅針對過去的執行階段統計資料間隔。 目前使用的間隔可能會表示所參考的計劃的執行階段統計資料的多個資料列**plan_id**，與所代表的執行類型**execution_type**。 一般而言，一個資料列代表執行階段統計資料會排清至磁碟，而其他 (s) 代表記憶體中狀態。 因此，若要取得每個間隔中的實際狀態您需要彙總的度量分組所依據**plan_id**， **execution_type**並**runtime_stats_interval_id**。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**plan_id**|**bigint**|外部索引鍵。 加入[sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。|  
|**runtime_stats_interval_id**|**bigint**|外部索引鍵。 加入[sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)。|  
|**execution_type**|**tinyint**|判斷執行查詢的類型：<br /><br /> 0-定期執行 （成功完成）<br /><br /> 3-用戶端起始已中止執行<br /><br /> 4-例外狀況已中止執行|  
|**execution_type_desc**|**nvarchar(128)**|文字執行的 [類型] 欄位的描述：<br /><br /> 0-一般<br /><br /> 3-已中止<br /><br /> 4-例外狀況|  
|**first_execution_time**|**datetimeoffset**|第一個彙總間隔內的查詢計劃的執行時間。|  
|**last_execution_time**|**datetimeoffset**|上次執行時間的查詢計劃的彙總間隔內。|  
|**count_executions**|**bigint**|執行查詢計劃的彙總間隔內的總計數。|  
|**avg_duration**|**float**|平均持續時間 （以微秒為單位報告） 的彙總間隔內的查詢計劃。|  
|**last_duration**|**bigint**|最後的持續時間的查詢計劃內彙總間隔 （以微秒為單位報告）。|  
|**min_duration**|**bigint**|中彙總間隔 （以微秒為單位報告） 的查詢計劃的最小持續期間。|  
|**max_duration**|**bigint**|中彙總間隔 （以微秒為單位報告） 的查詢計劃的最大持續期間。|  
|**stdev_duration**|**float**|持續時間 （以微秒為單位報告） 的彙總間隔內的查詢計劃的標準差。|  
|**avg_cpu_time**|**float**|平均 CPU 時間 （以微秒為單位報告） 的彙總間隔內的查詢計劃。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_cpu_time**|**bigint**|上次 CPU 時間的查詢計劃內彙總間隔 （以微秒為單位報告）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_cpu_time**|**bigint**|中彙總間隔 （以微秒為單位報告） 的查詢計劃的最小 CPU 時間。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_cpu_time**|**bigint**|中彙總間隔 （以微秒為單位報告） 的查詢計劃的最大 CPU 時間。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**stdev_cpu_time**|**float**|CPU 時間 （以微秒為單位報告） 的彙總間隔內的查詢計劃的標準差。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**avg_logical_io_reads**|**float**|查詢計劃的彙總間隔內讀取邏輯 IO 的平均數目。 （以 8 KB 的分頁讀取數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_logical_io_reads**|**bigint**|最後一個數字的邏輯 IO 讀取彙總間隔內的查詢計劃。 （以 8 KB 的分頁讀取數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_logical_io_reads**|**bigint**|查詢計劃的彙總間隔內讀取的邏輯 IO 數目下限。 （以 8 KB 的分頁讀取數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_logical_io_reads**|**bigint**|查詢計劃的彙總間隔內讀取的邏輯 IO 數目上限。（以 8 KB 的分頁讀取數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**stdev_logical_io_reads**|**float**|邏輯 IO 數目會讀取查詢計劃的彙總間隔內的標準差。 （以 8 KB 的分頁讀取數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**avg_logical_io_writes**|**float**|查詢計劃的彙總間隔內，寫入邏輯 IO 的平均數目。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_logical_io_writes**|**bigint**|最後一個數字的邏輯 IO 寫入彙總間隔內的查詢計劃。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_logical_io_writes**|**bigint**|為查詢計劃的彙總間隔內，寫入邏輯 IO 數目下限。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_logical_io_writes**|**bigint**|為查詢計劃的彙總間隔內，寫入的邏輯 IO 數目上限。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**stdev_logical_io_writes**|**float**|邏輯 IO 數目寫入查詢計劃的彙總間隔內的標準差。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**avg_physical_io_reads**|**float**|中彙總間隔 （以 8 KB 的分頁讀取數表示） 的查詢計劃讀取實體 IO 的平均數目。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_physical_io_reads**|**bigint**|最後一個的實體 IO 讀取數目 （以 8 KB 的分頁讀取數表示） 的彙總間隔內的查詢計劃。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_physical_io_reads**|**bigint**|最小數目的實體 IO 讀取 （以 8 KB 的分頁讀取數表示） 的彙總間隔內的查詢計劃。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_physical_io_reads**|**bigint**|中彙總間隔 （以 8 KB 的分頁讀取數表示） 的查詢計劃讀取實體 IO 的最大數目。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**stdev_physical_io_reads**|**float**|實體 IO 讀取數目 （以 8 KB 的分頁讀取數表示） 的彙總間隔內的查詢計劃的標準差。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**avg_clr_time**|**float**|CLR 之平均時間 （以微秒為單位報告） 的彙總間隔內的查詢計劃。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_clr_time**|**bigint**|查詢的最後一個 CLR 時間計劃內彙總間隔 （以微秒為單位報告）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_clr_time**|**bigint**|中彙總間隔 （以微秒為單位報告） 的查詢計劃的最小 CLR 時間。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_clr_time**|**bigint**|中彙總間隔 （以微秒為單位報告） 的查詢計劃的 CLR 時間上限。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**stdev_clr_time**|**float**|CLR 時間 （以微秒為單位報告） 的彙總間隔內的查詢計劃的標準差。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**avg_dop**|**float**|查詢計劃的彙總間隔內的平均 DOP （平行處理原則的程度）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_dop**|**bigint**|彙總間隔內的查詢計劃會持續 DOP （平行處理原則的程度）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_dop**|**bigint**|查詢計劃的彙總間隔內的最小 DOP （平行處理原則的程度）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_dop**|**bigint**|查詢計劃的彙總間隔內的最大 DOP （平行處理原則的程度）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**stdev_dop**|**float**|DOP （平行處理原則的程度） 彙總間隔內的查詢計劃的標準差。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**avg_query_max_used_memory**|**float**|平均記憶體授權 （報告為 8 KB 頁數） 彙總間隔內的查詢計劃。 一律使用原生查詢的 0 編譯記憶體最佳化程序。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_query_max_used_memory**|**bigint**|最後一個記憶體授權 （報告為 8 KB 頁數） 彙總間隔內的查詢計劃。 一律使用原生查詢的 0 編譯記憶體最佳化程序。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_query_max_used_memory**|**bigint**|最小記憶體授與 （報告為 8 KB 頁數） 彙總間隔內的查詢計劃。 一律使用原生查詢的 0 編譯記憶體最佳化程序。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_query_max_used_memory**|**bigint**|最大記憶體授與 （報告為 8 KB 頁數） 彙總間隔內的查詢計劃。 一律使用原生查詢的 0 編譯記憶體最佳化程序。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**stdev_query_max_used_memory**|**float**|記憶體授與彙總間隔內的查詢計畫 （報告為 8 KB 頁數） 的標準差。 一律使用原生查詢的 0 編譯記憶體最佳化程序。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**avg_rowcount**|**float**|傳回的資料列，查詢計劃的彙總間隔內的平均數目。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_rowcount**|**bigint**|最後一個執行的查詢計劃的彙總間隔內所傳回的資料列數目。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_rowcount**|**bigint**|查詢傳回的資料列的最小數目的計劃的彙總間隔內。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_rowcount**|**bigint**|彙總間隔內，計劃查詢傳回的資料列的最大數目。|  
|**stdev_rowcount**|**float**|傳回的資料列彙總間隔內的查詢計劃的標準差數目。|
|**avg_log_bytes_used**|**float**|中彙總間隔內的查詢計畫所使用的資料庫記錄檔的位元組的平均數目。 適用於**到 Azure SQL Database 只**。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**last_log_bytes_used**|**bigint**|中彙總間隔內的查詢計畫上次執行所使用的資料庫記錄檔的位元組數目。 適用於**到 Azure SQL Database 只**。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**min_log_bytes_used**|**bigint**|最小彙總間隔內的查詢計畫所使用的資料庫記錄檔中的位元組數目。  適用於**到 Azure SQL Database 只**。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**max_log_bytes_used**|**bigint**|中彙總間隔內的查詢計畫所使用的資料庫記錄檔的位元組數目上限。  適用於**到 Azure SQL Database 只**。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
|**stdev_log_bytes_used**|**float**|標準差的查詢計畫，彙總間隔內所使用的資料庫記錄中的位元組數目。  適用於**到 Azure SQL Database 只**。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零 (0)。|
  
## <a name="permissions"></a>Permissions  
 需要**VIEW DATABASE STATE**權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_query_store_options &#40;-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
