---
title: sys.dm_exec_query_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_stats_TSQL
- dm_exec_query_stats
- sys.dm_exec_query_stats
- sys.dm_exec_query_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_stats dynamic management view
ms.assetid: eb7b58b8-3508-4114-97c2-d877bcb12964
caps.latest.revision: 64
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: a5ad810ae111ce25311510a545f61915891f4e27
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmexecquerystats-transact-sql"></a>sys.dm_exec_query_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回的快取的查詢計畫中的彙總效能統計資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在此檢視中，快取計畫內的每個查詢陳述式各包含一個資料列，而資料列的存留期取決於計畫本身。 從快取移除計畫時，對應的資料列也會從這個檢視中刪除。  
  
> [!NOTE]
> 初始查詢**sys.dm_exec_query_stats**工作負載正在執行伺服器上是否可能會產生不正確的結果。 您可以重複執行查詢，以找出較精確的結果。  
  
> [!NOTE]
> 若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_exec_query_stats**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary(64)**  |這是指查詢所屬批次或預存程序的 Token。<br /><br /> **sql_handle**搭配**statement_start_offset**和**statement_end_offset**，可用來擷取查詢的 SQL 文字，藉由呼叫**sys.dm_exec_sql_文字**動態管理函數。|  
|**statement_start_offset**|**int**|表示資料列於其批次或保存物件的文字中所描述之查詢的起始位置 (由 0 開始並以位元組為單位)。|  
|**statement_end_offset**|**int**|表示資料列於其批次或保存物件的文字中所描述之查詢的結束位置 (由 0 開始並以位元組為單位)。 之前的版本[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，值為-1 表示批次的結尾。 已不再包含尾端的註解。|  
|**plan_generation_num**|**bigint**|可用於重新編譯之後區分計畫執行個體的序號。|  
|**plan_handle**|**varbinary(64)**|指查詢所屬編譯計畫的 Token。 此值可以傳遞至[sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)動態管理函數來取得查詢計畫。<br /><br /> 當原生編譯的預存程序查詢記憶體最佳化的資料表時，一律為 0x000。|  
|**creation_time**|**datetime**|計畫的編譯時間。|  
|**last_execution_time**|**datetime**|上次開始執行計畫的時間。|  
|**execution_count**|**bigint**|計畫從上次編譯以來被執行的次數。|  
|**total_worker_time**|**bigint**|這個計畫從編譯以來執行所耗用的 CPU 時間總量 (以毫秒為單位來報告，但是精確度只到毫秒)。<br /><br /> 如果原生編譯預存程序執行數次的時間都少於 1 毫秒， **total_worker_time** 可能就不準確。|  
|**last_worker_time**|**bigint**|計畫上次執行所耗用的 CPU 時間 (以毫秒為單位來報告，但是精確度只到毫秒)。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|這個計畫在單次執行期間曾經耗用的最少 CPU 時間 (以毫秒為單位來報告，但是精確度只到毫秒)。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|這個計畫在單次執行期間曾經耗用的最多 CPU 時間 (以毫秒為單位來報告，但是精確度只到毫秒)。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|這個計畫在編譯以來執行所執行的實體讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_physical_reads**|**bigint**|計畫上次執行所執行的實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_physical_reads**|**bigint**|這個計畫在單次期間曾執行的最小實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_physical_reads**|**bigint**|這個計畫在單次執行期間曾執行的最大實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_writes**|**bigint**|這個計畫在編譯以來執行所執行的邏輯寫入總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_writes**|**bigint**|上次執行計畫時修改的緩衝集區頁數。 如果已修改頁面，則不會計算寫入。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_writes**|**bigint**|這個計畫在單次執行期間曾執行的最小邏輯寫入數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_writes**|**bigint**|這個計畫在單次執行期間曾執行的最大邏輯寫入數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_reads**|**bigint**|這個計畫在編譯以來執行所執行的邏輯讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_reads**|**bigint**|計畫上次執行所執行的邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_reads**|**bigint**|這個計畫在單次執行期間曾執行的最小邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_reads**|**bigint**|這個計畫在單次執行期間曾經執行的最大邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_clr_time**|**bigint**|時間 （毫秒） （，但是精確度只到毫秒） 物件內部耗用報告[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]通用語言執行平台 (CLR) 編譯以來執行此計劃的物件。 CLR 物件可以是預存程序、函數、觸發程序、類型和彙總。|  
|**last_clr_time**|**bigint**|時間 （毫秒） （但是精確度只到毫秒） 內部執行所耗用報告[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]這個計畫上次執行期間的 CLR 物件。 CLR 物件可以是預存程序、函數、觸發程序、類型和彙總。|  
|**min_clr_time**|**bigint**|這個計畫在單次執行期間於 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 物件內部曾經耗用的最少時間 (以毫秒為單位來報告，但是精確度只到毫秒)。 CLR 物件可以是預存程序、函數、觸發程序、類型和彙總。|  
|**max_clr_time**|**bigint**|這個計畫在單次執行期間於 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 物件內部曾經耗用的最多時間 (以毫秒為單位來報告，但是精確度只到毫秒)。 CLR 物件可以是預存程序、函數、觸發程序、類型和彙總。|  
|**total_elapsed_time**|**bigint**|這個計畫完成執行經歷的總時間 (以毫秒為單位來報告，但是精確度只到毫秒)。|  
|**last_elapsed_time**|**bigint**|這個計畫最近完成所經歷的時間 (以毫秒為單位來報告，但是精確度只到毫秒)。|  
|**min_elapsed_time**|**bigint**|這個計畫的任何一次完成執行所經歷的最少時間 (以毫秒為單位來報告，但是精確度只到毫秒)。|  
|**max_elapsed_time**|**bigint**|這個計畫的任何一次完成執行所經歷的最多時間 (以毫秒為單位來報告，但是精確度只到毫秒)。|  
|**query_hash**|**Binary(8)**|針對查詢所計算的二進位雜湊值，可用來識別含有類似邏輯的查詢。 您可以使用查詢雜湊判別只有常值不同之查詢的彙總資源使用狀況。|  
|**query_plan_hash**|**binary(8)**|從查詢執行計畫計算所得的二進位雜湊值將用於識別類似的查詢執行計畫。 您可以使用查詢計劃雜湊尋找具有類似執行計畫之查詢的累計成本。<br /><br /> 當原生編譯的預存程序查詢記憶體最佳化的資料表時，一律為 0x000。|  
|**total_rows**|**bigint**|查詢傳回的資料列總數。 不可為 null。<br /><br /> 當原生編譯的預存程序查詢記憶體最佳化的資料表時，一律為 0。|  
|**last_rows**|**bigint**|上次執行查詢時所傳回的資料列數目。 不可為 null。<br /><br /> 當原生編譯的預存程序查詢記憶體最佳化的資料表時，一律為 0。|  
|**min_rows**|**bigint**|在每次執行期間曾經查詢所傳回的資料列的最小數目。 不可為 null。<br /><br /> 當原生編譯的預存程序查詢記憶體最佳化的資料表時，一律為 0。|  
|**max_rows**|**bigint**|在每次執行期間曾經查詢所傳回的資料列的數目上限。 不可為 null。<br /><br /> 當原生編譯的預存程序查詢記憶體最佳化的資料表時，一律為 0。|  
|**statement_sql_handle**|**varbinary(64)**|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 非 NULL 值開啟查詢存放區時才擴展和收集該特定查詢的統計資料。|  
|**statement_context_id**|**bigint**|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 非 NULL 值開啟查詢存放區時才擴展和收集該特定查詢的統計資料。|  
|**total_dop**|**bigint**|平行處理原則程度的總和編譯以來使用此計畫。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_dop**|**bigint**|這個計畫執行上一次時平行處理原則的程度。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_dop**|**bigint**|最小的平行處理原則程度每次執行期間曾使用此計劃。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_dop**|**bigint**|平行處理原則的最大程度每次執行期間曾使用此計劃。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_grant_kb**|**bigint**|保留的記憶體總數量授編譯自所接收到此計劃與以 kb 為單位。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_grant_kb**|**bigint**|這個計畫執行上一次時，以 kb 為單位授與保留的記憶體數量。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_grant_kb**|**bigint**|最小保留的記憶體數量將授與 （kb） 每次執行期間曾經收到此計劃。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_grant_kb**|**bigint**|以 kb 為單位授予的保留記憶體的最大數量每次執行期間曾經收到此計劃。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_used_grant_kb**|**bigint**|保留的記憶體總數量將授與 （kb） 使用，因為它已編譯這個計畫。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_used_grant_kb**|**bigint**|以 kb 為單位，此計劃執行最後一次時使用的記憶體授與數量。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_used_grant_kb**|**bigint**|已用記憶體的最小數量將授與以 kb 為單位在每次執行期間用過此計劃。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_used_grant_kb**|**bigint**|已用記憶體的最大數量將授與以 kb 為單位在每次執行期間用過此計劃。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_ideal_grant_kb**|**bigint**|理想的記憶體授與此計劃估計的編譯以來的 KB 總數。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_ideal_grant_kb**|**bigint**|這個計畫執行上一次時，以 kb 為單位授與的理想記憶體數量。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_ideal_grant_kb**|**bigint**|以 kb 為單位，在每次執行期間曾經估計此計劃，授與的最小的理想記憶體數量。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_ideal_grant_kb**|**bigint**|以 kb 為單位，在每次執行期間曾經估計此計劃，授與最大的理想記憶體數量。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_reserved_threads**|**bigint**|總和的保留的平行執行緒曾經使用，因為它已編譯這個計畫。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_reserved_threads**|**bigint**|這個計畫執行上一次時的保留平行執行緒數目。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_reserved_threads**|**bigint**|最小的保留的平行執行緒數目每次執行期間曾使用此計劃。  它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_reserved_threads**|**bigint**|保留的平行的最大數目執行緒在每次執行期間用過此計劃。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_used_threads**|**bigint**|總計的總和會使用平行執行緒曾經使用，因為它已編譯這個計畫。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**last_used_threads**|**bigint**|這個計畫執行上一次時的使用平行執行緒數目。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**min_used_threads**|**bigint**|這個計劃用過一次執行期間使用的平行執行緒最小數目。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**max_used_threads**|**bigint**|這個計劃用過一次執行期間使用的平行執行緒的數目上限。 它一律是 0 的查詢記憶體最佳化的資料表。<br /><br /> **適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**total_columnstore_segment_reads**|**bigint**|查詢所讀取的資料行存放區區段總計的總和。 不可為 null。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**last_columnstore_segment_reads**|**bigint**|上次執行查詢所讀取的資料行存放區區段數目。 不可為 null。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**min_columnstore_segment_reads**|**bigint**|在每次執行期間曾經讀取查詢的資料行存放區區段最小數目。 不可為 null。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**max_columnstore_segment_reads**|**bigint**|在每次執行期間曾經讀取查詢的資料行存放區區段數目上限。 不可為 null。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**total_columnstore_segment_skips**|**bigint**|資料行存放區區段已略過查詢總計的總和。 不可為 null。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**last_columnstore_segment_skips**|**bigint**|已略過最後一個執行查詢的資料行存放區區段數目。 不可為 null。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**min_columnstore_segment_skips**|**bigint**|查詢每次執行期間曾經略過的資料行存放區區段的最小數目。 不可為 null。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|    
|**max_columnstore_segment_skips**|**bigint**|查詢每次執行期間曾經略過的資料行存放區區段數目上限。 不可為 null。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|
|**total_spills**|**bigint**|編譯以來執行此查詢所溢出的頁面總數。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**last_spills**|**bigint**|頁數溢出的上次執行查詢。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**min_spills**|**bigint**|此查詢曾有在單次執行期間溢出的頁面最小數目。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**max_spills**|**bigint**|此查詢曾有在單次執行期間溢出的頁面的數目上限。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**pdw_node_id**|**int**|此發行版本上的節點識別碼。<br /><br /> **適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 

> [!NOTE]
> <sup>1</sup>原生編譯的預存程序啟用統計資料收集時，會收集的工作者時間以毫秒為單位。 如果查詢的執行少於一毫秒，值將會是 0。  
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
   
## <a name="remarks"></a>備註  
 完成查詢時，會更新檢視中的統計資料。  
  
## <a name="examples"></a>範例  
  
### <a name="a-finding-the-top-n-queries"></a>A. 尋找 TOP N 查詢  
 下列範例會傳回平均 CPU 時間之前五項查詢的相關資訊。 這個範例會根據查詢雜湊彙總查詢，以便依據累計資源耗用量分組邏輯對等查詢。  
  
```sql  
SELECT TOP 5 query_stats.query_hash AS "Query Hash",   
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",  
    MIN(query_stats.statement_text) AS "Statement Text"  
FROM   
    (SELECT QS.*,   
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,  
    ((CASE statement_end_offset   
        WHEN -1 THEN DATALENGTH(ST.text)  
        ELSE QS.statement_end_offset END   
            - QS.statement_start_offset)/2) + 1) AS statement_text  
     FROM sys.dm_exec_query_stats AS QS  
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats  
GROUP BY query_stats.query_hash  
ORDER BY 2 DESC;  
```  
  
### <a name="b-returning-row-count-aggregates-for-a-query"></a>B. 傳回查詢的資料列計數彙總  
 下列範例會傳回查詢的資料列計數彙總資訊 (資料列總數、最小資料列數目、最大資料列數目及上次傳回的資料列數目)。  
  
```sql  
SELECT qs.execution_count,  
    SUBSTRING(qt.text,qs.statement_start_offset/2 +1,   
                 (CASE WHEN qs.statement_end_offset = -1   
                       THEN LEN(CONVERT(nvarchar(max), qt.text)) * 2   
                       ELSE qs.statement_end_offset end -  
                            qs.statement_start_offset  
                 )/2  
             ) AS query_text,   
     qt.dbid, dbname= DB_NAME (qt.dbid), qt.objectid,   
     qs.total_rows, qs.last_rows, qs.min_rows, qs.max_rows  
FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS qt   
WHERE qt.text like '%SELECT%'   
ORDER BY qs.execution_count DESC;  
```  
  
## <a name="see-also"></a>另請參閱  
[執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)    
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)    
[sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)    
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)     
[sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)     
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)    
  


