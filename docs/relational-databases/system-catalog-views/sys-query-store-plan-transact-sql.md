---
title: sys.databases query_store_plan （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cc78decc0c911376b61cc429ba538be11cbaded6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831434"
---
# <a name="sysquery_store_plan-transact-sql"></a>sys.query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含與查詢相關聯之每個執行計畫的資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|
|**plan_id**|**bigint**|主索引鍵。|  
|**query_id**|**bigint**|外鍵。 [Query_store_query &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)的聯結。|  
|**plan_group_id**|**bigint**|方案群組的識別碼。 資料指標查詢通常需要多個（填入和提取）計畫。 同時編譯的填入和提取計畫位於相同的群組中。<br /><br /> 0表示方案不在群組中。|  
|**engine_version**|**nvarchar(32)**|用來以 **' 主要. 組建. 修訂版 '** 格式編譯計畫的引擎版本。|  
|**compatibility_level**|**smallint**|查詢中參考之資料庫的資料庫相容性層級。|  
|**query_plan_hash**|**binary （8）**|個別計畫的 MD5 雜湊。|  
|**query_plan**|**nvarchar(max)**|查詢計劃的執行程式表 XML。|  
|**is_online_index_plan**|**bit**|在線上索引建立期間使用了計畫。 <br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**is_trivial_plan**|**bit**|計畫是一個簡單的計畫（查詢最佳化工具的第0階段輸出）。 <br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**is_parallel_plan**|**bit**|方案為平行。 <br/>**注意：** Azure SQL 資料倉儲一律會傳回一（1）。|  
|**is_forced_plan**|**bit**|當使用者執行預存程式**sys. sp_query_store_force_plan**時，計畫會標示為強制。 強制機制*並不保證*會將此計畫用於**query_id**所參考的查詢。 強制執行計畫會再次編譯查詢，而且通常會針對**plan_id**所參考的計畫，產生完全相同或類似的計畫。 如果強制執行計畫不成功， **force_failure_count**會遞增，而**last_force_failure_reason**會填入失敗原因。 <br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**is_natively_compiled**|**bit**|方案包含原生編譯的記憶體優化程式。 （0 = FALSE，1 = TRUE）。 <br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**force_failure_count**|**bigint**|強制此計畫失敗的次數。 只有在重新編譯查詢（*而不是每次執行*時）時，它才會遞增。 每次**is_plan_forced**從**FALSE**變更為**TRUE**時，就會重設為0。 <br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**last_force_failure_reason**|**int**|計畫強制失敗的原因。<br /><br /> 0：沒有失敗，否則導致強制失敗的錯誤錯誤號碼<br /><br /> 8637： ONLINE_INDEX_BUILD<br /><br /> 8683： INVALID_STARJOIN<br /><br /> 8684： TIME_OUT<br /><br /> 8689： NO_DB<br /><br /> 8690： HINT_CONFLICT<br /><br /> 8691： SETOPT_CONFLICT<br /><br /> 8694： DQ_NO_FORCING_SUPPORTED<br /><br /> 8698： NO_PLAN<br /><br /> 8712： NO_INDEX<br /><br /> 8713： VIEW_COMPILE_FAILED<br /><br /> \<其他值>： GENERAL_FAILURE <br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Last_force_failure_reason_desc 的文字描述。<br /><br /> ONLINE_INDEX_BUILD：查詢嘗試修改資料，而目標資料表具有正在線上建立的索引<br /><br /> INVALID_STARJOIN：方案包含不正確 StarJoin 規格<br /><br /> TIME_OUT：優化工具在搜尋強制計畫所指定的計畫時，超過允許的作業數目<br /><br /> NO_DB：方案中指定的資料庫不存在<br /><br /> HINT_CONFLICT：無法編譯查詢，因為計畫與查詢提示衝突<br /><br /> DQ_NO_FORCING_SUPPORTED：無法執行查詢，因為計畫與分散式查詢或全文檢索作業的使用發生衝突。<br /><br /> NO_PLAN：查詢處理器無法產生查詢計劃，因為無法驗證強制計畫是否對查詢有效<br /><br /> NO_INDEX：方案中指定的索引已不存在<br /><br /> VIEW_COMPILE_FAILED：因為計畫中參考的索引視圖發生問題，所以無法強制查詢計劃<br /><br /> GENERAL_FAILURE：一般強制錯誤（未涵蓋上述原因） <br/>**注意：** Azure SQL 資料倉儲一律會傳回*NONE*。|  
|**count_compiles**|**bigint**|規劃編譯統計資料。|  
|**initial_compile_start_time**|**datetimeoffset**|規劃編譯統計資料。|  
|**last_compile_start_time**|**datetimeoffset**|規劃編譯統計資料。|  
|**last_execution_time**|**datetimeoffset**|上次執行時間指的是查詢/計畫的最後結束時間。|  
|**avg_compile_duration**|**float**|規劃編譯統計資料。 <br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**last_compile_duration**|**bigint**|規劃編譯統計資料。 <br/>**注意：** Azure SQL 資料倉儲一律會傳回零（0）。|  
|**plan_forcing_type**|**int**|計畫強制型別。<br /><br />0：無<br /><br />1：手動<br /><br />2：自動|  
|**plan_forcing_type_desc**|**nvarchar(60)**|Plan_forcing_type 的文字描述。<br /><br />無：不強制執行計畫<br /><br />手動：由使用者強制的計畫<br /><br />自動：自動調整所強制的計畫|  

## <a name="plan-forcing-limitations"></a>強制執行計劃的限制
查詢存放區有強制查詢最佳化工具使用特定執行計劃的機制。 不過，也有避免強制執行計劃的一些限制。 

首先，如果計劃包含下列建構：
* INSERT BULK 陳述式。
* 參考外部資料表
* 分散式查詢或全文檢索作業
* 使用全域查詢 
* 動態或索引鍵集資料指標 
* 無效的星型聯結規格 

> [!NOTE]
> Azure SQL Database 和 SQL Server 2019 支援計畫強制執行靜態和向前快轉資料指標。

其次，無法再使用計劃依賴的物件時：
* 資料庫 (如果計劃的來源資料庫不再存在)
* 索引 (不再存在或停用)

最後，計劃本身的問題：
* 查詢不合法
* 查詢最佳化工具超過允許的作業數目
* 計劃 XML 格式不正確

## <a name="permissions"></a>權限  
 需要**VIEW DATABASE STATE**許可權。  
  
## <a name="see-also"></a>另請參閱  
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [query_coNtext_settings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [query_store_query &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [query_store_query_text &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [query_store_runtime_stats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [query_store_runtime_stats_interval &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
