---
title: "sys.query_store_plan (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs: TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0950cf33d112d299de615a702d0fbac7cbfdc0e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysquerystoreplan-transact-sql"></a>sys.query_store_plan (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含與查詢相關聯的每個執行計畫的相關資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**bigint**|主索引鍵。|  
|**query_id**|**bigint**|外部索引鍵。 加入[sys.query_store_query &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md).|  
|**plan_group_id**|**bigint**|計劃群組的識別碼。 資料指標查詢通常需要多個 （填入和 fetch） 計畫。 填入並一起編譯的 fetch 計畫是在相同的群組。<br /><br /> 0 表示計畫不在群組中。|  
|**engine_version**|**nvarchar （32)**|用來編譯的計畫中的引擎版本**'的 major.minor.build.revision'**格式。|  
|**compatibility_level**|**smallint**|在查詢中參考之資料庫的資料庫相容性層級。|  
|**query_plan_hash**|**binary （8)**|個別的計劃的 MD5 雜湊。|  
|**query_plan**|**nvarchar(max)**|Showplan XML 查詢計劃。|  
|**is_online_index_plan**|**bit**|計劃在線上索引建立期間使用。|  
|**is_trivial_plan**|**bit**|計劃是一般的計畫 （在階段 0 中的查詢最佳化工具的輸出）。|  
|**is_parallel_plan**|**bit**|計劃是平行處理。|  
|**is_forced_plan**|**bit**|計劃會標記為強制，當使用者執行預存程序**sys.sp_query_store_force_plan**。 強制執行機制*不保證*完全此計劃將用於查詢所參考**query_id**。 強制執行計劃會導致重新編譯查詢，通常會產生完全相同或類似的計畫所參考的計劃**plan_id**。 如果強制執行計劃不成功， **force_failure_count**就會遞增並**last_force_failure_reason**填入包含失敗原因。|  
|**is_natively_compiled**|**bit**|計劃包含原生編譯的記憶體最佳化程序。 (0 = FALSE，1 = TRUE)。|  
|**force_failure_count**|**bigint**|數字的強制執行此計劃失敗的次數。 重新編譯查詢時，才可能會累加 (*不在每次執行*)。 它會重設為 0 每次**is_plan_forced**已從**FALSE**至**TRUE**。|  
|**last_force_failure_reason**|**int**|強制執行計劃失敗的原因。<br /><br /> 0： 沒有失敗，導致強制執行失敗之錯誤的其他錯誤數目<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684： 逾時<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<其他值 >: GENERAL_FAILURE|  
|**last_force_failure_reason_desc**|**nvarchar （128)**|Last_force_failure_reason_desc 的文字描述。<br /><br /> ONLINE_INDEX_BUILD： 查詢嘗試修改資料時目標資料表有正在線上建立索引<br /><br /> INVALID_STARJOIN： 計劃包含無效的 StarJoin 規格<br /><br /> 搜尋指定的強制計劃的計劃時允許之作業的逾時： 最佳化工具超過數字<br /><br /> NO_DB： 計劃中指定的資料庫不存在<br /><br /> HINT_CONFLICT： 無法編譯查詢，因為使用查詢提示的計畫相衝突<br /><br /> DQ_NO_FORCING_SUPPORTED： 無法執行查詢，因為計劃的分散式的查詢或全文檢索作業使用發生衝突。<br /><br /> NO_PLAN： 查詢處理器無法產生查詢計畫，因為無法驗證為有效的查詢強制執行的計畫<br /><br /> NO_INDEX： 存在不會再計劃中指定的索引<br /><br /> VIEW_COMPILE_FAILED： 無法強制執行查詢計畫，因為計畫中參考索引檢視表中的問題<br /><br /> GENERAL_FAILURE： 一般強制 （未涵蓋的錯誤與上述原因）|  
|**count_compiles**|**bigint**|規劃編譯統計資料。|  
|**initial_compile_start_time**|**datetimeoffset**|規劃編譯統計資料。|  
|**last_compile_start_time**|**datetimeoffset**|規劃編譯統計資料。|  
|**last_execution_time**|**datetimeoffset**|上次執行時間的最後一個參考查詢計畫結束的時間。|  
|**avg_compile_duration**|**float**|規劃編譯統計資料。|  
|**last_compile_duration**|**bigint**|規劃編譯統計資料。|  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [sys.database_query_store_options &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_query &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查詢存放區預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
