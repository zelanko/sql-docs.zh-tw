---
title: 使用 DMV 監視指令碼
description: 使用動態管理檢視 (DMV) 來監視 SQL Server 機器學習服務中的 Python 與 R 外部指令碼執行。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/14/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 6d94fc2d85ac0012347cb55f4981a25ba107f5df
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92679213"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>使用動態管理檢視 (DMV) 來監視 SQL Server 機器學習服務
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

使用動態管理檢視 (DMV) 來監視 SQL Server 機器學習服務中的外部指令碼 (Python 與 R) 執行、使用的資源、診斷問題，以及調整 效能。

在此文章中，您會發現 DMV 是可供 SQL Server 機器學習服務使用的特定功能。 您也會發現範例查詢，其顯示：

+ 機器學習的進階設定與組態選項
+ 執行外部 Python 或指令碼的作用中工作階段
+ Python 與 R 的外部執行階段的執行統計資料
+ 外部指令碼的效能計數器
+ OS、SQL Server 與外部資源集區的記憶體使用量
+ SQL Server 與外部資源集區的記憶體設定
+ Resource Governor 資源集區，包括外部資源集區
+ Python 與 R 的已安裝套件

如需更多有關 DMV 的一般資訊，請參閱[系統動態管理檢視](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。

> [!TIP]
> 您也可以使用自訂報表來監視 SQL Server 機器學習服務。 如需詳細資訊，請參閱[在 Management Studio 中使用自訂報表來監視機器學習](monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)。

## <a name="dynamic-management-views"></a>動態管理檢視

在 SQL Server 中監視機器學習工作負載時，可以使用下列動態管理檢視。 若要查詢 DMV，您需要執行個體的 `VIEW SERVER STATE` 權限。

| 動態管理檢視 | 類型 | 描述 |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | 執行 | 逐資料列傳回正在執行外部指令碼的每個使用中背景工作帳戶。 |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | 執行 | 逐資料列傳回各種類型的外部指令碼要求。 |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | 執行 | 針對伺服器所維護的每個效能計數器，各傳回一個資料列。 若使用搜尋條件 `WHERE object_name LIKE '%External Scripts%'`，您可以使用此資訊來查看執行了多少指令碼、使用了哪些驗證模式來執行哪些指令碼，或在執行個體上總共發出了多少 R 或 Python 呼叫。 |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | 資源管理員 | 傳回 Resource Governor 中目前外部資源集區狀態的相關資訊、資源集區的目前組態和資源集區統計資料。 |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | 資源管理員 | 傳回 Resource Governor 中目前外部資源集區設定的 CPU 親和性資訊。 針對 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中的每個排程器，各傳回一個資料列，其中每個排程器都會對應至個別的處理器。 請利用這份檢視來監視排程器的狀況或識別失控的工作。 |

如需有關監視 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體的資訊，請參閱[目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)與 [Resource Governor 相關的動態管理檢視](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。

## <a name="settings-and-configuration"></a>設定與組態

請參閱機器學習服務安裝設定與組態選項。

![設定與組態查詢的輸出](media/dmv-settings-and-configuration.png "來自設定與組態查詢的輸出")

執行下面的查詢以取得此輸出。 如需所使用之檢視與函式的詳細資訊，請參閱 [sys.databases dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)、[sys.databases](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 與 [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)。

```sql
SELECT CAST(SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS INT) AS IsMLServicesInstalled
    , CAST(value_in_use AS INT) AS ExternalScriptsEnabled
    , COALESCE(SIGN(SUSER_ID(CONCAT (
                    CAST(SERVERPROPERTY('MachineName') AS NVARCHAR(128))
                    , '\SQLRUserGroup'
                    , CAST(serverproperty('InstanceName') AS NVARCHAR(128))
                    ))), 0) AS ImpliedAuthenticationEnabled
    , COALESCE((
            SELECT CAST(r.value_data AS INT)
            FROM sys.dm_server_registry AS r
            WHERE r.registry_key LIKE 'HKLM\Software\Microsoft\Microsoft SQL Server\%\SuperSocketNetLib\Tcp'
            AND r.value_name = 'Enabled'
            ), - 1) AS IsTcpEnabled
FROM sys.configurations
WHERE name = 'external scripts enabled';
```

查詢會傳回下列資料行：

| 資料行                       | 描述 |
|------------------------------|-------------|
| IsMLServicesInstalled        | 如果已經為執行個體安裝 SQL Server 機器學習服務，則會傳回 1。 否則，會傳回 0。 |
| ExternalScriptsEnabled       | 如果已啟用執行個體的外部指令碼，則會傳回 1。 否則，會傳回 0。 |
| ImpliedAuthenticationEnabled | 如果已啟用隱含驗證，則會傳回 1。 否則，會傳回 0。 確認 SQLRUserGroup 的登入是否存在，以檢查隱含驗證的設定。 |
| IsTcpEnabled                 | 如果已針對執行個體啟用 TCP/IP 通訊協定，則會傳回 1。 否則，會傳回 0。 如需詳細資訊，請參閱[預設 SQL Server 網路通訊協定組態](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)。 |

## <a name="active-sessions"></a>作用中的工作階段

檢視外執行外部指令碼的作用中工作階段。

![來自作用中設定查詢的輸出](media/dmv-active-sessions.png "來自作用中設定查詢的輸出")

執行下面的查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱 [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)、[sys.dm_external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 與 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)。

```sql
SELECT r.session_id, r.blocking_session_id, r.status, DB_NAME(s.database_id) AS database_name
    , s.login_name, r.wait_time, r.wait_type, r.last_wait_type, r.total_elapsed_time, r.cpu_time
    , r.reads, r.logical_reads, r.writes, er.language, er.degree_of_parallelism, er.external_user_name
FROM sys.dm_exec_requests AS r
INNER JOIN sys.dm_external_script_requests AS er
ON r.external_script_request_id = er.external_script_request_id
INNER JOIN sys.dm_exec_sessions AS s
ON s.session_id = r.session_id;
```

查詢會傳回下列資料行：

| 資料行                | 描述 |
|-----------------------|-------------|
| session_id            | 識別每個使用中的主要連接所關聯的工作階段。 |
| blocking_session_id   | 封鎖要求之工作階段的識別碼。 如果這個資料行是 NULL，表示要求沒有被封鎖，或者封鎖工作階段的工作階段資訊無法使用 (或無法識別)。 |
| status                | 要求的狀態。 |
| database_name         | 每個工作階段之目前資料庫的名稱。 |
| login_name            | 目前用來執行工作階段的 SQL Server 登入名稱。 |
| wait_time             | 若要求目前被封鎖，這個資料行會傳回目前等候的持續時間 (以毫秒為單位)。 不可為 Null。 |
| wait_type             | 若要求目前被封鎖，這個資料行會傳回等候的類型。 如需有關等候類型的詳細資訊，請參閱 [sys.dm_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 |
| last_wait_type        | 如果這個要求先前被封鎖，這個資料行會傳回上次等候的類型。 |
| total_elapsed_time    | 要求到達後所經過的總時間 (以毫秒為單位)。 |
| cpu_time              | 要求所用的 CPU 時間 (以毫秒為單位)。 |
| reads                 | 這項要求所執行的讀取數。 |
| logical_reads         | 這項要求所執行的邏輯讀取數。 |
| writes                | 這項要求所執行的寫入數。 |
| 語言              | 代表支援的指令碼語言的關鍵字。 |
| degree_of_parallelism | 指出已建立之平行處理序數目的數字。 這個值可能與已要求的平行處理序數目不同。 |
| external_user_name    | 用來執行指令碼的 Windows 背景工作帳戶。 |

## <a name="execution-statistics"></a>執行統計資料

檢視 Python 與 R 外部執行階段的執行統計資料。 目前僅可提供 RevoScaleR、revoscalepy 或 microsoftml 套件函式的統計資料。

![來自執行統計資料查詢的輸出](media/dmv-execution-statistics.png "來自執行統計資料查詢的輸出")

執行下面的查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱  [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 查詢只會傳回已執行一次以上的函式。

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

查詢會傳回下列資料行：

| 資料行        | 描述 |
|---------------|-------------|
| 語言      | 註冊的外部指令碼語言名稱。 |
| counter_name  | 註冊的外部指令碼函數名稱。 |
| counter_value | 伺服器上已呼叫之註冊的外部指令碼函數總數。 這個值會從在執行個體上安裝功能之後開始累計，而且無法重設。 |

## <a name="performance-counters"></a>效能計數器

檢視與外部指令碼執行相關的效能計數器。

![來自效能計數器查詢的輸出](media/dmv-performance-counters.png "來自效能計數器查詢的輸出")

執行下面的查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱 [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)。

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**sys.dm_os_performance_counters** 會輸出外部指令碼的下列效能計數器：

| 計數器                   | 描述 |
|---------------------------|-------------|
| 執行總計          | 本機或遠端呼叫所啟動的外部處理序數目。 |
| 平行執行       | 指令碼包含 _\@parallel_ 規格且 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 能夠產生及使用平行查詢計劃的次數。 |
| 串流執行      | 叫用串流功能的次數。 |
| SQL CC 執行         | 從遠端將呼叫具現化且使用 SQL Server 作為計算內容的外部指令碼執行次數。 |
| 隱含驗證登入      | 使用隱含驗證來發出 ODBC 回送呼叫的次數；亦即 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 代表傳送指令碼要求的使用者執行呼叫。 |
| 執行時間總計 (毫秒) | 呼叫與完成呼叫之間的經過時間。 |
| 執行錯誤          | 指令碼回報錯誤的次數。 此計數不包含 R 或 Python 錯誤。 |

## <a name="memory-usage"></a>記憶體使用量

檢視 OS、SQL Server 與外部集區所使用之記憶體的相關資訊。

![來自記憶體使用狀況查詢的輸出](media/dmv-memory-usage.png "來自記憶體使用狀況查詢的輸出")

執行下面的查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱 [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) 與 [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)。

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

查詢會傳回下列資料行：

| 資料行                       | 描述                                                                                                           |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| physical_memory_kb           | 電腦上實體記憶體的總數。                                                                   |
| committed_kb                 | 記憶體管理員中已認可的記憶體 (KB)。 不包含記憶體管理員中的保留記憶體。 |
| external_pool_peak_memory_kb | 所有外部資源集區使用的記憶體數量上限 (以 KB為單位)。                          |

## <a name="memory-configuration"></a>記憶體組態

檢視 SQL Server 與外部資源集區的記憶體設定上限相關資訊 (以百分比為單位)。 若 SQL Server 是以 `max server memory (MB)` 的預設值執行，則會被視為 OS 記憶體的 100%。

![來自記憶體設定查詢的輸出](media/dmv-memory-configuration.png "來自記憶體設定查詢的輸出")

執行下面的查詢以取得此輸出。 如需所使用檢視的詳細資訊，請參閱 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 與 [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

```sql
SELECT 'SQL Server' AS name
    , CASE CAST(c.value AS BIGINT)
        WHEN 2147483647 THEN 100
        ELSE (SELECT CAST(c.value AS BIGINT) / (physical_memory_kb / 1024.0) * 100 FROM sys.dm_os_sys_info)
        END AS max_memory_percent
FROM sys.configurations AS c
WHERE c.name LIKE 'max server memory (MB)'
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name, ep.max_memory_percent
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

查詢會傳回下列資料行：

| 資料行             | 描述 |
|--------------------|-------------|
| NAME               | 外部資源集區或 SQL Server 的名稱。 |
| max_memory_percent | SQL Server 或外部資源集區可以使用的最大記憶體。 |

## <a name="resource-pools"></a>資源集區

在 [SQL Server 資源管理員](../../relational-databases/resource-governor/resource-governor.md)中，[資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)代表執行個體之實體資源的子集。 您可以針對內送應用程式要求指定可在資源集區內使用的 CPU、實體 IO 與記憶體數量限制。 檢視用於 SQL Server 與外部指令碼的資源集區。

![來自資源集區查詢的輸出](media/dmv-resource-pools.png "來自資源集區查詢的輸出")

執行下面的查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱 [sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) 與 [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

查詢會傳回下列資料行：

| 資料行                   | 描述  |
|--------------------------|--------------|
| pool_name                | 資源集區的名稱。 SQL Server 資源集區前面會加上 `SQL Server`，而外部資源集區前面會加上 `External Pool`。 |
| total_cpu_usage_hours    | Resource Govenor 統計資料重設之後的累積 CPU 使用量 (以毫秒為單位)。 |
| read_io_completed_total  | Resource Governor 統計資料重設之後完成的讀取 IO 總數。              |
| write_io_completed_total | Resource Governor 統計資料重設之後完成的寫入 IO 總數。             |

## <a name="installed-packages"></a>已安裝的套件

您可以透過執行 R 或 Python 指令碼來輸出這些套件，以檢視 SQL Server 機器學習服務中安裝的 R 或 Python 套件。

### <a name="installed-packages-for-r"></a>R 的已安裝套件

檢視 SQL Server 機器學習服務中安裝的 R 套件。

![來自 R 查詢的已安裝套件輸出](media/dmv-installed-packages-r.png "來自 R 查詢的已安裝套件輸出")

執行下面的查詢以取得此輸出。 查詢會使用 R 指令碼來判斷隨 SQL Server 安裝的 R 套件。

```sql
EXECUTE sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

傳回的資料行如下：

| 資料行  | 描述                                                 |
|---------|-------------------------------------------------------------|
| Package | 已安裝之套件的名稱。                              |
| 版本 | 套件的版本。                                     |
| 相依 | 列出已安裝之套件所相依的套件。 |
| 授權 | 已之安裝套件的授權。                          |
| LibPath | 可在其中找到套件的目錄。                   |

### <a name="installed-packages-for-python"></a>Python 的已安裝套件

檢視 SQL Server 機器學習服務中安裝的 Python 套件。

![來自 Python 查詢的已安裝套件輸出](media/dmv-installed-packages-python.png "來自 Python 查詢的已安裝套件輸出")

執行下面的查詢以取得此輸出。 查詢會使用 Python 指令碼來判斷隨 SQL Server 安裝的 Python 套件。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
, @script = N'
import pkg_resources
import pandas
OutputDataSet = pandas.DataFrame(sorted([(i.key, i.version, i.location) for i in pkg_resources.working_set]))'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

傳回的資料行如下：

| 資料行   | 描述                               |
|----------|-------------------------------------------|
| Package  | 已安裝之套件的名稱。            |
| 版本  | 套件的版本。                   |
| Location | 可在其中找到套件的目錄。 |

## <a name="next-steps"></a>後續步驟

+ [機器學習的擴充事件](extended-events.md)
+ [Resource Governor 相關的動態管理檢視](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [系統動態管理檢視](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [使用 Management Studio 中的自訂報表監視機器學習](monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
