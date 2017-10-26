---
title: "資料庫引擎的新功能 - SQL Server 2017 | Microsoft Docs"
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 5051d2d668105bd0a309eb64f2b8becd459d8a6b
ms.openlocfilehash: 6cc679441602d4aa1d125c2f61f9d538e3b716a2
ms.contentlocale: zh-tw
ms.lasthandoff: 10/12/2017

---
# <a name="whats-new-in-database-engine---sql-server-2017"></a>資料庫引擎的新功能 - SQL Server 2017
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

本主題描述對 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]的 [!INCLUDE[ssdenoversion-md](../includes/ssdenoversion-md.md)] 進行的改善。 如需各項目的詳細資訊，請按一下連結。

> [!NOTE]  
> SQL Server 2017 也包含 SQL Server 2016 Service Pack 中新增的功能。 如需這些項目，請參閱 [SQL Server 2016 (Database Engine) 的新功能](../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md)。

**增強功能**  

- CLR 使用 .NET Framework 中的程式碼存取安全性 (CAS)，而這不再作為安全性界限受支援。 使用 `PERMISSION_SET = SAFE` 所建立的 CLR 組件可以存取外部系統資源、呼叫 Unmanaged 程式碼，以及取得系統管理員權限。 從 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] 開始，引進稱為 `clr strict security` 的 `sp_configure` 選項，來增強 CLR 組件的安全性。 `clr strict security` 會依預設啟用，且將 `SAFE` 與 `EXTERNAL_ACCESS` 組件視作已標記為 `UNSAFE` 一樣。 可以基於回溯相容性停用 `clr strict security` 選項，但不建議這麼做。 Microsoft 建議透過具有已獲授與 master 資料庫中 `UNSAFE ASSEMBLY` 權限之對應登入的憑證或非對稱金鑰簽署所有組件。 CLR 組件現在可以新增至白名單，以解決 `clr strict security` 功能問題。 新增了 [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)、[sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) 和 [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) 以支援信任組件的白名單。 如需詳細資訊，請參閱 [CLR 嚴格安全性](configure-windows/clr-strict-security.md)。  
- 引進新的 DMF [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)，以公開摘要層級屬性與交易記錄檔的資訊；這在監視交易記錄的健康情況時非常實用。  
- 可繼續的線上索引重建。 「可繼續的線上索引重建」可讓您在線上索引重建作業發生失敗 (例如容錯移轉至複本或磁碟空間不足) 後，從停止處繼續。 您也可以暫停並於稍後繼續線上索引重建作業。 例如，您可能需要暫時釋出系統資源，才能執行高優先順序的工作；或者，如果大型資料表的可用維護期間太短，則會在另一個維護期間完成索引重建。 最後，可繼續線上索引重建不需要大量記錄空間，以讓您在可繼續重建作業執行時執行記錄截斷。 請參閱 [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) 和[線上索引作業的指導方針](../relational-databases/indexes/guidelines-for-online-index-operations.md)。
- **ALTER DATABASE SCOPED CONFIGURATION 的 IDENTITY_CACHE 選項**。 新選項 IDENTITY_CACHE 已新增至 `ALTER DATABASE SCOPED CONFIGURATION` T-SQL 陳述式。 此選項設定為 `OFF` 時，可讓資料庫引擎在伺服器意外地重新啟動或容錯移轉至次要伺服器時，避免識別資料行的值出現間隙。 請參閱 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。   
-  [!INCLUDE[ssnoversion](../includes/ssnoversion.md)] 現在提供圖形資料庫功能來建立多對多關聯性模型。 這包含建立節點和邊緣資料表的新 [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) 語法，以及查詢的 [MATCH](../t-sql/queries/match-sql-graph.md) 關鍵字。 如需詳細資訊，請參閱[圖形處理與 SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md)。   
- 新一代的查詢處理功能改進會調整最佳化策略，使其符合您應用程式工作負載的執行階段條件。 為了這個第一版**自適性查詢處理**功能家族，我們推出了三項新的功能更新：**批次模式自適性聯結**、**批次模式記憶體授與回饋**，以及適用於多陳述式資料表值函式的**交錯執行**。  請參閱 [SQL 資料庫中的自適性查詢處理](../relational-databases/performance/adaptive-query-processing.md)。
- 「自動調整」是一種資料庫功能，可深入探索潛在的查詢效能問題、建議解決方法，並且自動修正找到的問題。 [!INCLUDE[ssnoversion](../includes/ssnoversion.md)] 中的自動調整只要偵測到潛在的效能問題時就會通知您，並可讓您套用矯正措施，或可讓 [!INCLUDE[ssde-md](../includes/ssde-md.md)] 自動修正效能問題。 如需詳細資訊，請參閱[自動微調](../relational-databases/automatic-tuning/automatic-tuning.md)。
- 記憶體最佳化資料表上非叢集索引建置的效能增強。 資料庫復原期間 MEMORY_OPTIMIZED 資料表的 bwtree (非叢集) 索引建置效能已大幅最佳化。 這項改善可在使用非叢集索引時大幅減少資料庫復原時間。  
- [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 有三個新的資料行：socket_count、cores_per_socket、numa_node_count。 這在您於 VM 中執行伺服器的情況下很有用處，因為超出 NUMA 可能會造成過度認可的主機，並於最終轉變成效能問題。
- [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) 中引進新的資料行 modified_extent_page_count\,，以追蹤資料庫之每個資料庫檔案中的差異變更。 新的資料行 modified_extent_page_count 可讓您建置智慧型備份解決方案，以在資料庫中的百分比變更頁面低於臨界值 (即 70-80%) 時執行差異備份，否則請執行完整資料庫備份。
- SELECT INTO … ON FileGroup - [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) 現在使用 SELECT INTO TSQL 語法中所新增的 **ON** 關鍵字支援，來支援將資料表載入使用者預設檔案群組以外的檔案群組。
- Tempdb 安裝程式改善 - 安裝程式可讓您指定每個檔案最多 **256 GB (262,144 MB)** 的初始 tempdb 檔案大小，並出現警告向客戶提醒檔案大小是否設定為大於 1 GB 的值，以及是否未啟用 IFI。 務必了解這表示未啟用檔案立即初始化 (IFI)，其中，根據所指定 tempdb 資料檔案的初始大小，安裝時間可能會以指數方式大幅增加。 IFI 不適用於交易記錄大小，因此指定交易記錄的較大值一律可以增加安裝時間，但會在安裝期間啟動 tempdb，而與 SQL Server 服務帳戶的 IFI 設定無關。
- 已引進新的 dmv [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md)，以追蹤每個資料庫的版本存放區使用量。 這個新的 dmv 適用於監視 tempdb 的版本存放區使用量，可讓您根據每個資料庫的版本存放區使用量需求來主動規劃 tempdb 大小，而且在執行實際伺服器上執行它不會有任何效能損失或額外負荷。
- 引進新的 DMF [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)，以公開與 DBCC LOGINFO 類似的 VLF 資訊來監視、警示以及避免因客戶所遇到之 VLF 數目、VLF 大小或 shrinkfile 問題所造成的潛在交易記錄問題。
- 改善高端伺服器上小型資料庫的備份效能 - 在 SQL Server 中執行資料庫的備份時，備份程序需要多次反覆運算緩衝集區，才能清空進行中 I/O。 因此，備份時間不只是資料庫大小的函式，也是使用中緩衝集區大小的函式。 在 SQL Server 2017 中，備份已最佳化，避免多次反覆運算緩衝集區，因而導致大幅提升小型到中型資料庫的備份效能。 效能提升會隨著資料庫大小增加而減少，因為要備份的頁面和備份 IO 與反覆運算緩衝集區相較之下需要更多時間。  
- 查詢存放區現在會追蹤等候統計資料摘要資訊。 追蹤查詢存放區中每個查詢的等候統計資料別，可啟用下個層級的效能疑難排解體驗，甚至深入了解工作負載效能和其瓶頸，同時保留重要的查詢存放區優點。  
- 系統版本設定時態表現在支援 CASCADE DELETE 和 CASCADE UPDATE。  
- 間接檢查點效能的改進。
- 新增無叢集可用性群組的支援。
- 新增最小複本認可可用性群組的設定。
- 可用性群組現在可於 Windows 和 Linux 運作，以進行跨作業系統移轉及測試。
- 新增時態表保留原則的支援，
- 新的 DMV SYS.DM_DB_STATS_HISTOGRAM
- 新增建置及重建線上非叢集資料行存放區索引的支援
- 新增[sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) ，以供檢查統計資料。
- 隨 SQL Server Management Studio 16.4 版發行的 Database Tuning Advisor (DTA)，在分析 SQL Server 2016 和更新版本時會有額外選項。    
   - 提升效能。 如需詳細資訊，請參閱[使用 Database Engine Tuning Advisor (DTA) 的建議改進效能](../relational-databases/performance/performance-improvements-using-dta-recommendations.md)。
   - `-fc` 選項可允許資料行存放區索引的建議。 如需詳細資訊，請參閱 [DTA 公用程式](../tools/dta/dta-utility.md)和 [Database Engine Tuning Advisor (DTA) 中的資料行存放區索引建議](../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)。  
   - `-iq` 選項可允許 DTA 檢閱查詢存放區的工作負載。 如需詳細資訊，請參閱[使用查詢存放區的工作負載調整資料庫](../relational-databases/performance/tuning-database-using-workload-from-query-store.md)。  
- 針對記憶體內部功能，提供記憶體最佳化資料表和原生編譯函式的其他增強。 如需說明這些增強的程式碼範例，請參閱[使用記憶體內部 OLTP 最佳化 JSON 處理](../relational-databases/json/optimize-json-processing-with-in-memory-oltp.md)。
    - 支援記憶體最佳化資料表中的計算資料行，包括計算資料行的索引。
    - 完整支援原生編譯模組及 CHECK 條件約束中的 JSON 函數。  
    - 原生編譯模組中的`CROSS APPLY` 運算子。   
- 新增了字串函數 [CONCAT_WS](../t-sql/functions/concat-ws-transact-sql.md)、[TRANSLATE](../t-sql/functions/translate-transact-sql.md) 及 [TRIM](../t-sql/functions/trim-transact-sql.md)。   
- [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) 函數現在支援 `WITHIN GROUP` 子句。
- 新增了兩種新的日文定序系列 (Japanese_Bushu_Kakusu_140 和 Japanese_XJIS_140)，並新增區分變體選取器 (_VSS) 定序選項供日文定序使用。 如需詳細資料，請參閱[定序與 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md)   
- 新的大量存取選項 ([BULK INSERT](../t-sql/statements/bulk-insert-transact-sql.md) 和 [OPENROWSET(BULK...)](../t-sql/functions/openrowset-transact-sql.md)) 能夠從指定為 CSV 格式的檔案直接存取資料，也能透過 [EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md) 的新 `BLOB_STORAGE` 選項從儲存在 Azure Blob 儲存體的檔案直接存取資料。
- 已加入資料庫 **COMPATIBILITY_LEVEL** 140。   在此層級中執行的客戶會取得最新的語言功能及查詢最佳化工具行為。 這包括每個 Microsoft 發行的發行前版本變更。
- 計算累加統計資料更新臨界值的改善 (需要 140 相容性模式)。
- 已加入 [sys.dm_exec_query_statistics_xml](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)。
- 我們已進行記憶體最佳化物件的數個效能和語言增強：
    - 記憶體最佳化資料表現在支援 `sp_spaceused`。
    - 記憶體最佳化資料表和原生編譯 T-SQL 模組現在支援 `sp_rename`。
    - 原生編譯 T-SQL 模組現在支援 `CASE` 運算式。
    - 已消除記憶體最佳化資料表的 8 個索引限制。
    - 原生編譯 T-SQL 模組現在支援 `TOP (N) WITH TIES`。
    - 記憶體最佳化資料表的 `ALTER TABLE` 現在通常本質上會較快。
    - 現在會平行執行記憶體最佳化資料表的交易記錄重做。 這會加快復原時間，並且大幅增加 AlwaysOn 可用性群組組態的持續性輸送量。
    - 記憶體最佳化檔案群組檔案現在可以儲存在 Azure 儲存體上。 現在也可以備份/還原 Azure 儲存體上的記憶體最佳化檔案。
- 叢集資料行存放區索引現在支援 LOB 資料行 (nvarchar(max)、varchar(max)、varbinary(max))。
- 已新增 [STRING_AGG](../t-sql/functions/string-agg-transact-sql.md) 彙總函式。  
- 新的權限︰ `DATABASE SCOPED CREDENTIAL` 現在是一種安全性實體類別，支援 `CONTROL`、 `ALTER`、 `REFERENCES`、 `TAKE OWNERSHIP`和 `VIEW DEFINITION` 權限。 限制為 SQL Database 的 `ADMINISTER DATABASE BULK OPERATIONS` 現在可以在 `sys.fn_builtin_permissions` 中顯示。   
- 已加入 [Sys.dm_os_host_info](../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) DMV 以提供 Windows 和 Linux 作業系統資訊。   
- 資料庫角色是使用 R 服務建立，以管理與套件相關聯的權限。 如需詳細資訊，請參閱 [SQL Server 的 R 封裝管理](../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)。


