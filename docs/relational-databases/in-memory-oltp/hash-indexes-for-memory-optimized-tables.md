---
title: "記憶體最佳化資料表的雜湊索引 | Microsoft Docs"
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
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b1acbcd97dfabfa5d23fa82e55d4eb01101233aa
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="hash-indexes-for-memory-optimized-tables"></a>記憶體最佳化資料表的雜湊索引
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
本文說明適用於記憶體最佳化資料表的「雜湊」索引類型。 本文：  
  
- 提供簡短程式碼範例來示範 Transact-SQL 語法。  
- 描述雜湊索引的基礎觀念。  
- 描述 [如何估計適當的值區計數](#configuring_bucket_count)。  
- 說明如何設計和管理雜湊索引。  
  
  
#### <a name="prerequisite"></a>必要條件  
  
了解這篇文章的重要內容資訊位於︰  
  
- [記憶體最佳化資料表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. 記憶體最佳化索引的語法  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 語法的程式碼範例  
  
本小節包含 Transact-SQL 程式碼區塊，示範在記憶體最佳化資料表上建立雜湊索引的可用語法：  
  
- 此範例顯示雜湊索引是在 CREATE TABLE 陳述式內宣告。  
  - 您可以改為在個別 [ALTER TABLE...ADD INDEX](#h3-b2-declaration-limitations) 陳述式宣告雜湊索引。  
  
  
  
    DROP TABLE IF EXISTS SupportEventHash;  
    go  
      
    CREATE TABLE SupportIncidentRating_Hash  
    (  
      SupportIncidentRatingId   int      not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
      
      RatingLevel          int           not null,  
      
      SupportEngineerName  nvarchar(16)  not null,  
      Description          nvarchar(64)      null,  
      
      INDEX ix_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 100000)  
    )  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_ONLY);  
    go  
  

若要判斷您資料的正確 `BUCKET_COUNT` ，請參閱 [設定雜湊索引值區計數](#configuring_bucket_count)。 
  
## <a name="b-hash-indexes"></a>B. 雜湊索引  
  
  
### <a name="b1-performance-basics"></a>B.1 效能的基本概念  
  
雜湊索引的效能如下︰  
  
- 當 WHERE 子句為雜湊索引鍵中的每個資料行指定「確切」的值時極佳。  
- 當 WHERE 子句在索引鍵中尋找某個值「範圍」時效能低劣。  
- 當 WHERE 子句針對有兩個資料行的雜湊索引鍵的第一個資料行指定一個特定值，但未針對該索引鍵的「第二個」資料行指定值時，效能低劣。  
  
  
<a name="h3-b2-declaration-limitations"></a>  
  
### <a name="b2-declaration-limitations"></a>B.2 宣告限制  
  
雜湊索引只能存在於記憶體最佳化資料表上。 它無法存在於以磁碟為基礎的資料表上。  
  
雜湊索引可以宣告為︰  
  
- UNIQUE，或者可以預設為 Nonunique。  
- NONCLUSTERED，這是預設值。   
  
  
在 CREATE TABLE 陳述式之外建立雜湊索引的語法範例如下︰  
  
  
    ALTER TABLE MyTable_memop  
      ADD INDEX ix_hash_Column2 UNIQUE  
        HASH (Column2) WITH (BUCKET_COUNT = 64);  
  
  
  
### <a name="b3-buckets-and-hash-function"></a>B.3 值區和雜湊函數  
  
雜湊索引會將它的索引鍵值錨定在我們所謂的「值區」陣列上︰  
  
- 每個值區是 8 位元組，可用來儲存索引鍵項目連結清單的記憶體位址。  
- 每個項目都是一個索引鍵的值，加上其基礎記憶體最佳化資料表中對應資料列的位址。  
  - 每個項目指向項目連結清單中的下一個項目，全都連結到目前的值區。  
  
  
雜湊演算法會嘗試在其各個值區平均散佈所有唯一或相異索引鍵值，但總體平均是一項無法達成的理想。 任何給定索引鍵值的所有執行個體會鏈結到相同的值區。 值區可能也混合了不同索引鍵值的所有執行個體。  
  
- 這種混合稱為「雜湊衝突」。 衝突很常見，但並不理想。  
- 實際目標是包含兩個不同索引鍵值之值區的 30%。  
  
  
您宣告雜湊索引應該有多少個值區。  
  
- 值區與資料表資料列或相異值的比率越低，平均值區連結清單就越長。  
- 短連結清單的執行速度比長連結清單還快。  
  
  
SQL Server 有一個雜湊函式，可用於所有雜湊索引：  
  
- 雜湊函式具決定性︰假如有相同的輸入索引鍵值，其會一致性地輸出相同的值區位置。  
- 透過重複呼叫，雜湊函式的輸出通常會形成波氏或鐘型曲線分佈，而不是單層線性分佈。  
  
  
下圖摘要說明雜湊索引和值區的相互作用。  
  
  
![hekaton_tables_23d](../../relational-databases/in-memory-oltp/media/hekaton-tables-23d.png "輸入至雜湊函式的索引鍵，輸出是指向鏈結前端的雜湊值區位址。")  
  
  
  
### <a name="b4-row-versions-and-garbage-collection"></a>B.4 資料列版本和記憶體回收  
  
  
在記憶體最佳化資料表中，當資料列受到 SQL UPDATE 影響時，資料表會建立資料列的更新版本。 在更新交易期間，其他工作階段或許能夠讀取舊版資料列，藉此避免發生與資料列鎖定相關聯的效能低落。  
  
雜湊索引可能也有不同版本的項目來容納更新。  
  
不再需要較舊的版本之後，記憶體回收 (GC) 執行緒會周遊值區及其連結清單來清除舊項目。 如果連結清單鏈結長度很短，GC 執行緒的執行效能更好。   
  
<a name="configuring_bucket_count"></a>
  
## <a name="c-configuring-the-hash-index-bucket-count"></a>C. 設定雜湊索引值區計數  
  
雜湊索引值區計數是在索引建立時間指定，並可使用 ALTER TABLE...ALTER INDEX REBUILD 語法來變更。  
  
在大部分情況下，值區計數理想情況會介於索引鍵中相異值數目的 1 到 2 倍之間。   
您不一定能夠預測某個特定索引鍵可能擁有或將會擁有多少個值。 如果 **BUCKET_COUNT** 值在實際索引鍵值數目的 10 倍內，效能通常仍然不錯，高估一般而言會比低估好。  
  
值區太「少」會有下列缺點︰  
  
- 有更多相異索引鍵值的雜湊衝突。  
  - 每個相異值都會強制與不同的相異值共用相同的值區。  
  - 每個值區的平均鏈結長度都會增加。  
  - 值區鏈結越長，索引中的等號比較查閱的速度就越慢。  
  
值區太「多」會有下列缺點︰  
  
- 值區計數過高可能會導致更多的空值區。  
  - 空值區會影響完整索引掃描的效能。 如果是定期執行，請考慮挑選接近相異索引鍵值數目的值區計數。  
  - 空值區會使用記憶體，但每個值區只使用 8 個位元組。  
    
  
> [!NOTE]
> 新增更多值區，對於減少將共用重複值的項目鏈結在一起的情況，沒有任何助益。 您可以使用值重複的比率來決定雜湊是否為適當的索引類型，而不是計算值區計數。  
  
  
  
### <a name="c1-practical-numbers"></a>C.1 實際數字  
  
即使 **BUCKET_COUNT** 是在慣用範圍中間上下，雜湊索引的效能很可能是可容忍或可接受的。 不會產生任何危機。  
  
為雜湊索引提供 **BUCKET_COUNT** ，大約等於您預測記憶體最佳化資料表成長後將擁有的資料列數目。  
  
假設成長中的資料表擁有 2,000,000 個資料列，但您預測數量將成長 10 倍為 20,000,000 個資料列。 值區計數請從資料表中資料列數目的 10 倍開始。 這讓您有空間可容納增加的資料列數。  
  
- 在理想情況下，您會在資料列數量到達初始值區計數時，增加值區計數。  
- 即使資料列數量成長至值區計數的 5 倍，在大多數情況下的效能也仍然不錯。  
  
假設雜湊索引有 10,000,000 個相異索引鍵值。  
  
- 值區計數 2,000,000 正是您可接受的最低限度。 效能降低的程度是在容忍範圍內。  
  
### <a name="c2-too-many-duplicate-values-in-the-index"></a>C.2 索引中有太多重複的值？  
  
如果雜湊索引值有高比率的重複項目，則雜湊值區會受到較長鏈結影響。  
  
假設您有來自較早 T-SQL 語法程式碼區塊的相同 SupportEvent 資料表。 下列 T-SQL 程式碼示範如何尋找並顯示「所有」值與「唯一」值的比率︰  
  
        -- Calculate ratio of:  Rows / Unique_Values.  
    DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
      
    SELECT @allValues = Count(*) FROM SupportEvent;  
      
    SELECT @uniqueVals = Count(*) FROM  
      (SELECT DISTINCT SupportEngineerName  
         FROM SupportEvent) as d;  
      
        -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
    SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
    go  
  
- 10.0 或更高的比率表示雜湊是不適用的索引類型。 請考慮改用非叢集索引。   
  
## <a name="d-troubleshooting-hash-index-bucket-count"></a>D. 疑難排解雜湊索引值區計數  
  
本節將討論如何進行雜湊索引值區計數的疑難排解。  
  
### <a name="d1-monitor-statistics-for-chains-and-empty-buckets"></a>D.1 監視鏈結和空值區的統計資料  
  
您可以執行下列 T-SQL SELECT，來監視雜湊索引的統計健康狀況。 SELECT 會使用名為 **sys.dm_db_xtp_hash_index_stats**的資料管理檢視 (DMV)。  
  
  
```t-sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
      
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM  
         sys.dm_db_xtp_hash_index_stats  as h   
    JOIN sys.indexes                     as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
```
  
  
將 SELECT 結果與下列統計指導方針進行比較：  
  
- 空值區︰  
  - 33% 是適當的目標值，但較大的百分比 (甚至是 90%) 通常沒什麼問題。  
  - 當值區計數等於相異索引鍵值的數目時，大約有 33% 的值區是空的。  
  - 低於 10% 的值就太低。  
- 值區內的鏈結︰  
  - 如果沒有任何重複的索引鍵值，則平均鏈結長度 1 會很理想。 通常可接受的鏈結長度上限為 10。  
  - 如果平均鏈結長度大於 10，且空值區的百分比大於 10%，則資料就有這麼多雜湊索引可能不是最適當類型的重複項目。  
  

  
### <a name="d2-demonstration-of-chains-and-empty-buckets"></a>D.2 鏈結和空值區的示範  
  
  
下列 T-SQL 程式碼區塊可讓您輕鬆地測試 `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`。 程式碼區塊會在 1 分鐘內完成。 以下是下列程式碼區塊的階段︰  
  
  
1. 建立含有數個雜湊索引的記憶體最佳化資料表。  
2. 在資料表中填入數千個資料列。  
    A. 模數運算子可用來設定 StatusCode 資料行中重複值的比率。  
    B. 迴圈大約會在 1 分鐘內插入 (INSERT) 262144 個資料列。  
3. 列印 (PRINT) 訊息會要求您執行先前來自 **sys.dm_db_xtp_hash_index_stats**的 SELECT。  
  
  
```t-sql
    DROP TABLE IF EXISTS SalesOrder_Mem;  
    go  
      
      
    CREATE TABLE SalesOrder_Mem  
    (  
      SalesOrderId   uniqueidentifier  NOT NULL  DEFAULT newid(),  
      OrderSequence  int               NOT NULL,  
      OrderDate      datetime2(3)      NOT NULL,  
      StatusCode     tinyint           NOT NULL,  
      
      PRIMARY KEY NONCLUSTERED  
          HASH (SalesOrderId)  WITH (BUCKET_COUNT = 262144),  
      
      INDEX ix_OrderSequence  
          HASH (OrderSequence) WITH (BUCKET_COUNT = 20000),  
      
      INDEX ix_StatusCode  
          HASH (StatusCode)    WITH (BUCKET_COUNT = 8),  
      
      INDEX ix_OrderDate       NONCLUSTERED (OrderDate DESC)  
    )  
      WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    go  
      
        --------------------  
      
    SET NoCount ON;  
      
      -- Same as PK bucket_count.  68 seconds to complete.  
    DECLARE @i int = 262144;  
      
    BEGIN TRANSACTION;  
      
    WHILE @i > 0  
    Begin  
      
      INSERT SalesOrder_Mem  
          (OrderSequence, OrderDate, StatusCode)  
        Values  
          (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
      
      SET @i -= 1;  
    End  
    COMMIT TRANSACTION;  
      
    PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
    go  
```  
  
  
先前的 INSERT 迴圈會執行下列動作︰  
  
- 針對主索引鍵索引和 IX_OrderSequence 插入唯一值。  
- 插入數十萬個資料列，其中只針對 StatusCode 顯示 8 個相異值。 因此 ix_StatusCode 索引中，值重複的比率較高。  
  
若要在值區計數不是最佳選項時進行疑難排解，可檢查下列來自 **sys.dm_db_xtp_hash_index_stats**之 SELECT 的輸出。 我們對於這些結果將 `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` 新增到從 D.1 節複製的 SELECT。  
  
  
  
我們的 SELECT 結果顯示在程式碼之後，以手動方式分割成兩個較窄的結果資料表，以獲得較佳的顯示效果。  
  
- 以下是「值區計數」的結果。  
  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| ix_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
  
- 接下來是為「鏈結長度」的結果。  
  
  
| IndexName | avg_chain_length | max_chain_length |  
| :-------- | ---------------: | ---------------: |  
| ix_OrderSequence | 8 | 26 |  
| ix_StatusCode | 65536 | 65536 |  
| PK_SalesOrd_B14003... | 1 | 8 |  
  
  
  
  
讓我們解釋上述結果資料表中的三個雜湊索引︰  
  
*ix_StatusCode：*  
  
- 有 50% 的值區是空的，這是理想的狀況。  
- 不過，平均鏈結長度非常高 (65536)。  
  - 這表示有高比率的重複值。  
  - 因此，這種情況不適合使用雜湊索引。 應該改用非叢集索引。  
  
*ix_OrderSequence：*  
  
- 有 0% 的值區是空的，這個數字過低。  
- 平均鏈結長度為 8，儘管這個索引中的所有值都是唯一。  
  - 因此值區計數應會增加，以減少平均鏈結長度，使其更接近 2 或 3。  
- 由於索引鍵擁有 262144 個唯一值，因此值區計數至少應該為 262144。  
  - 如果預期未來會有所成長，則值區計數應該更高。  
  
*主索引鍵索引 (PK_SalesOrd_...)：*  
  
- 有 36% 的值區是空的，這是理想的狀況。  
- 平均鏈結長度為 1，這也很理想。 不需進行任何變更。  
  
  
### <a name="d3-balancing-the-trade-off"></a>D.3 平衡取捨  
  
OLTP 工作負載專注於個別的資料列。 完整的資料表掃描通常不會在 OLTP 工作負載的關鍵效能路徑中。 因此，您仍必須在下列項目之間平衡取捨︰  
  
- 記憶體使用量的數量；與  
- 等號比較測試的效能，以及插入作業的效能。  
  
  
*如果比較顧慮記憶體使用量：*  
  
- 請選擇接近索引鍵值記錄數目的值區計數。  
- 值區計數不應該大幅低於索引鍵值數目，因為這樣會影響大部分 DML 作業，以及影響在伺服器重新啟動後復原資料庫所需的時間。  
  
  
*如果比較顧慮等號比較測試的效能︰*  
  
- 適合使用較高的值區計數 (唯一索引值數目的二到三倍)。 較高的計數表示︰  
  - 尋找某個特定值時更快速地擷取。  
  - 提高記憶體使用量。  
  - 完整掃描雜湊索引所需的時間增加。  
  
  
  
  
## <a name="e-strengths-of-hash-indexes"></a>E. 雜湊索引的優點  
  
  
在下列情況中，雜湊索引會比非雜湊索引更適合︰  
  
- 查詢會搭配等號比較使用 WHERE 子句來測試索引資料行，如下所示：  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="e1-multi-column-hash-index-keys"></a>E.1 多重資料行的雜湊索引鍵  
  
  
您的兩個資料行索引可能是非叢集索引或雜湊索引。 假設索引資料行是 col1 和 col2。 假設有下列 SQL SELECT 陳述式，則只有非叢集索引會有助於查詢最佳化工具︰  
  
  
    SELECT col1, col3  
        FROM MyTable_memop  
        WHERE col1 = 'dn';  
  
  
雜湊索引需要 WHERE 子句來指定索引鍵中每個資料行的等號比較測試。 否則雜湊索引對最佳化工具沒有助益。  
  
如果 WHERE 子句只指定索引鍵的第二個資料行，則兩種索引類型皆無用。  

