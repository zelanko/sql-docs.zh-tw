---
title: SQL Server 2019 的新功能 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bfe22edbc76805fb821ddda42a07a3b74395bdb6
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893995"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 是以舊版本為基礎，可讓 SQL Server 成長為平台，以供您選擇開發語言、資料類型、內部部署或雲端以及作業系統。

本文摘要說明 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能和增強功能。

如需詳細資訊和已知問題，請參閱 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 版本資訊](sql-server-ver15-release-notes.md)。

**使用[最新的工具](what-s-new-in-sql-server-ver15-prerelease.md#tools)以獲得 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最佳體驗。**

## <a name="ctp-32-july-2019"></a>CTP 3.2 2019 年 7 月

Community Technical Preview (CTP) 3.2 是 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最新公開版本。 這個版本對先前的 CTP 版本做了改進，以修正 Bug，提升安全性，以及將效能最佳化。 如需 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2 之前每個 CTP 版本中引進或改善的功能清單，請參閱 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 公告封存](what-s-new-in-sql-server-ver15-prerelease.md)。

### <a name="new-in-big-data-clusters"></a>巨量資料叢集的新功能

|新功能或更新 | 詳細資料 |
|:---|:---|
|公開預覽 |在 CTP 3.2 之前，SQL Server 巨量資料叢集提供給註冊的早期採用者使用。 而此版本可讓任何人都能體驗 SQL Server 巨量資料叢集的功能。 <br/><br/> 請參閱[開始使用 SQL Server 巨量資料叢集](../big-data-cluster/deploy-get-started.md)。|
|`azdata` |CTP 3.2 引進了 `azdata`，這是一種以 Python 編寫的命令列公用程式，可讓叢集系統管理員透過 REST API 啟動和管理巨量資料叢集。 `azdata` 取代了 `mssqlctl`。 請參閱[安裝 `azdata`](../big-data-cluster/deploy-install-azdata.md)。 |
|PolyBase |外部資料表資料行名稱現在可用來查詢 SQL Server、Oracle、Teradata、MongoDB 和 ODBC 資料來源。 在先前的 CTP 版本中，資料行僅根據目的地上的序數進行繫結，而不會使用外部資料表定義中的資料行名稱。|
|HDFS 階層重新整理 |引進了 HDFS 階層處理的重新整理功能，以便能夠針對遠端資料的最新快照集重新整理現有掛接。 請參閱 [HDFS 階層處理](../big-data-cluster/hdfs-tiering.md) |
|以筆記本為基礎的疑難排解 |CTP 3.2 引進了 Jupyter Notebook，用來協助您針對 SQL Server 巨量資料叢集中的元件進行[開發](../big-data-cluster/deploy-notebooks.md)與[探索、診斷和疑難排解](../big-data-cluster/manage-notebooks.md)。 |
| &nbsp; | &nbsp; |

### <a name="new-in-analysis-services"></a>Analysis Services 的新功能

| 新功能或更新 | 詳細資料 |
|:---|:---| 
| Power BI 快取重新整理的治理設定。  | Power BI 服務會快取儀表板磚的資料和報表資料，以進行 Live Connect 報表的初始載入，進而導致將過多的快取查詢提交給 SSAS，且在極端情況下使伺服器超載。 此版本引進了 **ClientCacheRefreshPolicy** 屬性。 這個屬性可讓您在伺服器層級覆寫此行為。 若要深入了解，請參閱[一般屬性](https://docs.microsoft.com/analysis-services/server-properties/general-properties)。 |
| 線上附加  | 此功能可讓您將表格式模型附加為線上作業。 線上附加可用於同步處理內部部署查詢擴充環境中的唯讀複本。 若要深入了解，請參閱[線上附加](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32)的詳細資料。 |
| &nbsp; | &nbsp; |

### <a name="new-in-language-extensions"></a>語言延伸模組的新功能

|新功能或更新 | 詳細資料 |
|:---|:---|
| 新增預設 JAVA 執行階段  | SQL Server 現在在整個產品中包含 Azul 系統適用於 JAVA 的 Zulu Embedded 支援。 如需詳細資訊，請參閱 [Free supported Java in SQL Server 2019 is now available](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/) (現已推出 SQL Server 2019 中的免費支援 JAVA)。 |

### <a name="new-in-sql-server-on-linux"></a>Linux 上 SQL Server 的新功能

|新功能或更新 | 詳細資料 |
|:---|:---|
| 異動資料擷取 (CDC) 支援 | 在 Linux 上現在已針對 SQL Server 2019 支援異動資料擷取 (CDC)。 |

## <a name="includesql-server-2019includessssqlv15-mdmd-features-by-component"></a>依元件列出的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 功能

下列各節將重點說明在舊版 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中增強的新元件和功能。

## <a name="big-data-clusters"></a>巨量資料叢集

| 新功能或更新 | 詳細資料 |
|:---|:---|
| 可擴充的巨量資料解決方案 | 為 Kubernetes 上執行的 SQL Server、Spark 和 HDFS 容器[部署可擴充叢集](../big-data-cluster/deploy-get-started.md) <br/><br/> 讀取、寫入及處理來自 Transact-SQL 或 Spark 的巨量資料<br/><br/> 輕鬆結合及分析含有大量巨量資料的高價值關聯式資料<br/><br/>查詢外部資料來源<br/><br/>在 SQL Server 的受控 HDFS 中儲存巨量資料<br/><br/>透過叢集查詢來自多個外部資料來源的資料<br/><br/> 使用 AI、機器學習服務和其他分析工作的資料<br/><br/> 在巨量資料叢集中部署及執行應用程式 <br/>|
| &nbsp; | &nbsp; |

如需詳細資料，請參閱[什麼是 SQL Server 巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)

[[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP) 公告封存](what-s-new-in-sql-server-ver15-prerelease.md)包含此功能所有先前 CTP 版本所公告和變更的功能清單。

## <a name="database-engine"></a>資料庫引擎

### <a name="security"></a>Security

|新功能或更新 | 詳細資料 |
|:---|:---|
|功能限制| 防止某些形式的 SQL 資料隱碼洩漏資料庫相關資訊，即使是 SQL 資料隱碼成功時。 請參閱[功能限制](../relational-databases/security/feature-restrictions.md)|
|加密索引的資料行|可在使用隨機加密方式以及啟用記憶體保護區的索引鍵所加密的資料行上建立索引，改善雜雜查詢 (使用 `LIKE` 與比較運算子) 的效能。 請參閱[具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。
|暫止和繼續透明資料加密 (TDE) 的初始掃描|請參閱[透明資料加密 (TDE) 掃描 - 暫止和繼續](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)|
|SQL Server 組態管理員中的憑證管理|請參閱[憑證管理 (SQL Server 組態管理員)](../database-engine/configure-windows/manage-certificates.md)
| &nbsp; | &nbsp; |


### <a name="graph"></a>圖表

|新功能或更新 | 詳細資料 |
|:---|:---|
|邊緣條件約束串聯刪除動作 |在圖表資料庫的邊緣條件約束中定義串聯刪除動作。 請參閱[邊緣條件約束](../relational-databases/tables/graph-edge-constraints.md)。 |
|新的圖形函式 - `SHORTEST_PATH` | 可使用 `MATCH` 中的 `SHORTEST_PATH`，尋找圖形中兩個節點之間最短的路徑，或是執行任意長度的周遊。|
|分割區資料表與索引| 分割區資料表與索引的資料，會分成可分散於圖形資料庫中多個檔案群組之間的單位。 |
|在圖形比對查詢中使用衍生資料表或檢視別名 |請參閱[圖表邊緣條件約束](../relational-databases/tables/graph-edge-constraints.md)。 |
| &nbsp; | &nbsp; |

### <a name="indexes"></a>索引

|新功能或更新 | 詳細資料 |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|可在能協助改善對索引進行高並行插入之輸送量的資料庫引擎內，開啟最佳化。 此選項適用於可能出現最後一頁插入競爭的索引，通常是具有循序鍵 (例如識別資料行、序列或日期/時間資料行) 的索引。 如需詳細資訊，請參閱 [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys)。|
|線上建置和重建叢集資料行存放區索引 | 請參閱[線上執行索引作業](../relational-databases/indexes/perform-index-operations-online.md)。 |
| &nbsp; | &nbsp; |

### <a name="in-memory-databases"></a>記憶體內部資料庫

|新功能或更新 | 詳細資料 |
|:---|:---|
|混合式緩衝集區的 DDL 控制項 |透過[混合式緩衝集區](../database-engine/configure-windows/hybrid-buffer-pool.md)，坐落在置於持續性記憶體 (PMEM) 裝置上之資料庫檔案上的資料庫頁面，可在必要時直接存取。|
|經記憶體最佳化的 tempdb 中繼資料|請參閱[記憶體最佳化的 TempDB 中繼資料](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)|
| &nbsp; | &nbsp; |

### <a name="linked-servers"></a>連結的伺服器

|新功能或更新 | 詳細資料 |
|:---|:---|
|連結的伺服器支援 UTF-8字元編碼方式。 |[定序與 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md) |
| &nbsp; | &nbsp; |

### <a name="polybase"></a>PolyBase

|新功能或更新 | 詳細資料 |
|:---|:---|
|PolyBase |外部資料表資料行名稱現在可用來查詢 SQL Server、Oracle、Teradata、MongoDB 和 ODBC 資料來源。 |
| &nbsp; | &nbsp; |

### <a name="collation"></a>定序

|新功能或更新 | 詳細資料 |
|:---|:---|
|支援 UTF-8 字元編碼 |已針對 BIN2 定序啟用 (`Latin1_General_100_BIN2_UTF8`)。 請參閱[定序與 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md)。 |
|在安裝期間選取 UTF-8 定序作為預設 | 請參閱[定序與 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md#ctp23)。 |
| &nbsp; | &nbsp; |

### <a name="server-settings"></a>伺服器設定

|新功能或更新 | 詳細資料 |
|:---|:---|
|可於安裝期間設定 `MIN` 與 `MAX` 的伺服器記憶體值 |在安裝期間，您可設定伺服器記憶體的值。 可以使用預設值、導出的建議值，若您已選擇 [建議]  選項 [Server Memory Server Configuration Options](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)，也可以手動指定您自己的值。|
|SQL Server 安裝程式啟用 MAXDOP 設定 |新建議遵循記載的指導方針。請[設定 	[平行處理原則的最大程度] 伺服器組態選項](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)|
|混合式緩衝集區| 這是 SQL Server 資料庫引擎的新功能，其中坐落在位於持續性記憶體 (PMEM) 裝置資料庫檔案上的資料庫頁面，會在必要時被直接存取。 請參閱[混合式緩衝集區](../database-engine/configure-windows/hybrid-buffer-pool.md)。|
| &nbsp; | &nbsp; |

### <a name="performance-monitoring"></a>效能監控

|新功能或更新 | 詳細資料 |
|:---|:---|
|純量 UDF 內嵌 |將純量使用者定義函式 (UDF) 自動轉換成關聯運算式，並將它們內嵌在呼叫 SQL 查詢中。 請參閱[純量 UDF 內嵌](../relational-databases/user-defined-functions/scalar-udf-inlining.md)。 |
| `sys.dm_exec_requests` 資料行 `command` | 在 `SELECT` 正在等候同步統計資料更新作業完成以繼續查詢執行的情況下，顯示 `SELECT (STATMAN)`。 請參閱 [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | `sys.dm_os_wait_stats` 動態管理檢視中的新等候類型。 它會顯示花費在同步統計資料重新整理作業上的累積執行個體層級時間。 請參閱 [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|
|查詢存放區的自訂擷取原則|啟用後，即可在新的查詢存放區擷取原則設定下使用額外查詢存放區設定，來微調特定伺服器中的資料收集。 如需詳細資訊，請參閱 [ALTER DATABASE SET 選項](../t-sql/statements/alter-database-transact-sql-set-options.md)。|
|`sys.dm_exec_query_plan_stats` |新 DMF 在大多數查詢中會傳回最後一個已知實際執行計畫的對等項目。 請參閱 [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)。|
|`LAST_QUERY_PLAN_STATS` | 可啟用 `sys.dm_exec_query_plan_stats` 的新資料庫範圍設定。 請參閱 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|
|`LIGHTWEIGHT_QUERY_PROFILING`|新的資料庫範圍設定。 請參閱 [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp)。 |
|`query_post_execution_plan_profile` | 不同於使用標準分析的 `query_post_execution_showplan`，擴充事件會根據輕量型分析收集實際執行計畫的對等項目。 請參閱[查詢分析基礎結構](../relational-databases/performance/query-profiling-infrastructure.md)。|
|資料列模式記憶體授與意見反應。 |[資料列模式記憶體授與意見反應](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) |
|資料表變數延後編譯。|[資料表變數延後編譯](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation) |
|近似的 `COUNT DISTINCT`。|[近似查詢處理](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)|
|資料列存放區上的批次模式。|[資料列存放區上的批次模式](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore) |

### <a name="language-extensions"></a>語言延伸模組

|新功能或更新 | 詳細資料 |
|:---|:---|
|新增 Java 語言 SDK | 簡化可從 SQL Server 執行的 Java 程式開發。 請參閱 [SQL Server 機器學習服務的新功能](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。 |
|SQL Server 語言擴充功能 - [Java 語言擴充功能](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview) \(英文\)|[Microsoft SQL Server 中適用於 Java 的 Microsoft 擴充性 SDK](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) 現已提供開放原始碼且[可在 GitHub 上取得](https://github.com/microsoft/sql-server-language-extensions)。|
|註冊外部語言|新的 DDL `CREATE EXTERNAL LANGUAGE` 在 SQL Server 中註冊外部語言，如同 Java。 請參閱[建立外部語言](../t-sql/statements/create-external-language-transact-sql.md)。 |
|Java 資料類型的支援|請參閱 [Java 資料類型](../language-extensions/how-to/java-to-sql-data-types.md)。|

### <a name="spatial"></a>空間

|新功能或更新 | 詳細資料 |
|:---|:---|
| 新增空間參考識別碼 (SRID) |[澳洲 GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) 提供更強大且精確的資料，可與全球定位系統更加緊密結合。 新的 SRID 包含：<br/><br/> - 7843 - 地理 2D<br/> - 7844 - 地理 3D <br/><br/>[sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) 檢視包含新 SRID 的定義。 |
| &nbsp; | &nbsp; |

### <a name="performance"></a>效能

|新功能或更新 | 詳細資料 |
|:---|:---|
|加速資料庫復原 | 啟用每個資料庫的加速資料庫復原。 請參閱[加速資料庫復原](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)。|
|強制執行向前快轉及靜態資料指標 | 查詢存放區計畫強制支援向前快轉及靜態資料指標。 請參閱[計畫強制支援向前快轉及靜態資料指標](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23)。|
|減少對工作負載的重新編譯| 改善跨多個範圍使用暫存資料表的功能。 請參閱[減少對工作負載的重新編譯](../relational-databases/tables/tables.md#ctp23) |
|間接檢查點延展性 |請參閱[改善的間接檢查點延展性](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)。|
| &nbsp; | &nbsp; |

### <a name="availability-groups"></a>可用性群組

|新功能或更新 | 詳細資料 |
|:---|:---|
|最多五個同步複本|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 會將同步複本的數目上限，從 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中最多為 3 的狀態增加至 5。 您可以設定這五個複本的群組，使其在群組內具備自動容錯移轉。 有一個主要複本，再加上四個同步次要複本。|
|次要到主要複本連線重新導向| 可將用戶端應用程式連線導向至主要複本，而不論連接字串中指定的目標伺服器為何。 如需詳細資料，請參閱[次要到主要複本讀取/寫入連線重新導向 (Always On 可用性群組)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。|
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>錯誤訊息

|新功能或更新 | 詳細資料 |
|:---|:---|
|詳細資訊截斷警告 | 截斷錯誤訊息預設為包含資料表和資料行名稱，以及被截斷的值。 請參閱 [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation)。|
| &nbsp; | &nbsp; |

## <a name="sql-server-on-linux"></a>Linux 上的 SQL Server

| 新功能或更新 | 詳細資料 |
|:-----|:-----|
|新的容器登錄|[開始使用 Docker 上的 SQL Server 容器](../linux/quickstart-install-connect-docker.md) |
|具有 Kubernetes 之 Docker 容器上的 Always On 可用性群組 |[容器的 Always On 可用性群組](../linux/sql-server-ag-kubernetes.md) |
|複寫支援 |[Linux 上的 SQL Server 複寫](../linux/sql-server-linux-replication.md)
|Microsoft Distributed Transaction Coordinator (MSDTC) 支援 |[如何在 Linux 上設定 MSDTC](../linux/sql-server-linux-configure-msdtc.md) |
|第三方 AD 提供者的 OpenLDAP 支援 |[教學課程：在 Linux 上搭配使用 Active Directory 驗證與 SQL Server](../linux/sql-server-linux-active-directory-authentication.md) |
|Linux 上的機器學習 |[在 Linux 上設定機器學習服務](../linux/sql-server-linux-setup-machine-learning.md) |
|Tempdb 的改進內容 | 根據預設，在 Linux 上進行新的 SQL Server 安裝，會依據邏輯核心的數目 (最多 8 個資料檔案)，建立多個 tempdb 資料檔。 此情況不適用於就地次要或主要版本升級。 每個 tempdb 檔為 8 MB，且可自動成長到 64 MB。 此行為類似於 Windows 上的預設 SQL Server 安裝。 |
| Linux 上的 PolyBase | 在 Linux 上為非 Hadoop 連接器[安裝 PolyBase](../relational-databases/polybase/polybase-linux-setup.md)。<br/><br/>[PolyBase 類型對應](../relational-databases/polybase/polybase-type-mapping.md)。 |
| &nbsp; | &nbsp; |

## <a id="ml"></a> SQL Server 機器學習服務

|新功能或更新 | 詳細資料 |
|:---|:---|
|分割區型模型|使用新增至 `sp_execute_external_script` 的參數，處理您資料每個資料分割的外部指令碼。 此功能支援訓練許多小型模型 (每個資料的資料分割一個模型)，而不是一個大型模型。 請參閱[建立分割區型模型](../advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)|
|Windows Server 容錯移轉叢集| 在 Windows Server 容錯移轉叢集上設定機器學習服務的高可用性。|
| &nbsp; | &nbsp; |

## [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| 新功能或更新 | 詳細資料 |
|:---|:---|
|支援 Azure SQL Database 受控執行個體資料庫。| 在受控執行個體上裝載 [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]。 請參閱 [[!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] 安裝和設定](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb)。|
|新增 HTML 控制項| HTML 控制項取代所有先前的 Silverlight 元件。 已移除 Silverlight 相依性。|
| &nbsp; | &nbsp; |

## <a name="analysis-services"></a>Analysis Services

| 新功能或更新 | 詳細資料 |
|:---|:---|
|表格式模型中的計算群組| [表格式模型中的計算群組](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|MDX 查詢支援具有計算群組的表格式模型 | 請參閱[計算群組](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)。 |
|使用計算群組的量值動態格式 |這項功能可讓您依條件變更具有[計算群組](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)之量值的格式字串。 例如，透過貨幣轉換，量值可以使用不同的外幣格式顯示。|
|表格式模型中的多對多關聯性|[表格式模型中的多對多關聯性](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|資源管理的屬性設定|[資源治理的屬性設定](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

如需從支援中排除之特定功能的資訊，請參閱[版本資訊](sql-server-ver15-release-notes.md)。

此外，也為 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2 新增或強化了下列功能。

## <a name="see-also"></a>另請參閱

- [`SqlServer` PowerShell 模組](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell 文件](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>後續步驟

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 版本資訊](sql-server-ver15-release-notes.md)。

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]：Technical white paper](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />在 2018 年 9 月發佈。 適用於 Windows、Linux 及 Docker 容器的 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
