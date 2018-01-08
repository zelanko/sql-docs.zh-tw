---
title: "記憶體最佳化資料表的索引 | Microsoft Docs"
ms.custom: 
ms.date: 11/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: in-memory-oltp
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a7c3e4fb4a7082a1874c9fc320ff67a1ce6031b0
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="indexes-on-memory-optimized-tables"></a>記憶體最佳化資料表上的索引
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

所有經記憶體最佳化的資料表都必須至少有一個索引，因為它是將資料列連接在一起的索引。 在記憶體最佳化資料表上，每個索引也會進行記憶體最佳化。 有數種方式可用來區分記憶體最佳化索引上的索引和以磁碟為基礎之資料表上的傳統索引：  

- 資料列不會儲存在頁面上，因此沒有頁面或數量單位的集合，沒有可以參照以取得資料表所有頁面的資料分割或配置單位。 索引頁面的概念是可用類型的索引之一，但其儲存方式不同於以磁碟為基礎之資料表的索引。 其不會在網頁內產生傳統類型的的片段，因此不具填滿因數。
- 在資料操作期間，對經記憶體最佳化的資料表上索引的變更永遠不會寫入磁碟。 只有資料列和資料的變更會寫入交易記錄。 
- 當資料庫再次上線時，會重建記憶體最佳化索引。 

經記憶體最佳化的資料表上的所有索引都會根據資料庫復原期間的索引定義來建立。

索引必須是下列其中一項：  
  
- 雜湊索引  
- 記憶體最佳化非叢集索引 (表示 B 型樹狀結構的預設內部結構) 
  
「雜湊」索引會在[記憶體最佳化資料表的雜湊索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)中詳細討論。
「非叢集」索引會在[記憶體最佳化資料表的非叢集索引](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)中詳細討論。  
「資料行存放區」索引會在[另一篇文章](../../relational-databases/indexes/columnstore-indexes-overview.md)中討論。  

## <a name="syntax-for-memory-optimized-indexes"></a>記憶體最佳化索引的語法  
  
經記憶體最佳化的資料表的每個 CREATE TABLE 陳述式都必須明確透過 INDEX 或是隱含透過 PRIMAY KEY 或 UNIQUE 條件約束來包含一個索引。
  
經記憶體最佳化的資料表必須具備主索引鍵，才能以預設的 DURABILITY = SCHEMA\_AND_DATA 來宣告。 下列 CREATE TABLE 陳述式中的 PRIMARY KEY NONCLUSTERED 子句符合兩個需求：  
  
- 提供一個索引，以符合 CREATE TABLE 陳述式中的最低索引需求。  
- 提供 SCHEMA\_AND_DATA 子句所需的主索引鍵。  

    ```sql
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA\_AND_DATA);  
    ```
> [!NOTE]  
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 針對每個經記憶體最佳化的資料表或資料表類型最多可以有 8 個索引。 從 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 開始，在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中不再有特定於經記憶體最佳化的資料表和資料表類型的索引數目限制。
  
### <a name="code-sample-for-syntax"></a>語法的程式碼範例  
  
本小節包含 Transact-SQL 程式碼區塊，示範在記憶體最佳化資料表上建立各種索引的語法。 這個程式碼示範下列作業：  
  
1. 建立記憶體最佳化資料表。  
2. 使用 ALTER TABLE 陳述式新增兩個索引。  
3. 插入 (INSERT) 數個資料列的資料。  
   
    ```sql
    DROP TABLE IF EXISTS SupportEvent;  
    go  

    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int               not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  

        StartDateTime        datetime2     not null,  
        CustomerName         nvarchar(16)  not null,  
        SupportEngineerName  nvarchar(16)      null,  
        Priority             int               null,  
        Description          nvarchar(64)      null  
    )  
        WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA\_AND_DATA);  
    go  
        
        --------------------  
        
    ALTER TABLE SupportEvent  
        ADD CONSTRAINT constraintUnique_SDT_CN  
        UNIQUE NONCLUSTERED (StartDateTime DESC, CustomerName);  
    go  

    ALTER TABLE SupportEvent  
        ADD INDEX idx_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 64);  -- Nonunique.  
    go  
        
        --------------------  
        
    INSERT INTO SupportEvent  
        (StartDateTime, CustomerName, SupportEngineerName, Priority, Description)  
        VALUES  
        ('2016-02-23 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-24 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-26 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go 
    ``` 
  
## <a name="duplicate-index-key-values"></a>重複的索引鍵值

重複的索引鍵值可能會影響記憶體最佳化資料表上的作業效能。 大量的重複項目 (例如，100+) 讓維護索引的工作效率不佳，因為大部分的索引作業都必須周遊重複鏈結。 經記憶體最佳化的資料表上的 `INSERT`、`UPDATE` 和 `DELETE` 作業中可以看到此影響。 

這個問題在雜湊索引的情況下更明顯可見，起因包括雜湊索引的每個作業成本較低，以及大型重複鏈結對雜湊衝突鏈結的干擾。 若要減少重複的索引，請使用非叢集索引，並在索引鍵的結尾加上額外的資料行 (例如，從主索引鍵)，以減少重複數量。 如需雜湊衝突的詳細資訊，請參閱[記憶體最佳化資料表的雜湊索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)。

例如，請考慮 `CustomerId` 上具有主索引鍵的 `Customers` 資料表，以及 `CustomerCategoryID` 資料行上的索引。 通常指定的類別中會有許多客戶，因此 CustomerCategoryID 索引中的指定索引鍵會有許多重複的值。 在此案例中，最佳做法是在 `(CustomerCategoryID, CustomerId)` 上使用非叢集索引。 此索引可用於使用牽涉到 `CustomerCategoryID` 之述詞的查詢，其並不包含重複，因此不會造成索引維護的效率低落。

下列查詢會顯示範例資料庫 `CustomerCategoryID` WideWorldImporters `Sales.Customers`的資料表 [中，](../../sample/world-wide-importers/wide-world-importers-documentation.md)上索引之重複索引鍵值的平均數目。

```sql
SELECT AVG(row_count) FROM
    (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

若要評估您自己的資料表和索引的索引鍵重複項目平均數目，請使用您的資料表名稱取代 `Sales.Customers` ，並使用索引鍵資料行的清單取代 `CustomerCategoryID` 。

## <a name="comparing-when-to-use-each-index-type"></a>比較使用每個索引類型的時機  
  
特定查詢的本質會決定哪個索引類型是最佳選擇。  

在現有的應用程式中實作記憶體最佳化資料表時，一般建議是由非叢集索引開始，因為其功能與傳統以磁碟為基礎之資料表上的叢集與非叢集索引之功能更為類似。 
  
### <a name="recommendations-for-nonclustered-index-use"></a>使用非叢集索引的建議  
  
在下列情況中，非叢集索引會比雜湊索引更適合︰  
  
- 查詢在索引資料行上有 `ORDER BY` 子句。  
- 多重資料行索引中，只有前置資料行會進行測試的查詢。  
- 查詢會搭配下列項目使用 `WHERE` 子句來測試索引資料行︰  
  - 不等比較：`WHERE StatusCode != 'Done'`  
  - 值範圍掃描：`WHERE Quantity >= 100`  
  
在下列所有 SELECT 中，非叢集索引會比雜湊索引更適合︰  

```sql
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE StartDateTime > DateAdd(day, -7, GetUtcDate());  
    
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE CustomerName != 'Ben';  
    
SELECT StartDateTime, CustomerName  
FROM SupportEvent  
ORDER BY StartDateTime;  
    
SELECT CustomerName  
FROM SupportEvent  
WHERE StartDateTime = '2016-02-26';  
```
  
### <a name="recommendations-for-hash-index-use"></a>使用雜湊索引的建議   
  
[雜湊索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)主要用於點查閱，而非用於範圍掃描。

當查詢使用等號比較述詞時，雜湊索引會比非叢集索引更合適，且 `WHERE` 子句會對應至所有索引鍵資料行，如下列範例所示：  
  
```sql
SELECT CustomerName 
FROM SupportEvent  
WHERE SupportEngineerName = 'Liz';
```  

### <a name="multi-column-index"></a>多重資料行索引  
  
多重資料行索引可能是非叢集索引或雜湊索引。 假設索引資料行是 col1 和 col2。 假設有下列 `SELECT` 陳述式，則只有非叢集索引會有助於查詢最佳化工具︰  
  
```sql
SELECT col1, col3  
FROM MyTable_memop  
WHERE col1 = 'dn';  
```

雜湊索引需要 `WHERE` 子句來指定索引鍵中每個資料行的等號比較測試。 否則雜湊索引對查詢最佳化工具沒有助益。  
  
如果 `WHERE` 子句只指定索引鍵中的第二個資料行，則兩種索引類型皆無用。  

### <a name="summary-table-to-compare-index-use-scenarios"></a>比較索引使用狀況案例的摘要資料表  
  
下表列出各種索引類型支援的所有運算。 「是」表示索引可以有效率地為要求提供服務，「否」則表示索引無法有效率地滿足要求。 
  
| 作業 | 記憶體最佳化， <br/> 雜湊 | 記憶體最佳化， <br/> 非叢集 | 以磁碟為基礎， <br/> (非)叢集 |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| 索引掃描，擷取所有資料表資料列。 | 是 | 是 | 是 |  
| 等號比較述詞 (=) 的索引搜尋。 | 是 <br/> (需要有完整索引鍵。) | 是  | 是 |  
| 不等比較和範圍述詞的索引搜尋 <br/> (>, <, <=, >=, `BETWEEN`)。 | 否 <br/> (造成索引掃描。) | 是 <sup>1</sup> | 是 |  
| 依照排序次序擷取符合索引定義的資料列。 | 否 | 是 | 是 |  
| 依照排序次序擷取符合相反索引定義的資料列。 | 否 | 否 | 是 |  

<sup>1</sup> 針對經記憶體最佳化的非叢集索引，不需要完整的索引鍵來執行索引搜尋。  

## <a name="automatic-index-and-statistics-management"></a>自動索引與統計資料管理

利用[自適性索引重組](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)等解決方案，為一或多個資料庫自動管理索引重組以及統計資料更新。 這項程序會根據索引分散程度與其他參數，自動選擇要進行重建或是重新組織索引，並以線性閾值更新統計資料。

## <a name="Additional_Reading"></a> 另請參閱   
 [SQL Server 索引設計指南](../../relational-databases/sql-server-index-design-guide.md)   
 [記憶體最佳化資料表的雜湊索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [記憶體最佳化資料表的非叢集索引](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)    
 [自適性索引重組](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)  
