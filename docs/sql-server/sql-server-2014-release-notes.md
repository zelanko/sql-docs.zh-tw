---
title: SQL Server 2014 版本資訊 | Microsoft Docs
description: 建議在安裝或對 Microsoft SQL Server 2014 (12.x) 版本進行疑難排解之前，先閱讀這份版本資訊文件所描述的已知問題。
ms.custom: ''
ms.date: 07/22/2020
ms.prod: sql
ms.technology: release-landing
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
author: rothja
ms.author: jroth
monikerRange: = sql-server-2016
ms.openlocfilehash: adfd91c6771626aa0979da622d95766a2e4e5613
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97409624"
---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]
本文描述 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 版本 (包括相關 Service Pack) 的已知問題。

## <a name="sql-server-2014-service-pack-2-sp2"></a>SQL Server 2014 Service Pack 2 (SP2)

SQL Server 2014 SP2 包含適用於 SQL Server 2014 SP1 CU7 的已發行 Hotfix 彙總套件。 它包含提升的效能和延展性，以及依據客戶和 SQL 社群之意見反應的診斷改善。

### <a name="performance-and-scalability-improvements-in-sp2"></a>SP2 的效能及延展性改善

|功能|描述|取得詳細資訊|
|---|---|---|
|自動軟體式 NUMA 資料分割|您可以在回報每一 NUMA 節點含 8 個以上 CPU 的系統上自動設定軟體式 NUMA。|[軟體式 NUMA (SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md)|
|緩衝集區擴充|可讓 SQL Server 緩衝集區擴充到 8 TB 以上。|[緩衝集區擴充](../database-engine/configure-windows/buffer-pool-extension.md)|
|動態記憶體物件調整| 根據節點與核心數目動態分割記憶體物件。 這項增強功能讓 SQL 2014 SP2 之後的版本不需要使用追蹤旗標 8048。|[動態記憶體物件調整](/archive/blogs/sql_server_team/dynamic-memory-object-scaling)|
|適用於 DBCC CHECK* 命令的 MAXDOP 提示|搭配 sp_configure 值以外的 MAXDOP 設定執行 DBCC CHECKDB 時，這項改善非常有用。|[提示 (Transact-SQL) - 查詢](../t-sql/queries/hints-transact-sql-query.md)|
|SOS_RWLock 的執行緒同步鎖定改善|不需要 SOS_RWLock 的執行緒同步鎖定，而改用類似於記憶體內部 OLTP 的無鎖定技術。 |[SOS_RWLock 重新設計](/archive/blogs/psssql/sql-2016-it-just-runs-faster-sos_rwlock-redesign)|
|空間原生實作|空間查詢效能已顯著改善。|[SQL Server 2012 和 2014 中的空間效能改善](https://support.microsoft.com/help/3107399/spatial-performance-improvements-in-sql-server-2012-and-2014)

### <a name="supportability-and-diagnostics-improvements-in-sp2"></a>SP2 的可支援性和診斷改善

|功能|描述|取得詳細資訊|
|---|---|---|
|AlwaysOn 逾時記錄|已新增「租用逾時」訊息的記錄功能，以便記錄目前的時間和預期的續約時間。 |[已改善 AlwaysOn 可用性群組租用逾時的診斷](/archive/blogs/alwaysonpro/improved-alwayson-availability-group-lease-timeout-diagnostics)
|AlwaysOn XEvent 和效能計數器|全新的 AlwaysOn XEvent 和效能計數器，可改善對 AlwaysOn 延遲問題進行疑難排解時的診斷。 |[KB 3107172](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve) 和 [KB 3107400](https://support.microsoft.com/help/3107400/improved-tempdb-spill-diagnostics-in-showplan-xml-schema-in-sql-server)
|變更追蹤清除|全新的預存程序 sp_flush_CT_internal_table_on_demand 可視需要清除變更追蹤內部資料表。|[KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)
|資料庫複製|使用新的 DBCC 命令，藉由複製結構描述、中繼資料及統計資料 (但不含資料)，以對現有的生產資料庫進行疑難排解。 複製的資料庫不適合用於生產環境。|[KB 3177838](https://support.microsoft.com/help/3177838/how-to-use-dbcc-clonedatabase-to-generate-a-schema-and-statistics-only)
|DMF 新增項目|新的 DMF sys.dm_db_incremental_stats_properties 會公開每個資料分割的資訊，以用於累加統計資料。|[KB 3170114](https://support.microsoft.com/help/3170114/update-to-add-dmf-sys-dm-db-incremental-stats-properties-in-sql-server)
|可擷取 SQL Server 中輸入緩衝區的 DMF|現已提供可擷取工作階段/要求 (sys.dm_exec_input_buffer) 輸入緩衝區的新 DMF。 其功能相當於 DBCC INPUTBUFFER。|[sys.dm_exec_input_buffer](../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
|支援複寫的 DROP DDL|可讓您從資料庫和發行集卸除資料表 (其是以發行項的形式隨附於異動複寫發行集中)。|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)
|SQL 服務帳戶的 IFI 權限|判斷立即檔案初始化 (IFI) 是否在 SQL Server 服務啟動時生效。|[資料庫檔案初始化](../relational-databases/databases/database-instant-file-initialization.md)
|記憶體授與 - 處理問題|透過限定記憶體授與以防止記憶體競爭的做法，您即可在執行查詢同時利用診斷提示。|[KB 3107401](https://support.microsoft.com/help/3107401/new-query-memory-grant-options-are-available-min-grant-percent-and-max)
|每個運算子的查詢執行輕量型分析 |可最佳化每個運算子的查詢執行統計資料收集情況，例如資料列的實際數目等。|[Developers Choice:Query progress - anytime, anywhere](/archive/blogs/sql_server_team/query-progress-anytime-anywhere) (開發人員選擇：查詢進度 - 隨時隨地)
|查詢執行的診斷|現在，查詢執行計畫中會回報實際讀取的資料列，以協助改善查詢效能的疑難排解。|[KB 3107397](https://support.microsoft.com/help/3107397/improved-diagnostics-for-query-execution-plans-that-involve-residual-p)
|針對 tempdb 溢出的查詢執行診斷|現在，Hash Warning 和 Sort Warnings 已具備可追蹤實體 I/O 統計資料、已使用的記憶體，以及受影響的資料列等其他資料行。 |[改善 temptdb 溢出診斷](https://support.microsoft.com/help/3107172/improve-tempdb-spill-diagnostics-by-using-extended-events-in-sql-serve)
|temptdb 可支援性 |您可以使用新的 tempdb 檔案數 Errorlog 訊息，而且 tempdb 資料檔案會在伺服器啟動時變更。|[KB 2963384](https://support.microsoft.com/help/2963384/fix-sql-server-crashes-when-the-log-file-of-tempdb-database-is-full-in)


此外，請注意下列修正：
- Xevent 呼叫堆疊現在包含模組名稱和位移，而不是絕對位址。
- 診斷 XE 和 DMV 之間的較佳關聯性 - 系統會使用 Query_hash 和 query_plan_hash 來唯一識別查詢。 DMV 會將其定義為 varbinary(8)，而 XEvent 會將其定義為 UINT64。 由於 SQL Server 沒有「不帶正負號的 Bigint」，因此轉型不一定會成功。 這項改善引進了相當於 query_hash 和 query_plan_hash 的新 XEvent 動作/篩選資料行 (但當這些資料行定義為 INT64 時則例外)。 此修正有助於將 XE 和 DMV 之間的查詢相互關聯。
- BULK INSERT 和 BCP 中的 UTF-8 支援 - 現在，BULK INSERT 和 BCP 中已啟用支援匯出和匯入以 UTF-8 字元集編碼的資料。

### <a name="download-pages-and-more-information-for-sp2"></a>SP2 的下載頁面和詳細資訊

- [下載 Microsoft SQL Server 2014 Service Pack 2](https://www.microsoft.com/download/details.aspx?id=53168)
- [現已提供 SQL Server 2014 Service Pack 2](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2012 SP2 Express](https://www.microsoft.com/download/details.aspx?id=53167)
- [SQL Server 2014 SP2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=53164)
- [SQL Server 2014 SP2 報表產生器](https://www.microsoft.com/download/details.aspx?id=53163)
- [適用於 Microsoft Sharepoint 的 SQL Server 2014 SP2 Reporting Services 增益集](https://www.microsoft.com/download/details.aspx?id=53162)
- [SQL Server 2014 SP2 語意語言統計資料](https://www.microsoft.com/download/details.aspx?id=53165)
- [SQL Server 2014 Service Pack 2 版本資訊](https://support.microsoft.com/help/3171021/sql-server-2014-service-pack-2-release-information)

## <a name="sql-server-2014-service-pack-1-sp1"></a>SQL Server 2014 Service Pack 1 (SP1)

SQL Server 2014 SP1 包含 SQL Server 2014 CU 1 到 (含) CU 5 中所提供的修正，以及先前隨附於 SQL Server 2012 SP2 中的修正彙總套件。

> [!NOTE]
> 如果您的 SQL Server 執行個體已啟用 SSISDB 目錄，並在升級至 SP1 時收到安裝錯誤，請遵循[在安裝 SQL Server 2014 SP1 時發生的錯誤 912 或 3417](https://support.microsoft.com/help/3018269/error-912-or-3417-when-you-install-sql-server-2014-sp1-build-12-0-4050/) 中對此問題的指示。

### <a name="download-pages-and-more-information-for-sp1"></a>SP1 的下載頁面和詳細資訊

- [下載 Microsoft SQL Server 2014 Service Pack 1](https://www.microsoft.com/download/details.aspx?id=46694)
- [SQL Server 2014 Service Pack 1 已發行 - 已更新](/archive/blogs/sqlreleaseservices/sql-server-2014-service-pack-1-has-released-updated)
- [Microsoft SQL Server 2014 SP1 Express](https://www.microsoft.com/download/details.aspx?id=42299)
- [Microsoft SQL Server 2014 SP1 Feature Pack](https://www.microsoft.com/download/details.aspx?id=46694)


## <a name="before-you-install-sql-server-2014-rtm"></a>安裝 SQL Server 2014 RTM 之前

### <a name="limitations-and-restrictions-in-sql-server-2014-rtm"></a>SQL Server 2014 RTM 的條件和限制

1.  不支援從 SQL Server 2014 CTP 1 升級至 SQL Server 2014 RTM。  
2.  不支援並存安裝 SQL Server 2014 CTP 1 與 SQL Server 2014 RTM。  
3.  不支援將 SQL Server 2014 CTP 1 資料庫附加或還原到 SQL Server 2014 RTM。  

**因應措施：** 無。

#### <a name="upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm"></a>從 SQL Server 2014 CTP 2 升級至 SQL Server RTM
完全支援升級。 具體而言，您可以：

1.  將 SQL Server 2014 CTP 2 資料庫附加到 SQL Server 2014 RTM 執行個體。    
2.  將 SQL Server 2014 CTP 2 上所建立的資料庫備份還原至 SQL Server 2014 RTM 執行個體。    
3.  就地升級至 SQL Server 2014 RTM。
4.  輪流升級至 SQL Server 2014 RTM。 您必須先切換到手動容錯移轉模式，才能起始輪流升級。 如需詳細資料，請參閱[在停機時間和資料遺失最少的情況下升級及更新可用性群組伺服器](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)。    
5.  SQL Server 2014 CTP 2 中安裝之交易效能收集組所收集的資料無法透過 SQL Server 2014 RTM 中的 SQL Server Management Studio 來檢視，反之亦然。
  
#### <a name="downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>從 SQL Server 2014 RTM 降級至 SQL Server 2014 CTP 2  
不支援這個動作。  
  
**因應措施：** 沒有降級的因應措施。 建議您先備份資料庫，再升級至 SQL Server 2014 RTM。  
  
#### <a name="incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>SQL Server 2014 媒體/ISO/CAB 上出現錯誤版本的 StreamInsight 用戶端  
錯誤版本的 StreamInsight.msi 和 StreamInsightClient.msi，位於下列 SQL Server 媒體/ISO/CAB 的路徑中 (StreamInsight\\\<Architecture\>\\\<Language ID\>)。  
  
**因應措施：** 從 [SQL Server 2014 功能套件下載頁面](https://www.microsoft.com/download/details.aspx?id=57474)下載並安裝正確的版本。  
  
### <a name="product-documentation-rtm"></a><a name="ProdDoc"></a>產品文件 RTM
  
報表產生器和 PowerPivit 的內容不提供某些語言版本。 

**問題：** 報表產生器的內容不提供以下這些語言版本：  
  
-   希臘文 (el-GR)  
-   挪威文 (巴克摩) (nb-NO)  
-   芬蘭文 (fi-FI)  
-   丹麥文 (da-DK)  
  
在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中，此內容可從隨附於產品的 CHM 檔案中取得，並且提供這些語言版本。 CHM 檔案不再隨附於產品，而報表產生器內容也只提供在 MSDN 上。 但 MSDN 不支援這些語言。 報表產生器也已從 TechNet 移除，無法再用於那些支援的語言。  
  
**因應措施：** 無。  
  
**問題：** 不提供下列語言版本的 Power Pivot 內容：
  
-   希臘文 (el-GR)  
-   挪威文 (巴克摩) (nb-NO)  
-   芬蘭文 (fi-FI)  
-   丹麥文 (da-DK)  
-   捷克文 (cs-CZ)  
-   匈牙利文 (hu-HU)  
-   荷蘭文 (荷蘭) (nl-NL)  
-   波蘭文 (pl-PL)  
-   瑞典文 (sv-SE)  
-   土耳其文 (tr-TR)  
-   葡萄牙文 (葡萄牙) (pt-PT)  
  
在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中，TechNet 與這些語言版本曾經提供此內容。 此內容已從 TechNet 移除，無法再用於這些支援的語言。  
  
**因應措施：** 無。  
  
### <a name="database-engine-rtm"></a><a name="DBEngine"></a>資料庫引擎 (RTM)
  
#### <a name="changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>針對 SQL Server 2014 RTM Standard Edition 所做的變更  
SQL Server 2014 Standard 版的變更如下：  
  
-   緩衝集區擴充功能最高允許使用已設定之記憶體大小的四倍。    
-   最大記憶體已經從 64 GB 增加至 128 GB。  
 
#### <a name="memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>記憶體最佳化 Advisor 會對預設條件約束標示不相容的旗標  
**問題：** SQL Server Management Studio 中的 Memory Optimized Advisor，會將所有預設條件約束標示為不相容。 並非所有預設條件約束在記憶體最佳化資料表中都有受到支援，此 Advisor 不會區分支援與未支援類型的預設條件約束。 支援的預設條件約束包括：在原生編譯之預存程序內受支援的所有常數、運算式和內建函式。 若要查看以原生方式編譯之預存程序內所支援的函數清單，請參閱 [原生編譯的預存程序中支援的建構](../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md?viewFallbackFrom=sql-server-2014)。  
  
**因應措施：** 如果您要使用這個 Advisor 來識別封鎖程式，請忽略相容的預設條件約束。 若要使用 Memory Optimization Advisor 來移轉具有相容預設條件約束的資料表，但沒有其他封鎖器，請遵循下列步驟進行：  
  
1.  從資料表定義中移除預設條件約束。    
2.  使用此 Advisor 針對資料表產生移轉指令碼。    
3.  在移轉指令碼中加回預設條件約束。    
4.  執行移轉指令碼。  
  
#### <a name="informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>「檔案存取遭拒」參考訊息誤報為 SQL Server 2014 錯誤記錄檔中的錯誤  
**問題：** 當重新啟動的伺服器擁有包含記憶體最佳化資料表資料庫時，可能會在 SQL Server 2014 錯誤記錄檔中看到下列類型的錯誤訊息：  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
此訊息實際上僅供參考，使用者不必採取任何動作。  
  
**因應措施：** 無。 這是參考訊息。  
  
#### <a name="missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>遺漏索引詳細資料誤報了經記憶體最佳化資料表所含的資料行  
**問題：** 如果 SQL Server 2014 偵測到記憶體最佳化資料表上的查詢有遺漏索引，它將會在 SHOWPLAN_XML 中回報索引遺漏，以及在 sys.dm_db_missing_index_details 之類的遺漏索引 DMV 中回報遺漏索引。 在某些情況下，遺漏索引詳細資料將會包含內含的資料行。 當所有資料行都隱含地隨附記憶體最佳化資料表上的所有索引時，不允許明確指定包含記憶體最佳化索引的內含資料行。  
  
**因應措施：** 請勿使用記憶體最佳化資料表上的索引來指定 INCLUDE 子句。  
  
#### <a name="missing-index-details-omit-missing-indexes-when-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>當雜湊索引存在但不適用於查詢時，遺漏索引詳細資料會省略遺漏的索引  
**問題：** 如果您在查詢中參考的記憶體最佳化資料表資料行上擁有 HASH 索引，但是此索引無法用於查詢，則 SQL Server 2014 不一定會在 SHOWPLAN_XML 和 DMV sys.dm_db_missing_index_details 中回報遺漏索引。  
  
特別是，如果查詢包含的等號比較述詞牽涉到索引鍵資料行的子集或是查詢包含的不等號比較述詞牽涉到索引鍵資料行，則 HASH 索引無法以其現狀使用，而且需要不同的索引才能有效率地執行查詢。  
  
**因應措施：** 如果您使用雜湊索引，請查看查詢和查詢計畫，以判斷查詢在索引鍵的子集或不等比較述詞上是否可以從索引搜尋作業獲益。 如果您需要進行索引鍵子集的搜尋，請使用 NONCLUSTERED 索引，或是在您正好需要搜尋的資料行上使用 HASH 索引。 如果您需要進行不等號比較述詞的搜尋，請使用 NONCLUSTERED 索引而不是 HASH 索引。  
  
#### <a name="failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-read_committed_snapshot-is-set-to-on"></a>在相同查詢中使用經記憶體最佳化資料表和經記憶體最佳化資料表變數時，如果資料庫選項 READ_COMMITTED_SNAPSHOT 設為 ON 則會發生失敗  
**問題：** 如果資料庫選項 READ_COMMITTED_SNAPSHOT 設為 ON，且您在使用者交易內容外的相同陳述式中存取記憶體最佳化資料表及記憶體最佳化資料表變數，可能會收到下列錯誤訊息：  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**因應措施：** 請搭配資料表變數使用資料表提示 WITH (SNAPSHOT)，或是使用下列陳述式將資料庫選項 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT 設定為 ON：  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>原生編譯預存程序的程序和查詢執行統計資料，會將工作者時間記錄為 1000 的倍數  
**問題：** 在使用 sp_xtp_control_proc_exec_stats 或 sp_xtp_control_query_exec_stats 為原生編譯的預存程序啟用程序或查詢執行統計資料收集之後，將會看到 DMV sys.dm_exec_procedure_stats 和 sys.dm_exec_query_stats 中回報的 *_worker_time 為 1000 的倍數。 工作者時間少於 500 微秒的查詢執行會將 worker_time 報告為 0。  
  
**因應措施：** 無。 若要在以原生方式編譯的預存程序中執行短期的查詢，請勿依賴執行統計資料 DMV 中所報告的 worker_time。  
  
#### <a name="error-with-showplan_xml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>如果原生編譯的預存程序包含長的運算式，則 SHOWPLAN_XML 會發生錯誤  
**問題：** 如果以原生方式編譯的預存程序包含長運算式，則使用 T-SQL 選項 SET SHOWPLAN_XML ON 或是使用 Management Studio 中 [顯示估計執行計畫] 選項來取得此程序的 SHOWPLAN_XML 時，就可能會產生下列錯誤：  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**因應措施：** 有兩種建議的因應措施：  
  
1.  為運算式加上括號，如以下範例所示：  
  
    不要這樣撰寫：  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    寫入：  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  以稍微簡化的運算式建立第二個程序以供執行程序表使用 - 計劃的一般形狀應該相同。 例如，不要這樣撰寫：  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    寫入：  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>在原生編譯的預存程序中，搭配 DATEPART 和相關函式使用字串參數或變數時，會產生錯誤  
**問題：** 在原生編譯的預存程序中，搭配字串參數或變數使用內建函式 DATEPART、DAY、MONTH 和 YEAR 時，會出現錯誤訊息顯示原生編譯的預存程序不支援 datetimeoffset。  
  
**因應措施：** 將字串參數或變數指派給 datetime2 類型的新變數，然後在函式 DATEPART、DAY、MONTH 或 YEAR 中使用該變數。 例如：  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>原生編譯 Advisor 會對 DELETE FROM 子句標示錯誤的旗標  
**問題：** 原生編譯 Advisor 會將預存程序內的 DELETE FROM 子句，誤標為不相容。  
  
**因應措施：** 無。  
  
#### <a name="register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>透過 SSMS 註冊時，系統會加入含不相符執行個體識別碼的 DAC 中繼資料  
**問題：** 透過 SQL Server Management Studio 註冊或刪除資料層應用程式封裝 (.dacpac) 時，系統未正確更新 sysdac* 資料表來讓使用者查詢資料庫的 dacpac 記錄。  sysdac_history_internal 和 sysdac_instances_internal 的 instance_id 不符合，無法允許聯結。  
  
**因應措施：** 修正此問題的方法為重新發佈 [資料層應用程式架構](https://www.microsoft.com/download/details.aspx?id=100297)的功能套件。  套用更新之後，所有新的記錄項目將使用 sysdac_instances_internal 資料表中針對 instance_id 所列的值。  
  
如果您已遇到不相符的 instance_id 值這項問題，更正不相符之值的唯一方法是以權限使用者身分連接到伺服器，進而寫入 MSDB 資料庫並更新 instance_id 值來使其相符。  如果相同資料庫出現多個註冊和取消註冊的事件，您可能需查看日期/時間，以找出哪個記錄與目前的 instance_id 值相符。  
  
1.  使用具有 MSDB 更新權限的登入身分在 SQL Server Management Studio 中連接到伺服器。    
2.  使用 MSDB 資料庫開啟新的查詢。    
3.  執行此查詢來查看所有使用中的 DAC 執行個體。  尋找您想要更正的執行個體，並記下 instance_id：  
  
    `select * from` sysdac_instances_internal  
  
4.  執行此查詢，並查看所有記錄項目：  
  
    `select * from` sysdac_history_internal  
  
5.  識別應該對應至您要修正之執行個體的資料列。 
6.  將 sysdac_history_internal.instance_id 值更新為您在步驟 3 記下的值 (來自 sysdac_instances_internal 資料表)：  
  
    `update` sysdac_history_internal `set` instance_id = '\<value from step 3\>' `where` \<expression that matches the rows you want to update\>  
  
### <a name="reporting-services-rtm"></a><a name="SSRS"></a>Reporting Services (RTM)
  
#### <a name="the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>SQL Server 2012 Reporting Services 原生模式報表伺服器無法與 SQL Server 2014 Reporting Services SharePoint 元件並存執行  
**問題：** 如果在同一部伺服器上安裝了 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 元件，[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式 Windows 服務 'SQL Server Reporting Services' (ReportingServicesService.exe) 便無法啟動。  
  
**因應措施：** 解除安裝 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 元件，並重新啟動 Microsoft SQL Server 2012 Reporting Services Windows 服務。  
  
**詳細資訊：**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式無法在下列任一情況中同時執行：  
  
-   適用於 SharePoint 產品的 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集    
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共用服務  
  
並存安裝會阻止 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式 Windows 服務啟動。 在 Windows 事件記錄檔中，會出現類似下面的錯誤訊息：  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
如需詳細資訊，請參閱＜ [SQL Server 2014 Reporting Services 提示、秘訣和疑難排解](https://go.microsoft.com/fwlink/?LinkID=391254)＞。  
  
#### <a name="required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>多節點 SharePoint 伺服器陣列升級至 SQL Server 2014 Reporting Services 的必要順序  
**問題：** 如果 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共用服務的執行個體，在所有適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集執行個體之前升級，多節點伺服器陣列中的報表轉譯會失敗。  
  
**因應措施：** 在多節點 SharePoint 伺服器陣列中：  
  
1.  請先升級適用於 SharePoint 產品之 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集的所有執行個體。    
2.  然後升級 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共用服務的所有執行個體。  
  
如需詳細資訊，請參閱 [SQL Server 2014 Reporting Services 提示、秘訣和疑難排解](https://go.microsoft.com/fwlink/?LinkID=391254)。  
  
### <a name="sql-server-2014-rtm-on-azure-virtual-machines"></a><a name="AzureVM"></a>Azure 虛擬機器上的 SQL Server 2014 RTM  
  
#### <a name="the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-azure"></a>在 Azure 中設定可用性群組接聽程式時，[新增 Azure 複本精靈] 傳回錯誤  
**問題：** 如果可用性群組有接聽程式，嘗試在 Azure 中設定接聽程式時，[新增 Azure 複本精靈] 將會傳回錯誤。  
  
這個問題會發生是因為可用性群組接聽程式需要在每一個主控可用性群組複本的子網路 (包括 Azure 子網路) 中指派一個 IP 位址。  
  
**因應措施：**  
  
1.  在 [接聽程式] 頁面中，將 Azure 子網路中將會主控可用性群組複本的免費靜態 IP 位址指派給可用性群組接聽程式。  
  
    這項因應措施可讓精靈完成在 Azure 中新增複本的工作。  
  
2.  當精靈完成之後，您必須在 Azure 中完成接聽程式的組態，如 [Azure 中 AlwaysOn 可用性群組的接聽程式設定](/previous-versions/azure/dn376546(v=azure.100))中所述  
  
### <a name="analysis-services-rtm"></a><a name="SSAS"></a>Analysis Services (RTM)
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>必須針對已使用 SQL Server 2014 設定的 SharePoint 2010 新伺服器陣列，下載、安裝及註冊 MSOLAP.5  
**問題：**  
  
-   如果是有設定 SQL Server 2014 RTM 部署的 SharePoint 2010 伺服器陣列，PowerPivot 活頁簿將無法連接到資料模型，因為連接字串中所參考的提供者並未安裝。必須針對已使用 SQL Server 2014 設定的 SharePoint 2013 新伺服器陣列，下載、安裝及註冊 MSOLAP.5。  
  
**因應措施：**  
  
1.  從 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能套件下載 MSOLAP.5 提供者。 在執行 Excel Services 的應用程式伺服器上安裝提供者。 如需詳細資訊，請參閱 [Microsoft SQL Server 2012 SP1 功能套件](https://www.microsoft.com/download/details.aspx?id=35575)中的＜Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1＞一節。  
  
2.  向 SharePoint Excel Services 註冊 MSOLAP.5 當做信任的提供者。 如需詳細資訊，請參閱 [加入 MSOLAP.5 做為 Excel Services 中受信任的資料提供者](/analysis-services/power-pivot-for-sharepoint-ssas?viewFallbackFrom=sql-server-ver15)。  
  
**詳細資訊：**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包含 MSOLAP.6。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 活頁簿使用 MSOLAP.5。 如果 MSOLAP.5 並未安裝在執行 Excel Services 的電腦上，Excel Services 將無法載入資料模型。  
  
#### <a name="msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>必須針對已使用 SQL Server 2014 設定的 SharePoint 2013 新伺服器陣列，下載、安裝及註冊 MSOLAP.5  
**問題：**  
  
-   如果是已使用 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 部署設定的 SharePoint 2013 伺服器陣列，參照 MSOLAP.5 提供者的 Excel 活頁簿無法連接到表格式資料模型，因為並未安裝連接字串中所參照的提供者。  
  
**因應措施：**  
  
1.  從 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能套件下載 MSOLAP.5 提供者。 在執行 Excel Services 的應用程式伺服器上安裝提供者。 如需詳細資訊，請參閱 [Microsoft SQL Server 2012 SP1 功能套件](https://www.microsoft.com/download/details.aspx?id=35575)中的＜Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1＞一節。  
  
2.  向 SharePoint Excel Services 註冊 MSOLAP.5 當做信任的提供者。 如需詳細資訊，請參閱 [加入 MSOLAP.5 做為 Excel Services 中受信任的資料提供者](/analysis-services/power-pivot-for-sharepoint-ssas?viewFallbackFrom=sql-server-ver15)。  
  
**詳細資訊：**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包含 MSOLAP.6。 但是 SQL Server 2014 PowerPivot 活頁簿會使用 MSOLAP.5。 如果 MSOLAP.5 並未安裝在執行 Excel Services 的電腦上，Excel Services 將無法載入資料模型。  
  
#### <a name="corrupt-data-refresh-schedules-rtm"></a>資料重新整理排程損毀 (RTM)
**問題：**  
  
-   您要更新重新整理排程，而排程已損毀且無法使用。  
  
**因應措施：**  
  
1.  在 Microsoft Excel 中，清除自訂進階屬性。 請參閱下列知識庫文章 [KB 2927748](https://support.microsoft.com/kb/2927748) 的＜因應措施＞一節。  
  
**詳細資訊：**  
  
-    當您更新活頁簿的資料重新整理排程時，如果重新整理排程的序列化長度小於原始排程，則無法正確更新緩衝區大小，且新的排程資訊會與舊的排程資訊合併，而導致排程損毀。  
  
### <a name="data-quality-services-rtm"></a><a name="DQS"></a>Data Quality Services (RTM)
  
#### <a name="no-cross-version-support-for-data-quality-services-in-master-data-services"></a>Master Data Services 中的 Data Quality Services 沒有跨版本支援  
**問題：** 不支援下列狀況：  
  
-   在已安裝 Data Quality Services 2012 的 SQL Server 2012 中，於 SQL Server Database Engine 資料庫中裝載 Master Data Services 2014。  
  
-   在已安裝 Data Quality Services 2014 的 SQL Server 2014 中，於 SQL Server Database Engine 資料庫中裝載 Master Data Services 2012。  
  
**因應措施：** 使用與資料庫引擎資料庫和 Data Quality Services 相同版本的 Master Data Services。  
  
### <a name="upgrade-advisor-issues-rtm"></a><a name="UA"></a>升級建議程式問題 (RTM)
  
#### <a name="sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>SQL Server 2014 升級建議程式會回報與 SQL Server Reporting Services 無關的升級問題  
**問題：** 隨附於 SQL Server 2014 媒體的 SQL Server Upgrade Advisor (SSUA)，在分析 SQL Server Reporting Services 伺服器時誤報多項錯誤。  
  
**因應措施：** [SSUA 的 SQL Server 2014 功能套件](https://www.microsoft.com/download/details.aspx?id=57474)中提供的 SQL Server Upgrade Advisor 已修正此問題。  
  
#### <a name="sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>SQL Server 2014 升級建議程式在分析 SQL Server Integration Services 伺服器時回報錯誤  
**問題：** 隨附於 SQL Server 2014 媒體的 SQL Server Upgrade Advisor (SSUA) 在分析 SQL Server Integration Services 伺服器時回報錯誤。  顯示給使用者看的錯誤如下：  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**因應措施：** [SSUA 的 SQL Server 2014 功能套件](https://www.microsoft.com/download/details.aspx?id=57474)中提供的 SQL Server Upgrade Advisor 已修正此問題。  
  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]