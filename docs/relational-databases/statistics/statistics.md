---
title: "統計資料 | Microsoft Docs"
ms.custom: 
ms.date: 04/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
caps.latest.revision: 70
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e098a8f837d216f18bb1310db3164b57f24575ba
ms.lasthandoff: 04/11/2017

---
# <a name="statistics"></a>Statistics
  查詢最佳化工具會使用統計資料來建立可改善查詢效能的查詢計劃。 對於大部分查詢而言，查詢最佳化工具已經產生高品質查詢計劃的必要統計資料。不過，在少數情況下，您必須建立其他統計資料或修改查詢設計，以便獲得最佳結果。 本主題將討論有效使用查詢最佳化統計資料的概念和指導方針。  
  
##  <a name="DefinitionQOStatistics"></a> 元件和概念  
 Statistics  
 查詢最佳化的統計資料是指包含資料表或索引檢視表之一個或多個資料行中值分佈相關統計資料的物件。 查詢最佳化工具會使用這些統計資料來估計查詢結果中的「基數」或資料列數目。 這些「基數估計值」可讓查詢最佳化工具建立高品質的查詢計劃。 例如，查詢最佳化工具可使用基數估計值來選擇索引搜尋運算子，而非需要更大量資源的索引掃描運算子，而且這樣做會改善查詢效能。  
  
 每個統計資料物件都是針對一或多個資料表資料行的清單所建立，而且包含顯示第一個資料行中值分佈的長條圖。 多個資料行的統計資料物件也會儲存這些資料行之間值相互關聯的相關統計資料。 這些相互關聯統計資料 (或稱「密度」) 衍生自資料行值之相異資料列的數目。 如需統計資料物件的詳細資訊，請參閱 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)。  
  
 篩選的統計資料  
 對於從定義完善的資料子集中選取的查詢而言，篩選的統計資料可以改善查詢效能。 篩選的統計資料會使用篩選述詞來選取統計資料中所含的資料子集。 設計完善的篩選統計資料可以改善查詢執行計畫 (相較於完整資料表統計資料而言)。 如需篩選述詞的詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)。 如需有關何時建立篩選統計資料的詳細資訊，請參閱本主題的 [何時建立統計資料](#UpdateStatistics) 一節。 如需個案研究，請參閱 SQLCAT 網站的部落格文章 [配合分割資料表使用已篩選的統計資料](http://go.microsoft.com/fwlink/?LinkId=178505)。  
  
 統計資料選項  
 您可以設定三個選項來影響何時及如何建立和更新統計資料。 這些選項只會在資料庫層級設定。  
  
 AUTO_CREATE_STATISTICS 選項  
 開啟自動建立統計資料選項 AUTO_CREATE_STATISTICS 時，查詢最佳化工具就會視需要針對查詢述詞中的個別資料行建立統計資料，以便改善查詢計劃的基數估計值。 這些單一資料行統計資料是針對在現有統計資料物件中尚未具有長條圖的資料行建立的。 AUTO_CREATE_STATISTICS 選項不會判斷系統是否針對索引建立了統計資料。 這個選項也不會產生篩選的統計資料。 它會嚴格套用至完整資料表的單一資料行統計資料。  
  
 當查詢最佳化工具由於使用 AUTO_CREATE_STATISTICS 選項而產生統計資料時，統計資料名稱就會以 `_WA`為開頭。 您可以使用下列查詢來判斷查詢最佳化工具是否已經針對查詢述詞資料行建立了統計資料。  
  
```  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
 AUTO_UPDATE_STATISTICS 選項  
 開啟自動更新統計資料選項 AUTO_UPDATE_STATISTICS 時，查詢最佳化工具就會判斷統計資料可能過期的時間，然後在查詢使用統計資料時加以更新。 當插入、更新、刪除或合併作業變更資料表或索引檢視表中的資料分佈之後，統計資料就會變成過期。 查詢最佳化工具會計算自從上次更新統計資料以來資料修改的次數，並且比較修改次數與臨界值，藉以判斷統計資料可能過期的時間。 此臨界值是以資料表或索引檢視表中的資料列數目為基礎。  
  
-   SQL Server (2014年及更早版本) 會根據變更的資料列百分比使用臨界值。 與資料表中的資料列數無關。  
  
-   SQL Server (從 2016 開始、相容性層級130 下) 使用的臨界值會依據資料表中的資料列數進行調整。 透過這項變更，大型資料表上的統計資料會經常更新。  
  
 在編譯查詢之前以及執行快取查詢計劃之前，查詢最佳化工具會檢查是否有過期的統計資料。 在編譯查詢之前，查詢最佳化工具會使用查詢述詞中的資料行、資料表和索引檢視表來判斷哪些統計資料可能已過期。 在執行快取查詢計劃之前， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會確認查詢計劃是否參考最新的統計資料。  
  
 AUTO_UPDATE_STATISTICS 選項會套用至針對索引所建立的統計資料物件、查詢述詞中的單一資料行，以及使用 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 陳述式所建立的統計資料。 此外，這個選項也會套用至篩選的統計資料。  
  
 AUTO_UPDATE_STATISTICS_ASYNC  
 非同步統計資料更新選項 AUTO_UPDATE_STATISTICS_ASYNC 會決定查詢最佳化工具要使用同步或非同步統計資料更新。 根據預設，非同步統計資料更新選項處於關閉狀態，而且查詢最佳化工具會以同步方式更新統計資料。 AUTO_UPDATE_STATISTICS_ASYNC 選項會套用至針對索引所建立的統計資料物件、查詢述詞中的單一資料行，以及使用 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 陳述式所建立的統計資料。  
  
 統計資料更新可以是同步 (預設值) 或非同步。 使用同步統計資料更新時，查詢一律會使用最新的統計資料進行編譯和執行。如果統計資料已過期，查詢最佳化工具就會先等候更新的統計資料，然後再編譯並執行查詢。 使用非同步統計資料更新時，查詢就會使用現有的統計資料進行編譯，即使現有的統計資料已過期也一樣。如果查詢進行編譯時統計資料已過期，查詢最佳化工具可能會選擇次佳查詢計劃。 在非同步更新完成之後進行編譯的查詢將會從使用更新的統計資料中獲益。  
  
 當您執行變更資料分佈的作業時 (例如截斷資料表，或大量更新大部分的資料列)，請考慮使用同步統計資料。 如果您沒有在完成此作業之後更新統計資料，使用同步統計資料將可在針對變更的資料執行查詢之前，確保統計資料處於最新狀態。  
  
 在下列狀況中，請考慮使用非同步統計資料來達到更可預測的查詢回應時間：  
  
-   您的應用程式經常會執行相同的查詢、相似的查詢或相似的快取查詢計劃。 相較於使用同步統計資料更新而言，使用非同步統計資料更新可能會讓您的查詢回應時間更可預測，因為查詢最佳化工具不需要等候最新的統計資料，就可以執行傳入的查詢。 這樣會避免延遲某些查詢，但無法避免延遲其他查詢。  
  
-   您的應用程式遇到等候更新統計資料之一或多個查詢所造成的用戶端要求逾時。 在某些情況下，等候同步統計資料可能會造成具有彙總逾時的應用程式失敗。  
  
 累加統計資料  
 開啟 (ON) 時，所建立的統計資料是依據每個分割區區的統計資料。 關閉 (OFF) 時，會卸除統計資料樹狀結構，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會重新計算統計資料。 預設值為 OFF。 此設定會覆寫資料庫層級 INCREMENTAL 屬性。  
  
 當新的分割區區加入到大型資料表時，應更新統計資料，以包含新的分割區區。 但是掃描整個資料表 (FULLSCAN 或 SAMPLE 選項) 所需的時間可能會很長。 此外，由於可能只需要新分割區區的統計資料，所以不需要掃描整個資料表。 累加選項會以每個分割區區為基礎，建立及儲存統計資料，更新時只會重新整理需要新統計資料之分割區區的統計資料。  
  
 如果不支援每個分割區區的統計資料，則會忽略該選項，並產生警告。 針對下列統計資料類型，不支援累加統計資料：  
  
-   建立統計資料時，所使用的索引未與基底資料表進行分割區對齊。  
  
-   在 AlwaysOn 可讀取次要資料庫上建立的統計資料。  
  
-   在唯讀資料庫上建立的統計資料。  
  
-   在篩選的索引上建立的統計資料。  
  
-   在檢視上建立的統計資料。  
  
-   在內部資料表上建立的統計資料。  
  
-   使用空間索引或 XML 索引建立的統計資料。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
  
##  <a name="CreateStatistics"></a> 何時建立統計資料  
 查詢最佳化工具已經用下列方式建立統計資料：  
  
1.  建立索引時，查詢最佳化工具就會針對資料表或檢視表的索引建立統計資料。 這些統計資料是針對索引的索引鍵資料行所建立的。 如果索引是篩選的索引，查詢最佳化工具就會在針對篩選索引所指定的相同資料列子集上建立篩選的統計資料。 如需篩選索引的詳細資訊，請參閱[建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)和 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
2.  開啟 AUTO_CREATE_STATISTICS 時，查詢最佳化工具會針對查詢述詞中的單一資料行建立統計資料。  
  
 對於大部分查詢而言，這兩種建立統計資料的方法可確保高品質的查詢計劃。不過，在少數情況下，您可以使用 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 陳述式來建立其他統計資料，以便改善查詢計劃。 這些額外的統計資料可以擷取查詢最佳化工具在建立索引或單一資料行的統計資料時無法解釋的統計相互關聯。 您的應用程式可能會在資料表資料中具有其他統計相互關聯，而且如果它們計算成統計資料物件，就可讓查詢最佳化工具改善查詢計劃。 例如，資料列子集的篩選統計資料或查詢述詞資料行的多重資料行統計資料可能會改善查詢計劃。  
  
 使用 CREATE STATISTICS 陳述式來建立統計資料時，我們建議您將 AUTO_CREATE_STATISTICS 選項保持開啟狀態，讓查詢最佳化工具能夠繼續例行地針對查詢述詞資料行建立單一資料行統計資料。 如需查詢述詞的詳細資訊，請參閱[搜尋條件 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)。  
  
 當下列任何情況適用時，請考慮使用 CREATE STATISTICS 陳述式來建立統計資料：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 建議您建立統計資料。  
  
-   查詢述詞包含多個尚未存在相同索引中的相互關聯資料行。  
  
-   查詢會從資料子集中選取。  
  
-   查詢具有遺失的統計資料。  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>查詢述詞包含多個相互關聯的資料行  
 當查詢述詞包含多個具有跨資料行關聯性與相依性的資料行時，多個資料行的統計資料可能會改善查詢計劃。 多個資料行的統計資料包含跨資料行相互關聯統計資料 (稱為「密度」，而且這些統計資料不會在單一資料行統計資料中提供。 當查詢結果相依於多個資料行之間的資料關聯性時，密度可以改善基數估計值。  
  
 如果資料行已經存在相同的索引中，就表示多重資料行統計資料物件已經存在，而且您不需要手動建立此物件。 如果資料行尚未存在相同的索引中，您可以針對資料行建立索引或使用 CREATE STATISTICS 陳述式，藉以建立多重資料行統計資料。 相較於統計資料物件而言，這種統計資料需要更多系統資源來維護索引。 如果應用程式不需要多重資料行索引，您就可以建立統計資料物件而不建立索引，藉以節省系統資源。  
  
 建立多重資料行統計資料時，統計資料物件定義中的資料行順序會影響建立基數估計值之密度的有效性。 統計資料物件會將索引鍵資料行之每個前置詞的密度儲存在統計資料物件定義中。 如需密度的詳細資訊，請參閱 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)。  
  
 若要建立對於基數估計值有用的密度，查詢述詞中的資料行必須與統計資料物件定義的其中一個資料行前置詞相符。 例如，下列命令會針對 `LastName`、 `MiddleName`和 `FirstName`資料行建立多重資料行統計資料物件。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
 在這則範例中，統計資料物件 `LastFirst` 具有下列資料行前置詞的密度：(`LastName`)、(`LastName, MiddleName`) 和 (`LastName, MiddleName, FirstName`)。 此密度不適用於 (`LastName, FirstName`)。 如果查詢使用 `LastName` 和 `FirstName` 而不使用 `MiddleName`，此密度就不適用於基數估計值。  
  
### <a name="query-selects-from-a-subset-of-data"></a>查詢會從資料子集中選取  
 當查詢最佳化工具針對單一資料行和索引建立統計資料時，它就會針對所有資料列中的值建立統計資料。 當查詢從資料列的子集中選取，而且該資料列子集具有唯一的資料分佈時，篩選的統計資料就可以改善查詢計劃。 您可以使用 CREATE STATISTICS 陳述式搭配 WHERE 子句來定義篩選述詞運算式，藉此建立篩選統計資料。  
  
 例如，在使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]時，Production.Product 資料表中的每個產品都屬於 Production.ProductCategory 資料表中的四個類別之一：Bikes、Components、Clothing 及 Accessories。 其中每個類別目錄都具有不同的重量資料分佈：腳踏車 (Bikes) 的重量範圍是從 13.77 到 30.0、元件 (Components) 的重量範圍是從 2.12 到 1050.00 且有些是 NULL 值、衣服 (Clothing) 的重量全部為 NULL，配件 (Accessories) 的重量也是 NULL。  
  
 以 Bikes 為例，相較於 Weight 資料行的完整資料表統計資料或不存在的統計資料而言，所有腳踏車重量的篩選統計資料將提供更精確的統計資料給查詢最佳化工具，而且可以改善查詢計畫品質。 雖然腳踏車重量資料行適合做為篩選的統計資料，但是不一定適合做為篩選的索引 (如果重量查閱的數目相當小的話)。 篩選索引為查閱所提供的效能提升程度可能不會超過將篩選索引加入至資料庫的額外維護和儲存成本。  
  
 下列陳述式會針對 Bikes 的所有子類別目錄建立 `BikeWeights` 篩選統計資料。 篩選述詞運算式會使用比較 `Production.ProductSubcategoryID IN (1,2,3)`來列舉所有腳踏車子類別目錄，藉以定義腳踏車。 此述詞無法使用 Bikes 類別目錄，因為它儲存在 Production.ProductCategory 資料表中，而且篩選運算式的所有資料行都必須位於相同的資料表中。  
  
 [!code-sql[StatisticsDDL#FilteredStats2](../../relational-databases/statistics/codesnippet/tsql/statistics_1.sql)]  
  
 查詢最佳化工具可以使用 `BikeWeights` 篩選統計資料來改善下列查詢的查詢計劃 (此查詢會選取所有重量超過 `25`的腳踏車)。  
  
```  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>查詢會識別遺失的統計資料  
 如果錯誤或其他事件讓查詢最佳化工具無法建立統計資料，查詢最佳化工具會建立查詢計劃，但不使用統計資料。 查詢最佳化工具會將統計資料標示為遺失，並且嘗試在下一次執行查詢時重新產生統計資料。  
  
 當查詢的執行計畫是利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]以圖形顯示時，遺失的統計資料就會表示成警告 (資料表名稱為紅色)。 此外，使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來監視 **Missing Column Statistics** 事件類別會指出統計資料遺失的時間。 如需詳細資訊，請參閱[錯誤和警告事件類別目錄 &#40;Database Engine&#41;](../../relational-databases/event-classes/errors-and-warnings-event-category-database-engine.md)。  
  
 如果統計資料已遺失，請執行下列步驟：  
  
-   確認已開啟 AUTO_CREATE_STATISTICS 和 AUTO_UPDATE_STATISTICS。  
  
-   確認資料庫不是唯讀的。 如果資料庫是唯讀的，查詢最佳化工具就無法儲存統計資料。  
  
-   使用 CREATE STATISTICS 陳述式來建立遺失的統計資料。  
  
 如果唯讀資料庫或唯讀快照集上的統計資料遺漏或過時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會在 **tempdb**中建立及維護暫時性統計資料。 當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 建立暫時統計資料時，統計資料名稱會附加後置詞 _readonly_database_statistic，以便區分暫時統計資料與永久統計資料。 後置詞 _readonly_database_statistic 會保留給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生的統計資料使用。 暫時統計資料的指令碼可以在讀寫資料庫上建立和複製。 當編寫指令碼時， [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會將統計資料名稱的後置詞從 _readonly_database_statistic 變更為 _readonly_database_statistic_scripted。  
  
 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以建立和更新暫時統計資料。 但是，您可以使用永久統計資料所使用的相同工具來刪除暫時統計資料及監控統計資料屬性：  
  
-   使用 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md) 陳述式所建立的統計資料。  
  
-   使用 **sys.stats** 和 **sys.stats_columns** 目錄檢視監控統計資料。 **sys_stats** 包含 **is_temporary** 資料行，以指示哪些統計資料為永久性及哪些統計資料為暫時性。  
  
 因為暫時統計資料會儲存在 **tempdb**中，所以重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務會導致所有暫時統計資料消失。  
  
  
##  <a name="UpdateStatistics"></a> 何時更新統計資料  
 查詢最佳化工具會判斷統計資料可能過期的時間，然後在查詢計劃需要它們時進行更新。 在某些情況下，您可以讓統計資料的更新頻率高於 AUTO_UPDATE_STATISTICS 開啟時的更新頻率，藉以改善查詢計劃，因而改善查詢效能。 您可以使用 UPDATE STATISTICS 陳述式或 sp_updatestats 預存程序來更新統計資料。  
  
 更新統計資料可確保查詢使用最新的統計資料進行編譯。 不過，更新統計資料會導致查詢重新編譯。 我們建議您不要太頻繁地更新統計資料，因為改善查詢計劃與重新編譯查詢所花費的時間之間具有效能權衡取捨。 特定的權衡取捨完全取決於您的應用程式。  
  
 使用 UPDATE STATISTICS 或 sp_updatestats 來更新統計資料時，我們建議您將 AUTO_UPDATE_STATISTICS 保持設定為 ON，讓查詢最佳化工具能夠繼續例行地更新統計資料。 如需如何針對資料行、索引、資料表或索引檢視表更新統計資料的詳細資訊，請參閱 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)。 如需如何針對資料庫中所有使用者定義和內部資料表更新統計資料的詳細資訊，請參閱預存程序 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)。  
  
 若要判斷上次更新統計資料的時間，請使用 [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 函數。  
  
 在下列狀況中，請考慮更新統計資料：  
  
-   查詢執行時間很慢。  
  
-   插入作業針對遞增或遞減索引鍵資料行進行。  
  
-   在維護作業之後。  
  
### <a name="query-execution-times-are-slow"></a>查詢執行時間很慢  
 如果查詢回應時間很慢或無法預測，請先確定查詢具有最新的統計資料，然後再執行其他疑難排解步驟。  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>插入作業針對遞增或遞減索引鍵資料行進行  
 遞增或遞減索引鍵資料行 (例如 IDENTITY 或即時時間戳記資料行) 之統計資料所需的統計資料更新頻率可能會比查詢最佳化工具所執行的更新頻率更高。 插入作業會將新的值附加至遞增或遞減資料行。 所加入的資料列數目可能會太小，而無法觸發統計資料更新。 如果統計資料不是最新的，而且查詢會從最近加入的資料列中選取，則目前的統計資料將不會具有這些新值的基數估計值。 這可能會導致基數估計值不精確以及查詢效能緩慢。  
  
 例如，如果統計資料沒有更新成包含最新銷售訂單日期的基數估計值，則從最新銷售訂單日期中選取的查詢就會具有不精確的基數估計值。  
  
### <a name="after-maintenance-operations"></a>在維護作業之後  
 在執行變更資料分佈的維護程序 (例如截斷資料表或針對大部分的資料列執行大量插入) 之後，請考慮更新統計資料。 這樣做可在查詢等候自動統計資料更新時，避免未來查詢處理產生延遲。  
  
 重建、重組或重新組織索引等作業都不會變更資料的分佈。 因此，在執行 ALTER INDEX REBUILD、DBCC REINDEX、DBCC INDEXDEFRAG 或 ALTER INDEX REORGANIZE 作業之後，您不需要更新統計資料。 當您使用 ALTER INDEX REBUILD 或 DBCC DBREINDEX 來重建資料表或檢視表的索引時，查詢最佳化工具就會更新統計資料。不過，這種統計資料更新是重新建立索引的副產品。 在 DBCC INDEXDEFRAG 或 ALTER INDEX REORGANIZE 作業之後，查詢最佳化工具則不會更新統計資料。  
  
  
##  <a name="DesignStatistics"></a> 有效使用統計資料的查詢  
 某些查詢實作 (例如查詢述詞中的區域變數和複雜運算式) 可能會導致次佳的查詢計劃。 不過，遵循查詢設計指導方針來有效使用統計資料有助於避免這種情況發生。 如需查詢述詞的詳細資訊，請參閱[搜尋條件 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)。  
  
 您可以套用有效使用統計資料的查詢設計指導方針來改善查詢述詞中使用之運算式、變數和函數的「基數估計值」，藉以改善查詢計劃。 當查詢最佳化工具不知道運算式、變數或函數的值時，它就不知道要在長條圖中查閱哪個值，因此無法從長條圖中擷取最佳的基數估計值。 此時，查詢最佳化工具會改為以長條圖中所有取樣資料列之每個相異值的平均資料列數目做為基數估計值的基礎。 這樣會導致次佳的基數估計值，而且可能會損及查詢效能。  
  
 下列指導方針描述的是如何撰寫查詢，以便透過改善基數估計值，改善查詢計劃。  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>改善運算式的基數估計值  
 若要改善運算式的基數估計值，請遵循下列指導方針：  
  
-   您應該盡可能簡化含有常數的運算式。 在判斷基數估計值之前，查詢最佳化工具不會評估包含常數的所有函數和運算式。 例如，請簡化運算式 ABS(`-100) to 100`。  
  
-   如果運算式使用多個變數，請考慮建立運算式的計算資料行，然後再針對計算資料行建立統計資料或索引。 例如，如果您建立了 `WHERE PRICE + Tax > 100` 運算式的計算資料行， `Price + Tax`查詢述詞可能會具有較佳的基數估計值。  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>改善變數和函數的基數估計值  
 若要改善變數和函數的基數估計值，請遵循下列指導方針：  
  
-   如果查詢述詞使用區域變數，請考慮將查詢重新撰寫成使用參數而非區域變數。 當查詢最佳化工具建立查詢執行計畫時，無法得知區域變數的值。 當查詢使用參數時，查詢最佳化工具就會使用傳遞給預存程序之第一個實際參數值的基數估計值。  
  
-   請考慮使用標準資料表或暫存資料表來保存多重陳述式資料表值函式的結果。 查詢最佳化工具不會針對多重陳述式資料表值函式建立統計資料。 透過這種方法，查詢最佳化工具就可以建立資料表資料行的統計資料，然後使用它們來建立較佳的查詢計劃。  
  
-   請考慮使用標準資料表或暫存資料表當做資料表變數的取代項目。 查詢最佳化工具不會針對資料表變數建立統計資料。 透過這種方法，查詢最佳化工具就可以建立資料表資料行的統計資料，然後使用它們來建立較佳的查詢計劃。 當您在判斷要使用暫存資料表或資料表變數時，存在權衡取捨。在預存程序中使用的資料表變數會讓預存程序重新編譯的次數比暫存資料表更少。 根據應用程式而定，使用暫存資料表來取代資料表變數可能不會改善效能。  
  
-   如果預存程序包含使用傳入參數的查詢，請避免在查詢中使用之前，變更預存程序中的參數值。 查詢的基數估計值是以傳入參數而非更新的值為基礎。 若要避免變更參數值，您可以將查詢重新撰寫成使用兩個預存程序。  
  
     例如，當 `Sales.GetRecentSales` 時，下列預存程序 `@date` 就會變更 `@date is NULL`參數的值。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     如果預存程序 `Sales.GetRecentSales` 的第一次呼叫傳遞 NULL 給 `@date` 參數，查詢最佳化工具就會使用 `@date = NULL` 的基數估計值來編譯此預存程序，即使沒有使用 `@date = NULL`來呼叫查詢述詞也一樣。 這個基數估計值可能會與實際查詢結果中的資料列數目具有大幅差異。 因此，查詢最佳化工具可能會選擇次佳查詢計劃。 為了協助避免這種情況發生，您可以將此預存程序重新撰寫成兩個程序，如下所示：  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>使用查詢提示來改善基數估計值  
 若要改善區域變數的基數估計值，您可以使用 OPTIMIZE FOR 或 OPTIMIZE FOR UNKNOWN 查詢提示搭配 RECOMPILE。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  
  
 對於某些應用程式而言，每次執行查詢都重新編譯查詢可能會花費太多時間。 即使您沒有使用 RECOMPILE 選項，OPTIMIZER FOR 查詢提示仍然有所幫助。 例如，您可以將 OPTIMIZER FOR 選項加入至預存程序 Sales.GetRecentSales，以便指定特定日期。 下列範例會將 OPTIMIZE FOR 選項加入至 Sales.GetRecentSales 程序。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>使用計畫指南來改善基數估計值  
 對於某些應用程式而言，查詢設計指導方針可能不適用，因為您無法變更查詢或者使用 RECOMPILE 查詢提示可能會導致重新編譯次數太多。 此時，您可以使用計畫指南來指定其他提示 (例如 USE PLAN)，以便控制查詢的行為，同時向應用程式廠商調查應用程式變更。 如需有關計畫指南的詳細資訊，請參閱 [計畫指南](../../relational-databases/performance/plan-guides.md)。  
  
  
## <a name="see-also"></a>另請參閱  
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)  
  
  

