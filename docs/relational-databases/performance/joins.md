---
title: 聯結 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- HASH join
- NESTED LOOPS join
- MERGE join
- ADAPTIVE join
- joins [SQL Server], about joins
- join hints [SQL Server]
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f4b2bd
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8808dc2befdcb2c31218e7dc155921bb10947e14
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287472"
---
# <a name="joins-sql-server"></a>聯結 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用記憶體內排序和雜湊聯結技術，來執行排序、交叉、聯集及差異作業。 使用這類查詢計畫，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可支援資料表垂直分割 (有時候稱為分欄儲存)。   

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 採用四種聯結作業：    
-   巢狀迴圈聯結     
-   合併聯結   
-   雜湊聯結   
-   自適性聯結 (開頭為 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)])

## <a name="join-fundamentals"></a><a name="fundamentals"></a> 聯結基本概念
透過使用聯結，您可以根據資料表之間的邏輯關聯性從二或多個資料表中擷取資料。 聯結指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何使用一個資料表的資料，以選取另一個資料表的資料列。    

聯結條件定義兩個資料表在查詢中相關的方式：    
-   指定每個資料表中要用於聯結的資料行。 典型的聯結條件會指定一個資料表的外部索引鍵，以及其在另一個資料表關聯的索引鍵。    
-   指定邏輯運算子 (例如 = 或 <>)，以便用來比較資料行的數值。    

您可以在 `FROM` 或 `WHERE` 子句中指定內部聯結。 外部聯結則只能在 `FROM` 字句中指定。 聯結條件會與 `WHERE` 和 `HAVING` 搜尋條件結合，以控制從 `FROM` 子句所參考之基底資料表中選取的資料列。    

在 `FROM` 子句中指定聯結條件有助於將它們與 `WHERE` 子句中可能指定的任何其他搜尋條件分開，建議您以此方式指定聯結。 簡化的 ISO FROM 子句聯結語法為：

```
FROM first_table join_type second_table [ON (join_condition)]
```

*join_type* 會指定所執行聯結的種類：內部、外部或交叉聯結。 *join_condition* 會定義要針對每一對聯結資料列評估的述詞。 下列是 FROM 子句聯結規格的範例：

```sql
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
     ON (ProductVendor.BusinessEntityID = Vendor.BusinessEntityID)
```

下列範例則是使用此聯結的簡單 SELECT 陳述式：

```sql
SELECT ProductID, Purchasing.Vendor.BusinessEntityID, Name
FROM Purchasing.ProductVendor JOIN Purchasing.Vendor
    ON (Purchasing.ProductVendor.BusinessEntityID = Purchasing.Vendor.BusinessEntityID)
WHERE StandardPrice > $10
  AND Name LIKE N'F%'
GO
```

此選取將傳回公司名稱以字母 F 開頭之公司所供應的零件，並且產品的價格大於 $10 之任何組合的產品與供應商資訊。   

若在單一查詢中參考多個資料表，所有的資料行參考都不可以模擬兩可。 在先前的範例中，ProductVendor 和 Vendor 資料表都有名稱為 BusinessEntityID 的資料行。 查詢所參考的二或多個資料表中，若有任何資料行名稱重複，則必須以資料表名稱來加以限定。 在範例中，所有對 Vendor 資料行的參考都有加以限定。   

當查詢所使用的二或多個資料表中，資料行名稱都沒有重複，對資料行的參考就不需要以資料表名稱加以限定。 如先前的範例所示。 這樣的 SELECT 陳述式有時候很難了解，因為無法指出提供每個資料行的資料表。 如果以資料表名稱限定所有資料行，可增進查詢的可讀性。 如果還使用資料表別名，特別是當資料表名稱本身還需要以資料庫和擁有者名稱加以限定時，可進一步增進可讀性。 下列是相同的範例，但是指定了資料表別名，並且以資料表別名限定資料行，以增進可讀性：

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv 
JOIN Purchasing.Vendor AS v
    ON (pv.BusinessEntityID = v.BusinessEntityID)
WHERE StandardPrice > $10
    AND Name LIKE N'F%';
```

上個範例在 FROM 子句中指定聯結條件，這是較好的方式。 下列查詢包含指定於 WHERE 子句中的相同聯結條件：

```sql
SELECT pv.ProductID, v.BusinessEntityID, v.Name
FROM Purchasing.ProductVendor AS pv, Purchasing.Vendor AS v
WHERE pv.BusinessEntityID=v.BusinessEntityID
    AND StandardPrice > $10
    AND Name LIKE N'F%';
```

聯結的選取清單可參考聯結資料表中的所有資料行，或是資料行的任何子集。 若要包含聯結中每個資料表的資料行，您並不需要用到選取清單。 例如，在三個資料表的聯結中，一個資料表可作為第二個資料表與第三個資料表的橋樑，並且中間的資料表不需要有任何資料行參考於選取清單中。   

雖然聯結條件通常擁有相等比較 (=)，您也可以指定其他的比較或關聯式運算子，就如同其他述詞一樣。 如需詳細資訊，請參閱[比較運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) 和 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)。  

當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理聯結時，查詢引擎將從多種可能性選擇最有效率的處理聯結方式。 不同聯結的實際執行可能會使用許多不同的最佳化方式，因此無法可靠地預測。   

用於聯結條件的資料行，並不需要擁有相同的名稱或相同的資料類型。 不過，如果資料類型不一致，則必須是相容的類型，或是 SQL 可用隱含方式轉換的類型。 若無法以隱含方式轉換資料類型，聯結條件就必須使用 `CAST` 函數來明確轉換資料類型。 如需有關隱含及明確轉換的詳細資訊，請參閱[資料類型轉換 &#40;資料庫引擎&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)。    

大多數使用聯結的查詢都可使用子查詢重新改寫 (查詢巢狀於另一個查詢之內)，而大多數的子查詢也可重新改寫成聯結。 如需有關子查詢的詳細資訊，請參閱[子查詢](../../relational-databases/performance/subqueries.md)。   

> [!NOTE]
> 您無法直接在 ntext、text 或 image 資料行上聯結資料表。 不過，可以藉由使用 `SUBSTRING`，以間接方式在 ntext、text 或 image 資料行上聯結資料表。    
> 例如，`SELECT * FROM t1 JOIN t2 ON SUBSTRING(t1.textcolumn, 1, 20) = SUBSTRING(t2.textcolumn, 1, 20)` 會對資料表 t1 和 t2 中每個 text 資料行的前 20 個字元執行兩個資料表的內部聯結。   
> 此外，另一個比較兩個資料表之 ntext 或 text 資料行的可能方式，就是使用 `WHERE` 子句來比較資料行的長度，例如：`WHERE DATALENGTH(p1.pr_info) = DATALENGTH(p2.pr_info)`

## <a name="understanding-nested-loops-joins"></a><a name="nested_loops"></a> 認識巢狀迴圈聯結
如果一個聯結輸入相當小 (少於 10 個資料列)，但另一個聯結輸入相當大而且在聯結資料行建有索引的話，索引巢狀迴圈是最快速的聯結作業，因為它們需要的 I/O 最少，需要的比較也最少。 

巢狀迴圈聯結 (也稱為「巢狀反覆運算」  ) 會使用一個聯結輸入作為外部輸入資料表 (在圖形化執行計劃中顯示為上方輸入)，另一個聯結作為內部 (下方) 輸入資料表。 外部迴圈會逐列消耗外部輸入資料表。 內部迴圈 (針對外部每一列各執行一次) 會在內部輸入資料表中搜尋符合的資料列。   

在最簡單的情況下，搜尋會掃描整個資料表或索引；這稱為「單純巢狀迴圈聯結」  。 如果搜尋會利用索引，就稱為「索引巢狀迴圈聯結」  。 如果索引是隨著查詢計劃一起建立 (並且在查詢完成時終結)，則稱為「暫存索引巢狀迴圈聯結」  。 「查詢最佳化工具」會將所有這些變化都列入考慮。   

如果外部輸入相當小，內部輸入已預先建立索引而且很大的話，巢狀迴圈聯結會特別有效率。 在許多小型交易中 (如只影響一小組資料列的交易)，索引巢狀迴圈聯結比合併聯結與雜湊聯結要好得多。 然而在大型查詢中，巢狀迴圈聯結多半不是最佳選擇。    

當巢狀迴圈聯結運算子的 OPTIMIZED 屬性設定為 **True** 時，代表會在內部資料表過大時使用巢狀迴圈聯結 (或稱批次排序) 來將 I/O 最小化，而不論資料表平行與否。 因為排序本身是隱藏作業，所以在分析執行計劃時，此最佳化在指定計劃內可能不會很明顯。 但如果仔細在計劃 XML 中尋找屬性 OPTIMIZED 的話，能看出來巢狀迴圈聯結可能在嘗試重新排序輸入資料列來改善 I/O 效能。

## <a name="understanding-merge-joins"></a><a name="merge"></a> 認識合併聯結
如果兩個聯結輸入都不小，而且依聯結資料行排序 (例如，是由掃描排序的索引所取得) 的話，合併聯結就是最快速的聯結作業。 如果兩個聯結輸入都相當大，而且兩個輸入的大小類似，先行排序再進行的合併聯結所提供的效能大致類似雜湊聯結。 然而，如果兩個輸入的大小差異極大的話，雜湊聯結作業多半快得多。       

合併聯結需要在合併資料行上將兩項輸入都加以排序，這是由聯結述詞的相等 (ON) 子句來定義的。 查詢最佳化工具通常會掃描索引 (如果適當的資料行集合建有索引的話)，或在合併聯結下放置排序運算子。 在極少的情況下，可以有多個相等子句，但只會從部份可用的相等子句中取得合併資料行。    

因為每個輸入都會經過排序，所以**合併聯結**運算子會從每個輸入各取得一列資料列，然後加以比較。 例如，對於內部聯結作業，會傳回是否相等的資料列。 如果不相等，就丟棄數值較小的資料列，再從該輸入取得另一個資料列。 這個處理程序會一再重複，直到處理過所有資料列為止。    

合併聯結作業可能是一般的，也可能是多對多的作業。 多對多合併聯結會使用暫存資料表來儲存資料列。 如果每個輸入有重複的值，在處理其他輸入的每個重複項時，必須將輸入之一倒回重複項的開始。    

如果出現殘餘述詞的話，滿足合併述詞的所有資料列都會計算殘餘述詞，只有滿足的資料列才會傳回。   

合併聯結本身非常快，但如果需要排序作業的話，有時候代價會很高。 但如果資料量很大，而且可以從現有的 B-tree 索引取得已排序的預期資料，那麼合併聯結往往是可用的最快速聯結演算法。    

## <a name="understanding-hash-joins"></a><a name="hash"></a> 認識雜湊聯結
雜湊聯結可以有效率地處理大型、未排序、無索引的輸入。 它們在做為複雜查詢的中繼結果方面很有用，因為：
-   中繼結果沒有索引 (除非明確地儲存到磁碟，然後建立索引)，而且通常產生時也不會做適當的排序供查詢計畫的下一個作業使用。
-   查詢最佳化工具只估計中繼結果的大小。 因為複雜查詢的估計值可能非常不準確，所以處理中繼結果的演算法不僅必須要有效率，而且萬一中繼結果顯著大於預期時，它的效能還不得惡化得太明顯。   

雜湊聯結允許少使用反正規化。 反正規化一般是利用減少聯結作業，來達成較佳的效能，但它會有備援性的危險，例如不一致的更新。 雜湊聯結降低了反正規化的需要。 雜湊聯結讓垂直分割 (以不同的檔案或索引來呈現一個資料表中的資料行群組) 可以成為實體資料庫設計可實行的選項。     

雜湊聯結有兩個輸入：**建置**輸入與**探查**輸入。 查詢最佳化工具會指派這些角色，使兩個輸入中比較小的一個做為建置輸入。    

雜湊聯結用於許多種集合比對作業：內部聯結；左方、右方與完整外部聯結；左方、右方半聯結；交集；聯合；與差異。 此外，雜湊聯結的變體還可以執行移除重複項及進行群組的作業，例如 `SUM(salary) GROUP BY department`。 這些修改方式只使用一個輸入，兼做組建與探查角色。   

下列章節描述不同類型的雜湊聯結：In-Memory 雜湊聯結、寬限雜湊聯結和遞迴雜湊聯結。    

### <a name="in-memory-hash-join"></a><a name="inmem_hash"></a> In-Memory 雜湊聯結
雜湊聯結會先掃描或計算整個建置輸入，然後在記憶體中建立雜湊表。 根據以雜湊鍵計算所得的雜湊值，將每一列插入雜湊桶中。 如果整個建置輸入小於可用記憶體，就可以將所有資料列都插入雜湊表。 這個組建階段後跟著探查階段。 這時候會以逐列方式掃描或計算整個探查輸入，針對每個探查列計算雜湊鍵值、掃描對應的雜湊桶，並產生符合項目。    

### <a name="grace-hash-join"></a><a name="grace_hash"></a> 寬限雜湊聯結
如果記憶體放不下建置輸入，就會以幾個步驟進行雜湊聯結。 這就是所謂的寬限雜湊聯結。 每個步驟分別有組建階段與探查階段。 最開始，會消耗整個組建與探查輸入，並分割 (對雜湊鍵使用雜湊函數) 成多個檔案。 對雜湊鍵使用雜湊函數會保證任何兩個聯結資料錄一定在同一對檔案中。 因此，本來是聯結兩個大型輸入的工作，變成是做好幾個相同的工作，但每個工作都變得比較小。 然後再對每對分割檔案套用雜湊聯結。    

### <a name="recursive-hash-join"></a><a name="recursive_hash"></a> 遞迴雜湊聯結
如果建置輸入太大，使得標準外部聯結排序的輸入需要多個合併層級，就需要多個分割步驟與多個分割層級。 如果只有一些分割很大，就僅對這部分使用額外的分割步驟。 為了使所有分割步驟都盡可能達到最快的速度，所以使用大型的非同步 I/O 作業，使單一執行緒可以讓多部磁碟機保持忙碌。    

> [!NOTE]
> 如果建置輸入只比可用記憶體稍微大一點，就會將 In-memory 雜湊聯結和寬限雜湊聯結的元素合併到單一步驟中，而產生混合型雜湊聯結。   

在最佳化期間不一定能夠判斷要使用哪一個雜湊聯結。 因此，SQL Server 會先從使用 In-Memory 雜湊聯結開始，然後再依據建置輸入的大小，逐漸轉換成寬限雜湊聯結和遞迴雜湊聯結。    

如果「查詢最佳化工具」誤判兩個輸入中哪個較小，因而選錯建置輸入，則建置和探查角色會動態地顛倒。 雜湊聯結會確定使用溢位較小的檔案做為建置輸入。 這項技術稱為角色反轉。 當至少有一個雜湊聯結蔓延至磁碟之後，角色反轉就會在雜湊聯結內發生。     

> [!NOTE]
> 角色反轉的發生與任何查詢提示或結構無關。 角色反轉不會顯示在查詢計畫中；當它發生時，使用者就會看到。

### <a name="hash-bailout"></a><a name="hash_bailout"></a> 雜湊釋出
雜湊釋出一詞有時候是用來描述寬限雜湊聯結或遞迴雜湊聯結。    

> [!NOTE]
> 遞迴雜湊聯結或 Hash Bailout 會導致伺服器的效能降低。 如果您在追蹤內看到許多 「雜湊警告」事件，請在要聯結的資料行上更新統計資料。    

如需有關雜湊釋出的詳細資訊，請參閱[雜湊警告事件類別](../../relational-databases/event-classes/hash-warning-event-class.md)。    

## <a name="understanding-adaptive-joins"></a><a name="adaptive"></a> 了解自適性聯結
[批次模式](../../relational-databases/query-processing-architecture-guide.md#batch-mode-execution)自適性聯結可讓選擇的[雜湊聯結](#hash)或[巢狀迴圈](#nested_loops)聯結方法，延後到已掃描的第一個輸入**之後**。 自適性聯結運算子定義的閾值是用於決定何時要切換至巢狀迴圈計劃。 因此，查詢計劃可在執行期間動態切換至較佳的聯結策略，而不需經過重新編譯。 

> [!TIP]
> 經常在小型和大型聯結輸入掃描間變動的工作負載，由此功能獲益最大。

執行階段決策以下列步驟為基礎：
-  如果組建聯結輸入的資料列計數小到巢狀迴圈聯結會比雜湊聯結更佳的情況，則計劃就會切換成巢狀迴圈演算法。
-  如果組建聯結輸入超過特定的資料列計數閾值，則不會切換，且您的計劃會繼續執行雜湊聯結。

下列查詢用來說明自適性聯結範例：

```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 360;
```

此查詢會傳回 336 個資料列。 透過啟用[即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)，會顯示下列計劃：

![查詢結果 336 個資料列](../../relational-databases/performance/media/4_AQPStats336Rows.png)

在計劃中，請注意：
1. 使用了資料行存放區索引掃描，為雜湊聯結建置階段提供資料列。
2. 新的自適性聯結運算子。 此運算子定義的閾值是用於決定何時要切換至巢狀迴圈計劃。 本例中的閾值是 78 個資料列。 凡是 &gt;= 78 個資料列的計劃都會使用雜湊聯結。 如果小於該閾值，則會使用巢狀迴圈聯結。
3. 因為查詢傳回 336 個資料列 (超過閾值)，所以第二個分支會表示標準雜湊聯結作業的探查階段。 請注意，即時查詢統計資料會顯示流經運算子的資料列，本例中為 "672 of 672"。
4. 而最後一個分支是叢集索引搜尋，供未超過閾值的巢狀迴圈聯結所使用。 請注意，我們看到的顯示是"0 of 336" 資料列 (分支未使用)。

現在對比使用相同查詢的計劃，但當 *Quantity* 值在資料表中只有一個資料列時：
 
```sql
SELECT [fo].[Order Key], [si].[Lead Time Days], [fo].[Quantity]
FROM [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE [fo].[Quantity] = 361;
```
查詢會傳回一個資料列。 啟用即時查詢統計資料會顯示下列計劃：

![查詢結果一個資料列](../../relational-databases/performance/media/5_AQPStatsOneRow.png)

在計劃中，請注意：
- 因為傳回一個資料列，現在叢集索引搜尋中有資料列通過。
- 而且，因為雜湊聯結建置階段並未繼續，所以不會有任何資料列通過第二個分支。

### <a name="adaptive-join-remarks"></a>自適性聯結備註
自調性聯結導入的記憶體需求，會比索引巢狀的迴圈聯結相等計劃更高。 系統會以巢狀迴圈有如雜湊聯結一般的方式要求額外的記憶體。 在時快時慢作業的建置階段與巢狀迴圈資料流相等聯結的比較中，會另外產生額外負荷。 加上額外的成本，隨組建輸入資料列計數浮動的案例而變動。

批次模式自適性聯結適合初次執行的陳述式使用，而且一旦編譯，連續執行仍會根據編譯的自適性聯結閾值和流經外部輸入建置階段的執行階段資料列聯結自動調整。

如果自適性聯結切換成巢狀迴圈作業，便會使用已由雜湊聯結組建讀取的資料列。 運算子「不會」  再次重新讀取外部參考資料列。

### <a name="tracking-adaptive-join-activity"></a>追蹤自適性聯結活動
自適性聯結運算子有下列計劃運算子屬性：

|計劃屬性|描述|
|---|---|
|AdaptiveThresholdRows|顯示從雜湊聯結切換至巢狀迴圈聯結所使用的閾值。|
|EstimatedJoinType|可能的聯結類型。|
|ActualJoinType|在實際的計劃中，顯示根據閾值最後選擇的聯結演算法。|

評估計劃會顯示自適性聯結計劃圖形，以及定義的自適性聯結閾值和預估的聯結類型。

> [!TIP]
> 查詢存放區擷取並可強制執行批次模式自適性聯結計劃。

### <a name="adaptive-join-eligible-statements"></a>符合自適性聯結的陳述式
讓邏輯聯結符合批次模式自適性聯結有幾個條件：
- 資料庫相容性層級為 140 以上。
- 查詢是 `SELECT` 陳述式 (資料修改陳述式目前不適合)。
- 聯結能夠由索引巢狀迴圈聯結或雜湊聯結實體演算法執行。
- 雜湊聯結使用[批次模式](../../relational-databases/query-processing-architecture-guide.md#batch-mode-execution)，不論是透過存在於整體查詢中的資料行存放區索引，或是由聯結直接參考的資料行存放區索引資料表。
- 產生的巢狀迴圈聯結和雜湊聯結替代解決方案應該有相同的第一個子系 (外部參考)。

### <a name="adaptive-threshold-rows"></a>自適性閾值資料列
下圖顯示雜湊聯結成本與巢狀迴圈聯結替代方案成本之間的交集範例。 在此交集點決定的閾值，會隨之決定用於聯結作業的實際演算法。

![聯結閾值](../../relational-databases/performance/media/6_AQPJoinThreshold.png)

### <a name="disabling-adaptive-joins-without-changing-the-compatibility-level"></a>停用自適性聯結而不變更相容性層級
您可以在資料庫或陳述式的範圍停用自適性聯結，同時仍將資料庫相容性層級維持在 140 以上。  
若要針對源自資料庫的所有查詢執行停用自適性聯結，請在適用資料庫的內容中執行下列程式碼：

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = ON;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ADAPTIVE_JOINS = OFF;
```

啟用時，此設定在 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 中會顯示為已啟用。
若要針對源自資料庫的所有查詢執行重新啟用自適性聯結，請在適用資料庫的內容中執行下列程式碼：

```sql
-- SQL Server 2017
ALTER DATABASE SCOPED CONFIGURATION SET DISABLE_BATCH_MODE_ADAPTIVE_JOINS = OFF;

-- Azure SQL Database, SQL Server 2019 and higher
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ADAPTIVE_JOINS = ON;
```

您也可以將 `DISABLE_BATCH_MODE_ADAPTIVE_JOINS` 指定為 [USE HINT 查詢提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint)，以針對特定查詢停用自適性聯結。 例如：

```sql
SELECT s.CustomerID,
       s.CustomerName,
       sc.CustomerCategoryName
FROM Sales.Customers AS s
LEFT OUTER JOIN Sales.CustomerCategories AS sc
       ON s.CustomerCategoryID = sc.CustomerCategoryID
OPTION (USE HINT('DISABLE_BATCH_MODE_ADAPTIVE_JOINS')); 
```

> [!NOTE]
> USE HINT　查詢提示的優先順序高於資料庫範圍設定或追蹤旗標設定。 

## <a name="null-values-and-joins"></a><a name="nulls_joins"></a> Null 值與聯結
當資料表的資料行中有 Null 值時，Null 值彼此並不相符。 若所要聯結之其中一個資料表的資料行中出現 Null 值，將只能藉由使用外部聯結來傳回該值 (除非 `WHERE` 子句會排除 Null 值)。     

以下列出兩個資料表，而每個資料表都有 NULL 值出現在參與於聯結的資料行中：     

```
table1                          table2
a           b                   c            d
-------     ------              -------      ------
      1        one                 NULL         two
   NULL      three                    4        four
      4      join4
```    

比較資料行 a 與資料行 c 之數值的聯結並不會針對擁有 NULL 值的資料行進行比對：

```sql
SELECT *
FROM table1 t1 JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```  

唯一傳回的只有在資料行 a 與 c 中有 4 的資料列：

```
a           b      c           d      
----------- ------ ----------- ------ 
4           join4  4           four   

(1 row(s) affected)
```   

基底資料表傳回的 Null 值，也很難與外部聯結傳回的 Null 值作區分。 例如，下列 `SELECT` 陳述式將對這兩個資料表進行左方外部聯結：   

```sql
SELECT *
FROM table1 t1 LEFT OUTER JOIN table2 t2
   ON t1.a = t2.c
ORDER BY t1.a;
GO
```   

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]   

```
a           b      c           d      
----------- ------ ----------- ------ 
NULL        three  NULL        NULL 
1           one    NULL        NULL 
4           join4  4           four   

(3 row(s) affected)
```   

此結果並無法讓您輕鬆地區分資料中的 NULL 與代表聯結失敗的 NULL。 當 Null 值出現在被聯結的資料中時，您最好透過使用一般聯結將它們從結果中刪除。    

## <a name="see-also"></a>另請參閱  
[執行程序邏輯和實體運算子參考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
[比較運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)    
[資料類型轉換 &#40;資料庫引擎&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
[子查詢](../../relational-databases/performance/subqueries.md)      
[自適性聯結](../../relational-databases/performance/intelligent-query-processing.md#batch-mode-adaptive-joins)    
