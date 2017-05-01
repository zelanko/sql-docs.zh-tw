---
title: "使用查詢存放區監視效能 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store
- Query Store, described
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5785d0283be2fe40b5010f6f9373f9a2ea81554a
ms.lasthandoff: 04/11/2017

---
# <a name="monitoring-performance-by-using-the-query-store"></a>使用查詢存放區監視效能
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢存放區功能為您提供關於查詢計劃選擇及效能的深入資訊。 其可協助您您快速找出由於查詢計劃變更所導致的效能差異，以簡化效能疑難排解作業。 查詢存放區會自動擷取查詢、計劃和執行階段統計資料的歷程記錄，並將其保留供您檢閱。 其會以時段來區分資料、供您查看資料庫使用模式，並了解何時在伺服器上發生查詢計劃變更。 使用 [ALTER DATABASE SET] [](../../t-sql/statements/alter-database-transact-sql-set-options.md) 選項可設定查詢存放區。 
  
 如需操作 Azure SQL Database 中查詢存放區的相關資訊，請參閱 [操作 Azure SQL Database 中的查詢存放區](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/)。  
  
##  <a name="Enabling"></a> Enabling the Query Store  
 新的資料庫預設不會啟用查詢存放區。  
  
#### <a name="use-the-query-store-page-in-management-studio"></a>使用 Management Studio 中的查詢存放區頁面  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下資料庫，然後按一下 [屬性] 。  
  
    > [!NOTE]  
    >  至少需要 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]版本。  
  
2.  在 [資料庫屬性]  對話方塊中，選取 [查詢存放區]  頁面。  
  
3.  在 [作業模式 (要求)]  方塊中，選取 [開啟] 。  
  
#### <a name="use-transact-sql-statements"></a>使用 Transact-SQL 陳述式  
  
1.  使用 **ALTER DATABASE** 陳述式可啟用查詢存放區。 例如：  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET QUERY_STORE = ON;  
    ```  
  
     如需和查詢存放區相關之語法選項的詳細資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。  
  
> [!NOTE]  
>  您無法為 **master** 或 **tempdb** 資料庫啟用查詢存放區。  
 
  
##  <a name="About"></a> 查詢存放區中的資訊  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中任何特定查詢的執行計劃通常會在一段時間後，因為統計資料的變更、結構描述變更、建立/刪除索引等數種不同原因而有所演變。儲存快取的查詢計劃之程序快取，只會儲存最新的執行計劃。 計劃也會因為記憶體不足的壓力，而從計劃快取中收回。 因此，因為執行計劃變更所造成的查詢效能低下，可能相形重要，而且可能需要許多時間才可解決。  
  
 因為查詢存放區會為每項查詢保留多個執行計劃，其可強制套用原則以指示查詢處理器要為查詢使用特定的執行計劃。 這也稱為強制執行計劃。 查詢存放區中的強制執行計劃，透過類似於 [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md) 查詢提示的機制加以提供，但它不需要在使用者應用程式中進行任何變更。 強制執行計劃可以解決在非常短的期間內，因計劃變更所導致的查詢效能低下。  
  
 使用查詢存放區功能的常見情況包括：  
  
-   強制執行先前的查詢計劃，快速找出並修正計劃效能低下。 修正因為執行計劃變更而最近出現的效能低下。  
  
-   判斷在指定的時段執行查詢的次數、協助 DBA 疑難排解資源的效能問題。  
  
-   識別過去 *x* 小時內的前 *n* 項查詢 (依據執行時間、記憶體耗用量等等)。  
  
-   稽核指定的查詢之查詢計劃記錄。  
  
-   分析特定資料庫的資源 (CPU、I/O 及記憶體) 使用模式。  
  
 查詢存放區包含兩個存放區。 **計劃存放區** 可保存執行計劃資訊，而 **執行階段統計資料存放區** 則會保存執行統計資料資訊。 計劃存放區中可為查詢儲存的不重複計劃數目，受限於 **max_plans_per_query** 組態選項。 若要增強效能，資訊會以非同步方式寫入兩個存放區。 若要將空間使用量降至最低，在執行階段統計資料存放區中的執行階段執行統計資料，會以固定的時段彙總。 對查詢存放區目錄檢視進行查詢時，會顯示這些存放區中的資訊。  
  
 下列查詢會傳回查詢存放區中查詢與計劃的相關資訊。  
  
```  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
 
  
##  <a name="Regressed"></a> Use the Regressed Queries Feature  
 啟用查詢存放區之後，重新整理物件總管窗格中的資料庫部分，以加入＜ **查詢存放區** ＞一節。  
  
 ![物件總管中的查詢存放區樹狀結構](../../relational-databases/performance/media/objectexplorerquerystore.PNG "物件總管中的查詢存放區樹狀結構")  
  
 選取 [迴歸查詢]  ，開啟 **中的 [迴歸查詢]**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]窗格。 [迴歸查詢] 窗格會顯示查詢存放區中的查詢與計劃。 頂端的下拉式清單方塊，可供您依據各種條件選取查詢。 選取計劃即可以圖形方式檢視查詢計劃。 提供有按鈕可供檢視來源查詢、強制執行或取消強制執行查詢計劃，以及重新整理顯示畫面。  
  
 ![物件總管中的迴歸查詢](../../relational-databases/performance/media/objectexplorerregressedqueries.PNG "物件總管中的迴歸查詢")  
  
 若要強制執行計劃，請選取查詢與計劃，然後按一下 [強制執行計劃] 。 您只可以強制執行由查詢計劃功能所儲存且仍保留在查詢計劃快取中的計劃。  
 
  
##  <a name="Options"></a> Configuration Options  
 OPERATION_MODE  
 可以是 READ_WRITE (預設) 或 READ_ONLY。  
  
 CLEANUP_POLICY (STALE_QUERY_THRESHOLD_DAYS)  
 設定 STALE_QUERY_THRESHOLD_DAYS 引數，可指定在查詢存放區中保留資料的天數。 預設值是 30。 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 版的預設值為 7 天。
  
 DATA_FLUSH_INTERVAL_SECONDS  
 決定將寫入查詢存放區的資料保存到磁碟的頻率。 為了獲得最佳效能，查詢存放區所收集的資料會以非同步方式寫入磁碟。 此非同步傳輸發生的頻率，以 DATA_FLUSH_INTERVAL_SECONDS 設定。 預設值為 900 (15 分鐘)。  
  
 MAX_STORAGE_SIZE_MB  
 設定查詢存放區的大小上限。 若查詢存放區中的資料到達了 MAX_STORAGE_SIZE_MB 限制，查詢存放區會自動從讀寫狀態變更為唯讀，並會停止收集新的資料。  預設值為 100Mb。 針對 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium 版本預設值為 1Gb，而針對 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic 版本預設值為 10Mb。
  
 INTERVAL_LENGTH_MINUTES  
 決定執行階段執行統計資料彙總至查詢存放區的時間間隔。 若要最佳化空間的使用量，在執行階段統計資料存放區中的執行階段執行統計資料，會以固定的時段彙總。 這個固定時段由 INTERVAL_LENGTH_MINUTES 所設定。 預設值為 60。 
  
 SIZE_BASED_CLEANUP_MODE  
 控制當總資料量接近大小上限時，是否要自動啟用清除。 可以 AUTO (預設) 或 OFF。  
  
 QUERY_CAPTURE_MODE  
 指定讓查詢存放區根據執行計數和資源耗用來擷取所有查詢或相關查詢，或是停止新增查詢而僅追蹤目前的查詢。 可以是 ALL (擷取所有的查詢)，AUTO (略過不頻繁及具有無意義編譯和執行期間的查詢) 或 NONE (停止擷取新的查詢)。 SQL Server 2016 的預設值為 ALL，而 Azure SQL Database 上的預設值為 AUTO。
  
 max_plans_per_query  
 表示維護每個查詢計劃的大數目的整數。 預設值為 200。  
  
 查詢 **sys.database_query_store_options** 檢視可判斷查詢存放區目前的選項。 如需有關值的詳細資訊，請參閱 [sys。database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)。  
  
 如需使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式設定選項的詳細資訊，請參閱 [選項管理](#OptionMgmt)。  
 
  
##  <a name="Related"></a> Related Views, Functions, and Procedures  
 透過 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或使用下列檢視與程序，檢視及管理查詢存放區。  
  
-   [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
### <a name="query-store-catalog-views"></a>查詢存放區目錄檢視  
 共有七個目錄檢視可提供有關查詢存放區的資訊。  
  
-   [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
  
-   [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)  
  
-   [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)  
  
-   [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)  
  
-   [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)  
  
-   [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)  
  
-   [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)  
  
### <a name="query-store-stored-procedures"></a>查詢存放區預存程序  
 共有六個預存程序可設定查詢存放區。  
  
-   [sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)  
  
-   [sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)  
  
-   [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)  
  
-   [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)  
  
-   [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)  
  
-   [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)  
 
  
##  <a name="Scenarios"></a> 主要使用方式案例  
  
###  <a name="OptionMgmt"></a> Option Management  
 本節提供管理查詢存放區功能本身的一些指導方針。  
  
 **查詢存放區目前為作用中？**  
  
 查詢存放區會將其資料儲存在使用者資料庫中，這也就是為什麼它有大小的限制 (以 **MAX_STORAGE_SIZE_MB**設定)。 若查詢存放區中的資料達到上限，查詢存放區會自動從讀寫狀態變更為唯讀，並會停止收集新的資料。  
  
 查詢 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) 可判斷查詢存放區目前是否在作用中，以及其目前是否正在收集執行階段統計資料。 currently collects runtime stats or not.  
  
```  
SELECT actual_state, actual_state_desc, readonly_reason,   
    current_storage_size_mb, max_storage_size_mb  
FROM sys.database_query_store_options;  
```  
  
 查詢存放區的狀態取決於 actual_state 資料行。 若與想要的狀態不同，readonly_reason 資料行可以提供更多的資訊。   
當查詢存放區的大小超過配額時，此功能會切換為 readon_only 模式。  
  
 **取得查詢存放區選項**  
  
 若要找出查詢存放區狀態的詳細資訊，請於使用者資料庫中執行下列作業。  
  
```  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **設定查詢存放區間隔**  
  
 您可以覆寫彙總查詢執行階段統計資料的間隔 (預設為 60 分鐘)。  
  
```  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 請注意，不得使用任意值，您應使用下列其中之一：1、5、10、15、30、60 和 1440 分鐘。  
  
 新的間隔值是透過 **sys.database_query_store_options** 檢視而公開。  
  
 **查詢存放區空間使用量**  
  
 若要檢查目前的查詢存放區的大小和限制，請在使用者資料庫中執行下列陳述式。  
  
```  
SELECT current_storage_size_mb, max_storage_size_mb   
FROM sys.database_query_store_options;  
```  
  
 如果查詢存放區的儲存體已滿，請使用下列陳述式來擴充該儲存體。  
  
```  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **設定所有查詢存放區選項**  
  
 使用單一 ALTER DATABASE 陳述式即可一次設定多個查詢存放區選項。  
  
```  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY =   
    (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15,  
    SIZE_BASED_CLEANUP_MODE = AUTO,  
    QUERY_CAPTURE_MODE = AUTO,  
    MAX_PLANS_PER_QUERY = 1000  
);  
```  
  
 **清理空間**  
  
 查詢存放區內部資料表於建立資料庫時建立在 PRIMARY 檔案群組中，且該組態之後無法變更。 如果您快要用完了空間，可能會想要使用下列陳述式，來清除舊的查詢存放區資料。  
  
```  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 或者，您也可能只想要清除特定查詢資料，因為它對於查詢最佳化和計劃分析來說較不相關，但也佔用一樣的空間。  
  
 **刪除臨機操作查詢** 如此做會刪除只執行一次且超過 24 小時的查詢。  
  
```  
DECLARE @id int  
DECLARE adhoc_queries_cursor CURSOR   
FOR   
SELECT q.query_id  
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON q.query_text_id = qt.query_text_id  
JOIN sys.query_store_plan AS p   
    ON p.query_id = q.query_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
GROUP BY q.query_id  
HAVING SUM(rs.count_executions) < 2   
AND MAX(rs.last_execution_time) < DATEADD (hour, -24, GETUTCDATE())  
ORDER BY q.query_id ;  
  
OPEN adhoc_queries_cursor ;  
FETCH NEXT FROM adhoc_queries_cursor INTO @id;  
WHILE @@fetch_status = 0  
    BEGIN   
        PRINT @id  
        EXEC sp_query_store_remove_query @id  
        FETCH NEXT FROM adhoc_queries_cursor INTO @id  
    END   
CLOSE adhoc_queries_cursor ;  
DEALLOCATE adhoc_queries_cursor;  
```  
  
 您可以用不同的邏輯來定義自己的程序，以清除不再需要的資料。  
  
 以上範例使用 **sp_query_store_remove_query** 擴充預存程序，以移除不必要的資料。 您也可以使用：  
  
-   **sp_query_store_reset_exec_stats** – 為給定的計劃清除執行階段統計資料。  
  
-   **sp_query_store_remove_plan** – 以移除單一計畫。  
 
  
###  <a name="Peformance"></a> Performance Auditing and Troubleshooting  
 查詢存放區會保留整個查詢執行過程當中的編譯和執行階段度量歷程記錄，以讓您詢問關於工作負載的問題。  
  
 **前 *n* 個在資料庫上執行的查詢？**  
  
```  
SELECT TOP 10 qt.query_sql_text, q.query_id,   
    qt.query_text_id, p.plan_id, rs.last_execution_time  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
ORDER BY rs.last_execution_time DESC;  
```  
  
 **每項查詢的執行次數？**  
  
```  
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,   
    SUM(rs.count_executions) AS total_execution_count  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text  
ORDER BY total_execution_count DESC;  
```  
  
 **前一個小時內，平均執行時間最長的查詢數目？**  
  
```  
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,  
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,   
    rs.last_execution_time   
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())  
ORDER BY rs.avg_duration DESC;  
```  
  
 **過去 24 小時內，有相對應的平均資料列計數與執行計數，且平均實體 IO 讀取最大的查詢數目？**  
  
```  
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,   
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,   
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id  
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())   
ORDER BY rs.avg_physical_io_reads DESC;  
```  
  
 **具有多項計畫的查詢？** 這些查詢特別有趣的原因是，它們都是因為計劃選擇變更而導致低下的對象。 下列查詢能找出這些查詢以及所有計劃：  
  
```  
WITH Query_MultPlans  
AS  
(  
SELECT COUNT(*) AS cnt, q.query_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q  
    ON qt.query_text_id = q.query_text_id  
JOIN sys.query_store_plan AS p  
    ON p.query_id = q.query_id  
GROUP BY q.query_id  
HAVING COUNT(distinct plan_id) > 1  
)  
  
SELECT q.query_id, object_name(object_id) AS ContainingObject,   
    query_sql_text, plan_id, p.query_plan AS plan_xml,  
    p.last_compile_start_time, p.last_execution_time  
FROM Query_MultPlans AS qm  
JOIN sys.query_store_query AS q  
    ON qm.query_id = q.query_id  
JOIN sys.query_store_plan AS p  
    ON q.query_id = p.query_id  
JOIN sys.query_store_query_text qt   
    ON qt.query_text_id = q.query_text_id  
ORDER BY query_id, plan_id;  
```  
  
 **最近效能低下的查詢 (與時間中的不同點相較)？** 下列查詢範例會傳回所有過去 48 小時內，因為計劃選擇變更而導致執行時間為兩倍的查詢。 查詢會並列比較所有執行階段。  
  
```  
SELECT   
    qt.query_sql_text,   
    q.query_id,   
    qt.query_text_id,   
    rs1.runtime_stats_id AS runtime_stats_id_1,  
    rsi1.start_time AS interval_1,   
    p1.plan_id AS plan_1,   
    rs1.avg_duration AS avg_duration_1,   
    rs2.avg_duration AS avg_duration_2,  
    p2.plan_id AS plan_2,   
    rsi2.start_time AS interval_2,   
    rs2.runtime_stats_id AS runtime_stats_id_2  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p1   
    ON q.query_id = p1.query_id   
JOIN sys.query_store_runtime_stats AS rs1   
    ON p1.plan_id = rs1.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi1   
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id   
JOIN sys.query_store_plan AS p2   
    ON q.query_id = p2.query_id   
JOIN sys.query_store_runtime_stats AS rs2   
    ON p2.plan_id = rs2.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi2   
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id  
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())   
    AND rsi2.start_time > rsi1.start_time   
    AND p1.plan_id <> p2.plan_id  
    AND rs2.avg_duration > 2*rs1.avg_duration  
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;  
```  
  
 如果您想要查看所有低下的效能 (不只因方案選擇變更的相關項目)，只要從上一個查詢移除條件 `AND p1.plan_id <> p2.plan_id` 即可。  
  
 **最近效能低下的查詢 (比較最近的執行與記錄的執行)？** 下一個查詢會依據執行時段，比較查詢的執行。 在此特別的範例中，查詢會比較最近期間內 (1 小時) 與歷程記錄期間 (前一天) 的執行，並找出因 `additional_duration_workload`所引發的項目。 此度量會計算最近的平均執行與記錄的平均執行之間的差，乘以最近執行的數目。 它實際上代表與記錄相較，最近的執行引發了多少額外的時間：  
  
```  
--- "Recent" workload - last 1 hour  
DECLARE @recent_start_time datetimeoffset;  
DECLARE @recent_end_time datetimeoffset;  
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());  
SET @recent_end_time = SYSUTCDATETIME();  
  
--- "History" workload  
DECLARE @history_start_time datetimeoffset;  
DECLARE @history_end_time datetimeoffset;  
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());  
SET @history_end_time = SYSUTCDATETIME();  
  
WITH  
hist AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
     FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @history_start_time   
               AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time \<= @history_start_time   
               AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time \<= @history_end_time   
               AND rs.last_execution_time > @history_end_time)  
    GROUP BY p.query_id  
),  
recent AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
    FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @recent_start_time   
               AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time \<= @recent_start_time   
               AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time \<= @recent_end_time   
               AND rs.last_execution_time > @recent_end_time)  
    GROUP BY p.query_id  
)  
SELECT   
    results.query_id query_id,  
    results.query_text query_text,  
    results.additional_duration_workload additional_duration_workload,  
    results.total_duration_recent total_duration_recent,  
    results.total_duration_hist total_duration_hist,  
    ISNULL(results.count_executions_recent, 0) count_executions_recent,  
    ISNULL(results.count_executions_hist, 0) count_executions_hist   
FROM  
(  
    SELECT  
        hist.query_id query_id,  
        qt.query_sql_text query_text,  
        ROUND(CONVERT(float, recent.total_duration/  
                   recent.count_executions-hist.total_duration/hist.count_executions)  
               *(recent.count_executions), 2) AS additional_duration_workload,  
        ROUND(recent.total_duration, 2) total_duration_recent,   
        ROUND(hist.total_duration, 2) total_duration_hist,  
        recent.count_executions count_executions_recent,  
        hist.count_executions count_executions_hist     
    FROM hist   
        JOIN recent   
            ON hist.query_id = recent.query_id   
        JOIN sys.query_store_query AS q   
            ON q.query_id = hist.query_id  
        JOIN sys.query_store_query_text AS qt   
            ON q.query_text_id = qt.query_text_id      
) AS results  
WHERE additional_duration_workload > 0  
ORDER BY additional_duration_workload DESC  
OPTION (MERGE JOIN);  
```  
 
  
###  <a name="Stability"></a> Maintaining Query Performance Stability  
 若是執行多次的查詢，您可會注意到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用不同的計劃，而產生了不同的資源使用率與持續時間。 您可利用查詢存放區，輕鬆偵測查詢效能何時低下，以及判斷在意時段中的最佳計劃。 然後可以對未來的查詢強制執行該最佳計劃。  
  
 也可以為具有參數 (自動設定參數或手動設定參數) 的查詢，找出不一致的查詢效能。 您可以在不同的計劃間，找出適合所有或大部分參數值的良好且快速之計劃，並強制執行該計劃，為更多使用者案例留下可預測的效能。  
  
 **為查詢強制執行計劃 (套用強制原則)。** 若要為特定的查詢強制執行一項計劃，則每次查詢執行時，就會強制以該計劃執行。  
  
```  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
 使用 **sp_query_store_force_plan** 時，只能強制執行查詢存放區所記錄的計劃，作為該查詢的計劃。 換句話說，可用於查詢的計劃，是已經用於執行該查詢的計劃 (查詢存放區當時在作用中)。  
  
 **為查詢移除強制執行計劃。** 若要再次依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具來計算最佳的查詢計劃，請使用 **sp_query_store_unforce_plan** 以取消為該查詢所選取的強制計劃。  
  
```  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  
 
  
## <a name="see-also"></a>另請參閱  
 [查詢存放區的最佳作法](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [使用含有記憶體內部 OLTP 的查詢存放區](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [查詢存放區使用案例](../../relational-databases/performance/query-store-usage-scenarios.md)   
 [查詢存放區如何收集資料](../../relational-databases/performance/how-query-store-collects-data.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [查詢存放區目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [效能監視及微調工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [開啟活動監視器 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)   
 [活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
 [操作 Azure SQL Database 中的查詢存放區](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/) 
  

