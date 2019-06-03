---
title: 資料庫引擎的新功能 - SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 850f0bac65f0c8955c50514145fb0d2998d6139a
ms.sourcegitcommit: 249c0925f81b7edfff888ea386c0deaa658d56ec
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/30/2019
ms.locfileid: "66413608"
---
# <a name="whats-new-in-database-engine---sql-server-2016"></a>資料庫引擎的新功能 - SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

本主題摘要說明 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]版中引進的增強功能。  這些新功能和增強功能可提升設計、開發和維護資料儲存系統之架構設計師、開發人員和管理員的能力和生產力。

若要檢閱其他 SQL Server 元件的新功能，請參閱 [SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)。

> [!NOTE]
>  [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 是 64 位元應用程式。 即使有些元素是以 32 位元元件的形式執行，32 位元安裝已然中止。

#### <a name="try-it-out"></a>現在就試試看

- 若要下載 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]，請前往 **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** ![下載](../analysis-services/media/download.png "下載")。

- 有 Azure 帳戶嗎？  接著前往 **[這裡](https://azure.microsoft.com/services/virtual-machines/sql-server/)** ，來加速已安裝 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的虛擬機器。

> [!NOTE]
> 如需目前的版本資訊，請參閱 [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)。
  
## <a name="sql-server-2016-service-pack-1-sp1"></a>SQL Server 2016 Service Pack 1 (SP1)  
-  [程序](../t-sql/statements/create-procedure-transact-sql.md)、[檢視](../t-sql/statements/create-view-transact-sql.md)、[函式](../t-sql/statements/create-function-transact-sql.md)和[觸發程序](../t-sql/statements/create-trigger-transact-sql.md)現在可以使用 `CREATE OR ALTER <object>` 語法。
-   已新增更一般的查詢提示模型支援︰ `OPTION (USE HINT('<hint1>', '<hint2>'))`。 如需詳細資訊，請參閱 [查詢提示 (Transact-SQL)](../t-sql/queries/hints-transact-sql-query.md)。  
- [sys.dm_exec_valid_use_hints](../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) DMV 已新增至清單提示。  
- 已新增 [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) DMV 來傳回 showplan XML 暫時性統計資料。  
- [sys.dm_db_incremental_stats_properties](../relational-databases/system-dynamic-management-views/sys-dm-db-incremental-stats-properties-transact-sql.md) DMV 已新增至指定資料表的累加統計資料。  
- `instant_file_initialization_enabled` 資料行已新增至 [sys.dm_server_services](../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)。  
- `estimated_read_row_count` 資料行已新增至 [sys.dm_exec_query_profiles](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)。  
-  `sql_memory_model` 和 `sql_memory_model_desc` 資料行已新增至 [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 來提供記憶體頁面鎖定模型的相關資訊。
-  已擴充支援多項功能的版本。 這包括在所有版本中新增資料列層級安全性、Always Encrypted、動態資料遮罩、資料庫稽核、記憶體內部 OLTP 和其他數項功能。 如需詳細資訊，請參閱 [SQL Server 2016 的版本及支援功能](../sql-server/editions-and-supported-features-for-sql-server-2016.md)。   
-  使用 Always On 加密的物件重新定義時，[sp_refresh_parameter_encryption](../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) 允許 Always On 加密來更新中繼資料。  


##  <a name="Feature"></a> SQL Server 2016 RTM
本節包含下列小節：

-   [資料行存放區索引](#columnstore-indexes)
-   [資料庫範圍的組態](#database-scoped-configurations)
-   [記憶體內部 OLTP](#in-memory-oltp)
-   [查詢最佳化工具](#query-optimizer)
-   [即時查詢統計資料](#live-query-statistics)
-   [查詢存放區](#query-store)
-   [時態表](#temporal-tables)
-   [Microsoft Azure Blob 儲存體的等量備份](#striped-backups-to-microsoft-azure-blob-storage)
-   [Microsoft Azure Blob 儲存體的檔案快照備份](#file-snapshot-backups-to-microsoft-azure-blob-storage)
-   [受管理備份](#managed-backup)
-   [TempDB 資料庫](#tempdb-database)
-   [內建 JSON 支援](#built-in-json-support)
-   [PolyBase](#polybase)
-   [Stretch Database](#stretch-database)
-   [UTF-8 支援](#support-for-utf-8)
-   [新的預設資料庫大小和自動成長值](#new-default-database-size-and-autogrow-values)
-   [Transact-SQL 增強功能](#transact-sql-enhancements)
-   [系統檢視表增強功能](#system-view-enhancements)
-   [安全性增強功能](#security-enhancements)
-   [高可用性增強功能](#high-availability-enhancements)
-   [複寫增強功能](#replication-enhancements)
-   [工具增強功能](#tools-enhancements)

## <a name="columnstore-indexes"></a>資料行存放區索引

此版本提供了資料行存放區索引的改進，包括可更新的非叢集資料行存放區索引、記憶體內部資料表上的資料行存放區索引，以及作業分析的許多新功能。

- 升級後可以更新唯讀的非叢集資料行存放區索引。  不需要重建索引，即可進行更新。

- 已改進資料行存放區索引 (尤其是彙總和字串述詞) 的分析查詢效能。

- DMV 和 XEvent 的支援能力有所改進。

如需詳細資訊，請參閱《線上叢書》的[資料行存放區索引指南](../relational-databases/indexes/columnstore-indexes-overview.md)一節中的下列主題：

- [資料行存放區索引建立版本功能摘要](~/relational-databases/indexes/columnstore-indexes-what-s-new.md) - 包含新功能。

- [資料行存放區索引資料載入](../relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)

- [資料行存放區索引效能](~/relational-databases/indexes/columnstore-indexes-query-performance.md)

- [開始使用資料行存放區進行即時作業分析](../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)

- [資料倉儲的資料行存放區索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

- [資料行存放區索引重組](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)


## <a name="database-scoped-configurations"></a>資料庫範圍的設定


新的 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 陳述式可讓您控制特定資料庫的特定組態。 這些組態設定會影響應用程式行為。

[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 和 [!INCLUDE[sqldbesa](../includes/sqldbesa-md.md)] 都提供此新的陳述式。



## <a name="in-memory-oltp"></a>記憶體內部 OLTP


### <a name="storage-format-change"></a>儲存格式變更

SQL Server 2014 和 2016 的記憶體最佳化資料表的儲存格式已變更。 針對 SQL Server 2014 的升級及附加/還原，已序列化新的儲存格式，並在資料庫復原期間重新啟動資料庫一次。

- [升級為 SQL Server 2016](../database-engine/install-windows/upgrade-sql-server.md)


### <a name="alter-table-is-log-optimized-and-runs-in-parallel"></a>ALTER TABLE 已最佳化記錄檔，並且會平行執行

現在，當您在記憶體最佳化資料表上執行 ALTER TABLE 陳述式時，只有中繼資料變更會寫入記錄檔。 這可大幅減少記錄 IO。 此外，大部分的 ALTER TABLE 案例現在會平行執行，因此可大幅縮減陳述式的持續時間。

- 如需非平行例外狀況 (包括 LOB)，請參閱[改變記憶體最佳化資料表](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)。



### <a name="statistics"></a>統計資料

現在會自動更新[記憶體最佳化資料表的統計資料](../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md)。 此外，現在支援透過取樣來收集統計資料，如此可讓您避免使用較費時的 fullscan 方法。


### <a name="parallel-and-heap-scan-for-memory-optimized-tables"></a>記憶體最佳化資料表的平行和堆積掃描

記憶體最佳化資料表及記憶體最佳化資料表索引現在都支援平行掃描。 這可改善分析查詢的效能。

此外，也支援堆積掃描，而且可以平行執行。 如果是記憶體最佳化資料表，堆積掃描指的是使用儲存資料列的記憶體內部堆積資料結構，掃描資料表的所有資料列。 若是完整資料表掃描，使用堆積掃描比索引更有效率。

### <a name="transact-sql-improvements-for-memory-optimized-tables"></a>記憶體最佳化資料表的 Transact-SQL 改進

針對 SQL Server 2014 記憶體最佳化資料表不支援的幾個 Transact-SQL 元素，SQL Server 2016 現在已提供支援：


- 支援 UNIQUE 條件約束和索引。


- 支援記憶體最佳化資料表之間的「外部索引鍵」參考。
  - 這些外部索引鍵只能參考主索引鍵，而無法參考唯一索引鍵。


- 支援 CHECK 條件約束。

- 非唯一索引可允許其索引鍵中有 NULL 值。

- 記憶體最佳化資料表支援「觸發程序」。
  - 僅支援 AFTER 觸發程序。 不支援 INSTEADOF 觸發程序。
  - 記憶體最佳化資料表上的所有觸發程序都必須使用 WITH NATIVE_COMPILATION。

- 完整支援所有的 SQL Server 字碼頁和索引定序，以及記憶體最佳化資料表和原生編譯 T-SQL 模組中的其他成品。


- 支援[改變記憶體最佳化資料表](../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)：
  - ADD 和 DROP 索引。 變更雜湊索引的 bucket_count。
  - 變更結構描述︰新增/卸除/改變資料行；新增/卸除條件約束。

- 記憶體最佳化資料表現在可以有長度合計超過 8060 個位元組頁面長度的多個資料行。 例如，資料表可以有三個 `nvarchar(4000)`類型的資料行。 在此範例中，部分資料行現在會以非資料列形式儲存。 您的查詢並不知道資料行是否在資料列上。

- 記憶體最佳化資料表現在也支援 [LOB (大型物件) 類型](../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) `varbinary(max)`、`nvarchar(max)` 和 `varchar(max)`。


如需整體資訊，請參閱：

- [記憶體內部 OLTP 不支援的 Transact-SQL 建構](../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)
- [記憶體內部 OLTP 不支援的 SQL Server 功能](~/relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)



### <a name="performance-and-scaling-improvements"></a>效能和調整改進

- 資料大小不再有任何限制。 請參閱 [估計記憶體最佳化資料表的記憶體需求](~/relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)。

- 有多個並行執行緒負責 [將記憶體最佳化資料表的變更保存到磁碟](../relational-databases/in-memory-oltp/scalability.md)。

- [使用解譯的 Transact-SQL 存取記憶體最佳化資料表](../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md)的平行計畫支援。


### <a name="enhancements-in-sql-server-management-studio"></a>SQL Server Management Studio 的改進

- [判斷是否應將資料表或預存程序匯出至記憶體內部 OLTP](../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)不再需要設定資料收集器或管理資料倉儲。 報告現在可以直接在生產資料庫上執行。

- [用於移轉評估的 PowerShell Cmdlet](../relational-databases/in-memory-oltp/powershell-cmdlet-for-migration-evaluation.md)，可評估 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中多個物件的移轉適用性。

- 以滑鼠右鍵按一下資料庫，然後選取 [工作] -> [產生記憶體內 OLTP 移轉檢查清單]，即可產生移轉檢查清單。

### <a name="cross-feature-support"></a>跨功能支援

- 支援使用暫時系統版本設定功能搭配記憶體內部 OLTP。 如需詳細資訊，請參閱[系統版本設定時態表與記憶體最佳化資料表](../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)

- 對記憶體內部 OLTP 工作負載中原生編譯程式碼的查詢存放區支援。 如需詳細資訊，請參閱 [使用含有記憶體內部 OLTP 的查詢存放區](../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)。

- [記憶體最佳化資料表中的資料列層級安全性](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md#rls)

- [使用 Multiple Active Result Set &#40;MARS&#41;](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) 連接現在可以存取記憶體最佳化資料表和原生編譯的預存程序。

- [透明資料加密 (TDE)](../relational-databases/security/encryption/transparent-data-encryption.md) 支援。 如果資料庫已設定加密，則[記憶體最佳化檔案群組](../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)中的檔案現在也會加密。

如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。


## <a name="query-optimizer"></a>查詢最佳化工具
### <a name="compatibility-level-guarantees"></a>相容性層級保證
將資料庫升級至 SQL Server 2016 時，如果沿用舊版的相容性層級 (例如，120 或 110)，就不會出現任何計畫變更。 與查詢最佳化工具有關的新功能和增強功能，只有在最新的相容性層級下才能使用。 
### <a name="trace-flag-4199"></a>追蹤旗標 4199
一般而言，您不需要在 SQL Server 2016 中使用追蹤旗標 4199，因為在 SQL Server 2016 中的最新相容性層級 (130) 下已無條件地啟用此追蹤旗標所控制的大部分查詢最佳化工具行為。
### <a name="new-referential-integrity-operator"></a>新的參考完整性運算子
一個資料表最多可以參考其他 253 個資料表和資料行作為外部索引鍵 (連出參考)。 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 將單一資料表中資料行可以參考的其他資料表和資料行數目限制 (連入參考) 從 253 提高至 10,000。 相關限制，請參閱 [Create Foreign Key Relationships](../relational-databases/tables/create-foreign-key-relationships.md)。 引進的新參考完整性運算子 (相容性層級 130) 會就地執行參考完整性檢查。 對有大量內送參考的資料表，這會改善 UPDATE 和 DELETE 作業的整體效能，讓它可容納大量的傳入參考。 如需詳細資訊，請參閱 [Query Optimizer Additions in SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/23/query-optimizer-additions-in-sql-server/)(SQL Server 2016 的查詢最佳化工具新增項目)。
### <a name="parallel-update-of-sampled-statistics"></a>取樣統計資料的平行更新
取樣資料建立統計資料現在可以平行方式完成 (相容性層級 130)，改善統計資料集合的效能。 如需詳細資訊，請參閱[更新統計資料](../t-sql/statements/update-statistics-transact-sql.md)。
### <a name="sublinear-threshold-for-update-of-statistics"></a>統計資料更新的次線性閾值
大型資料表的統計資料自動更新現在更為積極 (相容性層級 130)。 觸發自動更新統計資料的閾值為 20%，自 SQL Server 2016 起，當大型資料表中的列數增加時，這個閾值會開始降低 (仍為百分比)。 您不再需要設定追蹤旗標 2371 來降低此閾值。 
### <a name="other-enhancements"></a>其他增強功能
Insert-select 陳述式中的 Insert 是多執行緒，或可以有平行計畫 (相容性層級 130)。 若要取得平行計劃，請使用 INSERT ...SELECT 陳述式必須使用 TABLOCK 提示。 如需詳細資訊，請參閱 [Parallel Insert Select](https://blogs.msdn.microsoft.com/sqlcat/2016/07/06/sqlsweet16-episode-3-parallel-insert-select/)(平行的 Insert Select)。

## <a name="live-query-statistics"></a>即時查詢統計資料
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 可供檢視作用中查詢的即時執行計畫。 這個即時查詢計畫會隨著控制項在查詢計畫運算子之間流動，提供查詢執行程序的即時深入資訊。 如需相關資訊，請參閱 [Live Query Statistics](../relational-databases/performance/live-query-statistics.md)。

## <a name="query-store"></a>查詢存放區
查詢存放區是一項新功能，可為 DBA 提供查詢計劃選擇及效能的深入資訊。 它能讓您快速找出因為查詢計劃中的變更所導致的效能差異，以簡化效能疑難排解。 該功能會自動擷取查詢、計劃及執行階段統計資料的記錄，並會保留這些記錄供您檢閱。 其會以時段來區分資料、供您查看資料庫使用模式，並了解何時在伺服器上發生查詢計劃變更。 查詢存放區會使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 對話方塊呈現資訊，並可讓您對其中一個選取的查詢計劃強制執行查詢。 如需相關資訊，請參閱 [Monitoring Performance By Using the Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)。


## <a name="temporal-tables"></a>時態表
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 現在支援系統版本設定時態表。 時態表是新的資料表類型，可提供任何時間點的預存事實相關正確資訊。 實際上每個時態表都包含兩個資料表，一個用於目前資料，一個用於歷史資料。 系統會確保資料表中的資料隨著目前資料變更時，先前的值會存放在歷史資料表中。 系統會提供查詢建構，對使用者隱藏此複雜部分。 如需相關資訊，請參閱 [Temporal Tables](../relational-databases/tables/temporal-tables.md)。

## <a name="backups"></a>備份

### <a name="striped-backups-to-microsoft-azure-blob-storage"></a>Microsoft Azure Blob 儲存體的等量備份
在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 中，使用 Microsoft Azure Blob 儲存體服務的 SQL Server 備份至 URL 功能現在支援使用區塊 Blob 的等量備份組，最多可支援 12.8 TB 的備份大小。 如需範例，請參閱＜ [Code Examples](../relational-databases/backup-restore/sql-server-backup-to-url.md#Examples)＞。

### <a name="file-snapshot-backups-to-microsoft-azure-blob-storage"></a>Microsoft Azure Blob 儲存體的檔案快照備份
 在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]中，SQL Server 備份至 URL 功能現在支援使用 Azure 快照集來備份資料庫，其中所有的資料庫檔案都是使用 Microsoft Azure Blob 儲存體服務來進行儲存。 如需詳細資訊，請參閱 [Azure 中資料庫檔案的檔案快照集備份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。

### <a name="managed-backup"></a>受控備份
在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 中，SQL Server Managed Backup to Microsoft Azure 會對備份檔案使用新的區塊 Blob 儲存體。 Managed Backup 還有幾項變更和增強功能。

-   支援備份的自動化和自訂排程。

-   支援系統資料庫的備份

-   支援使用簡單復原模式的資料庫。

 如需相關資訊，請參閱 [SQL Server Managed Backup to Microsoft Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)

> [!NOTE]
>  對於 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]，這些新的受管理備份功能在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中還沒有對應的 UI 支援。

## <a name="tempdb-database"></a>TempDB 資料庫
 TempDB 有數個增強功能︰

-   tempdb 不再需要追蹤旗標 1117 和 1118。 如果有多個 tempdb 資料庫檔案，則視成長設定而定，所有的檔案會都同時成長。 此外，tempdb 中的所有配置都會使用統一範圍。

-   根據預設，安裝程式會新增與 CPU 計數一樣多個或 8 個 empdb 檔案 (以較低者為準)

-   在安裝期間，您可以使用新的 UI 輸入控制項，在 SQL Server 安裝精靈的 [資料庫引擎組態 - TempDB] 區段上，設定 tempdb 資料庫檔案數目、初始大小、自動成長和目錄位置。

-   預設初始大小為 8MB，而預設自動成長為 64 MB。

-   您可以為 tempdb 資料庫檔案指定多個磁碟區。 若指定多個目錄，tempdb 資料檔案將以循環配置資源方式跨多個目錄存放。

## <a name="built-in-json-support"></a>內建 JSON 支援
SQL Server 2016 新增對匯入和匯出 JSON 以及使用 JSON 字串的內建支援。 此內建支援包含下列陳述式和函數。

-   將 **FOR JSON** 子句加入 **SELECT** 陳述式，以將查詢結果格式化為 JSON，或匯出 JSON。 例如，使用 **FOR JSON** 子句，將來自用戶端應用程式的 JSON 輸出格式設定委派給 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱[使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。

-   呼叫 **OPENJSON** 資料列集提供者函數，以將 JSON 資料轉換成資料列和資料行。 使用 **OPENJSON** 將 JSON 資料匯入 SQL Server，或者針對目前無法直接取用 JSON 的應用程式或服務，將 JSON 資料轉換為資料列和資料行。 如需詳細資訊，請參閱[使用 OPENJSON 將 JSON 資料轉換成資料列和資料行 &#40;SQL Server&#41;](../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)。

-   **ISJSON** 函數可測試字串是否包含有效的 JSON。 如需詳細資訊，請參閱 [ISJSON &#40;Transact-SQL&#41;](../t-sql/functions/isjson-transact-sql.md)

-   **JSON_VALUE** 函數可從 JSON 字串擷取純量值。如需詳細資訊，請參閱 [JSON_VALUE &#40;Transact-SQL&#41;](../t-sql/functions/json-value-transact-sql.md)。

-   **JSON_QUERY** 函數可從 JSON 字串擷取物件或陣列。 如需詳細資訊，請參閱 [JSON_QUERY &#40;Transact-SQL&#41;](../t-sql/functions/json-query-transact-sql.md)。

-   **JSON_MODIFY** 函數可更新 JSON 字串中的屬性值，並傳回更新後的 JSON 字串。 如需詳細資訊，請參閱 [JSON_MODIFY &#40;Transact-SQL&#41;](../t-sql/functions/json-modify-transact-sql.md)。

## <a name="polybase"></a>PolyBase
 PolyBase 可讓您使用 T-SQL 陳述式來存取 Hadoop 或 Azure Blob 儲存體中儲存的資料，並以臨機操作方式查詢它。 也可讓您查詢半結構化資料，並聯結結果與 SQL Server 中儲存的關聯式資料集。 PolyBase 已針對資料倉儲工作負載最佳化，適合用於分析查詢案例。

 如需詳細資訊，請參閱 [PolyBase 指南](../relational-databases/polybase/polybase-guide.md)。

## <a name="stretch-database"></a>Stretch Database
 Stretch Database 是 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 的新功能，可以透明且安全的方式，將您的歷程記錄資料移轉到 Microsoft Azure 雲端。 無論您的 SQL Server 資料位於內部部署或已延展到雲端，都能平順地存取。 您可以設定原則以決定資料的儲存位置，而 SQL Server 會在背景處理資料移動。 整個資料表都會一直在線上，而且可供查詢。 此外，因為資料位置對應用程式而言完全透明，所以 Stretch Database 不會要求對現有查詢或應用程式進行任何變更。 如需詳細資訊，請參閱 [Stretch Database](../sql-server/stretch-database/stretch-database.md)。
 
## <a name="support-for-utf-8"></a>UTF-8 支援
[bcp 公用程式](../tools/bcp-utility.md)、[BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) 和 [OPENROWSET](../t-sql/functions/openrowset-transact-sql.md) 現在支援 UTF-8 字碼頁。 如需詳細資訊，請參閱這些主題和[建立格式檔案 &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)。

## <a name="new-default-database-size-and-autogrow-values"></a>新的預設資料庫大小和自動成長值
模型資料庫的新值和新資料庫的預設值 (以模型為基礎)。 資料和記錄檔的初始大小現在是 8 MB。 資料和記錄檔的預設自動成長現在是 64 MB。


## <a name="transact-sql-enhancements"></a>Transact-SQL 增強功能
眾多增強功能可支援本主題中其他各節所述的功能。 下列是可以使用的其他增強功能。
- TRUNCATE TABLE 陳述式現在允許截斷指定的分割區。 如需詳細資訊，請參閱 [TRUNCATE TABLE &#40;Transact-SQL&#41;](../t-sql/statements/truncate-table-transact-sql.md)。
- [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md) 現在允許在資料表仍可使用時，執行多個改變資料行動作。
- 全文檢索索引 DMV [sys.dm_fts_index_keywords_position_by_document &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-position-by-document-transact-sql.md) 會傳回文件中關鍵字的位置。 此 DMV 也已加入 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP2 和 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP1 中。
- 新的查詢提示 **NO_PERFORMANCE_SPOOL** 可以防止多工緩衝處理運算子加入查詢計劃。 這可以改善利用多工緩衝處理作業執行許多並行查詢時的效能。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md)。
- [FORMATMESSAGE &#40;Transact-SQL&#41;](../t-sql/functions/formatmessage-transact-sql.md) 陳述式已增強以接受 msg_string 引數。
- NONCLUSTERED 索引的索引金鑰大小上限已提升至 1700 個位元組。
- 針對與 AGGREGATE、ASSEMBLY、COLUMN、CONSTRAINT、DATABASE、DEFAULT、FUNCTION、INDEX、PROCEDURE、ROLE、RULE、SCHEMA、SECURITY POLICY、SEQUENCE、SYNONYM、TABLE、TRIGGER、TYPE、USER 和 VIEW 相關的 DROP 陳述式加入新的 DROP IF 語法。 請參閱個別語法主題中的語法。
- MAXDOP 選項已加入 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)、[DBCC CHECKDB &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 和 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)，以便指定平行處理原則的程度。
- 現在可以設定 SESSION_CONTEXT。 包含 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../t-sql/functions/session-context-transact-sql.md) 函數、[CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../t-sql/functions/current-transaction-id-transact-sql.md) 函數和 [sp_set_session_context &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) 程序。
- 進階分析擴充功能允許使用者執行以支援的語言 (例如 R) 撰寫的指令碼。[!INCLUDE[tsql](../includes/tsql-md.md)] 藉由引進 [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 預存程序以及[啟用外部指令碼伺服器組態選項](../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)來支援 R。 如需相關資訊，請參閱 [SQL Server R Services](../advanced-analytics/r-services/sql-server-r-services.md)。
- 此外，為了支援 R，現在可建立外部資源集區。 如需詳細資訊，請參閱 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-external-resource-pool-transact-sql.md)。  新的目錄檢視和 DMV ([sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) 和 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md))。 [sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 和 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md) 有其他引數可以使用。 某些現有的資源管理員目錄檢視和 DMV 已加入其他資料行。
- 利用 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 選項增強 [CREATE USER](../t-sql/statements/create-user-transact-sql.md) 語法以支援「永遠加密」功能。 如需詳細資訊，請參閱[移轉透過永遠加密保護的敏感性資料](../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。
- [COMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/compress-transact-sql.md) 和 [DECOMPRESS &#40;Transact-SQL&#41;](../t-sql/functions/decompress-transact-sql.md) 函數可進行值與 GZIP 演算法的雙向轉換。
- 加入 [DATEDIFF_BIG &#40;Transact-SQL&#41;](../t-sql/functions/datediff-big-transact-sql.md) 和 [AT TIME ZONE &#40;Transact-SQL&#41;](../t-sql/queries/at-time-zone-transact-sql.md) 函數以及 [sys.time_zone_info &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) 檢視來支援日期和時間互動。
- 現在可以在資料庫層級建立認證 (除了先前可用的伺服器層級認證以外)。 如需詳細資訊，請參閱 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md)。
- [SERVERPROPERTY &#40;Transact-SQL&#41;](../t-sql/functions/serverproperty-transact-sql.md) 已新增八個新屬性：InstanceDefaultDataPath、InstanceDefaultLogPath、ProductBuild、ProductBuildType、ProductMajorVersion、ProductMinorVersion、ProductUpdateLevel 和 ProductUpdateReference。
- 已移除 [HASHBYTES &#40;Transact-SQL&#41;](../t-sql/functions/hashbytes-transact-sql.md) 函數的 8,000 個位元組輸入長度限制。
- 加入新的字串函數 [STRING_SPLIT &#40;Transact-SQL&#41;](../t-sql/functions/string-split-transact-sql.md) 和 [STRING_ESCAPE &#40;Transact-SQL&#41;](../t-sql/functions/string-escape-transact-sql.md)。
- 自動成長選項：ALTER DATABASE 的 AUTOGROW_SINGLE_FILE 和 AUTOGROW_ALL_FILES 選項取代了追蹤旗標 1117，所以追蹤旗標 1117 沒有任何作用。 如需詳細資訊，請參閱 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 和 [sys.filegroups &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) 的新 is_autogrow_all_files 資料行。
- 混合範圍配置：在使用者資料庫中，物件前 8 頁的預設配置將從使用混合頁面範圍變更為使用統一範圍。 ALTER DATABASE 的 SET MIXED_PAGE_ALLOCATION 選項取代了追蹤旗標 1118，所以追蹤旗標 1118 沒有任何作用。 如需詳細資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-set-options.md) 和 [sys.databases &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 的新 `is_mixed_page_allocation_on` 資料行。

### <a name="transact-sql-improvements-for-natively-compiled-modules"></a>原生編譯模組的 Transact-SQL 改善

針對 SQL Server 2014 原生編譯模組不支援的一些 Transact-SQL 元素，SQL Server 2016 現在已提供支援：


- 查詢會建構：
  - UNION 和 UNION ALL
  - SELECT DISTINCT
  - OUTER JOIN
  - SELECT 中的子查詢


- INSERT、UPDATE 和 DELETE 陳述式現在可以包含 [OUTPUT 子句](../t-sql/queries/output-clause-transact-sql.md)。

- 現在可透過下列方式在原生處理序中使用 LOB：
  - 變數的宣告。
  - 收到的輸入參數。
  - 在原生處理序中傳入字串函數的參數 (例如 LTrim 或子字串)。


- 內嵌 (亦即單一陳述式) 資料表值函數 (TVF) 現在可以原生方式編譯。

- 純量使用者定義函數 (UDF) 現在可以原生方式編譯。

- 增加對原生處理序的支援，以便呼叫：
  - 內建[安全性函數](../t-sql/functions/security-functions-transact-sql.md)。
  - 內建[數學函數](../t-sql/functions/mathematical-functions-transact-sql.md)。
  - 內建函數 `@@SPID`。


- 現在支援 EXECUTE AS CALLER，這表示建立原生編譯的 T-SQL 模組時，不再需要 EXECUTE AS 子句。


如需整體資訊，請參閱：

- [原生編譯的 T-SQL 模組支援的功能](../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)
- [改變原生編譯的 T-SQL 模組](../relational-databases/in-memory-oltp/altering-natively-compiled-t-sql-modules.md)

## <a name="system-view-enhancements"></a>系統檢視表增強功能
- 有兩個新檢視支援資料列層級安全性。 如需詳細資訊，請參閱 [sys.security_predicates &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md) 和 [sys.security_policies &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)。
- 有七個新檢視支援查詢存放區功能。 如需詳細資訊，請參閱[查詢存放區目錄檢視 &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)。
- [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 加入 24 個新資料行，以提供記憶體授與的相關資訊。
- 已加入兩個新查詢提示 (MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT) 來指定記憶體授與。 請參閱[查詢提示 &#40;Transact-SQL&#41;](../t-sql/queries/hints-transact-sql-query.md)。
- [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) 提供了類似全伺服器 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) 的每一工作階段報告。
- [sys.dm_exec_function_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-function-stats-transact-sql.md) 提供有關純量值函數的執行統計資料。
- 從 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 開始，[sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md) 中的項目會保持 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 之前的樣子。
- 新的動態管理函數 [sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) 可以傳回已提交至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的陳述式相關資訊。
- 有兩個新檢視支援 [SQL Server R 服務](../advanced-analytics/r-services/sql-server-r-services.md)： [sys.dm_external_script_requests](../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) 和 [sys.dm_external_script_execution_stats](../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 


## <a name="security-enhancements"></a>安全性增強功能

### <a name="row-level-security"></a>資料列層級安全性
資料列層級安全性引進述詞型的存取控制。 其特色為彈性、集中式、以述詞為基礎的評估，依據適當情況，考量中繼資料 (例如標籤) 或系統管理員所決定的任何其他準則。 述詞作為準則，以根據使用者屬性判斷使用者是否具有適當的資料存取權。 可以使用以述詞為基礎的存取控制來實作以標籤為基礎的存取控制。 如需詳細資訊，請參閱[資料列層級安全性](../relational-databases/security/row-level-security.md)。


### <a name="always-encrypted"></a>Always Encrypted
透過 Always Encrypted，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以對加密資料執行作業；而最棒的是，所有加密金鑰都與應用程式一起置於客戶信任的環境中，而不是位於伺服器上。 永遠加密可保護客戶資料，所以 DBA 無法存取純文字資料。 以透明方式在驅動程式層級進行資料加密和解密，可讓必須對現有應用程式執行的變更減至最少。 如需詳細資訊，請參閱[永遠加密 &#40;Database Engine&#41;](../relational-databases/security/encryption/always-encrypted-database-engine.md)。


### <a name="dynamic-data-masking"></a>動態資料遮罩
動態資料遮罩會對不具權限的使用者遮罩機密資料，從而限制其曝光。 動態資料遮罩讓使用者能夠指定要顯示多少機密資料，藉此協助防止未經授權存取機密資料，同時盡可能減少對應用程式層的影響。 這項原則式安全性功能會將敏感性資料隱藏在指定資料庫欄位的查詢結果集內，而資料庫中的資料則不會變更。 如需相關資訊，請參閱 [Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md)。


### <a name="new-permissions"></a>新的權限
- **ALTER ANY SECURITY POLICY** 權限可作為資料列層級安全性實作的一部分。
- **ALTER ANY MASK** 和 **UNMASK** 權限可做為動態資料遮罩實作的一部分。
- **ALTER ANY COLUMN ENCRYPTION KEY**、 **VIEW ANY COLUMN ENCRYPTION KEY**、 **ALTER ANY COLUMN MASTER KEY DEFINITION**和 **VIEW ANY COLUMN MASTER KEY DEFINITION** 權限可做為「永遠加密」功能實作的一部分。
- **ALTER ANY EXTERNAL DATA SOURCE** 和 **ALTER ANY EXTERNAL FILE FORMAT** 權限可顯示在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 中，但只會套用到 [!INCLUDE[ssAPS](../includes/ssaps-md.md)] ([!INCLUDE[ssDW](../includes/ssdw-md.md)])。
- **EXECUTE ANY EXTERNAL SCRIPT** 權限可作為 R 指令碼支援的一部分。
 - **ALTER ANY DATABASE SCOPED CONFIGURATION** 權限可用於授權使用 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 陳述式。

### <a name="transparent-data-encryption"></a>透明資料加密
- 已利用 Intel AES-NI 硬體加密加速支援來增強「透明資料加密」。 這會降低開啟透明資料加密的 CPU 額外負荷。

### <a name="aes-encryption-for-endpoints"></a>端點的 AES 加密
- 端點的預設加密已從 RC4 變成 AES。

### <a name="new-credential-type"></a>新的認證類型
- 現在可以在資料庫層級建立認證 (除了先前可用的伺服器層級認證以外)。 如需詳細資訊，請參閱 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-database-scoped-credential-transact-sql.md)。


## <a name="high-availability-enhancements"></a>高可用性增強功能
SQL Server 2016 Standard Edition 現在支援 AlwaysOn 基本可用性群組。 基本可用性群組提供主要和次要複本的支援。 這項功能取代了過時的資料庫鏡像技術，以提供高可用性。 如需基本和進階可用性群組之間差異的詳細資訊，請參閱[基本可用性群組 &#40;AlwaysOn 可用性群組&#41;](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。

現在有一組唯讀複本支援讀取意圖的連接要求負載平衡。 先前的行為一律將連接導向路由清單中第一個可用的唯讀複本。 如需詳細資訊，請參閱[設定唯讀複本之間的負載平衡](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)。

 支援自動容錯移轉的複本數目已從 2 增加到 3。

 AlwaysOn 容錯移轉叢集現在支援群組受管理的服務帳戶。 如需相關資訊，請參閱 [群組受管理的服務帳戶](https://technet.microsoft.com/library/hh831782.aspx)。 在 Windows Server 2012 R2 中，需有一項更新來避免在密碼變更後發生暫時停機。 若要取得此更新，請參閱 [gMSA-based services can't log on after a password change in a Windows Server 2012 R2 domain](https://support.microsoft.com/kb/2998082/)(在 Windows Server 2012 R2 網域中變更密碼後，以 gMSA 為基礎的服務就無法登入)。

 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 在 Windows Server 2016 上支援分散式交易和 DTC。 如需詳細資訊，請參閱[分散式交易支援](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md#dtcsupport)。

 您現在可以設定 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 以在資料庫離線時容錯移轉。 這項變更需要在 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) 或 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) 陳述式中將 **DB_FAILOVER**選項設定為 **ON**。

AlwaysOn 現在支援加密的資料庫。 當您建立新的可用性群組時，或將資料庫或複本新增到現有的可用性群組時，可用性群組精靈現在會提示針對包含資料庫主要金鑰的任何資料庫，輸入密碼。

現在可以將兩個不同 Windows Server 容錯移轉叢集 (WSFC) 中的兩個可用性群組合併成分散式可用性群組。 如需詳細資訊，請參閱[分散式可用性群組 &#40;AlwaysOn 可用性群組&#41;](../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)。

直接植入可讓次要複本透過網路自動植入 (而不是手動植入，其需要在次要複本上還原目標資料庫的實體備份)。 在 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-availability-group-transact-sql.md) 或 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) 陳述式中設定 **SEEDING_MODE=AUTOMATIC**，即可指定直接植入。 您也必須在搭配直接植入使用的每個次要複本上利用 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-availability-group-transact-sql.md) 指定 **GRANT CREATE ANY DATABASE**。

**效能改善** - 透過平行和加速壓縮主要複本上的記錄檔區塊、最佳化同步處理通訊協定，以及平行解壓縮和重做次要複本上的記錄檔記錄，可用性群組的同步處理輸送量已增加 10 倍以上。 這會增加可讀取次要複本的有效期限，並減少容錯移轉時的資料庫復原時間。 請注意，在 SQL Server 2016 中，還無法平行重做記憶體最佳化資料表。

## <a name="replication-enhancements"></a>複寫增強功能
- 現在支援記憶體最佳化資料表的複寫。 如需詳細資訊，請參閱[複寫至記憶體最佳化資料表訂閱者](../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)。
- 現在支援複寫至 [!INCLUDE[ssSDSFull](../includes/sssdsfull-md.md)]。 如需相關資訊，請參閱 [Replication to SQL Database](../relational-databases/replication/replication-to-sql-database.md)。

## <a name="tools-enhancements"></a>工具增強功能

### <a name="management-studio"></a>Management Studio
請下載最新版的 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 支援為了連接到 Microsoft Azure 而開發的 Active Directory 驗證程式庫 (ADAL)。 這會取代 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中使用的憑證式驗證。
- 新的查詢結果方格選項支援在複製或儲存結果方格中的文字時保留歸位字元/換行字元 (新行字元)。 從 [工具] / [選項] 功能表設定此選項。
- SQL Server 管理工具已不再從主要的功能樹狀目錄中安裝。如需詳細資訊，請參閱 [使用 SSMS 安裝 SQL Server 管理工具](https://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)。

### <a name="upgrade-advisor"></a>Upgrade Advisor
SQL Server 2016 Upgrade Advisor Preview 是獨立的工具，可讓舊版使用者對其 SQL Server 資料庫執行一組升級規則，以指出重大行為變更和已被取代的功能，以及協助新功能 (例如 Stretch Database) 採用。

 您可以在 [這裡](https://docs.microsoft.com/sql/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades#how-to-install-and-run-upgrade-advisor) 下載 Upgrade Advisor Preview，或使用 Web Platform Installer 進行安裝。

## <a name="see-also"></a>另請參閱
[SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)
 
[SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md) 
 
[安裝 SQL Server 管理工具與 SSMS](https://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)
