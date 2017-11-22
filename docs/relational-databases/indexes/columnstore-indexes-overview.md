---
title: "資料行存放區索引 - 概觀 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
caps.latest.revision: "80"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7ee09bc377beed53a4af3a43111deeec03830e98
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="columnstore-indexes---overview"></a>資料行存放區索引 - 概觀
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  *「資料行存放區索引」* (Columnstore Index) 是儲存及查詢大型資料倉儲事實資料表的標準。 它使用以資料行為基礎的資料儲存和查詢處理，最高可在您的資料倉儲中達到 **10 倍查詢效能** 改善，與未壓縮資料大小相較之下，最高可達到 **10 倍資料壓縮** 。 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，資料行存放區索引可使用作業分析，這是對交易式工作負載執行高效能即時分析的功能。  
  
 跳至案例：  
  
-   [資料倉儲的資料行存放區索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
  
-   [開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
  
## <a name="what-is-a-columnstore-index"></a>何謂資料行存放區索引？  
 *columnstore index* 是使用單欄式資料格式 (稱為「資料行存放區」) 來儲存、擷取及管理資料的一項技術。  
  
### <a name="key-terms-and-concepts"></a>主要詞彙和概念  
 以下是與資料行存放區索引相關聯的主要詞彙和概念。  
  
 資料行存放區  
 「資料行存放區」是以邏輯方式組織成資料表的資料，其中包含資料列和資料行，並且會以資料行取向的資料格式實際儲存。  
  
 資料列存放區  
 「資料列存放區」是以邏輯方式組織成資料表的資料，其中包含資料列和資料行，並且會以資料列取向的資料格式實際儲存。 這是傳統儲存關聯式資料表資料的方式。 在 SQL Server 中，資料列存放區是指其基礎資料格式為堆積、叢集索引或記憶體最佳化資料表的資料表。  
  
> [!NOTE]  
>  在資料行存放區索引的相關討論中，我們使用「資料列存放區」和「資料行存放區」等詞強調資料儲存格式。  
  
 資料列群組  
 「資料列群組」是指同時壓縮成資料行存放區格式的一組資料列。 資料列群組通常包含了每一資料列群組的資料列數目上限，即 1,048,576 個資料列。  
  
 為達到高效能和高壓縮率，資料行存放區索引會將資料表配量為資料列的群組，稱為資料列群組，然後以資料行取向的方式壓縮每個資料列群組。 資料列群組中的資料列數目必須多到足以改善壓縮率，並且少到足以獲益於記憶體中作業。  
  
 資料行區段  
 「資料行區段」是指資料列群組內部的資料行。  
  
-   每一個資料列群組會針對資料表中的每一個資料行包含一個資料行區段。  
  
-   每個資料行區段會各自壓縮成一體並且儲存到實體媒體上。  
  
 ![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
  
 叢集資料行存放區索引  
 「叢集資料行存放區索引」是整個資料表的實體儲存體。  
  
 ![Clustered Columnstore Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Clustered Columnstore Index")  
  
 為了減少資料行區段的分散程度並改善效能，資料行存放區索引可能會暫時將一些資料儲存到叢集索引 (稱為差異存放區)，並儲存已刪除之資料列識別碼的 BTree 清單。 差異存放區作業將由幕後處理。 為了能傳回正確的查詢結果，叢集資料行存放區索引會結合資料行存放區和差異存放區兩方面的查詢結果。  
  
 差異存放區  
 「差異存放區」是僅限搭配叢集資料行存放區索引使用的叢集索引，藉由儲存資料列直到資料列數達到臨界值後移入資料行存放區，來改善資料行存放區的壓縮和效能。  
  
 在大規模的大量載入過程中，大多數資料列會直接進入資料行存放區，而不經過差異存放區。 大量載入結束時，某些資料列可能因為數量太少，而不符合資料列群組 102,400 個資料列的大小下限。 發生這種情況時，最後這些資料列就會進入差異存放區，而不是資料行存放區。 若是少於 102,400 個資料列的小規模大量載入，則所有資料列都將直接進入差異存放區。  
  
 差異存放區一旦達到資料列數目上限，就會隨即關閉。 Tuple Mover 處理序將檢查是否有資料列群組已關閉。 只要一發現已關閉的資料列群組，處理序便會予以壓縮並儲存至資料行存放區。  
  
 非叢集資料行存放區索引  
 「非叢集資料行存放區索引」和叢集資料行存放區索引的功能相同。 差別在於非叢集索引是建立在資料列存放區資料表上的次要索引，而叢集資料行存放區索引則是整個資料表的主要儲存體。  
  
 非叢集索引包含基礎資料表中部分或所有資料列和資料行的複本。 此索引會定義為資料表的一或多個資料行，並具有篩選資料列的選用條件。  
  
 非叢集資料行存放區索引可使用即時作業分析，其中 OLTP 工作負載會使用基礎叢集索引，並同時對資料行存放區索引執行分析。 如需詳細資訊，請參閱 [開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)。  
  
 批次執行  
 「批次執行」是查詢同時處理多個資料列的查詢處理方法。 資料行存放區索引的查詢使用批次模式執行，通常可改善查詢效能 2-4 倍。 批次執行已針對資料行存放區儲存格式最佳化並與其密切整合。 批次模式執行有時又稱為向量式或向量化執行。  
  
##  <a name="benefits"></a> 為什麼應該使用資料行存放區索引？  
 資料行存放區索引可提供很高度的資料壓縮，通常是 10 倍，因此可大幅降低資料倉儲儲存體成本。 此外，它在分析時所提供的效能遠比 Btree 索引還高。 這是資料倉儲和分析工作負載的慣用資料儲存格式。 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，您可以使用資料行存放區索引，對您的作業工作負載進行即時分析。  
  
 資料行存放區索引之所以很快的原因︰  
  
-   資料行會儲存來自相同網域的值，並且通常會有類似的值，因此壓縮率會很高。 這會將您系統中的 IO 瓶頸降到最低或完全排除，並同時大幅降低記憶體耗用量。  
  
-   高壓縮率會透過使用較小的記憶體中耗用量改善查詢效能。 而查詢效能可獲得改善是因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠執行更多記憶體中查詢及資料作業。  
  
-   批次執行藉由同時處理多個資料列來改善查詢效能，通常是 2-4 倍。  
  
-   查詢通常只會選取資料表中的少數資料行，如此可降低讀取實體媒體的總 I/O 量。  
  
## <a name="when-should-i-use-a-columnstore-index"></a>何時應該使用資料行存放區索引？  
 建議使用案例：  
  
-   使用叢集資料行存放區索引，儲存資料倉儲工作負載的事實資料表和大型維度資料表。 這可以改善查詢效能和資料壓縮最多 10 倍。 請參閱 [Columnstore Indexes for Data Warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)。  
  
-   使用非叢集資料行存放區索引，對 OLTP 工作負載執行即時分析。 請參閱 [開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)。  
  
### <a name="how-do-i-choose-between-a-rowstore-index-and-a-columnstore-index"></a>如何在資料列存放區索引與資料行存放區索引之間進行選擇？  
 資料列存放區索引在搜尋資料的查詢、搜尋特定值，或查詢一小段值範圍的效果最佳。 對交易式工作負載使用資料列存放區索引，因為它們通常需要大量資料表搜尋，而不是資料表掃描。  
  
 資料行存放區索引可提升分析查詢的效能，現在可掃描大量資料，特別是大型資料表上的資料。  請在資料倉儲和分析工作負載上 (尤其是在事實資料表上) 使用資料行存放區索引，因為它們通常需要完整資料表掃描，而不是資料表搜尋。  
  
### <a name="can-i-combine-rowstore-and-columnstore-on-the-same-table"></a>我可以將資料列存放區和資料行存放區合併到同一個資料表嗎？  
 是的。 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，您可以在資料列存放區資料表上建立可更新的非叢集資料行存放區索引。 資料行存放區索引會儲存所選資料行的複本，因此您需要額外的空間來存放此複本，但平均可壓縮 10 倍。 如此一來，您就可以同時在資料行存放區索引上執行分析，並在資料列存放區索引上執行交易。 當資料列存放區資料表中的資料變更時，會更新資料行存放區，讓兩個索引會針對相同的資料執行。  
  
 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，您可以在資料行存放區索引上有一或多個非叢集資料列存放區索引。 如此一來，您就可以對基礎資料行存放區執行有效率的資料表搜尋。 其他選項現在也可以使用。 例如，您可以在資料列存放區資料表上使用 UNIQUE 條件約束，強制執行主索引鍵條件約束。 由於非唯一的值將無法插入資料列存放區資料表中，因此 SQL Server 無法將值插入資料行存放區中。  
  
## <a name="metadata"></a>中繼資料  
 資料行存放區索引中的所有資料行都將儲存於中繼資料內成為內含資料行。 資料行存放區索引沒有索引鍵資料行。  
  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
-   [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)  
  
-   [sys.internal_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)  
  
-   [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)  
  
-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md)  
  
-   [sys.dm_column_store_object_pool &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-column-store-object-pool-transact-sql.md)  
  
-   [sys.dm_db_column_store_row_group_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
## <a name="related-tasks"></a>相關工作  
 所有關聯式資料表都會使用資料列存放區作為基礎資料格式，除非您將其指定為叢集資料行存放區索引。 CREATE TABLE 會建立資料列存放區資料表，除非您指定 WITH CLUSTERED COLUMNSTORE INDEX 選項。  
  
 當您使用 CREATE TABLE 陳述式建立資料表時，您可以指定 WITH CLUSTERED COLUMNSTORE INDEX 選項建立資料表作為資料行存放區。 若您已經有一個資料列存放區資料表，並想要將它轉換成資料行存放區，您可以使用 CREATE COLUMNSTORE INDEX 陳述式。 如需範例，請參閱。  
  
|工作|參考主題|注意|  
|----------|----------------------|-----------|  
|建立資料表作為資料行存放區。|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，您可以建立資料表作為叢集資料行存放區索引。 您不需要先建立資料列存放區資料表，再將它轉換成資料行存放區。|  
|建立具有資料行存放區索引的記憶體資料表。|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，您可以建立具有資料行存放區索引的記憶體最佳化資料表。 建立資料表之後，也可以使用 ALTER TABLE ADD INDEX 語法來加入資料行存放區索引。|  
|將資料列存放區資料表轉換成資料行存放區。|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|將現有的堆積或二進位樹狀目錄轉換成資料行存放區。 範例示範如何在執行這項轉換時處理現有的索引及索引名稱。|  
|將資料行存放區資料表轉換成資料列存放區。|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|這通常並非必要，但有時您需要執行這項轉換。 範例示範如何將資料行存放區轉換成堆積或叢集索引。|  
|在資料列存放區資料表上建立資料行存放區索引。|[CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)|資料列存放區資料表可以有一個資料行存放區索引。  從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，資料行存放區索引可以有一個篩選條件。 範例示範基本語法。|  
|為作業分析建立高效能的索引。|[開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)|描述如何建立互補資料行存放區和 Btree 索引，讓 OLTP 查詢使用 Btree 索引，而分析查詢使用資料行存放區索引。|  
|為資料倉儲建立高效能的資料行存放區索引。|[資料倉儲的資料行存放區索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|描述如何在資料行存放區資料表上使用 Btree 索引，建立高效能的資料倉儲查詢。|  
|使用 Btree 索引，在資料行存放區索引上強制執行主索引鍵條件約束。|[資料倉儲的資料行存放區索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)|示範如何合併 Btree 和資料行存放區索引，在資料行存放區索引上強制執行主索引鍵條件約束。|  
|卸除資料行存放區索引|[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)|卸除資料行存放區索引，其使用 Btree 索引所使用的標準 DROP INDEX 語法。 若卸除叢集資料行存放區索引，會將資料行存放區資料表轉換成堆積。|  
|從資料行存放區索引刪除資料列|[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|使用 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) 刪除資料列。<br /><br /> **資料行存放區** 資料列： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將該資料列標示為邏輯刪除，但在重建索引之前，不會回收該資料列的實體儲存體。<br /><br /> **差異存放區** 資料列： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會以邏輯方式實際刪除該資料列。|  
|更新資料行存放區索引中的資料列|[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)|使用 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) 更新資料列。<br /><br /> **資料行存放區** 資料列：  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將該資料列標示為邏輯刪除，然後將更新的資料列插入差異存放區中。<br /><br /> **差異存放區** 資料列： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會更新差異存放區中的該資料列。|  
|將資料載入資料行存放區索引|[資料行存放區索引資料載入](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)||  
|強制將差異存放區中的所有資料列移入資料行存放區。|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) ...REBUILD<br /><br /> [資料行存放區索引重組](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)|ALTER INDEX 搭配 REBUILD 選項會強制將所有資料列移入資料行存放區。|  
|重組資料行存放區索引|[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)|ALTER INDEX … REORGANIZE 會線上重組資料行存放區索引。|  
|合併具有資料行存放區索引的資料表。|[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)||  
  
## <a name="see-also"></a>另請參閱  
 [資料行存放區索引資料載入](~/relational-databases/indexes/columnstore-indexes-data-loading-guidance.md)   
 [資料行存放區索引建立版本功能摘要](~/relational-databases/indexes/columnstore-indexes-what-s-new.md)   
 [資料行存放區索引效能](~/relational-databases/indexes/columnstore-indexes-query-performance.md)   
 [開始使用資料行存放區進行即時作業分析](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
 [資料倉儲的資料行存放區索引](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)   
 [資料行存放區索引重組](~/relational-databases/indexes/columnstore-indexes-defragmentation.md)  
  
  





