---
title: sys.dm_os_sys_info (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
caps.latest.revision: 57
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9a6b6cb757e2944df8a0e50e6e63a1f58cedda11
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="sysdmossysinfo-transact-sql"></a>sys.dm_os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  傳回有關電腦以及有關 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 可用和耗用資源的其他有用資訊。  
  
> **注意：**呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_sys_info**。  
  
|資料行名稱|資料類型|描述與特定版本資訊 |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|指定目前的 CPU 滴答計數。 CPU 滴答數是從處理器的 RDTSC 計數器取得。 它是一個單純遞增的數字。 不可為 Null。|  
|**ms_ticks**|**bigint**|指定自電腦啟動之後的毫秒數。 不可為 Null。|  
|**cpu_count**|**int**|指定系統上的邏輯 CPU 數目。 不可為 Null。|  
|**hyperthread_ratio**|**int**|指定單一實體處理器封裝所公開的邏輯或實體核心數目比率。 不可為 Null。|  
|**physical_memory_in_bytes**|**bigint**|**適用於：**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 指定電腦上實體記憶體的總數。 不可為 Null。|  
|**physical_memory_kb**|**bigint**|**適用於：**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定電腦上實體記憶體的總數。 不可為 Null。|  
|**virtual_memory_in_bytes**|**bigint**|**適用於：**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 使用者模式之處理序可用的虛擬記憶體數量。 這可用來判斷 SQL Server 是否藉由使用 3-GB 參數來啟動。|  
|**virtual_memory_kb**|**bigint**|**適用於：**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定使用者模式之處理序可用的虛擬位址空間總數。 不可為 Null。|  
|**bpool_commited**|**int**|**適用於：**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 代表記憶體管理員中已認可的記憶體 (KB)。 不包含記憶體管理員中的保留記憶體。 不可為 Null。|  
|**committed_kb**|**int**|**適用於：**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 代表記憶體管理員中已認可的記憶體 (KB)。 不包含記憶體管理員中的保留記憶體。 不可為 Null。|  
|**bpool_commit_target**|**int**|**適用於：**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 代表可由 SQL Server 記憶體管理員耗用的記憶體數量 (KB)。|  
|**committed_target_kb**|**int**|**適用於：**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 代表可由 SQL Server 記憶體管理員耗用的記憶體數量 (KB)。 目標數量是透過各種輸入來計算，例如：<br /><br /> -目前的狀態，包括其負載的系統<br /><br /> -目前的程序所要求的記憶體<br /><br /> -電腦上安裝的記憶體數量<br /><br /> -設定參數<br /><br /> 如果**committed_target_kb**大於**committed_kb**，記憶體管理員會嘗試取得額外的記憶體。 如果**committed_target_kb**小於**committed_kb**，記憶體管理員會嘗試壓縮已認可的記憶體數量。 **Committed_target_kb**一定會包含遭奪取和保留記憶體。 不可為 Null。|  
|**bpool_visible**|**int**|**適用於：**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 緩衝集區中可以直接在處理虛擬位址空間中存取的 8 KB 緩衝區數目。 如果沒有使用 Address Windowing Extensions (AWE)，則當緩衝集區已經取得記憶體目標量 (bpool_committed = bpool_commit_target) 時，bpool_visible 的值等於 bpool_committed 的值。在 SQL Server 的 32 位元版本上使用 AWE 時，bpool_visible 代表用來存取緩衝集區所配置之實體記憶體的 AWE 對應視窗大小。 這個對應視窗的大小將由處理位址空間界定，因此可見量會比認可量小，而且還可能因為內部元件為了資料庫頁面以外的用途耗用記憶體而進一步減少。 如果 bpool_visible 的值太小，可能會接到記憶體不足的錯誤。|  
|**visible_target_kb**|**int**|**適用於：**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 等同於**committed_target_kb**。 不可為 Null。|  
|**stack_size_in_bytes**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立之每一個執行緒的呼叫堆疊大小。 不可為 Null。|  
|**os_quantum**|**bigint**|代表非先佔式工作的配量 (以毫秒為單位)。 配量 （以秒為單位） = **os_quantum** / CPU 時脈速度。 不可為 Null。|  
|**os_error_mode**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序的錯誤模式。 不可為 Null。|  
|**os_priority_class**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序的優先權類別。 可為 Null。<br /><br /> 32 = 一般 (錯誤記錄檔指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在以一般優先權基底 (=7) 啟動)。<br /><br /> 128 = 高 (錯誤記錄檔指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在以高優先權基底   (=13) 執行)。<br /><br /> 如需詳細資訊，請參閱 [設定 priority boost 伺服器組態選項](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)。|  
|**max_workers_count**|**int**|代表可建立的工作者數目上限。 不可為 Null。|  
|**scheduler_count**|**int**|代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中設定的使用者排程器數目。 不可為 Null。|  
|**scheduler_total_count**|**int**|代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的排程器總數。 不可為 Null。|  
|**deadlock_monitor_serial_number**|**int**|指定目前死結監視順序的識別碼。 不可為 Null。|  
|**sqlserver_start_time_ms_ticks**|**bigint**|代表**ms_tick**數目時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上次啟動。 與目前的 ms_ticks 資料行比較。 不可為 Null。|  
|**sqlserver_start_time**|**datetime**|指定上一次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的日期和時間。 不可為 Null。|  
|**affinity_type**|**int**|**適用於：**[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定目前使用中伺服器 CPU 處理序相似性的類型。 不可為 Null。 如需詳細資訊，請參閱[ALTER SERVER CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)。<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**適用於：**[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 描述**affinity_type**資料行。 不可為 Null。<br /><br /> MANUAL = 已經至少為一個 CPU 設定相似性。<br /><br /> AUTO = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以自由地在 CPU 之間移動執行緒。|  
|**process_kernel_time_ms**|**bigint**|**適用於：**[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 核心模式中所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒所使用的總時間，以毫秒為單位。 因為這個值包含伺服器上所有處理器的時間，所以它可能會大於單一處理器時脈。 不可為 Null。|  
|**process_user_time_ms**|**bigint**|**適用於：**[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 使用者模式中所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒所使用的總時間，以毫秒為單位。 因為這個值包含伺服器上所有處理器的時間，所以它可能會大於單一處理器時脈。 不可為 Null。|  
|**time_source**|**int**|**適用於：**[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用於擷取時鐘時間的 API。 不可為 Null。<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar(60)**|**適用於：**[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 描述**time_source**資料行。 不可為 Null。<br /><br /> QUERY_PERFORMANCE_COUNTER = [QueryPerformanceCounter](http://go.microsoft.com/fwlink/?LinkId=163095) API 會擷取時鐘時間。<br /><br /> MULTIMEDIA_TIMER =[多媒體計時器](http://go.microsoft.com/fwlink/?LinkId=163094)擷取時鐘時間的 API。|  
|**virtual_machine_type**|**int**|**適用於：**[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否在虛擬化環境中執行。  不可為 Null。<br /><br /> 0 = NONE<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar(60)**|**適用於：**[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 描述**virtual_machine_type**資料行。 不可為 Null。<br /><br /> NONE =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並未在虛擬機器內執行。<br /><br /> HYPERVISOR = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行於 Hypervisor 內部，也就是硬體輔助虛擬化。 安裝 Hyper_V 角色時，Hypervisor 會裝載作業系統，以便在主機作業系統上執行的執行個體會在 Hypervisor 中執行。<br /><br /> OTHER = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行於沒有採用硬體助理的虛擬機器內部，例如 Microsoft Virtual PC。|  
|**softnuma_configuration**|**int**|**適用於：**[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定已設定的方式 NUMA 節點。 不可為 Null。<br /><br /> 0 = OFF 指出硬體預設值<br /><br /> 1 = 自動軟體 NUMA<br /><br /> 2 = 透過登錄的手動軟體 NUMA|  
|**softnuma_configuration_desc**|**nvarchar(60)**|**適用於：**[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> OFF = NUMA 功能是關閉<br /><br /> 在 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NUMA 會自動決定 NUMA 節點大小<br /><br /> 手動 = 手動設定的軟體 NUMA|
|**process_physical_affinity**|**nvarchar(3072)** |**適用於：**開頭[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]。<br /><br />尚未將於提供的資訊。 |
|**sql_memory_model**|**int**|**適用於：** [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br />指定所使用的記憶體模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置記憶體。 不可為 Null。<br /><br />1 = 傳統記憶體模型<br />2 = 鎖定記憶體分頁<br /> 3 = 記憶體中的大型分頁|
|**sql_memory_model_desc**|**nvarchar(120)**|**適用於：** [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br />指定所使用的記憶體模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置記憶體。 不可為 Null。<br /><br />**傳統** =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置的記憶體使用傳統記憶體模式。 這是預設 sql 記憶體模型時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶中並沒有鎖定的分頁記憶體的權限在啟動期間。<br />**LOCK_PAGES**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用鎖定分頁記憶體中配置記憶體。 SQL Server 服務帳戶在 SQL Server 啟動期間記憶體的權限擁有鎖定的分頁時，這是預設 sql 記憶體管理員。<br /> **LARGE_PAGES**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用大型分頁記憶體中配置記憶體。 SQL Server 會使用大型分頁配置器配置記憶體，只能使用 Enterprise edition 時 SQL Server 服務帳戶會持有記憶體的權限鎖定分頁在伺服器啟動期間與追蹤旗標 834 已開啟。|
|**pdw_node_id**|**int**|**適用於：** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
|**socket_count** |**int** | **適用於：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 至[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br />在系統上指定可用的處理器插槽的數目。 |  
|**cores_per_socket** |**int** | **適用於：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 至[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br />指定系統上的每個通訊端可用的處理器數目。 |  
|**numa_node_count** |**int** | **適用於：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 至[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br />指定系統上的可用的 numa 節點數目。 此資料行包含實體 numa 節點，以及軟體 numa 節點。 |  
  
## <a name="permissions"></a>Permissions

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



