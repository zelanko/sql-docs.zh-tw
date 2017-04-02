---
title: "SQL Server R services Dmv | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# SQL Server R services Dmv

本主題列出系統目錄檢視和相關的 Dmv [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]。 


擴充事件的相關資訊，請參閱 [擴充的事件，適用於 SQL Server R Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)。

> [!TIP]
> 產品小組提供了可用來監視 R 服務工作階段和封裝的自訂報表。 如需詳細資訊，請參閱 [監視 R 服務在 Management Studio 中使用自訂報告](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)。
> 

## <a name="system-configuration-and-system-resources"></a>系統組態和系統資源

您可以監視和分析使用 R 指令碼所使用的資源 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 系統目錄檢視和 Dmv。


**一般**
+ [ sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  傳回使用者連接和系統工作階段的資訊。 您可以藉由查看識別系統工作階段 *session_id* 資料行; 值大於或等於 51 都是使用者連接，而值超過 51 為系統處理程序。 



+ [sys.dm_os_performance_counters (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  傳回伺服器正在使用的每個系統效能計數器的資料列。  您可以使用這項資訊以查看多少指令碼執行時，使用的驗證模式，或多少個 R 呼叫所發出的整體的執行個體上執行的指令碼。

  這個範例會取得只將 R 指令碼與相關的計數器︰

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%Extended Scripts%'
  ```

  此 DMV 的每個執行個體的外部指令碼所報告的下列計數器︰

  + **總執行**: R 程序啟動的本機或遠端呼叫
  + **平行執行**︰ 包含指令碼的次數 @parallel 規格， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 能夠產生並使用平行查詢計畫
  + **資料流執行**︰ 已叫用的串流處理功能的次數。 
  + **SQL 副本執行**︰ 數字的 R 指令碼執行位置呼叫具現化時從遠端與 SQL Server 做為計算內容 
  + **隱含 auth]。登入**︰ 所使用的 ODBC 回送呼叫次數隱含驗證; 也就是說， [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行代表指令碼要求傳送的使用者呼叫
  + **總執行時間 （毫秒）**︰ 呼叫和完成呼叫之間經過的時間。
  + **執行錯誤**︰ 的指令碼會報告錯誤的次數。 這個計數不包含 R 的錯誤。


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  此 DMV 報告每個背景工作帳戶目前正在執行外部指令碼的單一資料列。 請注意，此工作的帳戶不同的認證傳送指令碼的人員。 如果單一的 Windows 使用者會傳送多個指令碼要求，則會以處理來自該使用者的所有要求指派只有一個背景工作帳戶。 如果不同的 Windows 使用者登入時執行外部指令碼，會由不同的背景工作帳戶處理要求。 
  這個 DMV 不會傳回任何結果如果目前正在不執行任何指令碼。因此，它是最適合監控長期執行的指令碼。 它會傳回這些值︰
  + **external_script_request_id**: GUID，它也會做為用來儲存指令碼和中繼結果的工作目錄的暫存名稱。  
  + **語言**︰ 值，例如 `R` 表示外部指令碼語言。
  + **degree_of_parallelism**︰ 整數，表示平行數目的處理序所使用。 
  + **external_user_name**︰ 啟動列背景工作帳戶，例如 SQLRUser01。 
  

+ [sys.dm_external_script_execution_stats (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  這個 DMV 提供內部監視 （遙測） 來追蹤多少 R 呼叫的執行個體上。 遙測服務啟動時 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 並呼叫特定的 R 函式每次增加磁碟的計數器。

  此計數器會遞增每個呼叫的函式。 例如，如果呼叫 `rxLinMod` 並以平行方式執行，此計數器會遞增 1。
  
  一般而言，只要產生效能計數器的處理序正在使用，效能計數器就會有效。 因此，DMV 上的查詢無法顯示已停止執行之服務的詳細資料。 例如，如果 [啟動列] 會建立多個平行的 R 工作，但是它們會非常快速地執行，並由 Windows 作業物件然後清除 DMV 可能不會顯示任何資料。
 
  不過，這個 DMV 所追蹤的計數器會保持執行，並且針對 dm_external_script _execution 計數器會保留以供使用寫入磁碟，即使執行個體已關閉狀態。
 
 如需有關所使用的系統效能計數器 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，請參閱 [使用 SQL Server 物件](../../relational-databases/performance-monitor/use-sql-server-objects.md)。

**資源管理員的檢視**

+ [sys.resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  傳回目前資源集區狀態的相關資訊、資源集區的目前組態和資源集區統計資料。

  > [!IMPORTANT]
  > 
  > 您必須修改套用至其他伺服器服務之前，您可以將其他資源配置給 R 服務的資源集區。


+ [sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  新的目錄檢視會顯示外部的資源集區目前的組態值。
  在 Enterprise 版本中，您可以設定其他外部的資源集區︰ 例如，您可能會決定處理 R 執行的工作的資源 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 分開這些是來自遠端用戶端。 

  > [!NOTE]
  > 
  > 標準版 R 的所有工作都都在相同的外部的預設資源集區中執行。

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  傳回工作負載群組統計資料和目前的工作負載群組設定。 這個檢視可以使用 sys.dm_resource_governor_resource_pools 加入，以取得資源集區名稱。
  為外部指令碼、 新的資料行已經加入，以顯示外部工作負載群組相關聯的集區識別碼。 


+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  新的系統目錄檢視，可讓您看到的處理器和特定的資源集區會相似化為的資源。

  針對 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中的每個排程器，各傳回一個資料列，其中每個排程器都會對應至個別的處理器。 請利用這份檢視來監視排程器的狀況或識別失控的工作。

  在預設組態中，工作負載的集區會自動指派給處理器，因此沒有傳回任何相似性值。

  同質排程對應的資源集區 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 給定識別碼所識別的排程。 這些識別碼對應至 sys.dm_os_schedulers (TRANSACT-SQL) 中 scheduler_id 資料行的值。


> [!NOTE] 
> 
> 雖然設定和自訂資源集區的功能僅適用於企業和開發人員版本、 預設集區，以及 Dmv 可用於所有版本。 因此，您可以使用這些 Dmv Standard Edition 中以判斷資源 cap R 工作。 

如需有關監視的一般資訊 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體，請參閱 [目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) 和 [資源管理員相關動態管理檢視](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。

## <a name="r-script-execution-and-monitoring"></a>R 指令碼執行和監視

指令碼中執行的 R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 啟動 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 介面。 不過，[啟動列] 不是資源控管或分割區分開監視，因為它會被假設為適當地管理資源的 Microsoft 所提供的安全服務。

Launchpad 服務下執行的個別 R 指令碼使用管理 [Windows 作業物件](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)。 工作物件可讓處理程序當做一個單位來管理群組。 每個工作物件是階層式，並控制與它相關聯的所有處理程序的屬性。 工作的物件上執行的作業會影響所有的工作物件相關聯的處理程序。 

因此，如果您需要終止與物件相關聯的一項工作，請注意所有相關的處理程序也會終止。 如果您正在執行 R 指令碼指派給 Windows 作業物件，該指令碼會執行相關的 ODBC 工作必須終止父 R 指令碼處理序也將會終止。 

如果您開始使用平行處理的 R 指令碼時，單一的 Windows 工作物件會管理所有平行子處理程序。

若要判斷處理程序是否正在執行中的工作，請使用 `IsProcessInJob` 函式。

## <a name="see-also"></a>另請參閱
[管理及監視](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

