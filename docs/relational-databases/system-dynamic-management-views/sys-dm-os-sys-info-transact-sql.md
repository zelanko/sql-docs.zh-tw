---
title: sys.databases dm_os_sys_info （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d4e624323c2794afc38a9d8dcf948db69282af0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827915"
---
# <a name="sysdm_os_sys_info-transact-sql"></a>sys.dm_os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  傳回有關電腦以及有關 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 可用和耗用資源的其他有用資訊。  
  
> **注意：** 若要從或呼叫此 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，請使用**dm_pdw_nodes_os_sys_info**的名稱。  
  
|資料行名稱|資料類型|描述和版本特定的附注 |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|指定目前的 CPU 滴答計數。 CPU 滴答數是從處理器的 RDTSC 計數器取得。 它是一個單純遞增的數字。 不可為 Null。|  
|**ms_ticks**|**bigint**|指定自電腦啟動之後的毫秒數。 不可為 Null。|  
|**cpu_count**|**int**|指定系統上的邏輯 CPU 數目。 不可為 Null。|  
|**hyperthread_ratio**|**int**|指定單一實體處理器封裝所公開的邏輯或實體核心數目比率。 不可為 Null。|  
|**physical_memory_in_bytes**|**bigint**|**適用物件：** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。<br /><br /> 指定電腦上實體記憶體的總數。 不可為 Null。|  
|**physical_memory_kb**|**bigint**|**適用物件：** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更新版本。<br /><br /> 指定電腦上實體記憶體的總數。 不可為 Null。|  
|**virtual_memory_in_bytes**|**bigint**|**適用物件：** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。<br /><br /> 使用者模式之處理序可用的虛擬記憶體數量。 這可用來判斷 SQL Server 是否藉由使用 3-GB 參數來啟動。|  
|**virtual_memory_kb**|**bigint**|**適用物件：** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更新版本。<br /><br /> 指定使用者模式之處理序可用的虛擬位址空間總數。 不可為 Null。|  
|**bpool_commited**|**int**|**適用物件：** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。<br /><br /> 代表記憶體管理員中已認可的記憶體 (KB)。 不包含記憶體管理員中的保留記憶體。 不可為 Null。|  
|**committed_kb**|**int**|**適用物件：** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更新版本。<br /><br /> 代表記憶體管理員中已認可的記憶體 (KB)。 不包含記憶體管理員中的保留記憶體。 不可為 Null。|  
|**bpool_commit_target**|**int**|**適用物件：** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。<br /><br /> 代表可由 SQL Server 記憶體管理員耗用的記憶體數量 (KB)。|  
|**committed_target_kb**|**int**|**適用物件：** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更新版本。<br /><br /> 代表可由 SQL Server 記憶體管理員耗用的記憶體數量 (KB)。 目標數量是透過各種輸入來計算，例如：<br /><br /> -系統的目前狀態，包括其負載<br /><br /> -目前進程所要求的記憶體<br /><br /> -電腦上安裝的記憶體數量<br /><br /> -設定參數<br /><br /> 如果**committed_target_kb**大於**committed_kb**，記憶體管理員會嘗試取得額外的記憶體。 如果**committed_target_kb**小於**committed_kb**，記憶體管理員會嘗試壓縮已認可的記憶體數量。 **Committed_target_kb**一定會包含遭竊和保留的記憶體。 不可為 Null。|  
|**bpool_visible**|**int**|**適用物件：** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。<br /><br /> 緩衝集區中可以直接在處理虛擬位址空間中存取的 8 KB 緩衝區數目。 如果沒有使用 Address Windowing Extensions (AWE)，則當緩衝集區已經取得記憶體目標量 (bpool_committed = bpool_commit_target) 時，bpool_visible 的值等於 bpool_committed 的值。在 SQL Server 的 32 位元版本上使用 AWE 時，bpool_visible 代表用來存取緩衝集區所配置之實體記憶體的 AWE 對應視窗大小。 這個對應視窗的大小將由處理位址空間界定，因此可見量會比認可量小，而且還可能因為內部元件為了資料庫頁面以外的用途耗用記憶體而進一步減少。 如果 bpool_visible 的值太小，可能會接到記憶體不足的錯誤。|  
|**visible_target_kb**|**int**|**適用物件：** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更新版本。<br /><br /> 與**committed_target_kb**相同。 不可為 Null。|  
|**stack_size_in_bytes**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立之每一個執行緒的呼叫堆疊大小。 不可為 Null。|  
|**os_quantum**|**bigint**|代表非先佔式工作的配量 (以毫秒為單位)。 量子（以秒為單位） = **os_quantum** /CPU 頻率速度。 不可為 Null。|  
|**os_error_mode**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序的錯誤模式。 不可為 Null。|  
|**os_priority_class**|**int**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序的優先權類別。 可為 Null。<br /><br /> 32 = 一般 (錯誤記錄檔指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在以一般優先權基底 (=7) 啟動)。<br /><br /> 128 = 高 (錯誤記錄檔指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在以高優先權基底   (=13) 執行)。<br /><br /> 如需詳細資訊，請參閱 [設定 priority boost 伺服器組態選項](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)。|  
|**max_workers_count**|**int**|代表可建立的工作者數目上限。 不可為 Null。|  
|**scheduler_count**|**int**|代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中設定的使用者排程器數目。 不可為 Null。|  
|**scheduler_total_count**|**int**|代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的排程器總數。 不可為 Null。|  
|**deadlock_monitor_serial_number**|**int**|指定目前死結監視順序的識別碼。 不可為 Null。|  
|**sqlserver_start_time_ms_ticks**|**bigint**|代表**ms_tick** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上一次啟動時的 ms_tick 數位。 與目前的 ms_ticks 資料行比較。 不可為 Null。|  
|**sqlserver_start_time**|**datetime**|指定上一次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的日期和時間。 不可為 Null。|  
|**affinity_type**|**int**|**適用物件：** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更新版本。<br /><br /> 指定目前使用中伺服器 CPU 處理序相似性的類型。 不可為 Null。 如需詳細資訊，請參閱[ALTER SERVER CONFIGURATION &#40;transact-sql&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)。<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**適用物件：** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更新版本。<br /><br /> 描述**affinity_type**資料行。 不可為 Null。<br /><br /> MANUAL = 已經至少為一個 CPU 設定相似性。<br /><br /> AUTO = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以自由地在 CPU 之間移動執行緒。|  
|**process_kernel_time_ms**|**bigint**|**適用物件：** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更新版本。<br /><br /> 核心模式中所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒所使用的總時間，以毫秒為單位。 因為這個值包含伺服器上所有處理器的時間，所以它可能會大於單一處理器時脈。 不可為 Null。|  
|**process_user_time_ms**|**bigint**|**適用物件：** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更新版本。<br /><br /> 使用者模式中所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行緒所使用的總時間，以毫秒為單位。 因為這個值包含伺服器上所有處理器的時間，所以它可能會大於單一處理器時脈。 不可為 Null。|  
|**time_source**|**int**|**適用物件：** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更新版本。<br /><br /> 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用於擷取時鐘時間的 API。 不可為 Null。<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar(60)**|**適用物件：** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更新版本。<br /><br /> 描述**time_source**資料行。 不可為 Null。<br /><br /> QUERY_PERFORMANCE_COUNTER = [QueryPerformanceCounter](https://go.microsoft.com/fwlink/?LinkId=163095) API 會抓取時鐘時間。<br /><br /> MULTIMEDIA_TIMER = 用來抓取時鐘時間的[多媒體計時器](https://go.microsoft.com/fwlink/?LinkId=163094)API。|  
|**virtual_machine_type**|**int**|**適用物件：** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更新版本。<br /><br /> 指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否在虛擬化環境中執行。  不可為 Null。<br /><br /> 0 = NONE<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar(60)**|**適用物件：** [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和更新版本。<br /><br /> 描述**virtual_machine_type**資料行。 不可為 Null。<br /><br /> NONE = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不是在虛擬機器內執行。<br /><br /> 在執行虛擬機器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OS （採用硬體輔助虛擬化的主機 OS）內部，執行程式管理者（virtual machine）中會執行「虛擬機器」。<br /><br /> OTHER = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是在不採用硬體助理（例如 Microsoft VIRTUAL PC）的 OS 所裝載的虛擬機器內執行。|  
|**softnuma_configuration**|**int**|**適用物件：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]和更新版本。<br /><br /> 指定 NUMA 節點的設定方式。 不可為 Null。<br /><br /> 0 = 關閉表示硬體預設值<br /><br /> 1 = 自動軟體 NUMA<br /><br /> 2 = 透過登錄手動軟體 NUMA|  
|**softnuma_configuration_desc**|**nvarchar(60)**|**適用物件：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]和更新版本。<br /><br /> OFF = 軟 NUMA 功能已關閉<br /><br /> ON = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自動決定軟體 numa 的 numa 節點大小<br /><br /> MANUAL = 手動設定的軟體 NUMA|
|**process_physical_affinity**|**Nvarchar （3072）** |**適用物件：** 從開始 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 。<br /><br />尚未推出的資訊。 |
|**sql_memory_model**|**int**|**適用物件：** [!INCLUDE[sssql11](../../includes/sssql11-md.md)]SP4、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 和更新版本。<br /><br />指定用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來配置記憶體的記憶體模型。 不可為 Null。<br /><br />1 = 傳統記憶體模型<br />2 = 鎖定記憶體中的分頁<br /> 3 = 記憶體中的大型分頁|
|**sql_memory_model_desc**|**nvarchar(120)**|**適用物件：** [!INCLUDE[sssql11](../../includes/sssql11-md.md)]SP4、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 和更新版本。<br /><br />指定用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來配置記憶體的記憶體模型。 不可為 Null。<br /><br />**CONVENTIONAL**  =  傳統 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用傳統記憶體模型來配置記憶體。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶在啟動期間沒有鎖定記憶體中的分頁許可權時，這是預設的 sql 記憶體模型。<br />**LOCK_PAGES**  =  LOCK_PAGES [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用鎖定記憶體中的分頁來配置記憶體。 當 SQL Server 服務帳戶在 SQL Server 啟動期間擁有 [鎖定記憶體中的分頁] 許可權時，這就是預設的 sql 記憶體管理員。<br /> **LARGE_PAGES**  =  LARGE_PAGES [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在記憶體中使用大型分頁來配置記憶體。 SQL Server 使用大型頁面配置器，只 SQL Server 在伺服器啟動期間和追蹤旗標834開啟時，將記憶體配置給 Enterprise edition。|
|**pdw_node_id**|**int**|**適用于：** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
|**socket_count** |**int** | **適用物件：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和更新版本。<br /><br />指定系統上可用的處理器通訊端數目。 |  
|**cores_per_socket** |**int** | **適用物件：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和更新版本。<br /><br />指定系統上每個通訊端可用的處理器數目。 |  
|**numa_node_count** |**int** | **適用物件：** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP2 和更新版本。<br /><br />指定系統上可用的 numa 節點數目。 此資料行包含實體 numa 節點和軟性 numa 節點。 |  
  
## <a name="permissions"></a>權限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="see-also"></a>另請參閱  
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



