---
title: sys.query_store_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 60b9137e52b34b79fa4faddbef7b9e4da8734142
ms.sourcegitcommit: e3f5b70bbb4c66294df8c7b2c70186bdf2365af9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2019
ms.locfileid: "54397607"
---
# <a name="sysquerystoreplan-transact-sql"></a>sys.query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  包含與查詢相關聯的每個執行計畫的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**plan_id**|**bigint**|主索引鍵。|  
|**query_id**|**bigint**|外部索引鍵。 加入[sys.query_store_query &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)。|  
|**plan_group_id**|**bigint**|計劃群組的識別碼。 資料指標查詢通常需要多個 （填入和擷取） 計劃。 填入並一起編譯的擷取方案都位於相同的群組。<br /><br /> 0 表示計畫不在群組中。|  
|**engine_version**|**nvarchar(32)**|若要編譯的計畫中使用的引擎版本 **'major.minor.build.revision'** 格式。|  
|**compatibility_level**|**smallint**|在查詢中參考之資料庫的資料庫相容性層級。|  
|**query_plan_hash**|**binary(8)**|個別的計劃的 MD5 雜湊。|  
|**query_plan**|**nvarchar(max)**|Showplan XML 查詢計劃。|  
|**is_online_index_plan**|**bit**|計劃的線上索引建立期間使用。|  
|**is_trivial_plan**|**bit**|計劃是簡式的計劃 （查詢最佳化工具的階段 0 中的輸出）。|  
|**is_parallel_plan**|**bit**|計劃是平行。|  
|**is_forced_plan**|**bit**|計劃會標示為強制，當使用者執行預存程序**sys.sp_query_store_force_plan**。 強制執行機制*並不保證*完全此方案將用於查詢所參考**query_id**。 強制執行計劃會導致重新編譯的查詢，並通常會產生完全相同或類似的計畫所參考的計劃**plan_id**。 如果強制執行計劃不成功， **force_failure_count**會遞增並**last_force_failure_reason**會填入失敗原因。|  
|**is_natively_compiled**|**bit**|計劃包含原生編譯的記憶體最佳化程序。 (0 = FALSE,1 = TRUE)。|  
|**force_failure_count**|**bigint**|強制執行此計劃已失敗的次數的數目。 可以只在重新編譯查詢時，才會遞增 (*不會在每次執行*)。 它會重設為 0 每次**is_plan_forced**已從**FALSE**來**TRUE**。|  
|**last_force_failure_reason**|**int**|強制執行計劃失敗的原因。<br /><br /> 0： 沒有失敗，否則為錯誤號碼的錯誤，導致無法強制執行<br /><br /> 8637:ONLINE_INDEX_BUILD<br /><br /> 8683:INVALID_STARJOIN<br /><br /> 8684:TIME_OUT<br /><br /> 8689:NO_DB<br /><br /> 8690:HINT_CONFLICT<br /><br /> 8691:SETOPT_CONFLICT<br /><br /> 8694:DQ_NO_FORCING_SUPPORTED<br /><br /> 8698:NO_PLAN<br /><br /> 8712:NO_INDEX<br /><br /> 8713:VIEW_COMPILE_FAILED<br /><br /> \<其他值 >:GENERAL_FAILURE|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Last_force_failure_reason_desc 的文字描述。<br /><br /> ONLINE_INDEX_BUILD： 嘗試修改資料，而目標資料表有正在線上建立索引的查詢<br /><br /> INVALID_STARJOIN： 計劃包含無效的 StarJoin 規格<br /><br /> TIME_OUT:最佳化工具超過允許的作業，搜尋指定的強制計劃的計劃時的數字<br /><br /> NO_DB:計劃中指定的資料庫不存在<br /><br /> HINT_CONFLICT:無法編譯查詢，因為使用查詢提示相衝突的計劃<br /><br /> DQ_NO_FORCING_SUPPORTED:無法執行查詢，因為計劃的分散式的查詢或全文檢索作業使用發生衝突。<br /><br /> NO_PLAN:查詢處理器無法產生查詢計劃，因為無法驗證強制執行的計畫，有效的查詢<br /><br /> NO_INDEX:不會再計劃中指定的索引存在<br /><br /> VIEW_COMPILE_FAILED:因為計劃中參考的索引檢視表中的問題而無法強制執行查詢計劃<br /><br /> GENERAL_FAILURE： 一般的強制錯誤 （未涵蓋上述原因）|  
|**count_compiles**|**bigint**|規劃編譯統計資料。|  
|**initial_compile_start_time**|**datetimeoffset**|規劃編譯統計資料。|  
|**last_compile_start_time**|**datetimeoffset**|規劃編譯統計資料。|  
|**last_execution_time**|**datetimeoffset**|上次執行時間的最後一個參考查詢/計劃的結束的時間。|  
|**avg_compile_duration**|**float**|規劃編譯統計資料。|  
|**last_compile_duration**|**bigint**|規劃編譯統計資料。|  
|**plan_forcing_type**|**int**|計畫強制執行型別。<br /><br />
0：無<br /><br />
1：MANUAL<br /><br />
2：自動 | |**plan_forcing_type_desc**|**nvarchar(60)**|Plan_forcing_type 的文字描述。<br /><br />
NONE:強制執行任何計劃<br /><br />
MANUAL:已由使用者強制的計劃<br /><br />
自動：自動調整所強制的計劃 |

## <a name="plan-forcing-limitations"></a>計畫強制執行限制
查詢存放區有強制查詢最佳化工具使用特定執行計劃的機制。 不過，也有避免強制執行計劃的一些限制。 

首先，如果計劃包含下列建構：
* INSERT BULK 陳述式。
* INSERT BULK 陳述式。
* 參考外部資料表
* 分散式查詢或全文檢索作業
* 使用全域查詢 
* 資料指標
* 無效的星型聯結規格 

其次，無法再使用計劃依賴的物件時：
* 資料庫 (如果計劃的來源資料庫不再存在)
* 索引 (不再存在或停用)

最後，計劃本身的問題：
* 查詢不合法
* 查詢最佳化工具超過允許的作業數目
* 計劃 XML 格式不正確

## <a name="permissions"></a>Permissions  
 需要**VIEW DATABASE STATE**權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_query_store_options &#40;-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
