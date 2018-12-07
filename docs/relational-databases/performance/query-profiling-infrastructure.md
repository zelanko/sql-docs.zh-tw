---
title: 查詢分析基礎結構 | Microsoft Docs
ms.custom: ''
ms.date: 11/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual - "query plans [SQL Server]" - "execution plans [SQL Server]" - "query profiling" - "lightweight query profiling" - "lightweight profiling" - "lwp"
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: e0ee0bc2c99d997d6a44d5ca0e9944e0ae4bfeb3
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617248"
---
# <a name="query-profiling-infrastructure"></a>查詢分析基礎結構
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 讓您能夠存取有關查詢執行計畫的執行階段資訊。 發生效能問題時最重要的動作之一，是準確地了解正在執行的工作負載以及衍生資源使用量的方式。 基於此因素，存取[實際執行計畫](../../relational-databases/performance/display-an-actual-execution-plan.md)就很重要。

儘管完成查詢是取得實際查詢計畫可用性的必要條件，當資料從[查詢計畫運算子](../../relational-databases/showplan-logical-and-physical-operators-reference.md)流到另一個運算子時，[即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)可以提供查詢執行程序的即時深入解析。 即時查詢計畫會顯示整體的查詢進度，以及運算子層級的執行階段執行統計資料，如產生的資料列數目、耗用時間、運算子進度等等。因為此資料會即時提供，不需等待查詢完成，所以，這些執行統計資料在偵錯查詢效能問題方面非常有用，例如，長時間執行查詢，以及無限期執行且永遠不會完成的查詢。

## <a name="the-standard-query-execution-statistics-profiling-infrastructure"></a>標準查詢執行統計資料分析基礎結構

「查詢執行統計資料分析基礎結構」 (或標準分析) 必須啟用，才能收集執行計畫的相關資訊，也就是資料列計數、CPU 和 I/O 使用量。 下列針對**目標工作階段**收集執行計畫資訊的方法會利用標準分析基礎結構：

- [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md) 
- [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)
- [即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)

> [!NOTE]
> 搭配 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 使用即時查詢統計資料，會利用標準分析基礎結構。    
> 在更新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果啟用了[輕量型分析基礎結構](#lwp)，則即時查詢統計資料就會利用它而非標準分析。

下列針對**所有工作階段**全域收集執行計畫資訊的方法，會利用標準分析基礎結構：

-  ***query_post_execution_showplan*** 擴充事件。 若要啟用擴充事件，請參閱 [使用擴充事件監視系統活動](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。  
- [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)和 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md) 中的 **Showplan XML** 追蹤事件。 如需此追蹤事件的詳細資訊，請參閱 [Showplan XML 事件類別](../../relational-databases/event-classes/showplan-xml-event-class.md)。

執行擴充事件工作階段以使用 *query_post_execution_showplan* 事件時，接著也會填入 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV，其會使用[活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)或直接查詢 DMV，針對所有工作階段啟用即時查詢統計資料。 如需相關資訊，請參閱 [Live Query Statistics](../../relational-databases/performance/live-query-statistics.md)。

## <a name="lwp"></a> 輕量型查詢執行統計資料分析基礎結構

從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，引進了新的*輕量型查詢執行統計資料分析基礎結構* (或**輕量型分析**)。 

> [!NOTE]
> 輕量型分析不支援原生編譯的預存程序。  

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v1"></a>輕量型查詢執行統計資料分析基礎結構 v1

**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 至 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])。 
  
從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，已藉由引進輕量型分析來降低收集執行計畫相關資訊的效能額外負荷。 不同於標準分析，輕量型分析不會收集 CPU 執行階段資訊。 不過，輕量型分析仍會收集資料列計數和 I/O 使用量資訊。

同時，也引進了新的 ***query_thread_profile*** 擴充事件來利用輕量型分析。 此擴充事件會公開每個運算子執行統計資料，以便更深入了解每個節點和執行緒的效能。 您可以設定使用此擴充事件的範例工作階段，如下列範例所示：

```sql
CREATE EVENT SESSION [NodePerfStats] ON SERVER
ADD EVENT sqlserver.query_thread_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

> [!NOTE]
> 如需查詢分析的效能額外負荷詳細資訊，請參閱部落格文章[開發人員選擇：查詢進度 - 隨時隨地](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/) \(英文\)。 

執行擴充事件工作階段以使用 *query_thread_profile* 事件時，接著也會使用輕量型分析填入 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV，其會使用[活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)或直接查詢 DMV，針對所有工作階段啟用即時查詢統計資料。

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v2"></a>輕量型查詢執行統計資料分析基礎結構 v2

**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 至 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])。 

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 包含額外負荷最低的輕量型分析修訂版。 針對上方「適用於」中所述的版本，也可以使用[追蹤旗標 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 全域啟用輕量型分析。 已引進新的 DMF [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)，針對進行中的要求傳回查詢執行計畫。

從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11 開始，如果未全域啟用輕量型分析，則可使用新的 [USE HINT 查詢提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)引數 **QUERY_PLAN_PROFILE**，針對任何工作階段啟用查詢層級的輕量型分析。 當包含這個新提示的查詢完成時，也會輸出新的 ***query_plan_profile*** 擴充事件，以提供類似 *query_post_execution_showplan* 擴充事件的實際執行計畫 XML。 您可以設定使用此擴充事件的範例工作階段，如下列範例所示：

```sql
CREATE EVENT SESSION [PerfStats_LWP_Plan] ON SERVER
ADD EVENT sqlserver.query_plan_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v3"></a>輕量型查詢執行統計資料分析基礎結構 v3

**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 起)

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 包含最新修訂的輕量型分析版本，可收集所有執行的資料列計數資訊。 輕量型分析預設會在 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 上啟用，而追蹤旗標 7412 不會有任何作用。

## <a name="remarks"></a>Remarks

> [!IMPORTANT]
> 由於執行參考 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) 的監視預存程序時可能會產生隨機 AV，因而請確保會在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 中安裝 [KB 4078596](http://support.microsoft.com/help/4078596)。

從輕量型分析 v2 及其低額外負荷開始，尚未受限於 CPU 的任何伺服器都可**持續**執行輕量型分析，並讓資料庫專業人員可隨時點選任何執行中的執行 (例如，使用活動監視器，或直接查詢 `sys.dm_exec_query_profiles`)，並取得含執行階段統計資料的查詢計畫。

如需查詢分析的效能額外負荷詳細資訊，請參閱部落格文章[開發人員選擇：查詢進度 - 隨時隨地](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/) \(英文\)。 

## <a name="see-also"></a>另請參閱  
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [效能監視及微調工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [開啟活動監視器 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)     
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [使用擴充事件監視系統活動](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)      
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [執行程序邏輯和實體運算子參考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
 [實際執行計畫](../../relational-databases/performance/display-an-actual-execution-plan.md)    
 [即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)      
 [開發人員選擇：查詢進度 - 隨時隨地](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/)
