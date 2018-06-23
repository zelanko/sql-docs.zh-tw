---
title: 什麼&#39;s SQL Server 2014 的新功能 |Microsoft 文件
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- database-engine
- integration-services
- master-data-services
- replication
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
caps.latest.revision: 70
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9144eeb653649e36cfed3551e4ec465d403ffdcb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032014"
---
# <a name="what39s-new-in-sql-server-2014"></a>什麼&#39;s SQL Server 2014 的新功能
  本主題摘要說明中的新功能的詳細的連結[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]並摘要說明服務套件 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**現在就試試看：** ![Azure 虛擬機器小](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png)有 Azure 帳戶嗎？  接著前往**[這裡](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** 來微調 SQL Server 2014 Service Pack 1 (SP1) 的虛擬機器已安裝。 
  
-   [最新消息&#40;Database Engine&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [新功能 Analysis Services 和 Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [SQL Server 安裝的新增功能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 並未引進重大的新功能如下：**  
  
-   [最新消息&#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [最新消息&#40;複寫&#41;](../relational-databases/replication/what-s-new-replication.md)  
  
-   [最新消息&#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) 並未導入重大的新功能。
-  [SQL Server 2014 Service Pack 1 版本資訊](https://support.microsoft.com/en-us/kb/3058865)。
-  [![下載 Service Pack 1 的 Microsoft® SQL Server® 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [下載 Microsoft® SQL Server® 2014 Service Pack 1](https://www.microsoft.com/en-us/download/details.aspx?id=46694)。


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 2 (SP2)
- [SQL Server 2014 Service Pack 2 的版本資訊](https://support.microsoft.com/en-us/kb/3171021)。
-  [![下載 Service Pack 2 的 Microsoft® SQL Server® 2014](./media/what-s-new-in-sql-server-2016/download.png)](http://go.microsoft.com/fwlink/?LinkID=821558) [下載 Microsoft® SQL Server® 2014 Service Pack 2](http://go.microsoft.com/fwlink/?LinkID=821558)。
-  [![下載 SQL Server 2014 SP2 功能套件](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164)[下載 SQL Server 2014 SP2 功能套件](https://www.microsoft.com/en-us/download/details.aspx?id=53164)。

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2)包含下列增強功能：

### <a name="performance-and-scalability-improvements"></a>效能和延展性改善 
-   **自動軟體 NUMA 分割：** 與[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2，自動軟體 NUMA 已啟用追蹤旗標 8079 開啟執行個體啟動期間時。 在啟動期間，啟用追蹤旗標 8079 時[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 會查閱硬體版面配置和自動報告 8 或更多的 Cpu，每個 NUMA 節點的系統上設定軟體 NUMA。 自動、 軟體 NUMA 行為是 Hyperthread （HT/邏輯處理器） 感知。 其他節點的分割和建立可藉由增加接聽程式數目、調整以及網路和加密功能，來調整背景處理的規模。 建議您使用第一項測試效能工作負載與自動軟體 NUMA 之前在生產環境中開啟它。 [如需詳細資訊請參閱](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **動態記憶體物件的擴充：** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 動態磁碟分割的節點和現代硬體上縮放的核心數目為基礎的記憶體物件。 動態升級的目標是自動分割的執行緒安全的記憶體物件 (CMEMTHREAD)，如果您是效能瓶頸。 未分割的記憶體物件都可以動態地升級的節點 （NUMA 節點的分割區等於數字的數字），來分割，而且記憶體物件的節點來分割可由進一步提升至分割依 CPU （資料分割等數的數字Cpu)。 [如需詳細資訊請參閱](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **針對 DBCC CHECK 的 MAXDOP 提示\*命令：** 解決這項改進[connect 意見反應 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)。 您現在可以執行的 DBCC CHECKDB 的 sp_configure 值以外的 MAXDOP 設定。 如果 MAXDOP 超過使用 Resource Governor 所設定的值，資料庫引擎就會使用 ALTER WORKLOAD GROUP (Transact-SQL) 中所描述的 Resource Governor MAXDOP 值。 當您使用 MAXDOP 查詢提示時，適用所有搭配 max degree of parallelism 組態選項使用的語意規則。 如需詳細資訊，請參閱[DBCC CHECKDB (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms176064.aspx)。
-   **啟用 > 8 TB 緩衝集區：** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 可讓 128 TB 的緩衝區集區使用量的虛擬位址空間。 這項改進可讓 SQL Server 緩衝集區擴充超過 8 TB，在現代硬體上。
-   **SOS_RWLock 單一執行緒存取鎖改進：** SOS_RWLock 是整個 SQL Server 程式碼基底的不同位置中使用同步處理基本類型。  正如其名，程式碼可以擁有多個共用 （讀取器） 或單一 （寫入器） 的擁有權。 這項改進 SOS_RWLock 需要為單一執行緒存取鎖，而是使用類似於記憶體中 OLTP 無鎖定的技術。 透過這項變更，多執行緒可以讀取資料結構，以平行方式保護的 SOS_RWLock 而不需要封鎖彼此，並藉此提供更好的延展性。 在這項變更之前, 的單一執行緒存取鎖實作允許只有一個執行緒取得 SOS_RWLock 一次，即使要讀取的資料結構。  [如需詳細資訊請參閱](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空間的原生實作：** 空間查詢效能會顯著改善見於[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 至原生實作。 如需詳細資訊，請參閱[knowledge base 文章 KB3107399](https://support.microsoft.com/en-us/kb/3107399)。

### <a name="supportability-and-diagnostics-improvements"></a>可支援性和診斷增強功能
-   **資料庫複製：** 複製資料庫是新的 DBCC 命令，可增強疑難排解現有的生產資料庫複製結構描述，且沒有資料的中繼資料。 使用命令建立複製`DBCC clonedatabase(‘source_database_name’, ‘clone_database_name’)`。  **注意：** Cloned 資料庫不應該用於實際執行環境。 使用下列命令判斷從複製之資料庫的資料庫是否已產生： `select DATABASEPROPERTYEX('clonedb', 'isClone')`。 傳回值**1**表示資料庫從 clonedatabase 時建立**0**表示它不是複製。
-   **Tempdb 可支援性：** 伺服器啟動時，新的錯誤記錄檔訊息，指出 tempdb 檔案數目和大小/自動成長的 tempdb 資料檔案存在。
-   **資料庫立即檔案初始化記錄：** 一個新的錯誤記錄檔訊息，指出在伺服器 statup，資料庫立即檔案初始化 （啟用/停用） 的狀態。
-   **呼叫堆疊中的模組名稱：** Xevent 呼叫堆疊，現在包含的模組名稱 + 而不是絕對位址的位移。
-   **累加統計資料的新 DMF:** 解決這項改進[connect 意見反應 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics)啟用追蹤累加的統計資料，資料分割層級。 新的 DMF sys.dm_db_incremental_stats_properties 已引入來公開資訊每個資料分割的累加統計資料。
-   **更新索引使用量 DMV 行為：** 解決這項改進[connect 意見反應 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats)客戶將重建索引會從*不*清除 sys.dm_db 從任何現有資料列項目該索引的 _index_usage_stats。 行為現在會與 SQL 2008 和 SQL Server 2016 中的相同。 [如需詳細資訊請參閱](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **改善診斷 XE 和 Dmv 之間的相互關聯：** 解決這項改進[connect 意見反應 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)。 Query_hash 和 query_plan_hash 用於唯一識別查詢。 DMV 會將其定義為 varbinary(8)，而 XEvent 會將其定義為 UINT64。 由於 SQL server 並沒有"unisigned bigint"，轉型永遠無法。 這項改善引進了相當於 query_hash 和 query_plan_hash 的新 XEvent 動作/篩選資料行，不同之處在於這些資料行是定義為 INT64，以協助建立 XE 和 DMV 之間的查詢關聯。
-   **BULK INSERT 和 BCP 中的 utf-8 支援：** 解決這項改進[connect 意見反應 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001)現在 BULK INSERT 和 BCP 中啟用支援匯出和匯入編碼在 utf-8 字元集中的資料。
-   **輕量級的每個運算子查詢執行程式碼剖析：** 雖然 showplan 提供許多資訊的查詢執行計劃和運算子成本計劃中，但它具有有限的實際的詳細資訊，將查詢效能問題進行疑難排解時執行階段統計資料，像是 （CPU、 I/O 讀取，經過時間每個執行緒）。 SQL 2014 SP2 導入了這些每個運算子在執行程序表，以及 XEvent (query_thread_profile) 來協助疑難排解的查詢效能的其他執行階段統計資料。 [如需詳細資訊請參閱](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **為清除變更追蹤：** 新的預存程序`sp_flush_CT_internal_table_on_demand`已引入來清除變更追蹤隨選的內部資料表。
-   **AlwaysON 租用逾時記錄**加入新的租用逾時訊息的記錄功能，才會記錄目前的時間和預期的更新時間。 也新訊息中引進了 SQL 錯誤記錄檔有關的逾時。 [如需詳細資訊請參閱](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **擷取新 DMF 輸入 SQL Server 中的緩衝區：** 擷取工作階段/要求 (sys.dm_exec_input_buffer) 現在是可用的輸入的緩衝區的新 DMF。 其功能相當於 DBCC INPUTBUFFER。 [如需詳細資訊請參閱](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **低估和 overestimated 記憶體授與的風險降低：** 針對資源管理員透過 MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT 加入新的查詢提示。 這可讓您能夠運用這些提示時所須以防止記憶體競爭的情況其記憶體授與執行查詢。 如需詳細資訊，請參閱[knowledge base 文章 KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **更好的記憶體授權使用量/診斷：** 新擴充的事件已新增至清單的 SQL Server (query_memory_grant_usage) 中的追蹤功能，來追蹤要求和授與的記憶體授與。 這提供更好的追蹤和分析功能與記憶體授權的查詢執行問題進行疑難排解。 如需詳細資訊，請參閱[knowledge base 文章 KB3107173](https://support.microsoft.com/en-us/kb/3107173)。
-   **查詢執行診斷 tempdb 溢出：**-Hash Warning 和 Sort Warnings 現在有追蹤實體 I/O 統計資料、 使用的記憶體和受影響的資料列的其他資料行。 我們也引進新的 hash_spill_details 擴充的事件。 現在您可以在雜湊和排序的警告追蹤更細微的資訊 ([KB3107172](https://support.microsoft.com/en-us/kb/3107172))。 這項改進現在也會公開 XML SpillToTempDbType 複雜類型的新屬性的形式的查詢計畫 ([KB3107400](https://support.microsoft.com/en-us/kb/3107400))。 現在會顯示排序工作資料表統計資料，請在設定統計資料。 執行個體時提供 SQL Server 登入。
-   **改善查詢執行計畫，牽涉到殘餘述詞下推的診斷：** 讀取的實際資料列現在會報告在查詢執行計畫，以協助改善查詢效能的疑難排解。 這應該不必個別擷取 SET STATISTICS IO 變換正負號。 這可讓您查看與殘餘述詞下推，查詢計劃中的資訊。 如需詳細資訊，請參閱[knowledge base 文章 KB3107397](https://support.microsoft.com/en-us/kb/3107397)。


## <a name="additional-information"></a>其他資訊  
 [SQL Server 2014 資源](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](http://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 資源中心](http://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 網站](http://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  