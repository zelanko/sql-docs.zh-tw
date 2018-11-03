---
title: 監視 SQL Server Machine Learning 服務使用動態管理檢視 (Dmv) |Microsoft Docs
description: 您可以使用動態管理檢視 (Dmv) 來監視 SQL Server Machine Learning 服務。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: aa05c78f8bac4af5187b815126e0ec9e4b6fff4e
ms.sourcegitcommit: c2322c1a1dca33b47601eb06c4b2331b603829f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/01/2018
ms.locfileid: "50743451"
---
# <a name="monitor-sql-server-machine-learning-services-using-dynamic-management-views-dmvs"></a>監視 SQL Server Machine Learning 服務使用動態管理檢視 (Dmv)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用動態管理檢視 (Dmv) 監視執行中的外部指令碼 （R 和 Python） 使用的資源診斷問題和調整 SQL Server Machine Learning 服務中的效能。

在本文中，您會發現特有的 SQL Server Machine Learning 服務的 Dmv。 您也會看到顯示的範例查詢：

+ 設定和機器學習服務的組態選項
+ 執行外部 R 或 Python 指令碼的作用中工作階段
+ R 和 Python 的外部執行階段執行統計資料
+ 外部指令碼的效能計數器
+ 作業系統、 SQL Server 和外部資源集區的記憶體使用量
+ 適用於 SQL Server 和外部資源集區的記憶體組態
+ 資源管理員資源集區，包括外部資源集區
+ 已安裝的封裝，R 和 Python

如需 Dmv 的詳細資訊，請參閱 <<c0> [ 系統動態管理檢視](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。

> [!TIP]
> 您也可以使用自訂報表來監視 SQL Server Machine Learning 服務。 如需詳細資訊，請參閱 <<c0> [ 監視使用 Management Studio 中的自訂報表的機器學習服務](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)。

## <a name="dynamic-management-views"></a>動態管理檢視

監視 SQL Server 中的機器學習工作負載時，可以使用下列動態管理檢視。 若要查詢 Dmv，您需要`VIEW SERVER STATE`執行個體上的權限。

| 動態管理檢視 | 類型 | 描述 |
|-------------------------|------|-------------|
| [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) | 執行 | 逐資料列傳回正在執行外部指令碼的每個使用中背景工作帳戶。 |
| [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) | 執行 | 逐資料列傳回各種類型的外部指令碼要求。 |
| [sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) | 執行 | 針對伺服器所維護的每個效能計數器，各傳回一個資料列。 如果您使用的搜尋條件`WHERE object_name LIKE '%External Scripts%'`，您可以使用這項資訊以查看幾個指令碼執行時，執行指令碼所使用的驗證模式中或多少 R 或 Python 呼叫所發出的整體的執行個體上。 |
| [sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) | [資源管理員] | 在 資源管理員，資源集區和資源集區統計資料的目前組態傳回目前的外部資源集區狀態的相關資訊。 |
| [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md) | [資源管理員] | 在資源管理員會傳回目前的外部資源集區設定的 CPU 親和性資訊。 針對 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中的每個排程器，各傳回一個資料列，其中每個排程器都會對應至個別的處理器。 請利用這份檢視來監視排程器的狀況或識別失控的工作。 |

如需監視的相關資訊[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]執行個體，請參閱[目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)並[Resource Governor 相關動態管理檢視](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)。

## <a name="settings-and-configuration"></a>設定和組態

檢視 Machine Learning 服務的安裝設定和組態選項。

![從設定和設定查詢的輸出](media/dmv-settings-and-configuration.png "從設定和設定查詢輸出")

執行查詢，來取得此輸出。 如需有關檢視和使用函式的詳細資訊，請參閱[sys.dm_server_registry](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)， [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)，並[SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)。

```SQL
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

| 「資料行」 | 描述 |
|--------|-------------|
| IsMLServicesInstalled | 如果 SQL Server Machine Learning 服務已安裝執行個體，則傳回 1。 否則會傳回 0。 |
| ExternalScriptsEnabled | 如果執行個體啟用外部指令碼，則傳回 1。 否則會傳回 0。 |
| ImpliedAuthenticationEnabled | 傳回 1，表示隱含驗證已啟用。 否則會傳回 0。 隱含驗證組態會檢查確認 SQLRUserGroup 是否有登入。 |
| IsTcpEnabled | 如果執行個體啟用 TCP/IP 通訊協定，則傳回 1。 否則會傳回 0。 如需詳細資訊，請參閱 <<c0> [ 預設 SQL Server 網路通訊協定組態](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)。 |

## <a name="active-sessions"></a>作用中的工作階段

檢視作用中工作階段執行外部指令碼。

![使用中的設定查詢的輸出](media/dmv-active-sessions.png "從作用中設定查詢輸出")

執行查詢，來取得此輸出。 如需有關使用動態管理檢視的詳細資訊，請參閱[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)， [sys.dm_external_script_requests](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)，並[sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)。

```SQL
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

| 「資料行」 | 描述 |
|--------|-------------|
| session_id | 識別每個使用中的主要連接所關聯的工作階段。 |
| blocking_session_id | 封鎖要求之工作階段的識別碼。 如果這個資料行是 NULL，表示要求沒有被封鎖，或者封鎖工作階段的工作階段資訊無法使用 (或無法識別)。 |
| status | 要求的狀態。 |
| database_name | 每個工作階段目前的資料庫名稱。 |
| login_name | 工作階段目前執行的 SQL Server 登入名稱。 |
| wait_time | 若要求目前被封鎖，這個資料行會傳回目前等候的持續時間 (以毫秒為單位)。 不可為 Null。 |
| wait_type | 若要求目前被封鎖，這個資料行會傳回等候的類型。 如需等候的類型資訊，請參閱[sys.dm_os_wait_stats](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。 |
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

檢視 R 和 Python 的外部執行階段執行統計資料。 目前提供的 RevoScaleR、 revoscalepy 或 microsoftml 套件函式的統計資料。

![執行統計資料查詢的輸出](media/dmv-execution-statistics.png "執行統計資料查詢的輸出")

執行查詢，來取得此輸出。 如需有關使用動態管理檢視的詳細資訊，請參閱[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 查詢只會傳回執行一次以上的函式。

```SQL
SELECT language, counter_name, counter_value
FROM sys.dm_external_script_execution_stats
WHERE counter_value > 0
ORDER BY language, counter_name;
```

查詢會傳回下列資料行：

| 「資料行」 | 描述 |
|--------|-------------|
| language | 註冊的外部指令碼語言名稱。 |
| counter_name | 註冊的外部指令碼函數名稱。 |
| counter_value | 伺服器上已呼叫之註冊的外部指令碼函數總數。 這個值會從在執行個體上安裝功能之後開始累計，而且無法重設。 |

## <a name="performance-counters"></a>效能計數器

檢視與執行外部指令碼相關的效能計數器。

![輸出的效能計數器查詢](media/dmv-performance-counters.png "輸出效能計數器查詢")

執行查詢，來取得此輸出。 如需有關使用動態管理檢視的詳細資訊，請參閱[sys.dm_os_performance_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)。

```SQL
SELECT counter_name, cntr_value
FROM sys.dm_os_performance_counters 
WHERE object_name LIKE '%External Scripts%'
```

**sys.dm_os_performance_counters**輸出外部指令碼的下列效能計數器：

| 計數器 | 描述 |
|---------|-------------|
| 執行總計 | 本機或遠端呼叫所啟動的外部處理序數目。 |
| 平行執行 | 包含指令碼次數_@parallel_規格且[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]能夠產生及使用平行查詢計畫。 |
| 串流執行 | 已叫用的串流處理功能的次數的數目。 |
| SQL CC 執行 | 執行位置呼叫具現化遠端及 SQL Server 的外部指令碼已用作為計算內容。 |
| 隱含驗證登入 | 使用隱含的驗證; 進行 ODBC 回送呼叫的次數也就是[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]執行代表傳送指令碼要求的使用者呼叫。 |
| 執行時間總計 (毫秒) | 呼叫與完成呼叫之間所經過的時間。 |
| 執行錯誤 | 指令碼回報錯誤的次數。 這個計數不包含 R 或 Python 的錯誤。 |

## <a name="memory-usage"></a>記憶體使用狀況

檢視作業系統、 SQL Server 和外部集區所使用的記憶體的相關資訊。

![記憶體使用量查詢的輸出](media/dmv-memory-usage.png "輸出從記憶體使用量查詢")

執行查詢，來取得此輸出。 如需有關使用動態管理檢視的詳細資訊，請參閱[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)並[sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)。

```SQL
SELECT physical_memory_kb, committed_kb
    , (SELECT SUM(peak_memory_kb)
        FROM sys.dm_resource_governor_external_resource_pools AS ep
        ) AS external_pool_peak_memory_kb
FROM sys.dm_os_sys_info;
```

查詢會傳回下列資料行：

| 「資料行」 | 描述 |
|--------|-------------|
| physical_memory_kb | 在電腦上的實體記憶體總數量。 |
| committed_kb&lt | 記憶體管理員中的千位元組 (KB) 中認可的記憶體。 不包含記憶體管理員中的保留記憶體。 |
| external_pool_peak_memory_kb | 加總記憶體，以 kb 為單位，所有外部資源集區的最大數量。 |

## <a name="memory-configuration"></a>記憶體組態

檢視 SQL Server 和外部資源集區的百分比表示的最大記憶體組態資訊。 如果執行 SQL Server 的預設值是`max server memory (MB)`，它會被視為作業系統記憶體的 100%。

![記憶體設定查詢的輸出](media/dmv-memory-configuration.png "記憶體設定查詢的輸出")

執行查詢，來取得此輸出。 如需有關使用檢視的詳細資訊，請參閱[sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)並[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

```SQL
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

| 「資料行」 | 描述 |
|--------|-------------|
| NAME | 外部資源集區或 SQL Server 的名稱。 |
| max_memory_percent | SQL Server 或外部資源集區可用的記憶體上限。 |

## <a name="resource-pools"></a>資源集區

在  [SQL Server 資源管理員](../../relational-databases/resource-governor/resource-governor.md)，則[資源集區](../../relational-databases/resource-governor/resource-governor-resource-pool.md)代表的執行個體的實體資源子集。 您可以在 CPU、 實體 IO 和傳入的應用程式要求，包括執行外部指令碼，可以使用的資源集區中的記憶體數量指定限制。 檢視 SQL Server 和外部指令碼所使用的資源集區。

![輸出從資源集區的查詢](media/dmv-resource-pools.png "輸出從資源集區的查詢")

執行查詢，來取得此輸出。 如需有關使用動態管理檢視的詳細資訊，請參閱[sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)並[sys.dm_resource_governor_external_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)。

```SQL
SELECT CONCAT ('SQL Server - ', p.name) AS pool_name
    , p.total_cpu_usage_ms, p.read_io_completed_total, p.write_io_completed_total
FROM sys.dm_resource_governor_resource_pools AS p
UNION ALL
SELECT CONCAT ('External Pool - ', ep.name) AS pool_name
    , ep.total_cpu_user_ms, ep.read_io_count, ep.write_io_count
FROM sys.dm_resource_governor_external_resource_pools AS ep;
```

查詢會傳回下列資料行：

| 「資料行」 | 描述 |
|--------|-------------|
| pool_name | 資源集區的名稱。 SQL Server 資源集區前面會加上`SQL Server`前面加上外部資源集區和`External Pool`。
| total_cpu_usage_hours | 以毫秒為單位重設資源管理員統計資料之後累積的 CPU 使用量。 |
| read_io_completed_total | 重設資源管理員統計資料之後完成的讀取 IO 總數。 |
| write_io_completed_total | 重設資源管理員統計資料之後完成的寫入 IO 總數。 |

## <a name="installed-packages"></a>已安裝的套件

您可以檢視安裝在 SQL Server Machine Learning 服務的執行 R 或 Python 指令碼會輸出這些 R 和 Python 套件。

### <a name="installed-packages-for-r"></a>安裝 R 封裝

檢視安裝在 SQL Server Machine Learning 服務中的 R 套件。

![從 R 查詢已安裝的封裝輸出](media/dmv-installed-packages-r.png "輸出從 R 查詢已安裝的套件")

執行查詢，來取得此輸出。 查詢使用 R 指令碼來判斷哪些 R 套件安裝 SQL Server。

```SQL
EXEC sp_execute_external_script @language = N'R'
, @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
    , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
```

傳回的資料行如下：

| 「資料行」 | 描述 |
|--------|-------------|
| 封裝 | 已安裝封裝的名稱。 |
| 版本 | 封裝的版本。 |
| 相依 | 列出已安裝的套件相依的套件。 |
| 使用權 | 已安裝套件的授權。 |
| LibPath | 您可以在其中找到封裝的目錄。 |

### <a name="installed-packages-for-python"></a>已安裝適用於 Python 的套件

檢視安裝在 SQL Server Machine Learning 服務的 Python 套件。

![從 Python 查詢已安裝的封裝輸出](media/dmv-installed-packages-python.png "輸出從 Python 查詢已安裝的套件")

執行查詢，來取得此輸出。 查詢會使用 Python 指令碼，來判斷與 SQL Server 一起安裝的 Python 套件。

```SQL
EXEC sp_execute_external_script @language = N'Python'
, @script = N'
import pip
OutputDataSet = pandas.DataFrame([(i.key, i.version, i.location) for i in pip.get_installed_distributions()])'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128), Location NVARCHAR(1000)));
```

傳回的資料行如下：

| 「資料行」 | 描述 |
|--------|-------------|
| 封裝 | 已安裝封裝的名稱。 |
| 版本 | 封裝的版本。 |
| 位置 | 您可以在其中找到封裝的目錄。 |

## <a name="next-steps"></a>後續步驟

+ [管理及監視機器學習服務方案](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
+ [機器學習服務的擴充的事件](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)
+ [Resource Governor 相關的動態管理檢視](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)
+ [系統動態管理檢視](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
+ [在 Management Studio 中使用自訂報表監視機器學習服務](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)