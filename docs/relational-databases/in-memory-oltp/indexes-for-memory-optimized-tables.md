---
title: "記憶體最佳化資料表的索引 | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b468f44444a9c6cc031ea892f44849db401e0ab7
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="indexes-for-memory-optimized-tables"></a>記憶體最佳化資料表的索引
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
本文說明適用於記憶體最佳化資料表的索引類型。 本文：  
  
- 提供簡短程式碼範例來示範 Transact-SQL 語法。  
- 說明記憶體最佳化索引和以磁碟為基礎的傳統索引有何差異。  
- 說明每個類型的記憶體最佳化索引的最適用情況。  
  
  
「雜湊」索引會在[密切相關的文章](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)中更詳細地討論。  
  
  
「資料行存放區」索引會在[另一篇文章](~/relational-databases/indexes/columnstore-indexes-overview.md)中討論。  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. 記憶體最佳化索引的語法  
  
適用於記憶體最佳化資料表的每個 CREATE TABLE 陳述式必須包含 1 到 8 個子句來宣告索引。 索引必須是下列其中一項：  
  
- 雜湊索引。  
- 非叢集索引 (表示 B 型樹狀目錄的預設內部結構)。  
  
  
記憶體最佳化資料表必須具備主索引鍵，才能以預設的 DURABILITY = SCHEMA_AND_DATA 來宣告。 下列 CREATE TABLE 陳述式中的 PRIMARY KEY NONCLUSTERED 子句符合兩個需求：  
  
- 提供一個索引，以符合 CREATE TABLE 陳述式中的最低索引需求。  
- 提供 SCHEMA_AND_DATA 子句所需的主索引鍵。  
  
  
  
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 語法的程式碼範例  
  
本小節包含 Transact-SQL 程式碼區塊，示範在記憶體最佳化資料表上建立各種索引的語法。 這個程式碼示範下列作業：  
  
  
1. 建立記憶體最佳化資料表。  
2. 使用 ALTER TABLE 陳述式新增兩個索引。  
3. 插入 (INSERT) 數個資料列的資料。  
  
  
  
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
        DURABILITY = SCHEMA_AND_DATA);  
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
        ('2016-02-25 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-25 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-25 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go  
  
  
  
## <a name="b-nature-of-memory-optimized-indexes"></a>B. 記憶體最佳化索引的本質  
  
在記憶體最佳化資料表上，每個索引也會進行記憶體最佳化。 記憶體最佳化索引上的索引和以磁碟為基礎之資料表上的傳統索引有數種不同之處。  
  
每個記憶體最佳化的索引只存在於作用中的記憶體。 索引不會在磁碟上呈現。  
  
- 當資料庫再次上線時，會重建記憶體最佳化索引。  
  
  
當 SQL UPDATE 陳述式修改記憶體最佳化資料表中的資料時，不會將其索引的對應變更寫入記錄檔。  
  
  
記憶體最佳化索引中的項目包含資料表中資料列的直接記憶體位址。  
  
- 相較之下，磁碟上的傳統 B 型樹狀目錄索引中的項目則包含鍵值，系統必須先使用該鍵值以尋找相關聯之資料表資料列的記憶體位址。  
  
  
和以磁碟為基礎的索引一樣，記憶體最佳化索引沒有固定的分頁。  
  
- 其不會在網頁內產生傳統類型的的片段，因此不具填滿因數。  
  
## <a name="c-duplicate-index-key-values"></a>C. 重複的索引鍵值

重複的索引鍵值可能會影響記憶體最佳化資料表上的作業效能。 大量的重複項目 (例如，100+) 讓維護索引的工作效率不佳，因為大部分的索引作業都必須周遊重複鏈結。 記憶體最佳化資料表上的 INSERT、UPDATE 和 DELETE 作業中可以看到此等影響。 這個問題在雜湊索引的情況下更明顯可見，起因包括雜湊索引的每個作業成本較低，以及大型重複鏈結對雜湊衝突鏈結的干擾。 若要減少重複的索引，請使用非叢集索引，並在索引鍵的結尾加上額外的資料行 (例如，從主索引鍵)，以減少重複數量。

例如，請考慮 CustomerId 上有主索引鍵以及 CustomerCategoryID 資料行上有索引的 Customers 資料表。 通常指定的類別中會有許多客戶，因此 CustomerCategoryID 索引中的指定索引鍵會有許多重複的值。 在此案例中，最佳做法是在 (CustomerCategoryID, CustomerId) 上使用非叢集索引。 此索引可用於使用牽涉到 CustomerCategoryID 之述詞，且不包含重複的查詢，因此不會造成索引維護的效率低落。

下列查詢會顯示範例資料庫 `CustomerCategoryID` WideWorldImporters `Sales.Customers`的資料表 [中，](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)上索引之重複索引鍵值的平均數目。

```Transact-SQL
    SELECT AVG(row_count) FROM
       (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

若要評估您自己的資料表和索引的索引鍵重複項目平均數目，請使用您的資料表名稱取代 `Sales.Customers` ，並使用索引鍵資料行的清單取代 `CustomerCategoryID` 。

## <a name="d-comparing-when-to-use-each-index-type"></a>D. 比較使用每個索引類型的時機  
  
  
特定查詢的本質會決定哪個索引類型是最佳選擇。  

在現有的應用程式中實作記憶體最佳化資料表時，一般建議是由非叢集索引開始，因為其功能與傳統以磁碟為基礎之資料表上的叢集與非叢集索引之功能更為類似。 
  
  
### <a name="d1-strengths-of-nonclustered-indexes"></a>D.1 非叢集索引的優點  
  
  
在下列情況中，非叢集索引會比雜湊索引更適合︰  
  
- 查詢在索引資料行上有 ORDER BY 子句。  
- 多重資料行索引中，只有前置資料行會進行測試的查詢。  
- 查詢會搭配下列項目使用 WHERE 子句來測試索引資料行︰  
  - 不等比較︰*WHERE StatusCode != 'Done'*  
  - 值範圍︰*WHERE Quantity >= 100*  
  
  
在下列所有 SELECT 中，非叢集索引會比雜湊索引更適合︰  
  
  
  
    SELECT col2 FROM TableA  
        WHERE StartDate > DateAdd(day, -7, GetUtcDate());  
      
    SELECT col3 FROM TableB  
        WHERE ActivityCode != 5;  
      
    SELECT StartDate, LastName  
        FROM TableC  
        ORDER BY StartDate;  
      
    SELECT IndexKeyColumn2  
        FROM TableD  
        WHERE IndexKeyColumn1 = 42;  
  
  
  
### <a name="d2-strengths-of-hash-indexes"></a>D.2 雜湊索引的優點  
  
  
在下列情況中， [雜湊索引](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) 會比非雜湊索引更適合：  
  
- 查詢使用所有索引鍵資料行均完全相等的 WHERE 子句測試索引資料行，如下所示：  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="d3-summary-table-to-compare-index-strengths"></a>D.3 比較索引優點的摘要資料表  
  
  
下表列出各種索引類型支援的所有運算。  
  
  
| 運算 | 記憶體最佳化、 <br/> hash (雜湊) | 記憶體最佳化、 <br/> 非叢集 | 以磁碟為基礎、 <br/> (非)叢集 |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| 索引掃描，擷取所有資料表資料列。 | 是 | 是 | 是 |  
| 等號比較述詞 (=) 的索引搜尋。 | 是 <br/> (需要有完整索引鍵。) | 是  | 是 |  
| 不等比較和範圍述詞的索引搜尋 <br/> (>、<、<=、>=、BETWEEN)。 | 否 <br/> (產生索引掃描。) | 是 | 是 |  
| 依照排序次序擷取符合索引定義的資料列。 | 否 | 是 | 是 |  
| 依照排序次序擷取符合相反索引定義的資料列。 | 否 | 否 | 是 |  
  
  
在表格中，「是」表示索引可以有效率地為要求提供服務，「否」則表示索引無法有效率地滿足要求。  

