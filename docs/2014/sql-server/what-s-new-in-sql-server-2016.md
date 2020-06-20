---
title: 2014 SQL Server 的新功能 |Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cee52973ec114fc52aac17b9c7e4c51e66920269
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85041340"
---
# <a name="whats-new-in-sql-server-2014"></a>SQL Server 2014 的新功能

本主題摘要說明中新功能的詳細連結，並摘要說明下列各項 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 的服務套件[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**試試看：** ![Azure 虛擬機器小型 ](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) 擁有 azure 帳戶嗎？  移至 https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2 以加速已安裝 SQL Server 2014 Service Pack 1 （SP1）的虛擬機器。

> [!TIP]
> 如需 SQL Server 2014 的首頁檔頁面，[請按一下這裡](../2014-toc/index.yml)。

<!--
Do not let this file's filename fool you.
This filename contains "2016", but nevertheless...
This file, at this exact GitHub path, is dedicated to SQL Server version 2014.
-->

## <a name="whats-new-articles"></a>新功能文章

-   [資料庫引擎的新 &#40;&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Analysis Services 和商業智慧的新功能](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [SQL Server 安裝的新增功能](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]尚未對下列功能引進重要的新功能：**  
  
-   [Integration Services 的新 &#40;&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [Reporting Services 的新 &#40;&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="sssql14-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]（SP1）並未引入重大的新功能。
-  [SQL Server 2014 Service Pack 1 版本資訊](https://support.microsoft.com/kb/3058865)。
-  [ ![ 下載 Microsoft SQL Server 2014 的 service pack 1](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=46694) [下載 service pack 1 （適用于 Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=46694)）。


## <a name="sssql14-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 （SP2）
- [SQL Server 2014 Service Pack 2 版本資訊](https://support.microsoft.com/kb/3171021)。
-  [ ![ 下載 service pack 2 for Microsoft SQL Server 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [下載 service pack 2 for Microsoft SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=821558)。
-  [ ![ 下載 SQL SERVER 2014 Sp2 功能套件](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=53164)[下載 SQL Server 2014 sp2 功能套件](https://www.microsoft.com/download/details.aspx?id=53164)。

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2包括下列改良功能：

### <a name="performance-and-scalability-improvements"></a>效能和擴充性改善 
-   **自動的軟體 NUMA 分割：** 若使用 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2，在實例啟動期間開啟追蹤旗標8079時，就會啟用自動軟體 NUMA。 在啟動期間啟用追蹤旗標8079時， [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 會詢問硬體設定，並在報告8個或更多 cpu 的系統上，針對每個 NUMA 節點自動設定軟體 NUMA。 自動的軟 NUMA 行為是超執行緒（HT/邏輯處理器）感知。 其他節點的分割和建立可藉由增加接聽程式數目、調整以及網路和加密功能，來調整背景處理的規模。 我們建議您先使用自動軟體 NUMA 測試效能工作負載，再于生產環境中進行調整。 [如需詳細資訊，請參閱 blog](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/)。 
-  **動態記憶體物件調整：** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 會根據要在新式硬體上調整的節點和核心數目，動態分割記憶體物件。 動態升級的目標是要自動分割安全線程的記憶體物件（CMEMTHREAD）（如果它變成瓶頸）。 非資料分割記憶體物件可以依節點動態分割（資料分割數目等於 NUMA 節點數目）。 依節點分割的記憶體物件可以依 CPU 進一步分割（磁碟分割數目等於 Cpu 數目）。 [如需詳細資訊，請參閱 blog](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/)。
-  **DBCC CHECK 命令的 MAXDOP 提示 \* ：** 此改善可解決[connect 意見反應（468694）](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb)。 您現在可以使用 sp_configure 值以外的 MAXDOP 設定來執行 DBCC CHECKDB。 如果 MAXDOP 超過使用 Resource Governor 所設定的值，資料庫引擎就會使用 ALTER WORKLOAD GROUP (Transact-SQL) 中所描述的 Resource Governor MAXDOP 值。 當您使用 MAXDOP 查詢提示時，適用所有搭配 max degree of parallelism 組態選項使用的語意規則。 如需詳細資訊，請參閱[DBCC CHECKDB （transact-sql）](https://msdn.microsoft.com/library/ms176064.aspx)。
-   **為緩衝集區啟用 >8 TB：** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 可針對緩衝集區使用提供 128 TB 的虛擬位址空間。 這種改善可讓 SQL Server 緩衝集區在現代化硬體上擴充超過 8 TB。
-   **SOS_RWLock Spinlock 改善：** SOS_RWLock 是在整個 SQL Server 程式碼基底的各種位置中使用的同步處理原始物件。  顧名思義，此程式碼可以有多個共用（讀取器）或單一（寫入器）擁有權。 這項改善不需要對 SOS_RWLock 進行 spinlock，而是使用與記憶體內部 OLTP 類似的無鎖定技術。 有了這項變更，許多執行緒就可以同時讀取受 SOS_RWLock 保護的資料結構，而不會彼此封鎖。 這種平行處理可提供更高的擴充性。 在這項變更之前，spinlock 的執行一次只允許一個執行緒取得 SOS_RWLock，甚至是讀取資料結構。 [如需詳細資訊，請參閱 blog](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/)。
-    **空間原生實作為：** 在 SP2 中，對空間查詢效能的重大改進是 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 透過原生方式來引入。 如需詳細資訊，請參閱[知識庫文章 KB3107399](https://support.microsoft.com/kb/3107399)。

### <a name="supportability-and-diagnostics-improvements"></a>支援性和診斷改善
-   **資料庫複製：** 複製資料庫是新的 DBCC 命令，藉由複製不含資料的架構和中繼資料，來增強對現有生產資料庫的疑難排解。 複製是使用命令所建立 `DBCC clonedatabase('source_database_name', 'clone_database_name')` 。  **注意：** 複製的資料庫不應在生產環境中使用。 使用下列命令來判斷資料庫是否已從複製的資料庫產生： `select DATABASEPROPERTYEX('clonedb', 'isClone')` 。 傳回值**1**表示資料庫是從 clonedatabase 建立的，而**0**則表示它不是複製。
-   **Tempdb 可支援性：** 新的錯誤記錄檔訊息，指出在啟動 tempdb 檔案的數目，以及 tempdb 資料檔案的大小和自動成長。
-   **資料庫立即檔案初始化記錄：** 新的錯誤記錄檔訊息，指出伺服器啟動時，資料庫立即檔案初始化的狀態（已啟用/已停用）。
-   呼叫**堆疊中的模組名稱：** 擴充事件（XEvent）呼叫堆疊現在包含模組名稱加上位移，而不是絕對位址。
-   累加**式統計資料的新 DMF：** 這種改善可解決[connect 意見反應（797156）](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) ，以啟用追蹤分割層級的累加統計資料。 引進新的 DMF sys dm_db_incremental_stats_properties，以公開累加統計資料的每個資料分割資訊。
-   **索引使用 DMV 行為已更新：** 這項改善會解決客戶的連線[意見反應（739566）](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) ，而重建索引時，將*不*會從 sys.databases 中清除任何現有的資料列專案。 dm_db_index_usage_stats 該索引。 此行為現在會與 SQL 2008 和 SQL Server 2016 中的相同。 [如需詳細資訊，請參閱 blog](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/)。
-   **改善診斷 XE 和 dmv 之間的相互關聯：** 這種改善解決了[connect 意見反應（1934583）](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types)。 `Query_hash`和 `query_plan_hash` 可用來唯一識別查詢。 DMV 會將其定義為 varbinary(8)，而 XEvent 會將其定義為 UINT64。 由於 SQL server 沒有「不帶正負號的 Bigint」，因此轉型不一定會運作。 這種改進引進了新的 XEvent 動作和篩選資料行。 資料行相當於 `query_hash` 和 `query_plan_hash` ，但它們定義為 INT64。 INT64 定義有助於讓 XE 和 Dmv 之間的查詢相互關聯。
-   **支援 BULK INSERT 和 BCP 中的 utf-8：** 這種改善解決了[connect 意見反應（370419）](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001)。 BULK INSERT 和 BCP 現在可以匯出或匯入以 UTF-8 字元集編碼的資料。
-   **每個運算子的查詢執行輕量分析：**「執行程式表」提供計畫中每個運算子的成本資訊。 但是實際的執行時間統計資料僅限於 CPU、i/o 讀取及每個執行緒經過時間的專案。 SQL Server 2014 SP2 為執行程式表中的每個運算子引進這些額外的執行時間統計資料。 R2 也引進了名為的 XEvent `query_thread_profile` ，協助您進行查詢效能的疑難排解。 [如需詳細資訊，請參閱 blog](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/)。
-   **變更追蹤清除：** 引進新的預存程式 `sp_flush_CT_internal_table_on_demand` ，以視需要清除變更追蹤內部資料表。
-   **AlwaysON 租用超時記錄**已新增租用超時訊息的新記錄功能，以記錄目前時間和預期的更新時間。 此外，SQL 錯誤記錄檔中會引進關於超時的新訊息。 [如需詳細資訊，請參閱 blog](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/)。
-   **在 SQL Server 中抓取輸入緩衝區的新 DMF：** 現在可以使用新的 DMF 來抓取會話/要求的輸入緩衝區（sys.databases dm_exec_input_buffer）。 這個 DMF 在功能上相當於 DBCC INPUTBUFFER。 [如需詳細資訊，請參閱 blog](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/)。
-   **降低低估和非常重要記憶體授與的風險：** 已透過 MIN_GRANT_PERCENT 和 MAX_GRANT_PERCENT，為 Resource Governor 新增了查詢提示。 這個新的查詢可讓您在執行查詢時利用這些提示，方法是將其記憶體授與上限，以避免記憶體爭用。 如需詳細資訊，請參閱[知識庫文章 KB310740](https://support.microsoft.com/kb/3107401)。
-   **較佳的記憶體授與和使用方式診斷：** 已將新的擴充事件 `query_memory_grant_usage` 加入至 SQL Server 的追蹤功能清單中。 此事件會追蹤要求和授與的記憶體授權。 此事件提供更佳的追蹤和分析功能，可針對任何與記憶體授與相關的查詢執行問題進行疑難排解。 如需詳細資訊，請參閱[知識庫文章 KB3107173](https://support.microsoft.com/kb/3107173)。
-   **Tempdb 溢出的查詢執行診斷：**-雜湊警告和排序警告現在有額外的資料行可追蹤實體 i/o 統計資料、使用的記憶體和受影響的資料列。 我們也引進了新的 hash_spill_details 擴充事件。 現在您可以追蹤更細微的雜湊和排序警告資訊（[KB3107172](https://support.microsoft.com/kb/3107172)）。 這項改進現在也會透過 XML 查詢計劃，以新屬性（attribute）的形式（SpillToTempDbType 複雜類型（[KB3107400](https://support.microsoft.com/kb/3107400)））公開。 [設定統計資料] `ON` 現在會顯示排序工作資料表的統計資料。
-   **針對牽涉到剩餘述詞下推的查詢執行計畫改善診斷：** 現在會在查詢執行計畫中回報實際讀取的資料列，以協助改善查詢效能疑難排解。 這些資料列不需要分別捕捉 SET STATISTICS IO。 這些資料列也可以讓您在查詢計劃中查看與剩餘述詞下推的相關資訊。 如需詳細資訊，請參閱[知識庫文章 KB3107397](https://support.microsoft.com/kb/3107397)。


## <a name="additional-information"></a>其他資訊  
 [SQL Server 2014 資源](../2014-toc/index.yml)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 資源中心](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [SQLCat 網站](https://go.microsoft.com/fwlink/p/?linkID=220963)  
