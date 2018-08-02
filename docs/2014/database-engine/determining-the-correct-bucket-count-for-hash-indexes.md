---
title: 判斷雜湊索引的正確貯體計數 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d1ac280-87db-4bd8-ad43-54353647d8b5
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5dbb50c928f066e595b48737da2cc2fc6b9f45eb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306165"
---
# <a name="determining-the-correct-bucket-count-for-hash-indexes"></a>判斷雜湊索引的正確值區計數
  您必須指定的值`BUCKET_COUNT`參數，當您建立記憶體最佳化的資料表。 本主題將針對判斷適合 `BUCKET_COUNT` 參數的值提出建議。 如果您無法判斷正確的值區計數，請改用非叢集索引。  不正確的 `BUCKET_COUNT` 值 (尤其是過低的值) 可能會對工作負載的效能以及資料庫的復原時間造成嚴重影響。 最好是高估值區計數。  
  
 重複的索引鍵可能會因為雜湊索引而降低效能，因為索引鍵會雜湊到相同的貯體，使得貯體的鏈結增加。  
  
 如需有關非叢集雜湊索引的詳細資訊，請參閱 <<c0> [ 雜湊索引](hash-indexes.md)並[使用記憶體最佳化資料表索引的方針](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
 針對記憶體最佳化的資料表上的每個雜湊索引配置一個雜湊表。 所指定的索引配置的雜湊表的大小`BUCKET_COUNT`中的參數[CREATE TABLE &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql)或[CREATE TYPE &#40;-&#41; ](/sql/t-sql/statements/create-type-transact-sql). 值區計數會於內部四捨五入進位至下一個二的乘冪。 例如，指定值區計數 300,000 將產生實際值區計數 524,288。  
  
 如需有關貯體計數的文章和視訊的連結，請參閱 [如何判斷雜湊索引的正確貯體計數 (記憶體內 OLTP)](http://go.microsoft.com/fwlink/p/?LinkId=525853)。  
  
## <a name="recommendations"></a>建議  
 在大部分情況下，值區計數應該介於索引鍵中相異值數目的 1 到 2 倍之間。 如果索引鍵包含許多重複的值，平均每個索引鍵值都有超過 10 個資料列，則改用非叢集索引  
  
 您不一定能夠預測某個特定索引鍵可能擁有或將會擁有多少個值。 效能應該是可以接受如果`BUCKET_COUNT`值是在 5 次的索引鍵值實際數目。  
  
 若要判斷現有資料中的唯一索引鍵數目，請使用類似下列範例的查詢：  
  
### <a name="primary-key-and-unique-indexes"></a>主索引鍵和唯一索引  
 由於主索引鍵的索引是唯一的，因此索引鍵中的相異值數目會對應資料表中資料列的數目。 針對 AdventureWorks 資料庫的 Sales.SalesOrderDetail 資料表中 (SalesOrderID, SalesOrderDetailID) 上的主索引鍵，發出下列查詢來計算相異主索引鍵值的數目，該數目對應資料表中資料列的數目：  
  
```tsql  
SELECT COUNT(*) AS [row count]   
FROM Sales.SalesOrderDetail  
```  
  
 此查詢會顯示資料列計數 121,317。 如果資料列計數不會大幅變更，請使用值區計數 240,000。 如果資料表中的銷售訂單數目預計會變成四倍，請使用值區計數 480,000。  
  
### <a name="non-unique-indexes"></a>非唯一索引  
 對於其他索引，例如 (SpecialOfferID, ProductID) 上的多重資料行索引，發出下列查詢來判斷唯一索引鍵值的數目：  
  
```tsql  
SELECT COUNT(*) AS [SpecialOfferID_ProductID index key count]  
FROM   
   (SELECT DISTINCT SpecialOfferID, ProductID   
    FROM Sales.SalesOrderDetail) t  
```  
  
 此查詢會針對 (SpecialOfferID, ProductID) 傳回索引鍵計數 484，表示應該使用非叢集索引而不是非叢集雜湊索引。  
  
### <a name="determining-the-number-of-duplicates"></a>判斷重複數目  
 若要判斷索引鍵值的重複值平均數目，請將資料列總數除以唯一索引鍵數目。  
  
 針對 (SpecialOfferID, ProductID) 上的範例索引，此運算為 121317 / 484 = 251。 這表示索引鍵值的平均為 251，因此應該是非叢集索引。  
  
## <a name="troubleshooting-the-bucket-count"></a>對值區計數進行疑難排解  
 若要疑難排解記憶體最佳化資料表中的值區計數問題，請使用[sys.dm_db_xtp_hash_index_stats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-hash-index-stats-transact-sql)以取得關於空白貯體和資料列鏈結的長度的統計資料。 下列查詢可用來取得目前資料庫中所有雜湊索引的相關統計資料。 如果資料庫中有大型資料表，則查詢可能需要幾分鐘才能完成。  
  
```tsql  
SELECT   
   object_name(hs.object_id) AS 'object name',   
   i.name as 'index name',   
   hs.total_bucket_count,  
   hs.empty_bucket_count,  
   floor((cast(empty_bucket_count as float)/total_bucket_count) * 100) AS 'empty_bucket_percent',  
   hs.avg_chain_length,   
   hs.max_chain_length  
FROM sys.dm_db_xtp_hash_index_stats AS hs   
   JOIN sys.indexes AS i   
   ON hs.object_id=i.object_id AND hs.index_id=i.index_id  
```  
  
 雜湊索引健全狀況的兩個重要指標為：  
  
 *empty_bucket_percent*  
 *empty_bucket_percent*指出雜湊索引中空貯體數目。  
  
 如果 *empty_bucket_percent* 小於 10%，表示這個值區計數可能太低。 理想的 *empty_bucket_percent* 應該是 33% 或更高。 若值區計數與索引鍵值相符，則約 1/3 的貯體數目為空白，原因是雜湊散發。  
  
 *avg_chain_length*  
 *avg_chain_length*指出雜湊貯體中的資料列鏈結的平均長度。  
  
 如果 *avg_chain_length* 大於 10，且 *empty_bucket_percent* 大於 10%，則可能有許多重複的索引鍵值，那麼非叢集索引會較為理想。 理想的平均鏈結長度為 1。  
  
 影響鏈結長度的因素有兩個：  
  
1.  重複項目；所有重複的資料列屬於雜湊索引中的同一個鏈結。  
  
2.  多個索引鍵值對應到相同貯體。 值區計數越低，就會有越多的貯體擁有對應的多個值。  
  
 以下列資料表和指令碼為例，將範例資料列插入資料表中：  
  
```tsql  
CREATE TABLE [Sales].[SalesOrderHeader_test]  
(  
   [SalesOrderID] [uniqueidentifier] NOT NULL DEFAULT (newid()),  
   [OrderSequence] int NOT NULL,  
   [OrderDate] [datetime2](7) NOT NULL,  
   [Status] [tinyint] NOT NULL,  
  
PRIMARY KEY NONCLUSTERED HASH ([SalesOrderID]) WITH ( BUCKET_COUNT = 262144 ),  
INDEX IX_OrderSequence HASH (OrderSequence) WITH ( BUCKET_COUNT = 20000),  
INDEX IX_Status HASH ([Status]) WITH ( BUCKET_COUNT = 8),  
INDEX IX_OrderDate NONCLUSTERED ([OrderDate] ASC),  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
DECLARE @i int = 0  
BEGIN TRAN  
WHILE @i < 262144  
BEGIN  
   INSERT Sales.SalesOrderHeader_test (OrderSequence, OrderDate, [Status]) VALUES (@i, sysdatetime(), @i % 8)  
   SET @i += 1  
END  
COMMIT  
GO  
```  
  
 此指令碼會在資料表中插入 262,144 個資料列。 它會在主索引鍵索引和 IX_OrderSequence 中插入唯一值。 它會在索引 IX_Status 中插入大量重複的值：指令碼只會產生 8 個相異值。  
  
 BUCKET_COUNT 疑難排解查詢的輸出如下：  
  
|索引名稱|total_bucket_count|empty_bucket_count|empty_bucket_percent|avg_chain_length|max_chain_length|  
|----------------|--------------------------|--------------------------|----------------------------|------------------------|------------------------|  
|IX_Status|8|4|50|65536|65536|  
|IX_OrderSequence|32768|13|0|8|26|  
|PK_SalesOrd_B14003C3F8FB3364|262144|96319|36|1|8|  
  
 請考慮此資料表上的三個雜湊索引：  
  
-   IX_Status：有 50% 的貯體是空的，這是理想的狀況。 不過，平均鏈結長度非常高 (65,536)。 這表示有大量重複的值。 因此，這種情況不適合使用非叢集雜湊索引。 應該改用非叢集索引。  
  
-   IX_OrderSequence：有 0% 的貯體是空的，這個數字過低。 此外，平均鏈結長度為 8。 由於這個索引中的值是唯一的，因此這表示平均有 8 個值對應到每個貯體。 值區計數應該增加。 由於索引鍵擁有 262,144 個唯一值，因此值區計數至少應該為 262,144。 如果預期未來會有所成長，則這個數字應該更高。  
  
-   主索引鍵索引 (PK__SalesOrder…)：有 36% 的貯體是空的，這是理想的狀況。 另外，平均鏈結長度為 1，這也很理想。 不需要變更。  
  
 如需對記憶體最佳化雜湊索引的問題進行疑難排解的詳細資訊，請參閱＜ [針對記憶體最佳化雜湊索引常見效能問題進行疑難排解](../../2014/database-engine/troubleshooting-common-performance-problems-with-memory-optimized-hash-indexes.md)＞。  
  
## <a name="detailed-considerations-for-further-optimization"></a>進一步最佳化的詳細考量  
 本節將概述最佳化值區計數的進一步考量。  
  
 若要達成雜湊索引的最佳效能，請平衡配置給雜湊表的記憶體數量以及索引鍵中的相異值數目。 點查閱的效能和資料表掃描之間也有平衡點：  
  
-   值區計數的值越高，索引中就會有越多空的貯體。 這樣會影響記憶體使用量 (每個貯體 8 個位元組) 和資料表掃描的效能，因為資料表掃描的過程中會掃描每個貯體。  
  
-   值區計數越小，指派給單一貯體的值越多。 這會降低點查閱和插入的效能，因為[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]可能需要周遊尋找搜尋述詞所指定之值的單一值區中的數個值。  
  
 如果值區計數明顯低於唯一索引鍵數目，則將會有許多值對應至每個貯體。 這樣會降低大部分 DML 作業的效能，特別是點查閱 (個別索引鍵的查閱) 和插入作業。 例如，在 WHERE 子句中比對索引鍵資料行的等號比較述詞，您可能會發現 SELECT 查詢以及 UPDATE 與 DELETE 作業的效能不佳。 值區計數過低也會影響資料庫的復原時間，因為索引會在資料庫啟動時重新建立。  
  
### <a name="duplicate-index-key-values"></a>重複的索引鍵值  
 重複值可能會加重雜湊衝突的效能影響。 如果每個索引鍵的重複數目不高，通常不會造成問題。 不過，如果資料表中唯一索引鍵的數目和資料列數目之間的差異擴大，就有可能會產生問題。  
  
 具有相同索引鍵的所有資料列將會進入相同的重複鏈結。 如果同一個貯體中因為雜湊衝突而有多個索引鍵，索引掃描器就一定要先掃描整個重複鏈結找出第一個值，才能找到對應第二個值的第一個資料列。 重複索引鍵也會使記憶體回收更難找出資料列。 比方說，如果索引鍵具 1000 個重複項目，當其中一個資料列遭刪除時，記憶體回收行程就必須掃描 1000 個重複項目的鏈結，才能取消資料列與索引間的連結。 即使找出刪除的查詢使用較有效率的索引 (主索引鍵索引) 尋找資料列，但因為記憶體回收行程需要取消每個索引的連結，也會發生此情況。  
  
 若是雜湊索引，有兩種方式可減少重複的索引鍵值產生的工作：  
  
-   改用非叢集索引。 您可以藉由加入資料行至索引鍵來減少重複，不需要變更任何應用程式。  
  
-   指定非常高的索引值區計數。 例如，唯一索引鍵數目的 20 到 100 倍。 這樣一來就會減少雜湊衝突。  
  
### <a name="small-tables"></a>小型資料表  
 對於較小的資料表而言，記憶體使用量通常不是問題，因為與資料庫整體大小相較之下，索引的大小會很小。  
  
 現在您必須根據想要的效能類型做出選擇：  
  
-   如果索引上相當倚賴效能的作業主要是點查閱和 (或) 插入作業，則適合使用較高的值區計數，如此可降低雜湊衝突的可能性。 最理想的選擇會是資料列數目的三倍以上。  
  
-   如果完整索引掃描是主要倚賴效能的作業，請使用接近索引鍵值實際數目的值區計數。  
  
### <a name="big-tables"></a>大型資料表  
 對於大型資料表而言，記憶體使用量可能成為問題。 例如，有 250 萬個資料列的資料表具有 4 個雜湊索引，每個值區計數為十億，雜湊表的負擔是 4 個索引 * 1 億個貯體\*8 個位元組 = 32 gb 的記憶體使用量。 如果針對每個索引選擇的值區計數為 2500 萬，則雜湊表的總負擔將會是 8 GB。 請注意，這除了 8 個位元組記憶體使用量的每個索引加入至每個個別的資料列，也就是在此案例中應配備 8 gb (4 個索引\*8 個位元組\*250 萬個資料列)。  
  
 完整資料表掃描通常不在 OLTP 工作負載的關鍵效能路徑中。 因此，選擇會介於記憶體使用量與點查閱和插入作業的效能之間：  
  
-   如果記憶體使用量會是問題，請選擇接近索引鍵值數目的值區計數。 值區計數不應該大幅低於索引鍵值數目，因為這樣會影響大部分 DML 作業，以及影響在伺服器重新啟動後復原資料庫所需的時間。  
  
-   對點查閱的效能進行最佳化時，適合使用較高的值區計數，最好是唯一索引值數目的兩倍甚至三倍。 值區計數越高，表示記憶體使用量越高，而且完整索引掃描所需的時間也會越長。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表上的索引](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
