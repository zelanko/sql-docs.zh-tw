---
title: SQL Server 2019 的新功能 | Microsoft Docs
ms.date: 03/27/2018
ms.prod: sql-server-2019
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cfb679bdec74536d62b3f332ff644d80435907c0
ms.sourcegitcommit: 0c049c539ae86264617672936b31d89456d63bb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58618265"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 是以舊版本為基礎，可讓 SQL Server 成長為平台，以供您選擇開發語言、資料類型、內部部署或雲端以及作業系統。 本文摘要說明 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能。 第一節介紹最新預覽版本中新增的功能。 本文的其他章節會詳盡說明為此 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 最新發行的所有功能。

如需詳細資訊和已知問題，請參閱 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 版本資訊](sql-server-ver15-release-notes.md)。

**請試用 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]！**

- [![從評估中心下載](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [下載 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 以安裝於 Windows](https://go.microsoft.com/fwlink/?LinkID=862101)。
- 安裝於 Linux for [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)。
- [在 Docker 上的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 上執行](../linux/quickstart-install-connect-docker.md)。

**使用[最新的工具](#tools)以獲得 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最佳體驗。**

## <a name="ctp-24"></a>CTP 2.4

Community Technical Preview (CTP) 2.4 是 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最新公開版本。 這個版本對先前的 CTP 版本做了改進，以修正 Bug，提升安全性，以及將效能最佳化。 此外，也為 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.4 新增或強化了下列功能。

- [巨量資料叢集](#bigdatacluster)
  - 說明在 Spark 中透過 TensorFlow 執行深度學習時的 GPU 支援。
  - 將 Spark 執行階段升級至 Spark 2.4。
  - 資料集區的 `INSERT INTO SELECT` 支援。
  - 使用於外部資料表查詢的 `FORCE SCALEOUTEXECUTION` 和 `DISABLE SCALEOUTEXECUTION` 選項子句。

- [資料庫引擎](#databaseengine)
  - 截斷錯誤訊息預設為包含資料表和資料行名稱，以及被截斷的值。 請參閱[截斷](#truncation)。
  - 新的 DMF `sys.dm_exec_query_plan_stats` 在大多數的查詢中會傳回最後一個已知實際執行計畫的對等項目。
  - 透明資料加密 (TDE) 掃描 - 暫止和繼續。

- [SQL Server Analysis Services](#ssas)
  - 表格式模型中的多對多關聯性。
  - 資源治理的屬性設定。

下列各節說明已在前幾版的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md) 中導入的新功能。

## <a id="bigdatacluster"></a>巨量資料叢集

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)會啟用新的案例，包括下列：

- [在 Spark 中透過 TensorFlow 執行深度學習時的 GPU 支援](../big-data-cluster/spark-gpu-tensorflow.md)。 (CTP 2.4)
- 將 Spark 執行階段升級至 Spark 2.4。 (CTP 2.4)
- 資料集區的 `INSERT INTO SELECT` 支援。
- 使用於外部資料表查詢的 `FORCE SCALEOUTEXECUTION` 和 `DISABLE SCALEOUTEXECUTION` 選項子句。
- [在 IntelliJ 中提交 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 巨量資料叢集的 Spark 作業](../big-data-cluster/spark-submit-job-intellij-tool-plugin.md)。 (CTP 2.3)
- [各種資料相關應用程式的應用程式部署及管理體驗](../big-data-cluster/big-data-cluster-create-apps.md)，包括使用 R 和 Python 來運作機器學習模型、執行 SQL Server Integration Services (SSIS) 作業等。 (CTP 2.3)
- [在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 巨量資料叢集中使用 Sparklyr](../big-data-cluster/sparklyr-from-RStudio.md)。 (CTP 2.3)
- 將外部 HDFS 相容儲存體裝載至具備 [HDFS 階層處理](../big-data-cluster/hdfs-tiering.md)的巨量資料叢集。 (CTP 2.3)
- 對巨量資料叢集使用 Azure Data Studio 的 SparkR。 (CTP 2.2)
- [部署 Python 和 R 應用程式](../big-data-cluster/big-data-cluster-create-apps.md)。 (CTP 2.2)
- 在 Kubernetes 上部署具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 Spark Linux 容器的巨量資料叢集。 (CTP 2.0)
- 從 HDFS 中存取巨量資料。 (CTP 2.0)
- 使用 Spark 執行進階分析和機器學習。 (CTP 2.0)
- 使用 Spark 串流將資料串流至 SQL 資料集區。 (CTP 2.0)
- 在 [**Azure Data Studio**](../sql-operations-studio/what-is.md) 中執行可提供筆記型體驗的查詢活頁簿。 (CTP 2.0)
 
[!INCLUDE [Big data clusters preview](../includes/big-data-cluster-preview-note.md)]

## <a id="databaseengine"></a> 資料庫引擎

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 針對 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 推出或強化了下列新功能。

### <a name="new-querypostexecutionplanprofile-extended-event-ctp-24"></a>新的 query_post_execution_plan_profile 擴充事件 (CTP 2.4)

不同於使用標準分析的 `query_post_execution_showplan`，新的 `query_post_execution_plan_profile` 擴充事件會根據輕量型分析收集實際執行計畫的對等項目。 如需詳細資訊，請參閱[查詢分析基礎結構](../relational-databases/performance/query-profiling-infrastructure.md)。

#### <a name="example-1---extended-event-session-using-standard-profiling"></a>範例 1 - 使用標準分析的擴充事件工作階段

```sql
CREATE EVENT SESSION [QueryPlanOld] ON SERVER 
ADD EVENT sqlserver.query_post_execution_showplan(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename = N'C:\Temp\QueryPlanStd.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

#### <a name="example-2---extended-event-session-using-lightweight-profiling"></a>範例 2 - 使用輕量型分析的擴充事件工作階段

```sql
CREATE EVENT SESSION [QueryPlanLWP] ON SERVER 
ADD EVENT sqlserver.query_post_execution_plan_profile(
    ACTION(sqlos.task_time, sqlserver.database_id, 
    sqlserver.database_name, sqlserver.query_hash_signed, 
    sqlserver.query_plan_hash_signed, sqlserver.sql_text))
ADD TARGET package0.event_file(SET filename=N'C:\Temp\QueryPlanLWP.xel')
WITH (MAX_MEMORY=4096 KB, EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS, 
    MAX_DISPATCH_LATENCY=30 SECONDS, MAX_EVENT_SIZE=0 KB, 
    MEMORY_PARTITION_MODE=NONE, TRACK_CAUSALITY=OFF, STARTUP_STATE=OFF);
```

### <a name="new-dmf-sysdmexecqueryplanstats-ctp-24"></a>新的 DMF sys.dm_exec_query_plan_stats (CTP 2.4) 

新的 DMF `sys.dm_exec_query_plan_stats` 在大多數的查詢中，會根據輕量型分析傳回最後一個已知實際執行計畫的對等項目。 如需詳細資訊，請參閱 [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md) 和[查詢分析基礎結構](../relational-databases/performance/query-profiling-infrastructure.md)。 請參閱下列指令碼作為範例：

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

這是選擇加入的功能，需要啟用[追蹤旗標](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451。

### <a name="transparent-data-encryption-tde-scan---suspend-and-resume-ctp-24"></a>透明資料加密 (TDE) 掃描 - 暫止和繼續 (CTP 2.4)

若要在資料庫上啟用[透明資料加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md)，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 必須執行加密掃描，將資料檔案中的每個頁面讀取至緩衝集區，然後將加密的頁面寫回磁碟。 為了讓使用者能更充分地掌控加密掃描，[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 導入了 TDE 掃描暫止和繼續語法，以便您在系統的工作負載偏高時或商務關鍵性時段能夠暫停掃描，且稍後再繼續掃描。

使用下列語法可暫停 TDE 加密掃描：

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

同理，下列語法可繼續 TDE 加密掃描：

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

為了顯示目前的加密掃描狀態，`sys.dm_database_encryption_keys` 動態管理檢視中已新增 `encryption_scan_state`。 此外也有名為 `encryption_scan_modify_date` 的新資料行，會包含上次加密掃描狀態變更的日期和時間。 同時請注意，如果在加密掃描處於暫止狀態時重新啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，在啟動時將會在錯誤記錄中記錄一則訊息，指出有現有的掃描已暫停。

### <a name="accelerated-database-recovery-ctp-23"></a>加速資料庫復原 (CTP 2.3)

[加速資料庫復原](/azure/sql-database/sql-database-accelerated-database-recovery/)藉由重新設計 SQL Server 的資料庫引擎復原處理序來大幅提升資料庫可用性，尤其是針對長時間執行的交易。 [資料庫復原](../relational-databases/logs/the-transaction-log-sql-server.md?#recovery-of-all-incomplete-transactions-when--is-started)是一項 SQL Server 為了讓每個資料庫都能以交易一致 (或正常) 狀態啟動所使用的處理序。 啟用加速資料庫復原的資料庫，其在容錯移轉或其他非正常關機之後完成復原的速度會大幅加快。 自 CTP 2.3 起，可以使用下列語法為每個資料庫啟用加速資料庫復原：

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
```

> [!NOTE]
> 無須在 Azure SQL DB 中使用此語法也能利用這項功能，因為它預設為開啟。

若您有可能進行大型交易的重要資料庫，請在預覽期間實驗這項功能。 請將意見反應提供給 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]小組](<https://aka.ms/sqlfeedback>)。

### <a name="query-store-plan-forcing-support-for-fast-forward-and-static-cursors-ctp-23"></a>查詢存放區計畫強制支援向前快轉及靜態資料指標 (CTP 2.3)

查詢存放區現在支援強制查詢執行計畫，以進行向前快轉及提供靜態 T-SQL 和 API 資料指標。 現在可透過 `sp_query_store_force_plan` 或透過 SQL Server Management Studio 查詢存放區報告支援強制。

### <a name="reduced-recompilations-for-workloads-using-temporary-tables-across-multiple-scopes-ctp-23"></a>使用多個範圍的暫存資料表減少重新編譯工作負載 (CTP 2.3)

在此功能推出之前，使用資料操作語言 (DML) 陳述式 (`SELECT`、`INSERT`、`UPDATE`、`DELETE`) 參考暫存資料表時，若暫存資料表是由外部範圍批次建立的，便會導致在每一次執行陳述式時重新編譯 DML 陳述式。 透過這項改善，SQL Server 可執行額外的輕量檢查，避免不必要的重新編譯：

- 檢查在編譯時期用於建立暫存資料表之外部範圍模組是否與用於連續執行的模組相同。 
- 追蹤任何在初始編譯時進行的資料定義語言 (DDL) 變更，並與連續執行的 DDL 操作比較。 

最終結果便是減少無關的重新編譯及 CPU 額外負荷。

### <a name="improved-indirect-checkpoint-scalability-ctp-23"></a>改善的間接檢查點延展性 (CTP 2.3)

在先前版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，使用者可能會在資料庫產生大量中途分頁 (例如 tempdb) 時遇到無產量的排程錯誤。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進改善的間接檢查點延展性，其有助於避免在具備大量 UPDATE/INSERT 工作負載的資料庫上發生這類錯誤。

### <a name="utf-8-support-ctp-23"></a>UTF-8 支援 (CTP 2.3)

完整支援廣泛使用 UTF-8 字元編碼作為匯入或匯出編碼，或作為文字資料的資料庫層級或資料行層級定序。 UTF-8 允許用於 `CHAR` 和 `VARCHAR` 資料類型，並且在建立物件定序或將其變更為具有 `UTF8` 尾碼的定序時啟用。 

例如，`LATIN1_GENERAL_100_CI_AS_SC` 至 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`。 UTF-8 僅適用於支援增補字元的 Windows 定序，已於 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中推出。 `NCHAR` 和 `NVARCHAR` 只允許 UTF-16 編碼，並維持不變。

此功能可能會節省大量儲存空間 (視使用的字元集而定)。 例如，使用啟用 UTF-8 的定序，將具有 ASCII (拉丁文) 字串的現有資料行資料類型從 `NCHAR(10)` 變更為 `CHAR(10)`，會使儲存體需求減少 50%。 這項減少的原因是 `NCHAR(10)` 需要 20 個位元組作為儲存空間，而 `CHAR(10)` 針對相同的 Unicode 字串需要 10 個位元組。

如需詳細資訊，請參閱 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。

**CTP 2.1** 新增在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 安裝期間選取 UTF-8 定序作為預設的支援。

**CTP 2.2** 新增在 SQL Server 複寫中使用 UTF-8 字元編碼的支援。

**CTP 2.3** 新增在 BIN2 定序 (UTF8_BIN2) 中使用 UTF-8 字元編碼的支援。

### <a name="scalar-udf-inlining-ctp-21"></a>純量 UDF 內嵌 (CTP 2.1)

純量 UDF 內嵌會將純量使用者定義函數 (UDF) 自動轉換成關聯運算式，並將它們內嵌在呼叫 SQL 查詢中，以改善運用純量 UDF 之工作負載的效能。 純量 UDF 內嵌有助於對 UDF 內的作業進行以成本為基礎的最佳化，以促成集合導向、平行且有效率的計畫，而不是無效率、反覆且連續的執行計畫。 根據預設，資料庫相容性層級 150 會啟用此功能。

如需詳細資訊，請參閱[純量 UDF 內嵌](../relational-databases/user-defined-functions/scalar-udf-inlining.md)。

### <a name="a-nametruncation-truncation-error-message-improved-to-include-table-and-column-names-and-truncated-value-ctp-21"></a><a name="truncation" />改善截斷錯誤訊息，以包含資料表和資料行名稱，以及被截斷的值 (CTP 2.1)

許多曾開發或維護資料移動工作負載的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 開發人員，都很熟悉錯誤訊息識別碼 8152 `String or binary data would be truncated`；此錯誤會在於結構描述不同的來源與目的地之間轉送資料，且來源資料太大而無法納入目的地資料類型的情況下發生。 對此錯誤訊息進行疑難排解，可能需要花費很多時間。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 針對此案例引進了更加特定的新錯誤訊息 (2628)：  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

新的錯誤訊息 2628 能針對資料截斷問題提供更多內容，以簡化疑難排解的程序。 

**CTP 2.1 和 CTP 2.2**：這是選擇加入的錯誤訊息，需要啟用[追蹤旗標](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460。

**CTP 2.4**：錯誤訊息 2628 已成為預設截斷訊息，且已取代資料庫相容性層級 150 下的錯誤訊息 8152。 已導入新的資料庫範圍組態 `VERBOSE_TRUNCATION_WARNINGS`，以便在資料庫相容性層級為 150 時能夠在錯誤訊息 2628 與 8152 之間切換。 如需詳細資訊，請參閱 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。
在資料庫相容性層級 140 或更低層級下，錯誤訊息 2628 會保有必須啟用[追蹤旗標](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460 的選擇加入錯誤訊息。

### <a name="improved-diagnostic-data-for-stats-blocking-ctp-21"></a>改善統計資料封鎖的診斷資料 (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 能針對等候同步統計資料更新作業的長時間執行查詢，提供改善的診斷資料。 動態管理檢視 `sys.dm_exec_requests` 資料行 `command` 會在 `SELECT` 正在等候同步統計資料更新作業完成以繼續查詢執行的情況下，顯示 `SELECT (STATMAN)`。 此外，新的等候類型 `WAIT_ON_SYNC_STATISTICS_REFRESH` 會顯示在 `sys.dm_os_wait_stats` 動態管理檢視中。 它會顯示花費在同步統計資料重新整理作業上的累積執行個體層級時間。

### <a name="hybrid-buffer-pool-ctp-21"></a>混合式緩衝集區 (CTP 2.1)

混合式緩衝集區是 SQL Server 資料庫的新功能，其中坐落在置於持續性記憶體 (PMEM) 裝置上之資料庫檔案上的資料庫頁面，會在必要時被直接存取。 由於 PMEM 裝置能為資料存取提供非常低的延遲，引擎便能放棄為緩衝集區之「乾淨頁面」區域中的資料製作複本，而可以直接在 PMEM 上存取該頁面。 存取是使用記憶體對應的 I/O 來執行，與啟用檔案的情況相同。 這可透過避免針對 DRAM 複製頁面，以及透過避免作業系統的 I/O 堆疊以存取持續性儲存體上的頁面來提供效能優勢。 此功能已於 Windows 及 Linux 上的 SQL Server 提供使用。

如需詳細資訊，請參閱[混合式緩衝集區](../database-engine/configure-windows/hybrid-buffer-pool.md)

### <a name="static-data-masking-ctp-21"></a>靜態資料遮罩 (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供靜態資料遮罩。 您可以使用靜態資料遮罩來處理 SQL Server 資料庫複本中的敏感性資料。 靜態資料遮罩可協助建立已處理的資料庫複本，其中的所有敏感性資訊都已經被更改為使該複本可與非生產使用者共用的形式。 靜態資料遮罩可用於開發、測試、分析與商務報告、合規性、疑難排解，以及任何其他無法將特定資料複製到不同環境的案例。

靜態資料遮罩會在資料行層級運作。 請選取要進行遮罩的資料行，並針對每個選取的資料行指定遮罩功能。 靜態資料遮罩會複製資料庫，然後將指定的遮罩功能套用至資料行。

#### <a name="static-data-masking-vs-dynamic-data-masking"></a>靜態資料遮罩與動態資料遮罩

資料遮罩是將遮罩套用到資料庫上以隱藏敏感性資訊，並以新的或已刪除的資料取代它的程序。 Microsoft 提供兩個遮罩選項：靜態資料遮罩與動態資料遮罩。 動態資料遮罩已於 [!INCLUDE[ssSQL16](../includes/sssql16-md.md)] 中推出。 下表會比較這兩個解決方案：

|靜態資料遮罩 |動態資料遮罩|
|:----|:----|
|在資料庫的複本上發生 <br/><br/>無法擷取原始資料<br/><br/>遮罩會在儲存體層級上發生<br/><br/>所有使用者都可以存取相同的已遮罩資料<br/><br/>適用於持續的全體小組存取|在原始資料庫上發生<br/><br/>原始資料保持不變<br/><br/>遮罩會在查詢階段即時發生<br/><br/>遮罩會視使用者權限而有所不同 <br/><br/>適用於精確的使用者特定存取|

### <a name="database-compatibility-level-ctp-20"></a>資料庫相容性層級 (CTP 2.0)

新增資料庫 **COMPATIBILITY_LEVEL 150**。 若要針對特定使用者資料庫啟用，請執行：

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="resumable-online-index-create-ctp-20"></a>可繼續的線上索引建立 (CTP 2.0)

**可繼續的線上索引建立**允許索引建立作業暫停並稍後可從作業暫停或失敗處繼續，而不是從頭重新啟動。

可繼續的線上索引建立支援下列情節：
- 在索引建立失敗之後繼續索引建立作業；例如，在資料庫容錯移轉之後或磁碟空間不足之後。
- 暫停進行中索引建立作業，並稍後繼續視需要允許暫時釋放系統資源，然後稍後繼續此作業。
- 建立大型索引，而不需要使用最多記錄空間，以及封鎖其他維護活動並允許截斷記錄的長時間執行交易。

如果索引建立失敗，則沒有此功能，必須重新執行線上索引建立作業，而且必須從頭重新啟動作業。

使用此版本，我們會擴充可繼續的功能，以將此功能新增至可用的[可繼續線上索引重建](http://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/)。

此外，可以使用[線上和可繼續 DDL 作業的資料庫範圍預設設定](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)將此功能設定為特定資料庫的預設值。

如需詳細資訊，請參閱[可繼續的線上索引建立](../t-sql/statements/create-index-transact-sql.md#resumable-indexes)。

### <a name="build-and-rebuild-clustered-columnstore-indexes-online-ctp-20"></a>線上建置和重建叢集資料行存放區索引 (CTP 2.0)

將資料列存放區資料表轉換成資料行存放區格式。 建立叢集資料行存放區索引 (CCI) 是舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的離線程序；需要所有變更在建立 CCI 時停止。 使用 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]，您可以在線上建立或重新建立 CCI。 工作負載不會遭到封鎖，而且對基礎資料所做的所有變更都會以透明的方式新增至目標資料行存放區資料表。 可使用的新 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式範例如下：

  ```sql
  CREATE CLUSTERED COLUMNSTORE INDEX cci
    ON <tableName>
    WITH (ONLINE = ON);
  ```

  ```sql
  ALTER INDEX cci
    ON <tableName>
    REBUILD WITH (ONLINE = ON);
  ```

### <a name="always-encrypted-with-secure-enclaves-ctp-20"></a>具有安全記憶體保護區的 Always Encrypted (CTP 2.0)

在具有就地加密和豐富計算的 Always Encrypted 時展開。 在伺服器端的安全記憶體保護區內，擴充來自啟用純文字資料的計算。

密碼編譯作業包含資料行加密和資料行加密金鑰輪替。 現在可以使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 發出這些作業，而且它們不需要將該資料移出資料庫。 安全記憶體保護區將 Always Encrypted 提供給一組同時具有下列需求的更廣泛情節：  

- 讓高權限但未經授權的使用者 (包括資料庫管理員、系統管理員、雲端操作員或惡意程式碼) 無法存取敏感性資料的需求。
- 資料庫系統內支援對受保護資料進行豐富計算的需求。

如需詳細資料，請參閱[具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。

> [!NOTE]
> 只有在 Windows OS 上才能使用具有安全記憶體保護區的 Always Encrypted。

### <a name="intelligent-query-processing-ctp-20"></a>智慧查詢處理 (CTP 2.0)

- 藉由調整批次和資料列模式運算子的記憶體授與大小，以在 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 引進的記憶體授與意見反應功能上展開**資料列模式記憶體授與意見反應**。 針對記憶體授與過多的狀況，如果授與的記憶體超過實際使用記憶體大小的兩倍，記憶體授與回饋便會重新計算記憶體授與。 連續執行接著會要求較少的記憶體。 針對記憶體授與大小不足以致磁碟溢出，記憶體授與意見反應會觸發記憶體授與的重新計算。 連續執行接著會要求更多的記憶體。 根據預設，資料庫相容性層級 150 會啟用此功能。

- **近似 COUNT DISTINCT** 會傳回群組中唯一非 Null 值的近似數目。 此函式設計成用於巨量資料情節。 此函式最適合用於下列所有條件都成立的查詢：
   - 存取最少數百萬個資料列的資料集。
   - 彙總一或多個具有大量不同值的資料行。
   - 回應比絕對精確更為重要。
      - `APPROX_COUNT_DISTINCT` 會傳回通常位於 2% 準確答案內的結果。
      - 而且它會在準確答案所需的一小段時間傳回概略答案。

- **資料列存放區上的批次模式**不再需要資料行存放區索引以批次模式處理查詢。 批次模式可讓查詢運算子作用於一組資料列，而不是一次只有一個資料列。 根據預設，資料庫相容性層級 150 會啟用此功能。 下列所有條件都成立時，批次模式可改善存取資料列存放區資料表的查詢速度：
   - 此查詢使用分析運算子 (例如聯結或彙總運算子)。
   - 查詢包含 100,000 個以上的資料列。
   - 查詢是 CPU 繫結，而不是輸入/輸出資料繫結。
   - 建立和使用資料行存放區索引有下列其中一個缺點：
      - 會在查詢中新增太多的額外負荷。
      - 或者，不可行，因為您的應用程式相依於資料行存放區索引尚未支援的功能。

- **資料表變數延遲編譯**可針對參考資料表變數的查詢，提升計劃品質和整體效能。 在最佳化和初始編譯期間，此功能將會根據實際資料表變數的資料列計數，傳播基數估計值。 這個精確的資料列計數資訊將用於最佳化下游計劃作業。 根據預設，資料庫相容性層級 150 會啟用此功能。

若要使用智慧查詢處理功能，請設定資料庫 `COMPATIBILITY_LEVEL = 150`。

### <a id="programmability"></a> Java 語言可程式性延伸模組 (CTP 2.0)

- **Java 語言延伸模組 (預覽)**：使用 Java 語言延伸模組在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中執行 Java 程式碼。 在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，當您將 [機器學習服務 (資料庫內)] 功能新增至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體時，會安裝此延伸模組。

### <a id="sqlgraph"></a> SQL Graph 功能 (CTP 2.3)

- **圖表比對查詢中的使用者衍生資料表或檢視別名 (CTP 2.1)** [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Preview 上的圖表查詢支援在 `MATCH` 語法中使用檢視及衍生資料表別名。 若要在 `MATCH` 中使用這些別名，檢視和衍生資料表必須是在節點集合或邊緣資料表集合上使用 `UNION ALL` 運算子建立。 節點或邊緣資料表上有可能會有，也有可能不會有篩選。 在 `MATCH` 查詢中使用衍生資料表和檢視別名的能力，對於您想要查詢圖形中兩個或多個實體之間的異質實體或異質連線的案例來說非常有用。

- **`MERGE` DML 中的比對支援 (CTP 2.0)** 可讓您在單一陳述式中指定圖形關聯性，而不必使用個別的 `INSERT`、`UPDATE` 或 `DELETE` 陳述式。 在 `MERGE` 陳述式中使用 `MATCH` 述詞，以合併節點或邊緣資料表中的目前圖形資料與新資料。 此功能會在邊緣資料表上啟用 `UPSERT` 情節。 使用者現在可以使用單一合併陳述式來插入新的邊緣或更新兩個節點之間的現有邊緣。

- **邊緣條件約束 (CTP 2.0)** 是針對 SQL Graph 中的邊緣資料表而導入的。 邊緣資料表可以將任何節點連線至資料庫中的任何其他節點。 引進邊緣條件約束時，您現在可以對此行為套用一些限制。 新的 `CONNECTION` 條件約束可以用來指定將允許指定邊緣資料表連線至結構描述的節點類型。 

  **(CTP 2.3)**：進一步擴充這項功能，您便可以在邊緣條件約束上定義串聯刪除動作。 您可以定義資料庫引擎在使用者刪除指定邊緣連線的節點時，所要採取的動作。

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations-ctp-20"></a>線上和可繼續 DDL 作業的資料庫範圍預設設定 (CTP 2.0)

- **線上和可繼續 DDL 作業的資料庫範圍預設設定**允許資料庫層級 `ONLINE` 和 `RESUMABLE` 索引作業的預設行為設定，而不是針對每個個別索引 DDL 陳述式定義這些選項 (例如索引建立或重建)。

- 使用 `ELEVATE_ONLINE` 和 `ELEVATE_RESUMABLE` 資料庫範圍設定選項，設定這些預設值。 這兩個選項都會讓引擎自動將支援的作業提升為索引線上或可繼續執行。 您可以使用這些選項來啟用下列行為：

  - `FAIL_UNSUPPORTED` 選項允許線上或可繼續所有索引作業，並讓不支援線上或可繼續的索引作業失敗。
  - `WHEN_SUPPPORTED` 選項允許線上或可繼續支援的作業，並離線或不可繼續執行索引的不受支援作業。
  - 除非 DDL 陳述式中明確指定，否則 `OFF` 選項允許離線和不可繼續執行所有索引作業的目前行為。

若要覆寫預設設定，請在索引建立和重建命令中包含 `ONLINE` 或 `RESUMABLE` 選項。 

如果沒有此功能，您必須直接在索引 DDL 陳述式中指定線上和可繼續選項 (例如索引建立和重建)。

如需索引可繼續作業的詳細資訊，請參閱 [Resumable Online Index Create](https://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/) (可繼續的線上索引建立)。

### <a id="ha"></a>Always On 可用性群組 - 更多同步複本 (CTP 2.0)

- **最多五個同步複本**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 會將同步複本的數量上限，從 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中最多為 3 的狀態增加至 5。 您可以設定這五個複本的群組，使其在群組內具備自動容錯移轉。 有一個主要複本，再加上四個同步次要複本。

- **次要到主要複本連線重新導向**：可將用戶端應用程式連線導向至主要複本，而不論連接字串中指定的目標伺服器為何。 此功能允許在沒有接聽程式的情況下進行連線重新導向。 在下列情況下，使用次要到主要複本連線重新導向：

  - 叢集技術不提供接聽程式功能。
  - 重新導向變得複雜的多子網路設定。
  - 閱讀叢集類型為 `NONE` 的向外延展或災害復原情節。

如需詳細資料，請參閱[次要到主要複本讀取/寫入連線重新導向 (Always On 可用性群組)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。

### <a name="data-discovery-and-classification-ctp-20"></a>資料探索與分類 (CTP 2.0)

資料探索與分類提供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 原生內建的進階功能。 分類和標記您最敏感的資料具有下列優點：
- 協助符合資料隱私權標準和法規合規性需求。
- 支援安全性情節，例如監視 (稽核)，以及警示敏感性資料的異常存取。
- 更輕鬆地識別敏感性資料在企業中的位置，讓系統管理員可以採取正確的步驟來保護資料庫。

如需詳細資訊，請參閱 [SQL 資料探索與分類](../relational-databases/security/sql-data-discovery-and-classification.md)。

也已經增強[稽核](../relational-databases/security/auditing/sql-server-audit-database-engine.md)，在稱為 `data_sensitivity_information` 的稽核記錄中包含新欄位，其中記錄查詢所傳回的實際資料敏感度分類 (標籤)。 如需詳細資料和範例，請參閱[新增敏感度分類](../t-sql/statements/add-sensitivity-classification-transact-sql.md)。

>[!NOTE]
>啟用稽核方式沒有任何變更。 有一個新欄位新增至稽核記錄 `data_sensitivity_information`，以記錄查詢所傳回的實際資料敏感度分類 (標籤)。 請參閱[稽核存取敏感性資料](/azure/sql-database/sql-database-data-discovery-and-classification/#subheading-3)。

### <a name="expanded-support-for-persistent-memory-devices-ctp-20"></a>持續性記憶體裝置的擴充支援 (CTP 2.0)

任何放在持續性記憶體裝置上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 檔案現在可在「已啟用」模式中操作。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會直接存取裝置，並使用有效率的 memcpy 作業來略過作業系統的儲存體堆疊。 此模式會改善效能，因為它允許這類裝置的低延遲輸入/輸出。
    - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 檔案範例包含：
        - 資料庫檔案
        - 交易記錄檔
        - 記憶體內部 OLTP 檢查點檔案
    - 持續性記憶體也稱為儲存類別記憶體。
    - 在一些非 Microsoft 網站上，持續性記憶體偶而會非正式地稱為 *pmem*。

> [!NOTE]
> 在此預覽版本中，只有在 Linux 上才能在持續性記憶體裝置上啟用檔案。 自 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 開始，Windows 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援持續性記憶體裝置。

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase-ctp-20"></a>DBCC CLONEDATABASE 中資料行存放區統計資料的支援 (CTP 2.0)

`DBCC CLONEDATABASE` 會建立資料庫的僅限結構描述複本，其中包含為查詢效能問題進行疑難排解所需的所有項目，而不需要複製資料。 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，此命令不會複製準確疑難排解資料行存放區索引查詢所需的統計資料，而且需要手動步驟才能擷取這項資訊。 現在，在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，`DBCC CLONEDATABASE` 會自動擷取資料行存放區索引的統計資料 blob，因此不需要任何手動步驟。

### <a name="new-options-added-to-spestimatedatacompressionsavings-ctp-20"></a>新增至 sp_estimate_data_compression_savings 的新選項 (CTP 2.0)

`sp_estimate_data_compression_savings` 傳回所要求物件的目前大小，並針對所要求的壓縮狀態預估物件大小。 此程序目前支援三個選項：`NONE`、`ROW` 和 `PAGE`。 `COLUMNSTORE_ARCHIVE` 推出了兩個新選項：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 `COLUMNSTORE`。 如果在使用標準或封存資料行存放區壓縮的資料表上建立資料行存放區索引，則這些新選項可讓您估計節省的空間。

### <a id="ml"></a> SQL Server 機器學習服務容錯移轉叢集和磁碟分割型模型 (CTP 2.0)

- **資料分割型模型**：使用新增至 `sp_execute_external_script` 的參數，處理您資料每個資料分割的外部指令碼。 此功能支援訓練許多小型模型 (每個資料的資料分割一個模型)，而不是一個大型模型。

- **Windows Server 容錯移轉叢集**：在 Windows Server 容錯移轉叢集上設定機器學習服務的高可用性。

如需詳細資訊，請參閱 [SQL Server 機器學習服務的新功能](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default-ctp-20"></a>預設已啟用的輕量型查詢分析基礎結構 (CTP 2.0)

輕量型查詢分析基礎結構 (LWP) 提供比標準分析機制更具效率的查詢效能資料。 根據預設，現在會啟用輕量型分析。 它已在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 中引進。 相較於標準查詢分析機制有最多 75% CPU 的額外負荷，輕量型查詢分析提供預期額外負荷為 2% CPU 的查詢執行統計資料收集機制。 在舊版中，根據預設，它為 OFF。 資料庫管理員可以使用[追蹤旗標 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 來啟用它。 

如需輕量型分析的詳細資訊，請參閱[查詢分析基礎結構](../relational-databases/performance/query-profiling-infrastructure.md)。

**CTP 2.3** 引進了新的資料庫範圍設定 `LIGHTWEIGHT_QUERY_PROFILING`，來啟用或停用輕量型查詢分析基礎結構。

### <a id="polybase"></a>新的 PolyBase 連接器

- **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的新連接器**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的外部資料新連接器。

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information-ctp-20"></a>新的 sys.dm_db_page_info 系統函數會傳回頁面資訊 (CTP 2.0)

`sys.dm_db_page_info(database_id, file_id, page_id, mode)` 傳回資料庫中頁面的資訊。 此函式會傳回包含頁面中標頭資訊的資料列，包含 `object_id`、`index_id` 和 `partition_id`。 在大部分情況下，有此函式就不需要使用 `DBCC PAGE`。 

為了簡化頁面相關等候的疑難排解，也已將稱為 page_resource 的新資料行新增至 `sys.dm_exec_requests` 和 `sys.sysprocesses`。 這個新的資料行可讓您透過另一個新的系統函數 `sys.fn_PageResCracker` 將 `sys.dm_db_page_info` 加入這些檢視表。 請參閱下列指令碼作為範例：

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d 
  CROSS APPLY sys.fn_PageResCracker(d.page_resource) AS r
  CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id,'DETAILED')
    AS page_info;
```

## <a id="sqllinux"></a> Linux 上的 SQL Server

- **具有 Kubernetes 之 Docker 容器上的 Always On 可用性群組 (CTP 2.2)**：Kubernetes 可協調執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的容器，以提供一組具有 SQL Server Always On 可用性群組的高可用性資料庫。 Kubernetes 運算子會部署 StatefulSet，包括具有 **mssql-server 容器**和健康狀態監視的容器。

- **新容器登錄 (CTP 2.1)**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的所有容器映像現在都位於 Microsoft 容器登錄中。 Microsoft 容器登錄是散發 Microsoft 產品容器的官方容器登錄。 此外，現在已發佈認證的 RHEL 型映像。

  - Microsoft 容器登錄：`mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - 認證的 RHEL 型容器映像：`mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

- **複寫支援 (CTP 2.0)**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援 Linux 上的 SQL Server 複寫。 具有 SQL Agent 的 Linux 虛擬機器可以是發行者、散發者或訂閱者。 

  建立下列類型的發行：
  - 異動
  - 快照式
  - 合併式

  設定複寫 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或使用[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

- **支援 Microsoft Distributed Transaction Coordinator (MSDTC) (CTP 2.0)**：Linux 上的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援 Microsoft Distributed Transaction Coordinator (MSDTC)。 如需詳細資料，請參閱[如何在 Linux 上設定 MSDTC](../linux/sql-server-linux-configure-msdtc.md)。

- **協力廠商 AD 提供者的 OpenLDAP 支援 (CTP 2.0)**：Linux 上的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援 OpenLDAP，可讓協力廠商提供者加入 Active Directory。

- **Linux 上的機器學習 (CTP 2.0)**：Linux 現在支援 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 機器學習服務 (資料庫內)。 支援包含 `sp_execute_external_script` 預存程序。 如需如何在 Linux 上安裝機器學習服務的指示，請參閱[在 Linux 上安裝 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 機器學習服務 R 和 Python 支援](../linux/sql-server-linux-setup-machine-learning.md)。

## <a id="mds"></a> Master Data Services 

- **Silverlight 控制項已取代為 HTML (CTP 2.0)**：Master Data Services (MDS) 入口網站已不再相依於 Silverlight。 所有先前的 Silverlight 元件已取代為 HTML 控制項。

## <a id="security"></a>安全性

- **SQL Server 組態管理員中的憑證管理 (CTP 2.0)**：SSL/TLS 憑證普遍用來保護 SQL Server 執行個體的存取。 憑證管理現在整合至 SQL Server 組態管理員，並簡化一般工作，例如：

  - 檢視和驗證 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體中所安裝的憑證。 
  - 檢視即將到期的憑證。
  - 將憑證部署到參與 Always On 可用性群組的電腦 (從保留主要複本的節點)。
  - 將憑證部署到參與容錯移轉叢集執行個體的電腦 (從使用中節點)。

  > [!NOTE]
  > 使用者必須具有所有叢集節點的管理員權限。

## <a id="tools"></a>工具

- [**Azure Data Studio**](../azure-data-studio/what-is.md)：先前以 SQL Operations Studio 預覽名稱發行，Azure Data Studio 是輕量級、現代化、開放原始碼且跨平台的桌面工具，適用於資料開發和管理中的最常見工作。 使用 Azure Data Studio 及 [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Preview 延伸模組](../azure-data-studio/sql-server-2019-extension.md)，可在 Windows、macOS 和 Linux 上連線到內部部署及雲端中的 SQL Server。 Azure Data Studio 可讓您：

  - 現已支援 AAD。 (CTP 2.3)
  - 筆記本檢視 UI 已移動到 Azure Data Studio 核心。 (CTP 2.3)
  - 已新增新的精靈，可從 Hadoop 分散式檔案系統 (HDFS) 建立 SQL Server 巨量資料叢集的外部資料來源。 (CTP 2.3)
  - 改善筆記本檢視器 UI。 (CTP 2.3)
  - 新增新的筆記本 API。 (CTP 2.3)
  - 新增「重新安裝筆記本相依性」命令，協助更新 Python 套件。 (CTP 2.3)
  - 連線及管理 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 巨量資料叢集。 (CTP 2.1)
  - 在具有快速 Intellisense、程式碼片段和原始檔控制整合的新式開發環境中編輯和執行查詢。 (CTP 2.0) 
  - 使用內建結果集圖表，將資料快速視覺化。 (CTP 2.0)
  - 使用可自訂的小工具建立伺服器和資料庫的自訂儀表板。 (CTP 2.0)  
  - 輕鬆地管理更廣泛使用具有內建終端機的環境。 (CTP 2.0)
  - 分析建置在 Jupyter 上整合式筆記型體驗中的資料。 (CTP 2.0)
  - 使用自訂佈景主題和延伸模組來增強您的體驗。(CTP 2.0)
  - 以及使用內建訂用帳戶和資源瀏覽器來探索 Azure 資源。 (CTP 2.0)
  - 支援使用 SQL Server 巨量資料叢集的案例。 (CTP 2.0)
  
  > [!TIP]
  > 針對 Azure Data Studio 的最新改善，請參閱 [Azure Data Studio 版本資訊](../azure-data-studio/release-notes-azure-data-studio.md)。

- [**SQL Server Management Studio (SSMS) 18.0 (預覽)**](../ssms/sql-server-management-studio-ssms.md)：支援 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。

  - 從 SSMS 啟動 Azure Data Studio。 (CTP 2.3)
  - 具有安全記憶體保護區的 Always Encrypted 支援。 (CTP 2.0)
  - 較小的下載大小。 (CTP 2.0)
  - 現在根據 Visual Studio 2017 Isolated Shell。 (CTP 2.0)
  - 如需完整清單，請參閱 [SSMS 變更記錄](../ssms/sql-server-management-studio-changelog-ssms.md)。 (CTP 2.0)

- [**SQL Server PowerShell 模組**](http://www.powershellgallery.com/packages/SqlServer/21.1.18080)：SqlServer PowerShell 模組允許 SQL Server 開發人員、管理員及 BI 專業人員自動化資料庫部署及伺服器管理。

  - 從 21.0 升級至 21.1，以支援 SMO v150。
  - 更新 SQL Server 提供者 (SQLRegistration)，以顯示 AS/IS/RS 群組。
  - 修正瞄準 SQL Server 2014 時，`New-SqlAvailabilityGroup` Cmdlet 中的問題。
  - 將 `–LoadBalancedReadOnlyRoutingList` 參數新增至 `Set-SqlAvailabilityReplica` 及 `New-SqlAvailabilityReplica`。
  - 更新 `AnalysisService` Cmdlet，針對 Azure Analysis Services 使用來自 `Login-AzureAsAccount` 的快取登入權杖。

## <a id="ssas"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS) 

### <a name="many-to-many-relationships-in-tabular-models-ctp-24"></a>表格式模型中的多對多關聯性 (CTP 2.4)

這項功能可讓資料行並非唯一的兩個資料表建立彼此之間的多對多關聯性。 關聯性可定義於維度與事實資料表之間，且其細微性可高於維度的索引鍵資料行。 如此即無須將維度資料表正規化，並且可以改善使用者體驗，因為產生的模型會有較少的資料表，且具有以邏輯方式分組的資料行。 在此 CTP 2.4 版本中，多對多關聯性是僅限引擎的功能。 

要建立多對多關聯性，模型必須位於 1470 相容性層級，而目前只有 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 及更新版本可支援該層級。 在此 CTP 2.4 版本中，您可以使用表格式物件模型 (TOM) API、表格式模型指令碼語言 (TMSL) 及開放原始碼表格式編輯器工具，來建立多對多關聯性。 未來版本中將會包含 SQL Server Data Tools (SSDT) 中的支援及文件。 Analysis Services 部落格中會提供此項目的額外資訊及其他 CTP 功能版本。

### <a name="memory-settings-for-resource-governance-ctp-24"></a>資源治理的記憶體設定 (CTP 2.4)

此處說明的記憶體設定現已可在 Azure Analysis Services 中使用。 從 CTP 2.4 開始，[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Analysis Services 也已支援這些設定。 

- **Memory\QueryMemoryLimit** - 這個記憶體屬性可用來限制提交至模型的 DAX 查詢所建置的記憶體多工緩衝處理。 
- **DbpropMsmdRequestMemoryLimit** - 此 XMLA 屬性可用來覆寫連線的 Memory\QueryMemoryLimit 伺服器屬性值。
- **OLAP\Query\RowsetSerializationLimit** - 此伺服器屬性可限制資料列集中傳回的資料列數目，以防止伺服器資源用於大量的資料匯出。 此屬性對 DAX 和 MDX 查詢均適用。

這些屬性可使用最新版的 SQL Server Management Studio (SSMS) 來設定。 Analysis Services 部落格將提供此功能的相關資訊。

### <a name="calculation-groups-in-tabular-models-ctp-23"></a>表格式模型 (CTP 2.3) 中的計算群組 

計算群組解決可能擁有使用相同計算 (例如時間智慧) 測量擴散複雜模型中常見的問題。 計算群組會作為具有單一資料行的資料表，顯示在報告用戶端中。 資料行中每個值都代表可重複使用的計算或計算項目，且可以套用到任何量值。  

計算群組可擁有任意數量的計算項目。 每個計算項目都由一個 DAX 運算式定義。 我們引進了三個新的 DAX 函式，可搭配計算群組使用： 

- `SELECTEDMEASURE()` - 傳回目前處於內容中的量值參考。  

- `SELECTEDMEASURENAME()` - 傳回包含目前處於內容中量值名稱的字串。  

- `ISSELECTEDMEASURE(M1, M2, …)` - 傳回布林值，指出目前處於內容中之量值是否是其中一個指定為引數的項目。

除了新的 DAX 函式外，還引進了兩個新的動態管理檢視：

- `TMSCHEMA_CALCULATION_GROUPS`  
- `TMSCHEMA_CALCULATION_ITEMS`  

#### <a name="limitations-in-this-release"></a>此版本中的限制：

- 尚未支援 `ALLSELECTED DAX` 函式。
- 尚未支援計算群組資料表上定義的資料列層級安全性。
- 尚未支援計算群組資料表上定義的物件層級安全性。
- 尚未支援指向計算項目的 DetailsRows 運算式。
- 尚未支援 MDX。

#### <a name="known-issues-in-this-release"></a>此版本的已知問題：

- 模型中若有計算群組存在，可能導致量值傳回變異的資料類型，進而導致參考量值的計算資料行和資料表的重新整理失敗。

#### <a name="compatibility-level"></a>相容性層級

計算群組需要模型位於 1470 相容性層級，該層級目前只在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.3 及更新版本中獲得支援。 目前，您可以使用表格式物件模型 (TOM) API、表格式模型指令碼語言 (TMSL) 及開放原始碼表格式編輯器工具，來建立計算群組。 未來版本中將會包含 SQL Server Data Tools (SSDT) 中的支援及文件。 Analysis Services 部落格中會提供此項目的額外資訊及其他 CTP 功能版本。

## <a name="other-services"></a>其他服務

從 CTP 2.4 開始，[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 不會針對下列服務推出新功能：

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="next-steps"></a>後續步驟

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 版本資訊](sql-server-ver15-release-notes.md)。

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]：Technical white paper](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />在 2018 年 9 月發佈。 適用於 Windows、Linux 及 Docker 容器的 Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
