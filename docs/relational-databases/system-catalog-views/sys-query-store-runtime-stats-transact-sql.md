---
title: sys.databases query_store_runtime_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e90e93d0c56d96cc88b5be0eeed8680bf29c83cf
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834106"
---
# <a name="sysquery_store_runtime_stats-transact-sql"></a>sys.databases query_store_runtime_stats （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含查詢之執行時間執行統計資料資訊的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**runtime_stats_id**|**bigint**|資料列的識別碼，代表**plan_id**、 **execution_type**和**runtime_stats_interval_id**的執行時間執行統計資料。 只有過去的執行時間統計資料間隔才是唯一的。 對於目前作用中的間隔，可能會有多個資料列代表**plan_id**所參考之計畫的執行時間統計資料，並以**execution_type**表示的執行類型。 通常，一個資料列代表排清到磁片的執行時間統計資料，而其他則表示記憶體中的狀態。 因此，若要取得每個間隔的實際狀態，您需要匯總計量、依**plan_id**分組、 **execution_type**和**runtime_stats_interval_id**。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**plan_id**|**bigint**|外鍵。 [Query_store_plan &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)的聯結。|  
|**runtime_stats_interval_id**|**bigint**|外鍵。 [Query_store_runtime_stats_interval &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)的聯結。|  
|**execution_type**|**tinyint**|決定查詢執行的類型：<br /><br /> 0-正常執行（成功完成）<br /><br /> 3-用戶端起始的中止執行<br /><br /> 4-例外狀況已中止執行|  
|**execution_type_desc**|**nvarchar(128)**|執行類型欄位的文字描述：<br /><br /> 0-一般<br /><br /> 3-已中止<br /><br /> 4-例外狀況|  
|**first_execution_time**|**datetimeoffset**|匯總間隔內查詢計劃的首次執行時間。 這是指查詢執行的結束時間。|  
|**last_execution_time**|**datetimeoffset**|匯總間隔內查詢計劃的上次執行時間。 這是指查詢執行的結束時間。|  
|**count_executions**|**bigint**|匯總間隔內查詢計劃的執行次數總計。|  
|**avg_duration**|**float**|匯總間隔內查詢計劃的平均持續時間（以微秒為單位來報告）。|  
|**last_duration**|**bigint**|匯總間隔內查詢計劃的最後持續時間（以微秒為單位來報告）。|  
|**min_duration**|**bigint**|匯總間隔內查詢計劃的最短持續時間（以微秒為單位）。|  
|**max_duration**|**bigint**|匯總間隔內查詢計劃的最長持續時間（以微秒為單位）。|  
|**stdev_duration**|**float**|匯總間隔中查詢計劃的持續時間標準差（以微秒為單位）。|  
|**avg_cpu_time**|**float**|匯總間隔中查詢計劃的平均 CPU 時間（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_cpu_time**|**bigint**|匯總間隔內查詢計劃的最後 CPU 時間（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_cpu_time**|**bigint**|匯總間隔內查詢計劃的最小 CPU 時間（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_cpu_time**|**bigint**|匯總間隔內查詢計劃的最大 CPU 時間（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**stdev_cpu_time**|**float**|匯總間隔中查詢計劃的 CPU 時間標準差（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_logical_io_reads**|**float**|匯總間隔中查詢計劃的平均邏輯 i/o 讀取數。 （以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_logical_io_reads**|**bigint**|匯總間隔內查詢計劃的最後邏輯 i/o 讀取數。 （以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_logical_io_reads**|**bigint**|匯總間隔內查詢計劃的最小邏輯 i/o 讀取數。 （以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_logical_io_reads**|**bigint**|匯總間隔內查詢計劃的邏輯 i/o 讀取數上限。（以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**stdev_logical_io_reads**|**float**|邏輯 i/o 的數目會在匯總間隔內讀取查詢計劃的標準差。 （以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_logical_io_writes**|**float**|匯總間隔中查詢計劃的平均邏輯 i/o 寫入數。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_logical_io_writes**|**bigint**|匯總間隔中查詢計劃的最後邏輯 i/o 寫入數。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_logical_io_writes**|**bigint**|匯總間隔內查詢計劃的邏輯 i/o 寫入數目下限。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_logical_io_writes**|**bigint**|匯總間隔內查詢計劃的邏輯 i/o 寫入數目上限。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**stdev_logical_io_writes**|**float**|邏輯 i/o 的數目會在匯總間隔內寫入查詢計劃的標準差。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_physical_io_reads**|**float**|匯總間隔中查詢計劃的平均實體 i/o 讀取數（以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_physical_io_reads**|**bigint**|匯總間隔中查詢計劃的最後實體 i/o 讀取數（以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_physical_io_reads**|**bigint**|匯總間隔中查詢計劃的最小實體 i/o 讀取數（以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_physical_io_reads**|**bigint**|匯總間隔內查詢計劃的實體 i/o 讀取數目上限（以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**stdev_physical_io_reads**|**float**|實體 i/o 的數目會在匯總間隔內讀取查詢計劃的標準差（以讀取的8KB 頁數表示）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_clr_time**|**float**|匯總間隔中查詢計劃的平均 CLR 時間（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_clr_time**|**bigint**|匯總間隔內查詢計劃的上次 CLR 時間（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_clr_time**|**bigint**|匯總間隔中查詢計劃的最小 CLR 時間（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_clr_time**|**bigint**|匯總間隔內查詢計劃的 CLR 時間上限（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**stdev_clr_time**|**float**|匯總間隔中查詢計劃的 CLR 時間標準差（以微秒為單位）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_dop**|**float**|匯總間隔內查詢計劃的平均 DOP （平行處理原則程度）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_dop**|**bigint**|匯總間隔內查詢計劃的最後 DOP （平行處理原則程度）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_dop**|**bigint**|匯總間隔內查詢計劃的最小 DOP （平行處理原則程度）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_dop**|**bigint**|匯總間隔內查詢計劃的最大 DOP （平行處理原則程度）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**stdev_dop**|**float**|匯總間隔中查詢計劃的 DOP （平行處理原則程度）標準差。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_query_max_used_memory**|**float**|匯總間隔內查詢計劃的平均記憶體授與（回報為 8 KB 頁面的數目）。 若為使用原生編譯記憶體優化程式的查詢，一律為0。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_query_max_used_memory**|**bigint**|匯總間隔內的查詢計劃的上次記憶體授與（回報為 8 KB 頁面的數目）。 若為使用原生編譯記憶體優化程式的查詢，一律為0。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_query_max_used_memory**|**bigint**|匯總間隔內查詢計劃的最小記憶體授與（回報為 8 KB 頁面的數目）。 若為使用原生編譯記憶體優化程式的查詢，一律為0。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_query_max_used_memory**|**bigint**|匯總間隔內查詢計劃的最大記憶體授與（回報為 8 KB 頁面的數目）。 若為使用原生編譯記憶體優化程式的查詢，一律為0。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**stdev_query_max_used_memory**|**float**|匯總間隔內的查詢計劃記憶體授與標準差（回報為 8 KB 頁面的數目）。 若為使用原生編譯記憶體優化程式的查詢，一律為0。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**avg_rowcount**|**float**|匯總間隔內查詢計劃的平均傳回資料列數目。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_rowcount**|**bigint**|在匯總間隔內最後一次執行查詢計劃時，所傳回的資料列數目。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_rowcount**|**bigint**|匯總間隔內查詢計劃的傳回資料列數目下限。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_rowcount**|**bigint**|匯總間隔內查詢計劃的傳回資料列數目上限。|  
|**stdev_rowcount**|**float**|在匯總間隔內，查詢計劃的傳回資料列數目標準差。|
|**avg_log_bytes_used**|**float**|查詢計劃所使用之資料庫記錄中的平均位元組數目（匯總間隔內）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**last_log_bytes_used**|**bigint**|在匯總間隔內，上次執行查詢計劃所使用的資料庫記錄檔中的位元組數目。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**min_log_bytes_used**|**bigint**|查詢計劃所使用的資料庫記錄檔中的最小位元組數目，在匯總間隔內。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**max_log_bytes_used**|**bigint**|查詢計劃所使用的資料庫記錄檔中的最大位元組數目（在匯總間隔內）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|
|**stdev_log_bytes_used**|**float**|查詢計劃所使用之資料庫記錄中的位元組數目標準差（在匯總間隔內）。<br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**avg_tempdb_space_used**|**float**|匯總間隔內查詢計劃的平均分頁讀取數。 （以讀取的8KB 頁數表示）。<br><br/>**適用物件：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（從開始 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ）和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。|
|**last_tempdb_space_used**|**bigint**|匯總間隔內查詢計劃的最後頁面讀取數目。 （以讀取的8KB 頁數表示）。<br><br/>**適用物件：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（從開始 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ）和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。|
|**min_tempdb_space_used**|**bigint**|匯總間隔內查詢計劃的頁面讀取數目下限。 （以讀取的8KB 頁數表示）。<br><br/>**適用物件：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（從開始 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ）和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。|
|**max_tempdb_space_used**|**bigint**|匯總間隔內查詢計劃的頁面讀取數目上限。（以讀取的8KB 頁數表示）。<br><br/>**適用物件：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（從開始 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ）和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。|
|**stdev_tempdb_space_used**|**float**|分頁數目會在匯總間隔內讀取查詢計劃的標準差。 （以讀取的8KB 頁數表示）。<br><br/>**適用物件：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（從開始 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] ）和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。|
|**avg_page_server_io_reads**|**float**|匯總間隔內查詢計劃的頁面伺服器 i/o 讀取平均數目。 （以讀取的8KB 頁數表示）。<br><br/>**適用物件：** Azure SQL Database 超大規模資料庫</br>**注意：** Azure SQL 資料倉儲，Azure SQL DB，MI （非超大規模資料庫）一律會傳回零（0）。|
|**last_page_server_io_reads**|**bigint**|匯總間隔內查詢計劃的最後頁面伺服器 i/o 讀取數。 （以讀取的8KB 頁數表示）。<br><br/>**適用物件：** Azure SQL Database 超大規模資料庫</br>**注意：** Azure SQL 資料倉儲，Azure SQL DB，MI （非超大規模資料庫）一律會傳回零（0）。|
|**min_page_server_io_reads**|**bigint**|匯總間隔內查詢計劃的頁面伺服器 i/o 讀取次數下限。 （以讀取的8KB 頁數表示）。<br><br/>**適用物件：** Azure SQL Database 超大規模資料庫</br>**注意：** Azure SQL 資料倉儲，Azure SQL DB，MI （非超大規模資料庫）一律會傳回零（0）。|
|**max_page_server_io_reads**|**bigint**|匯總間隔內查詢計劃的頁面伺服器 i/o 讀取數上限。（以讀取的8KB 頁數表示）。<br><br/>**適用物件：** Azure SQL Database 超大規模資料庫</br>**注意：** Azure SQL 資料倉儲，Azure SQL DB，MI （非超大規模資料庫）一律會傳回零（0）。|
|**stdev_page_server_io_reads**|**float**|頁面伺服器 i/o 的數目會在匯總間隔內讀取查詢計劃的標準差。 （以讀取的8KB 頁數表示）。<br><br/>**適用物件：** Azure SQL Database 超大規模資料庫</br>**注意：** Azure SQL 資料倉儲，Azure SQL DB，MI （非超大規模資料庫）一律會傳回零（0）。|
  
## <a name="permissions"></a>權限  
需要 `VIEW DATABASE STATE` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_coNtext_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_plan &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)    
 [使用查詢存放區的最佳作法](../../relational-databases/performance/best-practice-with-the-query-store.md)   
  
