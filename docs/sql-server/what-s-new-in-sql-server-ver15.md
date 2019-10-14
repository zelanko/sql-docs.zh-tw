---
title: SQL Server 2019 的新功能 | Microsoft Docs
ms.date: 08/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e85461ef0a6395904b0f80590a01f035eb51dc3a
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952764"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 是以舊版本為基礎，可讓 SQL Server 成長為平台，以供您選擇開發語言、資料類型、內部部署或雲端以及作業系統。

本文摘要說明 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能和增強功能。

如需詳細資訊和已知問題，請參閱 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 版本資訊](sql-server-ver15-release-notes.md)。

**使用[最新的工具](what-s-new-in-sql-server-ver15-prerelease.md#tools)以獲得 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最佳體驗。**

>[!NOTE]
>該內容是針對 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 候選版所發行。 候選版是預先發行的軟體。 此資訊可能會有所變更。 如需支援情節的詳細資訊，請參閱[支援](#support)。
>
>此版本包含稍早在社群技術預覽 (CTP) 版本中宣佈的改良功能。 這些改良功能已新增功能、修復錯誤、提高安全性並最佳化效能。 如需 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 候選版之前 CTP 版本中引進或改善的功能清單，請參閱 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 公告封存](what-s-new-in-sql-server-ver15-prerelease.md)。

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引入了適用於 [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] 的 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]。 它也提供 SQL Server 資料庫引擎、SQL Server Analysis Services、SQL Server 機器學習服務、Linux 上的 SQL Server 與 SQL Server Master Data Services 的額外功能與改進。

下列各節將提供這些功能的概觀。

## <a name="data-virtualization-and-includebig-data-clusters-2019includesssbigdataclusters-ver15md"></a>資料虛擬化和 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]

現今企業通常會管轄大量資料資產，這是由整個公司的分散資料來源所裝載大量資料集所組成。 使用 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] 從您所有資料取得近乎即時的見解，可提供完整的環境來處理大型資料集，包括機器學習和人工智慧功能。

| 新功能或更新 | 詳細資料 |
|:---|:---|
| 可擴充的巨量資料解決方案 | 為 Kubernetes 上執行的 SQL Server、Spark 和 HDFS 容器[部署可擴充叢集](../big-data-cluster/deploy-get-started.md) <br/><br/> 讀取、寫入及處理來自 Transact-SQL 或 Spark 的巨量資料<br/><br/> 輕鬆結合及分析含有大量巨量資料的高價值關聯式資料<br/><br/>查詢外部資料來源<br/><br/>在 SQL Server 的受控 HDFS 中儲存巨量資料<br/><br/>透過叢集查詢來自多個外部資料來源的資料<br/><br/> 使用 AI、機器學習服務和其他分析工作的資料<br/><br/> [在 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] 中部署及執行應用程式](../big-data-cluster/concept-application-deployment.md) <br/><br/> SQL Server 主要執行個體使用 Always On 可用性群組技術，為所有資料庫提供高可用性和災害復原<br/>|
|使用 Polybase 的資料虛擬化 | 使用外部資料表來查詢來自外部 SQL Server、Oracle、Teradata、MongoDB & ODBC 資料來源的資料，現在具備 [UTF-8 編碼支援](../relational-databases/collations/collation-and-unicode-support.md)。 如需詳細資料，請參閱[什麼是 PolyBase](../relational-databases/polybase/polybase-guide.md)。|
| &nbsp; | &nbsp; |

如需詳細資料，請參閱[什麼是 SQL Server[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]](../big-data-cluster/big-data-cluster-overview.md)。

[[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP) 公告封存](what-s-new-in-sql-server-ver15-prerelease.md)包含此功能所有先前 CTP 版本所公告和變更的功能清單。

## <a name="intelligent-database"></a>智慧型資料庫

### <a name="intelligent-query-processing"></a>智慧查詢處理

|新功能或更新 | 詳細資料 |
|:---|:---|
|資料列模式記憶體授與意見反應 |透過調整批次和資料列模式運算子的記憶體授與大小，以在批次模式記憶體授與意見反應功能上擴充。 這會自動修正導致記憶體浪費和並行降低的過多授與，並修正導致佔用大量磁碟資源的記憶體授與不足。 請參閱[資料列模式記憶體授與意見反應](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback)。 |
|資料表變數延後編譯|針對參考資料表變數的查詢，提升計畫品質與整體效能。 在最佳化和初始編譯期間，此功能會根據實際資料表變數的資料列計數，傳播基數估計值。 這項精確的資料列計數資訊會最佳化下游計畫作業。 請參閱[資料表變數延後編譯](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation)。 |
|使用 `APPROX_COUNT_DISTINCT ` 的近似查詢處理|針對絕對有效位數不重要但回應性很重要的情節，`APPROX_COUNT_DISTINCT` 使用比 `COUNT(DISTINCT())` 更少的資源彙總大型資料集以獲得更高的並行。 請參閱[近似查詢處理](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)。|
|資料列存放區上的批次模式|資料列存放區上的批次模式可啟用批次模式執行功能，而不需要資料行存放區索引。 批次模式執行在分析工作負載期間會更有效率地使用 CPU，但在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 之前，只有當查詢包含具有資料行存放區索引的作業時才會使用它。 不過，有些應用程式可能使用資料行存放區索引不支援的功能，因此無法利用批次模式。 從 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 開始，會在符合條件的分析工作負載 (其查詢包括對任何類型索引 (資料列存放區或資料行存放區) 的作業) 上啟用批次模式。 請參閱[資料列存放區上的批次模式](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore)。 |
|純量 UDF 內嵌|將純量 UDF 自動轉換成關聯運算式，並將它們內嵌在呼叫 SQL 查詢中。 此轉換可改善利用純量 UDF 的工作負載效能。 請參閱[純量 UDF 內嵌](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)。|
| &nbsp; | &nbsp; |


### <a name="in-memory-database"></a>記憶體內資料庫

|新功能或更新 | 詳細資料 |
|:---|:---|
|混合式緩衝集區| [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的新功能，坐落在置於持續性記憶體 (PMEM) 裝置上之資料庫檔案上的資料庫頁面，可在必要時直接存取。 請參閱[混合式緩衝集區](../database-engine/configure-windows/hybrid-buffer-pool.md)。|
|經記憶體最佳化的 `tempdb` 中繼資料| [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進的新功能是[記憶體內部資料庫](../relational-databases/in-memory-database.md)功能系列的一部分，記憶體最佳化的 `tempdb` 中繼資料能有效移除此瓶頸，並解除鎖定大量 `tempdb` 工作負載的新層級延展性。 在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，涉及管理暫存資料表中繼資料的系統資料表，可以移至不需閂鎖之非持久性經記憶體最佳化的資料表。 請參閱[記憶體最佳化的 `tempdb` 中繼資料](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)。|
| 資料庫快照集的記憶體內部 OLTP 支援 | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進建立[資料庫快照集](../relational-databases/databases/database-snapshots-sql-server.md)的支援，包括記憶體最佳化檔案群組的資料庫。 |
| &nbsp; | &nbsp; |

### <a name="intelligent-performance"></a>智慧型效能

|新功能或更新 | 詳細資料 |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|在有助於改善對索引進行高並行插入之輸送量的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 內，開啟最佳化。 此選項適用於可能出現最後一頁插入競爭的索引，通常是具有循序鍵 (例如識別資料行、序列或日期/時間資料行) 的索引。 如需詳細資訊，請參閱 [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys)。|
|強制執行向前快轉及靜態資料指標 | 查詢存放區計畫強制支援向前快轉及靜態資料指標。 請參閱[計畫強制支援向前快轉及靜態資料指標](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23)。|
|資源管理| `CREATE WORKLOAD GROUP` 和 `ALTER WORKLOAD GROUP` 的 `REQUEST_MAX_MEMORY_GRANT_PERCENT` 選項可設定值，已從整數變更為浮動資料類型，以允許對記憶體限制採取更細微的控制。 請參閱 [ALTER 工作負載群組](../t-sql/statements/alter-workload-group-transact-sql.md)和[建立工作負載群組](../t-sql/statements/create-workload-group-transact-sql.md)。|
|減少對工作負載的重新編譯| 改善跨多個範圍使用暫存資料表的功能。 請參閱[減少對工作負載的重新編譯](../relational-databases/tables/tables.md#ctp23) |
|間接檢查點延展性 |請參閱[改善的間接檢查點延展性](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23)。|
|並行 PFS 更新|[PFS 分頁](https://techcommunity.microsoft.com/t5/SQL-Server/Under-the-covers-GAM-SGAM-and-PFS-pages/ba-p/383125) \(英文\) 是資料庫檔案中的特殊分頁，SQL Server 在配置物件的空間時，可使用這些特殊分頁來協助找出可用空間。 PFS 分頁上的頁面閂鎖爭用通常與 [`tempdb`](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d) 相關聯，但在有許多並行物件配置執行緒時，也可能會發生在使用者資料庫上。 這種改進會改變使用 PFS 更新來管理並行的方式，使其可以在共用閂鎖下更新，而不是獨佔閂鎖。 此行為在從 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 開始的所有資料庫 (包括 `tempdb`) 中預設為啟用。|
| &nbsp; | &nbsp; |

### <a name="monitoring"></a>監視

|新功能或更新 | 詳細資料 |
|:---|:---|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | `sys.dm_os_wait_stats` 動態管理檢視中的新等候類型。 它會顯示花費在同步統計資料重新整理作業上的累積執行個體層級時間。 請參閱 [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|
|查詢存放區的自訂擷取原則|啟用後，即可在新的查詢存放區擷取原則設定下使用額外查詢存放區設定，來微調特定伺服器中的資料收集。 如需詳細資訊，請參閱 [ALTER DATABASE SET 選項](../t-sql/statements/alter-database-transact-sql-set-options.md)。|
|`LIGHTWEIGHT_QUERY_PROFILING`|新的資料庫範圍設定。 請參閱 [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp)。 |
|`sys.dm_exec_requests` 資料行 `command` | 在 `SELECT` 正在等候同步統計資料更新作業完成以繼續查詢執行的情況下，顯示 `SELECT (STATMAN)`。 請參閱 [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|
|`sys.dm_exec_query_plan_stats` |新 DMF 在大多數查詢中會傳回最後一個已知實際執行計畫的對等項目。 請參閱 [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md)。|
|`LAST_QUERY_PLAN_STATS` | 可啟用 `sys.dm_exec_query_plan_stats` 的新資料庫範圍設定。 請參閱 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|
|`query_post_execution_plan_profile` | 不同於使用標準分析的 `query_post_execution_showplan`，擴充事件會根據輕量型分析收集實際執行計畫的對等項目。 請參閱[查詢分析基礎結構](../relational-databases/performance/query-profiling-infrastructure.md)。|
|`sys.dm_db_page_info(database_id, file_id, page_id, mode)` | 新的 DMF 會傳回資料庫中頁面相關資訊。 請參閱 [sys.dm_db_page_info (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)。|
| &nbsp; | &nbsp; |

## <a name="developer-experience"></a>開發人員體驗

### <a name="graph"></a>圖表

|新功能或更新 | 詳細資料 |
|:---|:---|
|邊緣條件約束串聯刪除動作 |在圖表資料庫的邊緣條件約束中定義串聯刪除動作。 請參閱[邊緣條件約束](../relational-databases/tables/graph-edge-constraints.md)。 |
|新的圖形函式 - `SHORTEST_PATH` | 可使用 `MATCH` 中的 `SHORTEST_PATH`，尋找圖形中兩個節點之間最短的路徑，或是執行任意長度的周遊。|
|分割區資料表與索引| 分割區資料表與索引的資料，會分成可分散於圖形資料庫中多個檔案群組之間的單位。 |
|在圖形比對查詢中使用衍生資料表或檢視別名 |請參閱[圖表比對查詢](../t-sql/queries/match-sql-graph.md)。 |
| &nbsp; | &nbsp; |

### <a name="unicode-support"></a>Unicode 支援

|新功能或更新 | 詳細資料 |
|:---|:---|
|支援 UTF-8 字元編碼 |支援匯入和匯出編碼的 UTF-8 字元，以及作為字串資料的資料庫層級或資料行層級定序。 這支援延伸至全球規模的應用程式，其中提供全球多語系資料庫應用程式與服務的需求，對於滿足客戶需求與特定市場法規而言非常重要。 請參閱[定序與 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md)。<br/><br/> [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 候選版啟用 Polybase 外部資料表和 Always Encrypted 的 UTF-8 支援。|
| &nbsp; | &nbsp; |

### <a name="language-extensions"></a>語言延伸模組

|新功能或更新 | 詳細資料 |
|:---|:---|
|新增 Java 語言 SDK | 簡化可從 SQL Server 執行的 Java 程式開發。 請參閱[適用於 SQL Server 的 Microsoft Extensibility SDK for Java](../language-extensions/how-to/extensibility-sdk-java-sql-server.md)。 |
|Java 語言 SDK 是開放原始碼 |[Microsoft SQL Server 中適用於 Java 的 Microsoft 擴充性 SDK](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) 現已提供開放原始碼且[可在 GitHub 上取得](https://github.com/microsoft/sql-server-language-extensions)。|
|Java 資料類型的支援|請參閱 [Java 資料類型](../language-extensions/how-to/java-to-sql-data-types.md)。|
|新增預設 JAVA 執行階段 | SQL Server 現在在整個產品中包含 Azul 系統適用於 Java 的 Zulu Embedded 支援。 如需詳細資訊，請參閱 [Free supported Java in SQL Server 2019 is now available](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/) (現已推出 SQL Server 2019 中的免費支援 JAVA)。 |
|SQL Server 語言延伸模組| 以擴充性架構執行外部程式碼。 請參閱 [SQL Server 語言延伸模組](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview) \(英文\)。
|註冊外部語言|新的 DDL `CREATE EXTERNAL LANGUAGE` 在 SQL Server 中註冊外部語言，如同 Java。 請參閱[建立外部語言](../t-sql/statements/create-external-language-transact-sql.md)。 |
| &nbsp; | &nbsp; |

### <a name="spatial"></a>空間

|新功能或更新 | 詳細資料 |
|:---|:---|
| 新增空間參考識別碼 (SRID) |[澳洲 GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) 提供更強大且精確的資料，可與全球定位系統更加緊密結合。 新的 SRID 包含：<br/><br/> - 7843 (適用於地理 2D)<br/> - 7844 (適用於地理 3D) <br/><br/>[sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) 檢視包含新 SRID 的定義。 |
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>錯誤訊息

|新功能或更新 | 詳細資料 |
|:---|:---|
|詳細資訊截斷警告 | 截斷錯誤訊息預設為包含資料表和資料行名稱，以及被截斷的值。 請參閱 [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation)。|
| &nbsp; | &nbsp; |

## <a name="mission-critical-security"></a>任務關鍵性安全性

|新功能或更新 | 詳細資料 |
|:---|:---|
|具有安全記憶體保護區的 Always Encrypted|透過在伺服器端安全記憶體保護區中啟用純文字資料上的計算，在具備就地加密和豐富計算的 Always Encrypted 上進行擴充。 就地加密可改善密碼編譯作業 (加密資料行、輪換資料行加密金鑰等) 的效能和可靠性，因為它會避免將資料移出資料庫。 支援豐富計算 (模式比對和比較作業) 可讓更多的範例適用 Always Encypted，以及要求敏感資料保護，但同時也需要在 Transact-SQL 查詢中擁有更豐富功能的應用程式。 請參閱[具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。|
|SQL Server 組態管理員中的憑證管理|請參閱[憑證管理 (SQL Server 組態管理員)](../database-engine/configure-windows/manage-certificates.md)。|
| &nbsp; | &nbsp; |

## <a name="high-availability"></a>高可用性

### <a name="availability-groups"></a>可用性群組

|新功能或更新 | 詳細資料 |
|:---|:---|
|最多五個同步複本|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 會將同步複本的數目上限，從 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中最多為 3 的狀態增加至 5。 您可以設定這五個複本的群組，使其在群組內具備自動容錯移轉。 有一個主要複本，再加上四個同步次要複本。|
|次要到主要複本連線重新導向| 可將用戶端應用程式連線導向至主要複本，而不論連接字串中指定的目標伺服器為何。 如需詳細資料，請參閱[次要到主要複本讀取/寫入連線重新導向 (Always On 可用性群組)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。|
| &nbsp; | &nbsp; |

### <a name="recovery"></a>復原

|新功能或更新 | 詳細資料 |
|:---|:---|
|加速資料庫復原 | 啟用每個資料庫的加速資料庫復原。 請參閱[加速資料庫復原](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr)。|
| &nbsp; | &nbsp; |

### <a name="resumable-operations"></a>可繼續的作業

|新功能或更新 | 詳細資料 |
|:---|:---|
|線上建置和重建叢集資料行存放區索引 | 請參閱[線上執行索引作業](../relational-databases/indexes/perform-index-operations-online.md)。 |
|可繼續的線上建置資料列存放區索引 | 請參閱[線上執行索引作業](../relational-databases/indexes/perform-index-operations-online.md)。 |
|暫止和繼續透明資料加密 (TDE) 的初始掃描|請參閱[透明資料加密 (TDE) 掃描 - 暫止和繼續](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)。|
| &nbsp; | &nbsp; |

## <a name="setup"></a>安裝程式 

|新功能或更新 | 詳細資料 | 
|:---|:---| 
|新的記憶體設定選項 | 設定安裝期間的 [最小伺服器記憶體 (MB)]  與 [最大伺服器記憶體 (MB)]  伺服器設定。 如需詳細資訊，請參閱[資料庫引擎組態 - 記憶體頁面](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory)，以及[從命令提示字元安裝 SQL Server](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install) 中的 `USESQLRECOMMENDEDMEMORYLIMITS`、`SQLMINMEMORY` 與 `SQLMAXMEMORY` 參數。 建議的值會與[伺服器記憶體設定選項](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually)中的記憶體設定指導方針一致。| 
|新平行處理原則設定選項 | 在安裝期間設定 [平行處理原則的最大程度]  伺服器設定。 如需詳細資訊，請參閱[資料庫引擎組態 - MaxDOP 頁面](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop)，以及[從命令提示字元安裝 SQL Server](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install) 中的 `SQLMAXDOP` 參數。 預設值將會與[設定 max degree of parallelism 伺服器組態選項](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)中的平行處理原則的最大程度指導方針一致。| 
| &nbsp; | &nbsp; |

## <a name="platform-choice"></a>平台選擇

### <a id="sql-server-on-linux"></a>Linux

| 新功能或更新 | 詳細資料 |
|:-----|:-----|
|新的容器登錄|[開始使用 Docker 上的 SQL Server 容器](../linux/quickstart-install-connect-docker.md) |
|複寫支援 |[Linux 上的 SQL Server 複寫](../linux/sql-server-linux-replication.md)
|Microsoft Distributed Transaction Coordinator (MSDTC) 支援 |[如何在 Linux 上設定 MSDTC](../linux/sql-server-linux-configure-msdtc.md) |
|第三方 AD 提供者的 OpenLDAP 支援 |[教學課程：在 Linux 上搭配使用 Active Directory 驗證與 SQL Server](../linux/sql-server-linux-active-directory-authentication.md) |
|Linux 上的機器學習 |[在 Linux 上設定機器學習服務](../linux/sql-server-linux-setup-machine-learning.md) |
|`tempdb` 改進功能 | 根據預設，在 Linux 上進行新的 SQL Server 安裝，會依據邏輯核心的數目建立多個 `tempdb` 資料檔 (最多 8 個資料檔案)。 此情況不適用於就地次要或主要版本升級。 每個 `tempdb` 檔都為 8 MB，且可自動成長到 64 MB。 此行為類似於 Windows 上的預設 SQL Server 安裝。 |
| Linux 上的 PolyBase | 在 Linux 上為非 Hadoop 連接器[安裝 PolyBase](../relational-databases/polybase/polybase-linux-setup.md)。<br/><br/>[PolyBase 類型對應](../relational-databases/polybase/polybase-type-mapping.md)。 |
| 異動資料擷取 (CDC) 支援 | 在 Linux 上現在已針對 SQL Server 2019 支援異動資料擷取 (CDC)。 |
| &nbsp; | &nbsp; |

### <a name="containers"></a>[設定 SSIS 記錄]

|新功能或更新 | 詳細資料 |
|:---|:---|
| Microsoft 容器登錄 | [Microsoft 容器登錄](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/)現在已取代適用於新官方 Microsoft 容器映像的 Docker Hub，包括 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。 |
| 非根容器 | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進以非根使用者身分啟動 [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] 程序來建立更安全容器的功能。 請參閱[以非根使用者的身分建置並執行 SQL Server 容器](../linux/sql-server-linux-configure-docker.md#buildnonrootcontainer)以取得詳細資料。 |
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

## <a name="sql-server-analysis-services"></a>SQL Server Analysis Services

| 新功能或更新 | 詳細資料 |
|:---|:---|
|查詢交錯| 請參閱[查詢交錯](https://docs.microsoft.com/analysis-services/tabular-models/query-interleaving) |
|MDX 查詢支援具有計算群組的表格式模型 | 請參閱[計算群組](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)。 |
|表格式模型中的計算群組| [表格式模型中的計算群組](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|MDX 查詢支援具有計算群組的表格式模型 | 請參閱[計算群組](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)。 |
|使用計算群組的量值動態格式 |這項功能可讓您依條件變更具有[計算群組](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24)之量值的格式字串。 例如，透過貨幣轉換，量值可以使用不同的外幣格式顯示。|
|表格式模型中的多對多關聯性|[表格式模型中的多對多關聯性](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|資源管理的屬性設定|[資源治理的屬性設定](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| Power BI 快取重新整理的治理設定。  | Power BI 服務會快取儀表板磚的資料和報表資料，以進行 Live Connect 報表的初始載入，進而導致將過多的快取查詢提交給 SSAS，且在極端情況下使伺服器超載。 此版本引進了 **ClientCacheRefreshPolicy** 屬性。 這個屬性可讓您在伺服器層級覆寫此行為。 若要深入了解，請參閱[一般屬性](https://docs.microsoft.com/analysis-services/server-properties/general-properties)。 |
| 線上附加  | 此功能可讓您將表格式模型附加為線上作業。 線上附加可用於同步處理內部部署查詢擴充環境中的唯讀複本。 若要深入了解，請參閱[線上附加](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32)的詳細資料。 |
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

如需從支援中排除之特定功能的資訊，請參閱[版本資訊](sql-server-ver15-release-notes.md)。

此外，也為 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2 新增或強化了下列功能。

## <a name="see-also"></a>另請參閱

- [`SqlServer` PowerShell 模組](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell 文件](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>後續步驟

- [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 版本資訊] (sql-server-ver15-release-notes.md)。

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]：Technical white paper](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />在 2018 年 9 月發佈。 適用於 Windows、Linux 及 Docker 容器的 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
