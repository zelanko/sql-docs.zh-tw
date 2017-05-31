---
title: "使用查詢存放區的最佳做法 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f00c5db3574f21010e682f964d06f3c2b61a1d09
ms.openlocfilehash: 9cd813b72eda096f780ed7140b6691f528251a30
ms.contentlocale: zh-tw
ms.lasthandoff: 04/29/2017

---
# <a name="best-practice-with-the-query-store"></a>使用查詢存放區的最佳作法
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主題概述搭配您的工作負載使用查詢存放區的最佳作法。  
  
##  <a name="SSMS"></a> Use the Latest SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 擁有一組針對設定查詢存放區，以及耗用有關工作負載之收集資料所設計的使用者介面。  
請於下列位置下載 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 最新版本：[https://msdn.microsoft.com/library/mt238290.aspx](https://msdn.microsoft.com/library/mt238290.aspx)  
  
 如需有關如何在疑難排解案例中使用查詢存放區的快速說明，請參閱[查詢存放區@Azure 部落格](https://azure.microsoft.com/en-us/blog/query-store-a-flight-data-recorder-for-your-database/)。  
  
##  <a name="Insight"></a> 在 Azure SQL 資料庫中使用查詢效能深入解析  
 如果您在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中執行查詢存放區，您可以使用「查詢效能深入解析」  分析經過一段時間的 DTU 耗用量。  
雖然您可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 取得您所有查詢的資源耗用量詳細資訊 (CPU、記憶體、IO 等等)，「查詢效能深入解析」能提供您一個快速且有效率的方式來判斷資源耗用對您的資料庫之整體 DTU 耗用量的影響。  
如需詳細資訊，請參閱 [Azure SQL 資料庫查詢效能深入解析](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/)。    

##  <a name="using-query-store-with-elastic-pool-databases"></a>搭配彈性集區資料庫使用查詢存放區
您可以放心地在所有資料庫中使用查詢存放區，即使在緊密壓縮的集區中也是一樣。 已經解決所有與過度使用資源有關的問題，這些問題可能發生在彈性集區中大量資料庫已啟用查詢存放區時。
##  <a name="Configure"></a> Keep Query Store Adjusted to your Workload  
 根據您的工作負載和效能疑難排解需求設定查詢存放區。   
預設的參數雖然適合快速使用，但是您應該監視一段時間的查詢存放區操作方式，並據以調整其設定 ︰  
  
 ![query-store-properties](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")  
  
 以下是設定參數值時可遵循的指導方針：  
  
 **大小上限 (MB)：** 指定查詢存放區將在您的資料庫內使用的資料空間的上限。  這是最重要的設定，它會直接影響查詢存放區的作業模式。  
  
 因為查詢存放區會收集查詢、執行計劃和統計資料，它在資料庫中的大小會逐漸增加，直到達到此限制為止。 發生此情況時，查詢存放區會自動將作業模式變更為唯讀，並停止收集新的資料，這表示您的效能分析已不再正確。  
  
 如果您的工作負載會產生很多不同的查詢和計劃，或者是如果您希望保留更長時間的查詢記錄，預設值 (100 MB) 可能不足。 追蹤目前的空間使用量，並增加大小上限 (MB) 以防止查詢存放區轉換為唯讀模式。  使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或執行下列指令碼取得有關查詢存放區大小的最新資訊：  
  
```  
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason  
FROM sys.database_query_store_options;  
```  
  
 下列指令碼會設定新的大小上限 (MB)：  
  
```  
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);  
```  
  
 **統計資料收集間隔：** 定義已收集之執行階段統計資料的資料粒度層級 (預設值是 1 小時)。 如果您需要更精細的資料粒度或使用較短的時間偵測與解決問題，請考慮使用較低的值，但請注意，它會直接影響查詢存放區資料的大小。 使用 SSMS 或 Transact-SQL 來針對統計資料收集間隔設定不同的值：  
  
```  
ALTER DATABASE [QueryStoreDB] SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 30);  
```  
  
 **過時的查詢臨界值 (天)：** 以時間為基礎的清除原則，可控制保存的執行階段統計資料和非使用中查詢的保留期限。  
根據預設，查詢存放區設定為保留資料 30 天，對您的狀況而言，這可能不必要地過長。  
  
 避免保留您沒有計畫使用的歷程記錄資料。 這會降低變更為唯讀狀態。 查詢存放區資料的大小以及偵測和解決問題的時間會更容易預測。 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或下列指令碼來設定以時間為基礎的清除原則：  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 14));  
```  
  
 **大小基礎的清除模式** ：指定查詢存放區的資料大小到達限制時是否自動清除資料。  
  
 強烈建議您啟用大小基礎的清除模式，以確保查詢存放區一律以讀寫模式執行並收集最新的資料。  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);  
```  
  
 **查詢存放區擷取模式** ：指定查詢存放區的查詢擷取模式。  
  
-   **All** – 擷取所有的查詢。 這是預設選項。  
  
-   **Auto** – 忽略不頻繁的查詢及包含無意義的編譯和執行期間的查詢。 執行計數、編譯和執行階段持續時間的臨界值會在內部決定。  
  
-   **None** – 查詢存放區會停止擷取新的查詢。  
  
 下列指令碼會將查詢擷取模式設定為 [Auto]：  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="how-to-start-with-query-performance-troubleshooting"></a>如何開始進行查詢效能的疑難排解  
 疑難排解查詢存放區的工作流程很簡單，如下圖所示：  
  
 ![query-store-troubleshooting](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")  
  
 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 啟用查詢存放區，如上一節中所述，或執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
```  
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;  
```  
  
 這需要一些時間，直到查詢存放區收集了可準確地呈現您的工作負載的資料集為止。 通常一天就已足夠，即使是非常複雜的工作負載。 不過，在您啟用功能之後，您可以開始探索資料並識別立即需要您注意的查詢。   
巡覽至 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的物件總管中資料庫節點下的 [查詢存放區] 子資料夾，以開啟特定案例的疑難排解檢視。   
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 查詢存放區檢視會操作執行計量組，每個都以下列任一統計資料函式表示：  
  
|執行計量|統計資料函式|  
|----------------------|------------------------|  
|CPU 時間、持續時間、執行計數、邏輯讀取、邏輯寫入、記憶體耗用量和實體讀取|平均值、最大值、最小值、標準差、總計|  
  
 下圖顯示顯示如何找出查詢存放區檢視 ︰  
  
 ![query-store-views](../../relational-databases/performance/media/query-store-views.png "query-store-views")  
  
 下表說明每個查詢存放區檢視的使用時機：  
  
|SSMS 檢視|狀況|  
|---------------|--------------|  
|迴歸查詢|找出執行計量最近迴歸的查詢 (也就是變更為更糟)。 <br />使用此檢視將您的應用程式中觀察到的需要修正或改善的效能問題，與實際查詢相互關聯。|  
|熱門資源取用查詢|選擇一個感興趣的執行計量，並識別針對提供的時間間隔具有最極端值的查詢。 <br />使用此檢視將注意力放在最相關的查詢， 也就是對資料庫資源耗用量有最大影響的查詢。|  
|追蹤查詢|即時追蹤最重要的查詢的執行。 一般而言，當您有包含強制計畫的查詢且想要確定查詢效能是否穩定時，會使用此檢視。|  
|整體資源耗用量|針對任何執行計量，分析資料庫的整體資源耗用量。<br />使用此檢視來識別資源模式 (每日與每晚的工作負載) 和最佳化資料庫的整體耗用量。|  
  
> [!TIP]  
>  如需如何使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 識別熱門資源取用查詢並修正那些因為計畫選擇變更而迴歸之查詢的詳細說明，請參閱[查詢存放區@Azure 部落格](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)。  
  
 當您識別次佳效能的查詢時，您的動作會取決於問題的本質。  
  
-   如果是以多個計劃執行查詢，且最後一個計劃明顯比前一個計畫差，您可以使用計劃強制機制來強制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 針對未來的執行一律使用最佳計畫。  
  
     ![query-store-force-plan](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")  
  
-   您可能會推斷您的查詢遺失最佳執行的索引。 此資訊會顯示於查詢執行計畫內。 建立遺失的索引，並使用查詢存放區檢查查詢效能。  
  
     ![query-store-show-plan](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")  
  
     如果您在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]上執行您的工作負載，請註冊 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 索引建議程式以自動接收索引建議。  
  
-   在某些情況下，如果您看到執行計畫中的預估和實際資料列數目之間的差異非常大，您可能會強制統計資料重新編譯。  
  
-   請重寫有問題的查詢。 例如，充分利用查詢參數化，或實作更最多最佳化邏輯。  
  
##  <a name="Verify"></a> Verify Query Store is Collecting Query Data Continuously  
 查詢存放區可以無訊息方式變更作業模式。 您應該定期監視查詢存放區的狀態，以確定查詢存放區正在運作，並採取動作避免因為預防因素造成的失敗。 執行下列查詢來判斷作業模式，並檢視最相關的參數：  
  
```  
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 `actual_state_desc` 和 `desired_state_desc` 之間的差異表示作業模式自動發生變更。 最常見的變更就是查詢存放區以無訊息模式切換到唯讀模式。 在極少的情況下，查詢存放區會因為內部錯誤而造成 ERROR 狀態。  
  
 當實際狀態是唯讀時，請使用 **readonly_reason** 資料行來判斷根本原因。 通常您會發現查詢存放區因為已超過大小配額而轉換為唯讀模式。 在此情況下，**readonly_reason** 是設定為 65536。 針對其他原因，請參閱 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)。  
  
 請考慮下列步驟將查詢存放區切換為讀寫模式並啟用資料收集：  
  
-   使用 **ALTER DATABASE** 的 **MAX_STORAGE_SIZE_MB**選項增加最大儲存體大小。  
  
-   使用下列陳述式清除查詢存放區資料：  
  
    ```  
    ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;  
    ```  
  
 您可以透過執行下列明確地將變更作業模式變更回讀寫，套用其中一個或兩個步驟：  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);  
```  
  
 採取下列積極步驟：  
  
-   您可以套用最佳作法，以避免無訊息的操作模式變更。 如果您確定查詢存放區大小一律會低於允許的最大值，將會大幅減少轉換為唯讀模式的機會。 啟動大小基礎的原則，如 [設定查詢存放區](#Configure) 一節中所述，以便查詢存放區會在接近大小限制時自動清除資料。  
  
-   若要確定會保留最新的資料，請設定以時間為基礎的原則，以定期移除過時的資訊。  
  
-   最後，您應該考慮將 [查詢擷取模式] 設定為 [Auto]，它會篩選掉和您的工作負載通常較不相關的查詢。  
  
### <a name="error-state"></a>錯誤狀態  
 若要復原查詢存放區， 請嘗試明確地重新設定讀寫模式，並檢查實際狀態。  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 如果問題持續發生，表示已損毀的查詢存放區資料會持續保存在磁碟上。 要求讀寫模式之前，您必須先清除查詢存放區。  
  
```  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE CLEAR;  
GO  
  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
## <a name="set-the-optimal-query-capture-mode"></a>設定最佳查詢擷取模式  
 在查詢存放區中保留最相關的資料。 下表說明每個查詢擷取模式的典型案例 ︰  
  
|查詢擷取模式|狀況|  
|------------------------|--------------|  
|All|根據所有查詢圖形和其執行頻率和其他統計資料，徹底分析您的工作負載。<br /><br /> 識別您的工作負載中的新查詢。<br /><br /> 偵測特定查詢是否用來識別使用者或自動參數化的機會。|  
|Auto|將注意力放在相關聯且可採取動作的查詢上；定期執行或耗用大量資源的那些查詢。|  
|None|您已擷取您想要在執行階段中監視的查詢集，且您想要排除其他查詢可能會造成的分心。<br /><br /> 「無」適合用於測試和效能評定環境。<br /><br /> 「無」也適用於在出貨時已將查詢存放區組態設定為監視其應用程式工作負載的軟體廠商。<br /><br /> 「無」應該謹慎使用，您可能會因此喪失機會來追蹤和最佳化重要的新查詢。 除非您有需要「無」的特定案例，否則請避免使用。|  
  
## <a name="keep-the-most-relevant-data-in-query-store"></a>在查詢存放區中保留最相關的資料  
 設定查詢存放區僅包含相關的資料，且可以持續提供絕佳的疑難排解體驗，對您的一般工作負載的影響最小。  
下表提供最佳作法：  
  
|最佳作法|設定|  
|-------------------|-------------|  
|限制保留的歷程記錄資料。|設定以時間為基礎的原則，以啟用自動清除。|  
|篩選掉不相關的查詢。|將 [查詢擷取模式] 設定為 [Auto]。|  
|當到達大小上限時，請刪除比較不相關的查詢。|啟用大小基礎的清除原則。|  
  
##  <a name="Parameterize"></a> Avoid Using Non-Parameterized Queries  
 非絕對必要時，使用非參數化查詢 (例如特定分析的情況) 並不是最佳作法。  快取的計畫無法重複使用，這會強制查詢最佳化工具編譯每一個唯一查詢文字的查詢。  
  此外，查詢存放區可以因為大量潛在不同的查詢文字且因此有大量具有類似圖形的不同執行計畫，而快速超過大小配額。  
因此，您的工作負載的效能會次佳，而查詢存放區可能會切換到唯讀模式，或可能不斷地刪除嘗試要跟上內送查詢的資料。  
  
 請考慮下列選項：  
  
-   在適用情況下參數化查詢，例如將查詢包裝在預存程序內。  
  
-   如果您的工作負載包含許多搭配不同查詢計劃的單次使用特定批次，請使用 [針對特定工作負載最佳化]  選項。  
  
    -   比較不同 query_hash 值的數目與 sys.query_store_query 中的項目總數。 如果比例接近 1，您的特定工作負載會產生不同的查詢。  
  
-   如果不同的查詢計畫數目不大，請針對資料庫或查詢子集套用「強制參數化」。  
  
    -   使用計畫指南以強制僅針對已選取查詢強制參數化。  
  
    -   如果您的工作負載中有少數不同的查詢計劃，請針對資料庫設定「強制參數化」。 (當不同 query_hash 計數和 sys.query_store_query 中的項目總數之間的比例遠小於 1 時。)  
  
-   將 [查詢擷取模式]  設定為 [自動]，以自動篩選掉小型資源耗用的特定查詢。  
  
##  <a name="Drop"></a> Avoid a DROP and CREATE Pattern When Maintaining Containing Objects for the Queries  
 查詢存放區會將查詢項目與包含物件 (預存程序、函式和觸發程序) 產生關聯。  當您重新建立一個包含物件時，將會針對相同的查詢文字產生新的查詢項目。 這會防止您針對該查詢追蹤一段時間的效能統計資料，並使用計畫強制機制。 若要避免這個問題，請使用 `ALTER <object>` 程序盡可能變更包含物件定義。  
  
##  <a name="CheckForced"></a> Check the Status of Forced Plans Regularly  
 強制執行計畫是一個針對重要查詢修正效能的方便的機制，並讓查詢變得更容易預測。 不過，因為有計畫提示與計畫指南，強制執行計畫並不保證它將在未來的執行中使用。 一般而言，當資料庫結構描述都以執行計畫所參考之物件都已改變或卸除的方式變更時，強制執行計畫就會開始失敗。 在此情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會退而重新編譯查詢，而實際的強制執行失敗原因會顯示在 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) 中。 下列查詢會傳回強制執行計畫的相關資訊 ︰  
  
```  
USE [QueryStoreDB];  
GO  
  
SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,  
    force_failure_count, last_force_failure_reason_desc  
FROM sys.query_store_plan AS p  
JOIN sys.query_store_query AS q on p.query_id = q.query_id  
WHERE is_forced_plan = 1;  
```  
  
 如需完整的原因清單，請參閱 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。 您也可以使用 **query_store_plan_forcing_failed** XEvent 追蹤疑難排解強制執行計畫失敗。  
  
##  <a name="Renaming"></a> Avoid Renaming Databases if you have Queries with Forced Plans  
 執行計畫參考使用三部分名稱 (`database.schema.object`) 的物件。   
如果您重新命名資料庫，強制執行計畫將會失敗，而導致重新編譯所有後續查詢執行。  
  
## <a name="see-also"></a>另請參閱  
 [查詢存放區目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [使用含有記憶體內部 OLTP 的查詢存放區](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  

