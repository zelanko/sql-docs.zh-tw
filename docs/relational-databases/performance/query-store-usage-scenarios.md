---
title: 查詢存放區使用案例 | Microsoft Docs
description: 了解如何使用查詢存放區來追蹤並確保可預測的工作負載效能。 請考慮 SQL Server 中的幾個範例。
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, usage scenarios
ms.assetid: f5309285-ce93-472c-944b-9014dc8f001d
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0ca2f3b6f30e87d9c545a3713ef157d8a9f4cc90
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505071"
---
# <a name="query-store-usage-scenarios"></a>查詢存放區使用案例
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  若追蹤並確保可預測的工作負載效能非常重要，就能在整組案例中廣泛使用查詢存放區。 以下是您可以考慮的一些範例︰  
  
-   透過計畫選擇迴歸找出並修正查詢  
-   識別與調整資源使用查詢  
-   A/B 測試  
-   在升級到新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 期間保持效能穩定性  
-   識別並改善臨機操作工作負載  
  
## <a name="pinpoint-and-fix-queries-with-plan-choice-regressions"></a>透過計畫選擇迴歸找出並修正查詢  
 在查詢最佳化工具的一般查詢執行期間，其可能因重要的輸入已改變，而決定採取不同的計畫：資料基數已變更；索引已建立、改變或卸除；統計資料已更新等。在大多數情況下，比起先前使用的計畫，新計畫會更好或不相上下。 不過，還是會出現新計畫明顯較糟的情況，而這類情況則稱為計畫選擇變更迴歸。 在具有查詢存放區功能之前，這是個難以找出並修正的問題，原因是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並未提供內建資料存放區，讓使用者可查看某一段時間內所使用的執行計畫。  
  
 有了查詢存放區，您就可快速地：  
  
-   識別在感興趣的時段 (過去小時、天、週等) 中執行計量已降低的所有查詢。 使用 **中的** 迴歸查詢 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來加速您的分析。  
  
-   在迴歸查詢之間，輕易地就能找出具有多個計畫的查詢，以及因選擇不正確的計畫而造成執行計量降低的查詢。 使用 [迴歸查詢]  中的 [計畫摘要]  窗格，以視覺化方式顯示某個迴歸查詢的所有計畫及其在某一段期間內的查詢效能。  
  
-   從歷程記錄強制執行先前的計畫 (如果已證實該計畫比較好)。 使用 [迴歸查詢] 中的 [強制計劃] 按鈕，強制執行針對查詢所選取的計劃。  
  
 ![顯示計劃摘要的查詢存放區螢幕擷取畫面。](../../relational-databases/performance/media/query-store-usage-1.png "query-store-usage-1")  
  
 如需此案例的詳細描述，請參閱 [Query Store:A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/) (查詢存放區︰適用於資料庫的飛行資料記錄器) 部落格。  
  
## <a name="identify-and-tune-top-resource-consuming-queries"></a>識別與調整資源使用查詢  
 雖然您的工作負載可能會產生成千上萬個查詢，但通常只有其中幾個實際上最常使用系統資源，因而需要您多加注意。 在前幾大耗用資源的查詢中，您通常會發現這類查詢若不是迴歸，就是可透過其他調整來改善的查詢。  
  
 開始探勘的最簡單方式是開啟 **中的 [熱門資源取用查詢]** [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 使用者介面會分成三個窗格︰代表熱門資源取用查詢的長條圖 (左)、所選取查詢的計畫摘要 (右)，以及所選取計畫的視覺化查詢計畫 (下方)。 按一下 [設定]  按鈕，來控制您想要分析的查詢數量以及感興趣的時間間隔。 此外，您可以在不同的資源耗用維度 (持續時間、CPU、記憶體、IO、執行數目) 和基準 (平均、最小值、最大值、總計、標準差) 之間進行選擇。  
  
 ![顯示可識別及調整前幾名耗用資源查詢的查詢存放區螢幕擷取畫面。](../../relational-databases/performance/media/query-store-usage-2.png "query-store-usage-2")  
  
 查看右邊的計畫摘要來分析執行歷程記錄，並了解不同的計畫及其執行階段統計資料。 使用下方窗格來檢查不同的計畫，或是以視覺化的並排顯示方式來比較它們 (使用 [比較] 按鈕)。  
  
當您識別出效能次佳的查詢時，您的動作將取決於問題的本質：  
  
1.  如果是以多個計畫來執行查詢，且最後一個計畫明顯比前一個計畫差，則您可以使用計畫強制執行機制，以確保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將一律使用最佳計畫來進行未來的執行。  
  
2.  檢查最佳化工具是否在 XML 計畫中建議任何遺漏的索引。 如果是，請建立遺漏的索引，並使用查詢存放區來評估索引建立之後的查詢效能  
  
3.  針對查詢所使用的基礎資料表，確定其中的統計資料為最新。  
  
4.  確定查詢所使用的索引會重組。  
  
5.  考慮重寫耗用資源的查詢。 例如，充分利用查詢參數化並減少動態 SQL 的使用。 在讀取資料時實作最佳邏輯 (在資料庫端套用資料篩選，而不是在應用程式端)。  

## <a name="ab-testing"></a>A/B 測試  
 使用查詢存放區，來比較您計畫引進之應用程式變更前後的工作負載效能。 下列清單包含數個範例，您可以使用查詢存放區，來評估環境或應用程式變更對工作負載效能的影響︰  
  
-   推出新的應用程式版本。  
  
-   在伺服器上新增硬體。  
  
-   在成本昂貴查詢所參考資料表上建立遺漏的索引。  
  
-   套用安全性原則以取得資料列層級安全性。 如需詳細資訊，請參閱[使用查詢存放區將資料列層級安全性最佳化](/archive/blogs/sqlsecurity/optimizing-rls-performance-with-the-query-store) \(英文\)。  
  
-   將暫時性系統版本設定新增到您 OLTP 應用程式經常修改的資料表中。  
  
在上述任何案例中，套用下列工作流程︰  
  
1.  在計畫的變更之前使用查詢存放區來執行您的工作負載，以產生效能基準。  
  
2.  在目前受控制的時段中套用應用程式變更。  
  
3.  繼續執行工作負載一段足夠的時間，才能產生變更之後的系統效能影像  
  
4.  比較 #1 和 #3 的結果。  
  
    1.  開啟 [整體資料庫耗用量] 來判斷對整個資料庫的影響。  
  
    2.  開啟 [資源耗用量排名在前的查詢]\ (或使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 執行您自己的分析)，以分析變更最重要的查詢的影響。  
  
5.  萬一無法接受新的效能，請決定要保留變更，或是執行復原。  
  
下圖顯示發生遺漏索引建立情況的查詢存放區分析 (步驟 4)。 開啟 [熱門資源取用查詢] / [計畫摘要] 窗格，即可針對應該會受到索引建立影響的查詢取得這個檢視︰  
  
![顯示發生遺漏索引建立情況時的查詢存放區分析 (步驟 4) 螢幕擷取畫面。](../../relational-databases/performance/media/query-store-usage-3.png "query-store-usage-3")  
  
此外，您可以將計畫在索引建立前後的情況並排顯示以進行比較 ([在另一個視窗中比較所選查詢的計畫] 工具列選項，工具列上以紅色方塊標示的選項)。  
  
![顯示查詢存放區及 [在另一個視窗中比較所選查詢的計劃] 工具列選項的螢幕擷取畫面。](../../relational-databases/performance/media/query-store-usage-4.png "query-store-usage-4")  
  
索引建立之前的計畫 (plan_id  = 1，上方) 具有遺漏索引提示，而您可以檢查叢集索引掃描是查詢中最耗用資源的運算子 (紅色矩形)。  
  
遺漏索引建立之後的計畫 (plan_id = 15，下方) 現在具有索引搜尋 (非叢集的)，可降低查詢的整體成本並提升其效能 (綠色矩形)。  
  
根據分析，您很可能會保留索引，因為查詢效能已改善。  
  
## <a name="keep-performance-stability-during-the-upgrade-to-newer-ssnoversion"></a><a name="CEUpgrade"></a>在升級到新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 期間保持效能穩定性  
在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]之前，使用者在升級到最新平台版本期間，會暴露在效能衰退的風險中。 原因在於，最新版的查詢最佳化工具會在安裝新的位元之後立即變成使用中狀態。  
  
從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 開始，所有的查詢最佳化工具變更都會繫結至最新的[資料庫相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)；因此，計劃不會在升級時立即變更，而是在使用者將 `COMPATIBILITY_LEVEL` 變更為最新版本時變更。 此功能會結合查詢存放區，可讓您在升級過程中對查詢效能擁有絕佳層級的控制。 下圖顯示建議的升級工作流程：  
  
![顯示建議升級工作流程的圖表。](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  
  
1.  升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 但不變更資料庫相容性層級。 它不會公開最新的查詢最佳化工具變更，但仍會提供較新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能 (包括查詢存放區)。  
  
2.  啟用查詢存放區。 如需本主題的詳細資訊，請參閱[針對您的工作負載調整查詢存放區](../../relational-databases/performance/best-practice-with-the-query-store.md#Configure)。

3.  讓查詢存放區擷取查詢和計劃，並利用來源/原資料庫相容性層級建立效能基準線。 請在這個步驟中待足時間，以擷取所有的計劃並取得穩定的基準。 這可以是生產工作負載之一般商務週期的持續時間。  
  
4.  移至最新的資料庫相容性層級︰將您的工作負載公開至最新的查詢最佳化工具變更，讓它有機會建立新計劃。  
  
5.  使用查詢存放區進行分析和迴歸修正︰在大多數情況下，新的查詢最佳化工具變更應該會產生更好的計劃。 不過，查詢存放區可讓您輕鬆找出計劃選擇迴歸，並使用計劃強制執行機制加以修正。 從 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 開始，使用[自動計畫更正](../../relational-databases/automatic-tuning/automatic-tuning.md#automatic-plan-correction)功能時，此步驟會自動執行。  

    a.  如果發生迴歸的情況，請強制執行查詢存放區中先前已知的良好計畫。  
  
    b.  如果無法強制執行查詢計畫，或效能仍然不足，請考慮將[資料庫相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)還原為先前的設定，然後通知 Microsoft 客戶支援。  
    
> [!TIP]
> 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [升級資料庫] 工作來將資料庫的[資料庫相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)升級。 如需詳細資訊，請參閱[使用查詢調整小幫手來升級資料庫](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)。
  
## <a name="identify-and-improve-ad-hoc-workloads"></a>識別並改善臨機操作工作負載  
某些工作負載沒有可調整的主控查詢，無法提高整體的應用程式效能。 這些工作負載通常是使用相對大量的各種查詢作為特性，這其中每一個查詢都會耗用部分的系統資源。 由於是唯一的，這些查詢很少執行 (通常只執行一次，因此會以特別的方式命名)，所以它們的執行階段耗用量並不重要。 另一方面，假設該應用程式會不停地產生全新的查詢，則絕大部分的系統資源會耗費在查詢編譯上，這並不能達到最佳效能。 這對查詢存放區而言不是理想的情況，假設有更大量的查詢和計畫湧進您所保留的空間，這表示查詢存放區很可能會非常快速地以唯讀模式結束。 若您啟用 [Size Based Cleanup Policy (大小基礎清除原則)] ([強烈建議](best-practice-with-the-query-store.md)持續啟動並執行查詢存放區)，則背景處理程序大部分的時間將會清除查詢存放區結構，並佔用大量系統資源。  
  
 [前幾大耗用資源的查詢] 檢視初步顯示出您工作負載在臨機操作方面的根本情況：  
  
![[熱門資源耗用查詢] 檢視的螢幕擷取畫面，其中顯示大部分的熱門資源耗用查詢都只執行過一次。](../../relational-databases/performance/media/query-store-usage-6.png "query-store-usage-6")  
  
使用 [執行計數] 計量來分析您排名最前面的查詢是否是特定的 (這需要您使用 `QUERY_CAPTURE_MODE = ALL` 來執行查詢存放區)。 您可以從上圖看見 90% 的 **前幾大耗用資源的查詢** 只執行了一次。  
  
或者，您可以執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼來取得系統中查詢文字、查詢和計畫的總數，並藉由比較 query_hash 和 plan_hash 來判斷其中的差異：  
  
```sql  
--Do cardinality analysis when suspect on ad hoc workloads
SELECT COUNT(*) AS CountQueryTextRows FROM sys.query_store_query_text;  
SELECT COUNT(*) AS CountQueryRows FROM sys.query_store_query;  
SELECT COUNT(DISTINCT query_hash) AS CountDifferentQueryRows FROM  sys.query_store_query;  
SELECT COUNT(*) AS CountPlanRows FROM sys.query_store_plan;  
SELECT COUNT(DISTINCT query_plan_hash) AS  CountDifferentPlanRows FROM  sys.query_store_plan;  
```  
  
若查詢臨機操作工作負載，這是您可能得到的一種結果：  
  
![如果工作負載使用臨機操作查詢的可能結果螢幕擷取畫面。](../../relational-databases/performance/media/query-store-usage-7.png "query-store-usage-7")  
  
查詢結果顯示，儘管查詢存放區中有大量的查詢和計畫，但其 query_hash 和 query_plan_hash 實際上是一樣的。 唯一查詢文字和唯一查詢雜湊之間的比率遠大於 1，這表示工作負載是適合用來參數化的候選項目，原因是查詢之間唯一的差異只有提供作為部分查詢文字的常值常數 (參數)。  
  
如果您的應用程式會產生查詢 (而不是叫用預存程序或參數化查詢)，或者它依賴預設會產生查詢的物件關聯式對應架構，通常就會發生這種狀況。  
  
如果您可以控制應用程式程式碼，或許能考慮重新撰寫資料存取層，以利用預存程序或參數化查詢。 不過，這種情況也會大幅改善，而不需要藉由針對整個資料庫 (所有查詢) 或含有相同 query_hash 的個別查詢範本強制執行查詢參數化來進行應用程式變更。  
  
使用個別查詢範本的方法需要建立計畫指南︰  
  
```sql  
--Apply plan guide for the selected query template 
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'<your query text goes here>',  
    @stmt OUTPUT,   
    @params OUTPUT;  
  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION (PARAMETERIZATION FORCED)';  
```  
  
含有計畫指南的解決方案來得更精確，但需要更多工作。  
  
如果您的所有查詢 (或大部分查詢) 均為適用於自動參數化的候選項目，則針對整個資料庫變更 `FORCED PARAMETERIZATION` 可能是更好的選項：  
  
```sql  
--Apply forced parameterization for entire database  
ALTER DATABASE <database name> SET PARAMETERIZATION FORCED;  
```  

> [!NOTE]
> 如需本主題的詳細資訊，請參閱[使用強制參數化的指導方針](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide)。

在您套用這其中任何步驟之後， **熱門資源取用查詢** 將會針對您的工作負載顯示不同的圖片。  
  
![顯示不同工作負載圖片的 [熱門資源耗用查詢] 檢視螢幕擷取畫面。](../../relational-databases/performance/media/query-store-usage-8.png "query-store-usage-8")  
  
在某些情況下，您的應用程式可能產生許多各種不適合用作自動參數化候選項目的查詢。 在此情況下，您會在系統中看到大量查詢，但唯一查詢與唯一 `query_hash` 之間的比率很可能接近 1。  
  
在此情況下，您可能想要啟用 [**針對臨機操作工作負載最佳化**](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)伺服器選項，以避免將快取記憶體浪費在可能不會再次執行的查詢上。 若要避免在查詢存放區中擷取這些查詢，請將 `QUERY_CAPTURE_MODE` 設為 `AUTO`。  
  
```sql  
EXEC sys.sp_configure N'show advanced options', N'1' RECONFIGURE WITH OVERRIDE
GO
EXEC sys.sp_configure N'optimize for ad hoc workloads', N'1'
GO
RECONFIGURE WITH OVERRIDE
GO 
  
ALTER DATABASE [QueryStoreTest] SET QUERY_STORE CLEAR;  
ALTER DATABASE [QueryStoreTest] SET QUERY_STORE = ON   
    (OPERATION_MODE = READ_WRITE, QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="see-also"></a>另請參閱  
 [相關檢視、函數與程序](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [查詢存放區的最佳作法](../../relational-databases/performance/best-practice-with-the-query-store.md)         
 [使用查詢調整小幫手來升級資料庫](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)           
