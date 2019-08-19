---
title: SQL Server&#39;2014 中的新功能 |Microsoft Docs
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
ms.openlocfilehash: f368da503c90595624f476344724719206cdb77c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893702"
---
# <a name="what39s-new-in-sql-server-2014"></a>SQL Server&#39;2014 中的新功能
  本主題摘要說明中新功能的詳細[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]連結, 並摘要說明下列各項的服務套件[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**現在就試試看：** ![Azure 虛擬機器小型](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png)擁有 azure 帳戶嗎？  然後前往 **[這裡](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** 來加速已安裝 SQL Server 2014 Service Pack 1 (SP1) 的虛擬機器。 
  
-   [新&#40;功能資料庫引擎&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Analysis Services 和商業智慧的新功能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [SQL Server 安裝的新增功能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]尚未引進下列重要的新功能:**  
  
-   [新&#40;功能 Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [新&#40;功能 Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) 並未引入重大的新功能。
-  [SQL Server 2014 Service Pack 1 版本資訊](https://support.microsoft.com/en-us/kb/3058865)。
-  [![要下載 Microsoft 的 Service Pack 1 嗎？SQL Server？](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) 2014[下載適用于 Microsoft 的 Service Pack 1？SQL Server？2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694)。


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [SQL Server 2014 Service Pack 2 版本資訊](https://support.microsoft.com/en-us/kb/3171021)。
-  [![要下載 Microsoft 的 Service Pack 2 嗎？SQL Server？](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) 2014[下載適用于 Microsoft 的 Service Pack 2？SQL Server？2014](https://go.microsoft.com/fwlink/?LinkID=821558)。
-  [![下載 SQL Server 2014 sp2 功能套件](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [下載 SQL Server 2014 sp2 功能套件](https://www.microsoft.com/en-us/download/details.aspx?id=53164)。

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2包括下列改良功能:

### <a name="performance-and-scalability-improvements"></a>效能和擴充性改善 
-   **自動的軟體 NUMA 分割:** 若[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]使用 SP2, 在實例啟動期間開啟追蹤旗標8079時, 就會啟用自動軟體 NUMA。 在啟動期間啟用追蹤旗標8079時[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] , SP2 會詢問硬體設定, 並在報告8個或更多 cpu 的系統上, 針對每個 NUMA 節點自動設定軟體 NUMA。 自動的軟 NUMA 行為是超執行緒 (HT/邏輯處理器) 感知。 其他節點的分割和建立可藉由增加接聽程式數目、調整以及網路和加密功能，來調整背景處理的規模。 建議先使用自動軟體 NUMA 測試效能工作負載, 然後再將它轉換成生產環境。 [如需詳細資訊, 請參閱 Blog](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **動態記憶體物件調整:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 會根據要在新式硬體上調整的節點和核心數目, 動態分割記憶體物件。 動態升級的目標是要自動分割安全線程的記憶體物件 (CMEMTHREAD) (如果它變成瓶頸)。 未分割的記憶體物件可以動態升級, 依節點分割 (資料分割數目等於 NUMA 節點數目), 而依節點分割的記憶體物件則可以進一步提升為依 CPU 分割 (磁碟分割數目等於數Cpu)。 [如需詳細資訊, 請參閱 blog](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **DBCC CHECK\*命令的 MAXDOP 提示:** 這種改善解決了[connect 意見反應 (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)。 您現在可以使用 sp_configure 值以外的 MAXDOP 設定來執行 DBCC CHECKDB。 如果 MAXDOP 超過使用 Resource Governor 所設定的值，資料庫引擎就會使用 ALTER WORKLOAD GROUP (Transact-SQL) 中所描述的 Resource Governor MAXDOP 值。 當您使用 MAXDOP 查詢提示時，適用所有搭配 max degree of parallelism 組態選項使用的語意規則。 如需詳細資訊，請參閱 < [DBCC CHECKDB &#40;transact-SQL&#41;](https://msdn.microsoft.com/library/ms176064.aspx)。
-   **啟用緩衝集區的 > 8TB:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 可128TB 虛擬位址空間以供緩衝集區使用。 這種改善可讓 SQL Server 緩衝集區在現代化硬體上擴充超過8TB。
-   **SOS_RWLock spinlock 改進:** SOS_RWLock 是在整個 SQL Server 程式碼基底的各種位置中使用的同步處理原始物件。  顧名思義, 此程式碼可以有多個共用 (讀取器) 或單一 (寫入器) 擁有權。 這項改進不需要對 SOS_RWLock 進行 spinlock, 而是使用與記憶體內部 OLTP 類似的無鎖定技術。 有了這項變更, 許多執行緒就能以平行方式讀取受 SOS_RWLock 保護的資料結構, 而不會彼此封鎖, 進而提供更高的擴充性。 在這項變更之前, spinlock 的執行只允許一個執行緒一次取得 SOS_RWLock, 甚至是讀取資料結構。  [如需詳細資訊, 請參閱 blog](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空間原生實作為:** 在 SP2 中, 對空間查詢效能的[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]重大改進是透過原生方式來引入。 如需詳細資訊, 請參閱[知識庫文章 KB3107399](https://support.microsoft.com/en-us/kb/3107399)。

### <a name="supportability-and-diagnostics-improvements"></a>支援性和診斷改善
-   **資料庫複製:** 複製資料庫是新的 DBCC 命令, 藉由複製不含資料的架構和中繼資料, 來增強對現有生產資料庫的疑難排解。 複製是使用命令`DBCC clonedatabase('source_database_name', 'clone_database_name')`所建立。  **注意：** 請勿在生產環境中使用複製的資料庫。 使用下列命令來判斷資料庫是否已從複製的資料庫產生: `select DATABASEPROPERTYEX('clonedb', 'isClone')`。 傳回值**1**表示資料庫是從 clonedatabase 建立的, 而**0**則表示它不是複製。
-   **Tempdb 可支援性:** 新的錯誤記錄訊息, 指出 tempdb 檔案的數目, 以及伺服器啟動時存在的 tempdb 資料檔案大小/自動成長。
-   **資料庫立即檔案初始化記錄:** 新的錯誤記錄訊息, 指出伺服器 statup 上的資料庫立即檔案初始化狀態 (已啟用/已停用)。
-   **呼叫堆疊中的模組名稱:** Xevent 呼叫堆疊現在包含模組名稱 + 位移, 而不是絕對位址。
-   **累加式統計資料的新 DMF:** 這種改善可解決[connect 意見反應 (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) , 以啟用追蹤分割層級的累加統計資料。 引進新的 DMF _db_incremental_stats_properties, 以公開累加統計資料每個資料分割的資訊。
-   **索引使用 DMV 行為已更新:** 這項改善會解決客戶的[connect 意見反應 (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) , 而重建索引的客戶*不*會清除該索引的 _db_index_usage_stats 中任何現有的資料列專案。 此行為現在會與 SQL 2008 和 SQL Server 2016 中的相同。 [如需詳細資訊, 請參閱 blog](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **改善診斷 XE 和 Dmv 之間的相互關聯:** 這種改善解決了[connect 意見反應 (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)。 Query_hash 和 query_plan_hash 是用來唯一識別查詢。 DMV 會將其定義為 varbinary(8)，而 XEvent 會將其定義為 UINT64。 由於 SQL server 沒有「unisigned Bigint」, 因此轉型不一定會運作。 這項改善引進了相當於 query_hash 和 query_plan_hash 的新 XEvent 動作/篩選資料行，不同之處在於這些資料行是定義為 INT64，以協助建立 XE 和 DMV 之間的查詢關聯。
-   **支援 BULK INSERT 和 BCP 中的 UTF-8:** 這項改善可解決連線[意見反應 (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) , 在 BULK INSERT 和 BCP 中, 現在已啟用以 utf-8 字元集編碼之資料的匯出和匯入支援。
-   **輕量每個運算子的查詢執行分析:** 針對查詢效能進行疑難排解時, 雖然執行程式表會提供查詢執行計畫的許多資訊, 以及計畫中的運算子成本, 但它對於實際的執行時間統計資料 (例如 CPU、i/o 讀取、每個執行緒的耗用時間) 有有限的資訊。 SQL 2014 SP2 在執行程式表中導入了這些額外的執行時間統計資料以及 XEvent (query_thread_profile), 以協助疑難排解查詢效能。 [如需詳細資訊, 請參閱 blog](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **變更追蹤清除:** 引進新的預`sp_flush_CT_internal_table_on_demand`存程式, 以視需要清除變更追蹤內部資料表。
-   **AlwaysON 租用超時記錄**已新增租用超時訊息的新記錄功能, 以記錄目前時間和預期的更新時間。 此外, SQL 錯誤記錄中會引進關於超時的新訊息。 [如需詳細資訊, 請參閱 blog](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **在 SQL Server 中抓取輸入緩衝區的新 DMF:** 現已提供可擷取工作階段/要求 (sys.dm_exec_input_buffer) 輸入緩衝區的新 DMF。 其功能相當於 DBCC INPUTBUFFER。 [如需詳細資訊, 請參閱 blog](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **降低低估和非常重要記憶體授與的風險:** 已透過 MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT 加入 Resource Governor 的新查詢提示。 這可讓您在執行查詢時使用這些提示, 方法是將其記憶體授與上限, 以避免記憶體爭用。 如需詳細資訊, 請參閱[知識庫文章 KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **較佳的記憶體授與/使用方式診斷:** SQL Server (query_memory_grant_usage) 中的追蹤功能清單中加入了新的擴充事件, 以追蹤要求和授與的記憶體授權。 這會提供更佳的追蹤和分析功能, 以便針對與記憶體授與相關的查詢執行問題進行疑難排解。 如需詳細資訊, 請參閱[知識庫文章 KB3107173](https://support.microsoft.com/en-us/kb/3107173)。
-   **Tempdb 溢出的查詢執行診斷:** -雜湊警告和排序警告現在有其他資料行可追蹤實體 i/o 統計資料、已使用的記憶體和受影響的資料列。 我們也引進了新的 hash_spill_details 擴充事件。 現在您可以追蹤更細微的雜湊和排序警告資訊 ([KB3107172](https://support.microsoft.com/en-us/kb/3107172))。 這項改進現在也會透過 XML 查詢計劃, 以新屬性 (attribute) 的形式 (SpillToTempDbType 複雜類型 ([KB3107400](https://support.microsoft.com/en-us/kb/3107400))) 公開。 [設定統計資料] 現在會顯示排序資料表的統計資料。 .
-   **針對牽涉到剩餘述詞下推的查詢執行計畫改善診斷:** 現在會在查詢執行計畫中報告實際讀取的資料列, 以協助改善查詢效能疑難排解。 這應該會否定獨立捕捉 SET STATISTICS IO 的需要。 這現在可讓您在查詢計劃中查看與剩餘述詞下推的相關資訊。 如需詳細資訊, 請參閱[知識庫文章 KB3107397](https://support.microsoft.com/en-us/kb/3107397)。


## <a name="additional-information"></a>其他資訊  
 [SQL Server 2014 資源](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 資源中心](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 網站](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
