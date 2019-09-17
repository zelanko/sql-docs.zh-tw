---
title: 使用 Dmv 監視 Python 和 R 腳本執行
description: 使用動態管理檢視（Dmv）來監視 SQL Server Machine Learning 服務中的 Python 和 R 外部腳本執行。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0e541e1d0eb2a8bb1ac512276fa395f8d8c6379f
ms.sourcegitcommit: 5a61854ddcd2c61bb6da30ccad68f0ad90da0c96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/13/2019
ms.locfileid: "70978399"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>使用動態管理檢視 (Dmv) 監視 SQL Server Machine Learning 服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用動態管理檢視（Dmv）來監視外部腳本的執行（Python 和 R）、使用的資源、診斷問題，以及微調 SQL Server Machine Learning 服務中的效能。

在本文中, 您會找到 SQL Server Machine Learning 服務的特定 Dmv。 您也會找到範例查詢, 其中顯示:

+ 機器學習服務的設定和設定選項
+ 執行外部 Python 或腳本的作用中會話
+ 適用于 Python 和 R 的外部執行時間的執行統計資料
+ 外部腳本的效能計數器
+ OS、SQL Server 和外部資源集區的記憶體使用量
+ SQL Server 和外部資源集區的記憶體配置
+ Resource Governor 資源集區, 包括外部資源集區
+ 適用于 Python 和 R 的已安裝套件

如需有關 Dmv 的一般資訊, 請參閱[系統動態管理檢視](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。

> [!TIP]
> 您也可以使用自訂報表來監視 SQL Server Machine Learning 服務。 如需詳細資訊, 請參閱[在 Management Studio 中使用自訂報表來監視機器學習](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)服務。

## <a name="dynamic-management-views"></a>動態管理檢視

在 SQL Server 中監視機器學習服務工作負載時, 可以使用下列動態管理檢視。 若要查詢 dmv, 您需要`VIEW SERVER STATE`實例的許可權。

| 動態管理檢視 | Type | 描述 |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | 執行 | 逐資料列傳回正在執行外部指令碼的每個使用中背景工作帳戶。 |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | 執行 | 逐資料列傳回各種類型的外部指令碼要求。 |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | 執行 | 針對伺服器所維護的每個效能計數器，各傳回一個資料列。 如果您使用搜尋條件`WHERE object_name LIKE '%External Scripts%'`, 您可以使用此資訊來查看已執行的腳本數目、哪些腳本是使用哪一個驗證模式執行, 或是在實例上發出多少個 R 或 Python 呼叫。 |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | [資源管理員] | 傳回 Resource Governor 中目前外部資源集區狀態的相關資訊、資源集區的目前設定, 以及資源集區統計資料。 |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | [資源管理員] | 傳回 Resource Governor 中目前外部資源集區設定的 CPU 親和性資訊。 針對 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中的每個排程器，各傳回一個資料列，其中每個排程器都會對應至個別的處理器。 請利用這份檢視來監視排程器的狀況或識別失控的工作。 |

如需監視[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]實例的詳細資訊, 請參閱[目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)和[Resource Governor 相關的動態管理檢視](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。

## <a name="settings-and-configuration"></a>設定和設定

請參閱 Machine Learning 服務安裝設定和設定選項。

![設定和設定查詢的輸出](media/dmv-settings-and-configuration.png "設定和設定查詢的輸出")

執行下列查詢以取得此輸出。 如需所使用之視圖和功能的詳細資訊，請參閱[_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)、 [sys.databases](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)和[SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)。

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

此查詢會傳回下列資料行:

| 「資料行」 | 描述 |
|--------|-------------|
| IsMLServicesInstalled | 如果已安裝實例的 SQL Server Machine Learning 服務, 則傳回1。 否則, 會傳回0。 |
| ExternalScriptsEnabled | 如果已啟用實例的外部腳本, 則傳回1。 否則, 會傳回0。 |
| ImpliedAuthenticationEnabled | 如果已啟用隱含驗證, 則會傳回1。 否則, 會傳回0。 確認 SQLRUserGroup 的登入是否存在, 以檢查隱含驗證的設定。 |
| IsTcpEnabled | 如果已針對實例啟用 TCP/IP 通訊協定, 則會傳回1。 否則, 會傳回0。 如需詳細資訊, 請參閱[預設 SQL Server 網路通訊協定](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)設定。 |

## <a name="active-sessions"></a>作用中的工作階段

查看正在執行外部腳本的使用中會話。

![使用中設定查詢的輸出](media/dmv-active-sessions.png "使用中設定查詢的輸出")

執行下列查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱[_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)、 [_external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)和[sys.databases _exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)。

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

此查詢會傳回下列資料行:

| 「資料行」 | 描述 |
|--------|-------------|
| session_id | 識別每個使用中的主要連接所關聯的工作階段。 |
| blocking_session_id | 封鎖要求之工作階段的識別碼。 如果這個資料行是 NULL，表示要求沒有被封鎖，或者封鎖工作階段的工作階段資訊無法使用 (或無法識別)。 |
| status | 要求的狀態。 |
| database_name | 每個會話的目前資料庫名稱。 |
| login_name | 目前用來執行會話的 SQL Server 登入名稱。 |
| wait_time | 若要求目前被封鎖，這個資料行會傳回目前等候的持續時間 (以毫秒為單位)。 不可為 Null。 |
| wait_type | 若要求目前被封鎖，這個資料行會傳回等候的類型。 如需等候類型的詳細資訊，請參閱[sys.databases _os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 |
| last_wait_type | 如果這個要求先前被封鎖，這個資料行會傳回上次等候的類型。 |
| total_elapsed_time | 要求到達後所經過的總時間 (以毫秒為單位)。 |
| cpu_time | 要求所用的 CPU 時間 (以毫秒為單位)。 |
| reads | 這項要求所執行的讀取數。 |
| logical_reads | 這項要求所執行的邏輯讀取數。 |
| writes | 這項要求所執行的寫入數。 |
| language | 代表支援的指令碼語言的關鍵字。 |
| degree_of_parallelism | 指出已建立之平行處理序數目的數字。 這個值可能與已要求的平行處理序數目不同。 |
| external_user_name | 用來執行指令碼的 Windows 背景工作帳戶。 |

## <a name="execution-statistics"></a>執行統計資料

查看適用于 R 和 Python 的外部執行時間的執行統計資料。 目前僅可使用 RevoScaleR、revoscalepy 或 microsoftml 封裝函數的統計資料。

![執行統計資料查詢的輸出](media/dmv-execution-statistics.png "執行統計資料查詢的輸出")

執行下列查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱[_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 查詢只會傳回已執行一次以上的函式。

```sql
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

此查詢會傳回下列資料行:

| 「資料行」 | 描述 |
|--------|-------------|
| language | 註冊的外部指令碼語言名稱。 |
| counter_name | 註冊的外部指令碼函數名稱。 |
| counter_value | 伺服器上已呼叫之註冊的外部指令碼函數總數。 這個值會從在執行個體上安裝功能之後開始累計，而且無法重設。 |

## <a name="performance-counters"></a>效能計數器

查看與外部腳本執行相關的效能計數器。

![效能計數器查詢的輸出](media/dmv-performance-counters.png "效能計數器查詢的輸出")

執行下列查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱[_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)。

```sql
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**_os_performance_counters**會輸出下列外部腳本的效能計數器：

| 計數器 | 描述 |
|---------|-------------|
| 執行總計 | 由本機或遠端呼叫啟動的外部進程數目。 |
| 平行執行 | 腳本包含 _\@平行_規格，且[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]能夠產生和使用平行查詢計劃的次數。 |
| 串流執行 | 已叫用串流功能的次數。 |
| SQL CC 執行 | 外部腳本的執行次數, 其中會從遠端具現化呼叫, 並使用 SQL Server 做為計算內容。 |
| 隱含驗證登入 | 使用隱含驗證進行 ODBC 回送呼叫的次數;也就是說, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]會代表傳送腳本要求的使用者執行呼叫。 |
| 執行時間總計 (毫秒) | 通話和呼叫完成之間經過的時間。 |
| 執行錯誤 | 腳本報告錯誤的次數。 此計數不包含 R 或 Python 錯誤。 |

## <a name="memory-usage"></a>記憶體使用狀況

查看 OS、SQL Server 和外部集區所使用之記憶體的相關資訊。

![記憶體使用量查詢的輸出](media/dmv-memory-usage.png "記憶體使用量查詢的輸出")

執行下列查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱[_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)和[_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)。

```sql
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

此查詢會傳回下列資料行:

| 「資料行」 | 描述 |
|--------|-------------|
| physical_memory_kb | 電腦上的實體記憶體總量。 |
| committed_kb | 記憶體管理員中的認可記憶體 (以 kb 為單位)。 不包含記憶體管理員中的保留記憶體。 |
| external_pool_peak_memory_kb | 所有外部資源集區使用的記憶體數量上限 (以 kb 為單位)。 |

## <a name="memory-configuration"></a>記憶體組態

以 SQL Server 和外部資源集區的百分比來查看最大記憶體設定的相關資訊。 如果 SQL Server 是以預設值`max server memory (MB)`執行，則會將它視為 OS 記憶體的 100%。

![記憶體設定查詢的輸出](media/dmv-memory-configuration.png "記憶體設定查詢的輸出")

執行下列查詢以取得此輸出。 如需所使用之視圖的詳細資訊，請參閱[sys.databases](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)和[_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

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

此查詢會傳回下列資料行:

| 「資料行」 | 描述 |
|--------|-------------|
| name | 外部資源集區或 SQL Server 的名稱。 |
| max_memory_percent | SQL Server 或外部資源集區可以使用的最大記憶體。 |

## <a name="resource-pools"></a>資源集區

在[SQL Server Resource Governor](../../relational-databases/resource-governor/resource-governor.md)中,[資源集](../../relational-databases/resource-governor/resource-governor-resource-pool.md)區代表實例的實體資源子集。 您可以指定傳入應用程式要求的 CPU、實體 IO 和記憶體數量限制, 包括外部腳本的執行, 可以在資源集區中使用。 查看用於 SQL Server 和外部腳本的資源集區。

![資源集區查詢的輸出](media/dmv-resource-pools.png "資源集區查詢的輸出")

執行下列查詢以取得此輸出。 如需所使用動態管理檢視的詳細資訊，請參閱[_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)和[_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

```sql
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

此查詢會傳回下列資料行:

| 「資料行」 | 描述 |
|--------|-------------|
| pool_name | 資源集區的名稱。 SQL Server 資源集區的前面`SQL Server`會加上, 而外部資源`External Pool`集區前面會加上。
| total_cpu_usage_hours | 已重設資源管理員之後統計資料之後的累計 CPU 使用量 (以毫秒為單位)。 |
| read_io_completed_total | 重設資源管理員統計資料之後完成的讀取 IO 總數。 |
| write_io_completed_total | 重設資源管理員統計資料之後完成的寫入 IO 總數。 |

## <a name="installed-packages"></a>已安裝的套件

您可以藉由執行 R 或 Python 腳本來輸出這些套件, 以查看安裝在 SQL Server Machine Learning 服務中的 R 和 Python 封裝。

### <a name="installed-packages-for-r"></a>適用于 R 的已安裝套件

查看安裝在 SQL Server Machine Learning 服務中的 R 套件。

![R 查詢的已安裝套件輸出](media/dmv-installed-packages-r.png "R 查詢的已安裝套件輸出")

執行下列查詢以取得此輸出。 查詢會使用 R 腳本來判斷隨 SQL Server 安裝的 R 封裝。

```sql
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

傳回的資料行包括:

| 「資料行」 | 描述 |
|--------|-------------|
| 套件 | 已安裝之封裝的名稱。 |
| Version | 封裝的版本。 |
| 相依 | 列出已安裝之封裝所相依的封裝。 |
| 使用權 | 已安裝之套件的授權。 |
| LibPath | 可在其中找到封裝的目錄。 |

### <a name="installed-packages-for-python"></a>適用于 Python 的已安裝套件

查看安裝在 SQL Server Machine Learning 服務中的 Python 套件。

![適用于 Python 查詢之已安裝套件的輸出](media/dmv-installed-packages-python.png "適用于 Python 查詢之已安裝套件的輸出")

執行下列查詢以取得此輸出。 此查詢會使用 Python 腳本來判斷隨 SQL Server 安裝的 Python 套件。

```sql
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

傳回的資料行包括:

| 「資料行」 | 描述 |
|--------|-------------|
| 套件 | 已安裝之封裝的名稱。 |
| Version | 封裝的版本。 |
| Location | 可在其中找到封裝的目錄。 |

## <a name="next-steps"></a>後續步驟

+ [管理及監視機器學習服務方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [機器學習服務的擴充事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Resource Governor 相關的動態管理檢視](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [系統動態管理檢視](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [在 Management Studio 中使用自訂報表監視機器學習服務](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
