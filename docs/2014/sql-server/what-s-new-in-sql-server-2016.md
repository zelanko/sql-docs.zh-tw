---
title: 什麼&#39;SQL Server 2014 的新功能 |Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 57acb73332f90f4084243184f480edf0a1395a7b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124818"
---
# <a name="what39s-new-in-sql-server-2014"></a>什麼&#39;SQL Server 2014 的新功能
  本主題摘要說明中的新功能的詳細的連結[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]，並摘要說明適用於服務組件 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**現在就試試看：**![Azure 虛擬機器小型](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png)有 Azure 帳戶嗎？  接著前往**[此處](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** 到已安裝 SQL Server 2014 Service Pack 1 (SP1) 的虛擬機器的加速。 
  
-   [新功能&#40;Database Engine&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [新 Analysis Services 和 Business Intelligence 功能](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [SQL Server 安裝的新增功能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 並未引進重要的新功能如下：**  
  
-   [新功能&#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [新功能&#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) 並未導入重大的新功能。
-  [SQL Server 2014 Service Pack 1 版本資訊](https://support.microsoft.com/en-us/kb/3058865)。
-  [![下載 Microsoft 的 Service Pack 1 」SQL Server??2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [下載 Microsoft 的 Service Pack 1 」SQL Server??2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694)。


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 2 (SP2)
- [SQL Server 2014 Service Pack 2 版本資訊](https://support.microsoft.com/en-us/kb/3171021)。
-  [![下載 Microsoft 的 Service Pack 2？SQL Server??2014](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [下載 Service Pack 2 的 Microsoft??SQL Server??2014](https://go.microsoft.com/fwlink/?LinkID=821558)。
-  [![下載 SQL Server 2014 SP2 功能套件](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164)[下載 SQL Server 2014 SP2 功能套件](https://www.microsoft.com/en-us/download/details.aspx?id=53164)。

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2)包含下列增強功能：

### <a name="performance-and-scalability-improvements"></a>改善效能和延展性 
-   **自動軟體式 NUMA 資料分割：** 使用[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2、 自動軟體式 NUMA 執行個體啟動期間開啟追蹤旗標 8079 時啟用。 在啟動期間，啟用追蹤旗標 8079 時[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 會質詢硬體配置和回報 8 個以上的 Cpu，每個 NUMA 節點的系統上的 自動設定軟體式 NUMA。 自動、 軟體 NUMA 會以超執行緒 （HT/邏輯處理器） 感知。 其他節點的分割和建立可藉由增加接聽程式數目、調整以及網路和加密功能，來調整背景處理的規模。 建議您使用第一項測試使用自動軟體式 NUMA 的效能工作負載之前在生產環境中開啟它。 [請參閱部落格以取得更多資訊](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **動態記憶體物件調整：**[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 動態分割記憶體物件為基礎的節點及調整新式硬體上的核心數目。 動態升級的目標是要自動分割安全執行緒記憶體物件 (CMEMTHREAD)，如果它變成瓶頸。 不分割記憶體物件可動態升級成依節點 （NUMA 節點的分割區等於數字的數字），進行分割並依節點分割的物件可以藉由進一步的記憶體升級成依 CPU （分割區等於數字的數字進行分割Cpu)。 [請參閱部落格以取得更多資訊](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **針對 DBCC CHECK 的 MAXDOP 提示\*命令：** 這項改善解決[connect 意見反應 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)。 您現在可以執行的 DBCC CHECKDB 的 sp_configure 值以外的 MAXDOP 設定。 如果 MAXDOP 超過使用 Resource Governor 所設定的值，資料庫引擎就會使用 ALTER WORKLOAD GROUP (Transact-SQL) 中所描述的 Resource Governor MAXDOP 值。 當您使用 MAXDOP 查詢提示時，適用所有搭配 max degree of parallelism 組態選項使用的語意規則。 如需詳細資訊，請參閱 < [DBCC CHECKDB & Amp;#40;transact-SQL&AMP;#41;](https://msdn.microsoft.com/library/ms176064.aspx)。
-   **啟用 > 8 TB，緩衝集區：**[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 可讓 128 TB 的緩衝集區使用量的虛擬位址空間。 這項改善可讓 SQL Server 緩衝集區擴充到 8 tb 以上新式硬體上。
-   **SOS_RWLock spinlock 改進：** SOS_RWLock 是在整個 SQL Server 程式碼基底的不同位置同步處理原始物件。  如同名稱所暗示，程式碼可以有多個共用 （讀取器） 或單一 （編寫器） 的擁有權。 這項改善不需要 SOS_RWLock 的執行緒同步鎖定，並改為使用類似於記憶體內部 OLTP 的 無鎖定技術。 透過這項變更，多個執行緒可以讀取而不需要封鎖彼此，並藉此提供更好的延展性保護 SOS_RWLock 的平行資料結構。 之前這項變更，單一執行緒存取鎖實作允許只有一個執行緒取得 SOS_RWLock 一次，即使是要讀取的資料結構。  [請參閱部落格以取得更多資訊](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空間原生實作：** 空間查詢效能的重大改進在引進[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 至原生實作。 如需詳細資訊，請參閱 < [KB3107399 眭妎踱恅](https://support.microsoft.com/en-us/kb/3107399)。

### <a name="supportability-and-diagnostics-improvements"></a>可支援性和診斷的改良
-   **資料庫複製：** 複製資料庫是新的 DBCC 命令，可增強疑難排解現有的生產資料庫，藉由複製結構描述和不含資料的中繼資料。 使用命令建立複製`DBCC clonedatabase('source_database_name', 'clone_database_name')`。  **請注意：** 請勿在生產環境中使用複製的資料庫。 使用下列命令判斷從複製資料庫的資料庫是否已產生： `select DATABASEPROPERTYEX('clonedb', 'isClone')`。 傳回值**1**表示從 clonedatabase 時建立資料庫**0**表示它不是複製。
-   **Temptdb 可支援：** 新的錯誤記錄檔訊息，指出 tempdb 檔案數目和大小/自動成長的 tempdb 資料檔案出現在伺服器啟動。
-   **資料庫檔案立即初始化記錄：** 新的錯誤記錄檔訊息，指出在伺服器 statup，資料庫立即檔案初始化 （啟用/停用） 的狀態。
-   **在 呼叫堆疊中的模組名稱：** Xevent 呼叫堆疊現在包含模組名稱 + 而不是絕對位址的位移。
-   **累加統計資料的新 DMF:** 這項改善解決[connect 意見反應 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics)啟用追蹤累加的統計資料，資料分割層級。 引進新的 DMF sys.dm_db_incremental_stats_properties 會公開 （expose） 的資訊每個資料分割的累加統計資料。
-   **更新的索引使用量 DMV 行為：** 這項改善解決[connect 意見反應 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats)重建索引會在哪裡的客戶*不*清除任何現有的資料列項目從這個索引的 sys.dm_db_index_usage_stats。 行為現在會與 SQL 2008 和 SQL Server 2016 相同。 [請參閱部落格以取得更多資訊](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **診斷 XE 和 Dmv 之間的關聯性改良：** 這項改善解決[connect 意見反應 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)。 Query_hash 和 query_plan_hash 用於唯一識別查詢。 DMV 會將其定義為 varbinary(8)，而 XEvent 會將其定義為 UINT64。 因為 SQL server 沒有 「 unisigned 的 bigint 」，轉型不一定運作。 這項改善引進了相當於 query_hash 和 query_plan_hash 的新 XEvent 動作/篩選資料行，不同之處在於這些資料行是定義為 INT64，以協助建立 XE 和 DMV 之間的查詢關聯。
-   **BULK INSERT 和 BCP 中的 utf-8 支援：** 這項改善解決[connect 意見反應 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001)現在 BULK INSERT 和 BCP 中啟用支援匯出和匯入 utf-8 字元集編碼的資料。
-   **每個運算子的輕量型查詢執行程式碼剖析：** 雖然 showplan 計劃中的查詢執行計畫和運算子的成本提供許多資訊，但是它受到限制實際的詳細資訊，疑難排解查詢效能，而執行階段統計資料，例如 (CPU、 I/O 讀取時，所經過時間每個執行緒)。 SQL 2014 SP2 導入了這些額外的執行階段統計資料，每個運算子在執行程序表，以及 XEvent (query_thread_profile) 來協助疑難排解查詢效能。 [請參閱部落格以取得更多資訊](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **變更追蹤清除：** 新的預存程序`sp_flush_CT_internal_table_on_demand`引進清除變更追蹤內部資料表，依需求。
-   **AlwaysON 租用逾時記錄**新增新的租用逾時訊息的記錄功能，以便記錄目前的時間和預期的續約時間。 也新訊息中引進了 SQL 錯誤記錄檔有關的逾時。 [請參閱部落格以取得更多資訊](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **擷取 SQL Server 中的輸入的緩衝區的新 DMF:** 現已提供可擷取工作階段/要求 (sys.dm_exec_input_buffer) 輸入緩衝區的新 DMF。 其功能相當於 DBCC INPUTBUFFER。 [請參閱部落格以取得更多資訊](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **低估和 overestimated 記憶體授與的風險降低：** 已新增新查詢提示的 Resource Governor 透過 MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT。 這可讓您藉由將達到上限以防止記憶體競爭記憶體授與執行查詢時運用這些提示。 如需詳細資訊，請參閱[KB310740 眭妎踱恅](https://support.microsoft.com/en-us/kb/3107401)
-   **更佳的記憶體授與/使用量診斷：** 新的擴充的事件已新增至 SQL Server (query_memory_grant_usage) 中的追蹤功能，來追蹤要求和授與的記憶體授與的清單。 這可提供更佳的追蹤和分析功能針對記憶體授與相關的查詢執行問題進行疑難排解。 如需詳細資訊，請參閱 < [KB3107173 眭妎踱恅](https://support.microsoft.com/en-us/kb/3107173)。
-   **查詢執行診斷，針對 tempdb 溢出：**-Hash Warning 和 Sort Warnings 現在有額外的資料行，以追蹤實體 I/O 統計資料、 使用的記憶體及受影響的資料列。 我們也引進了新的 hash_spill_details 擴充的事件。 現在您可以在您的雜湊和排序警告追蹤更細微的資訊 ([KB3107172](https://support.microsoft.com/en-us/kb/3107172))。 這項改進現在也會公開透過 XML 查詢計劃 」，SpillToTempDbType 複雜類型的新屬性的形式 ([KB3107400](https://support.microsoft.com/en-us/kb/3107400))。 現在會顯示排序工作資料表的統計資料，請在設定統計資料。 .
-   **針對涉及殘餘述詞下推的查詢執行計畫的改良的診斷：** 實際讀取的資料列現在會在查詢執行計畫，以協助改善查詢效能的疑難排解報告。 這應該不必個別擷取 SET STATISTICS IO 變換正負號。 這可讓您查看剩餘的述詞下推查詢計劃中的相關資訊。 如需詳細資訊，請參閱 < [KB3107397 眭妎踱恅](https://support.microsoft.com/en-us/kb/3107397)。


## <a name="additional-information"></a>其他資訊  
 [SQL Server 2014 資源](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 資源中心](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 網站](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
