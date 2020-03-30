---
title: 針對雜湊索引進行疑難排解 - 記憶體最佳化資料表
ms.custom: seo-dt-2019
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6216e8e008bff92ce502aa6dda8025c5ef63f0ba
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412664"
---
# <a name="troubleshooting-hash-indexes-for-memory-optimized-tables"></a>為記憶體最佳化資料表的雜湊索引進行疑難排解
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="prerequisite"></a>必要條件  
  
了解這篇文章的重要內容資訊位於︰  
  
- [記憶體最佳化資料表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)
- [記憶體最佳化資料表的雜湊索引](../../relational-databases/sql-server-index-design-guide.md#hash_index) 
 
## <a name="practical-numbers"></a>實際數字  
  
當為經記憶體最佳化的資料表建立雜湊索引時，值區數目必須在建立時指定。 在大部分情況下，值區計數理想情況會介於索引鍵中相異值數目的 1 到 2 倍之間。 

不過，即使 **BUCKET_COUNT** 是在慣用範圍中間上下，雜湊索引的效能很可能是可容忍或可接受的。 請考慮至少為雜湊索引提供 **BUCKET_COUNT**，大約等於您預測經記憶體最佳化的資料表成長後將擁有的資料列數目。  
假設成長中的資料表擁有 2,000,000 個資料列，但預測將成長 10 倍為 20,000,000 個資料列。 值區計數請從資料表中資料列數目的 10 倍開始。 這讓您有空間可容納增加的資料列數。  
  
- 在理想情況下，您會在資料列數量到達初始值區計數時，增加值區計數。  
- 即使資料列數量成長至值區計數的 5 倍，在大多數情況下的效能也仍然不錯。  
  
假設雜湊索引有 10,000,000 個相異索引鍵值。  
  
- 值區計數 2,000,000 正是您可接受的最低限度。 效能降低的程度是在容忍範圍內。  
  
## <a name="too-many-duplicate-values-in-the-index"></a>索引中有太多重複的值？  
  
如果雜湊索引值有高比率的重複項目，則雜湊值區會受到較長鏈結影響。  
  
假設您有來自較早 T-SQL 語法程式碼區塊的相同 SupportEvent 資料表。 下列 T-SQL 程式碼示範如何尋找並顯示「所有」  值與「唯一」  值的比率︰  
  
```sql
-- Calculate ratio of:  Rows / Unique_Values.  
DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
  
SELECT @allValues = Count(*) FROM SupportEvent;  
  
SELECT @uniqueVals = Count(*) FROM  
  (SELECT DISTINCT SupportEngineerName  
      FROM SupportEvent) as d;  
  
    -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
go  
```
  
- 10.0 或更高的比率表示雜湊是不適用的索引類型。 請考慮改用非叢集索引。   
  
## <a name="troubleshooting-hash-index-bucket-count"></a>疑難排解雜湊索引值區計數  
  
本節將討論如何進行雜湊索引值區計數的疑難排解。  
  
### <a name="monitor-statistics-for-chains-and-empty-buckets"></a>監視鏈結和空值區的統計資料  
  
您可以執行下列 T-SQL SELECT，來監視雜湊索引的統計健康狀況。 SELECT 會使用名為 **sys.dm_db_xtp_hash_index_stats**的資料管理檢視 (DMV)。  
  
```sql
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
  
### <a name="demonstration-of-chains-and-empty-buckets"></a>鏈結和空值區的示範  
  
下列 T-SQL 程式碼區塊可讓您輕鬆地測試 `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`。 程式碼區塊會在 1 分鐘內完成。 以下是下列程式碼區塊的階段︰  
  
1. 建立含有數個雜湊索引的記憶體最佳化資料表。  
2. 在資料表中填入數千個資料列。  
    a. 模數運算子可用來設定 StatusCode 資料行中重複值的比率。  
    b. 迴圈大約會在 1 分鐘內插入 262,144 個資料列。  
3. 列印 (PRINT) 訊息會要求您執行先前來自 **sys.dm_db_xtp_hash_index_stats**的 SELECT。  

```sql
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
  
SET NOCOUNT ON;  
  
-- Same as PK bucket_count.  68 seconds to complete.  
DECLARE @i int = 262144;  
  
BEGIN TRANSACTION;  
  
WHILE @i > 0  
BEGIN  
  
  INSERT SalesOrder_Mem  
      (OrderSequence, OrderDate, StatusCode)  
    Values  
      (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
  
  SET @i -= 1;  
END  
COMMIT TRANSACTION;  
  
PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
go  
```  
  
先前的 `INSERT` 迴圈會執行下列動作︰  
  
- 針對主索引鍵索引和 *ix_OrderSequence* 插入唯一值。  
- 插入數十萬個資料列，其中只針對 `StatusCode` 顯示 8 個相異值。 因此，*ix_StatusCode* 索引中值重複的比例較高。  
  
若要在值區計數不是最佳選項時進行疑難排解，可檢查下列來自 **sys.dm_db_xtp_hash_index_stats**之 SELECT 的輸出。 我們對於這些結果將 `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` 新增到從 D.1 節複製的 SELECT。  
  
我們的 `SELECT` 結果顯示在程式碼之後，以手動方式分割成兩個較窄的結果資料表，以獲得較佳的顯示效果。  
  
- 以下是「值區計數」的結果  。  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| ix_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
- 接下來是為「鏈結長度」  的結果。  
  
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
  
### <a name="balancing-the-trade-off"></a>平衡取捨  
  
OLTP 工作負載專注於個別的資料列。 完整的資料表掃描通常不會在 OLTP 工作負載的關鍵效能路徑中。 因此，您必須在**記憶體使用量**與**等號比較測試和插入作業的效能**之間平衡取捨。  
  
**如果比較顧慮記憶體使用量：**  
  
- 請選擇接近索引鍵值記錄數目的值區計數。  
- 值區計數不應該大幅低於索引鍵值數目，因為這樣會影響大部分 DML 作業，以及影響在伺服器重新啟動後復原資料庫所需的時間。  
  
**如果比較顧慮等號比較測試的效能︰**  
  
- 適合使用較高的值區計數 (唯一索引值數目的二到三倍)。 較高的計數表示︰  
  - 尋找某個特定值時更快速地擷取。  
  - 提高記憶體使用量。  
  - 完整掃描雜湊索引所需的時間增加。  
  

##  <a name="additional-reading"></a><a name="Additional_Reading"></a> 其他閱讀資料  
 [記憶體最佳化資料表的雜湊索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [記憶體最佳化資料表的非叢集索引](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)  
