---
title: "資料行存放區索引 - 架構 | Microsoft 文件"
ms.custom: 
ms.date: 01/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 96b8e884-8244-425f-b856-72a8ff6895a6
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 835e3acd76972eef01b4d286cbc1f6ecf6fac605
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="columnstore-indexes---architecture"></a>資料行存放區索引 - 架構
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

了解資料行存放區索引的架構方式。 了解這些基本知識，可讓您更容易理解其他說明有效使用方式的資料行存放區文章。

## <a name="data-storage-uses-columnstore-and-rowstore-compression"></a>使用資料行存放區和資料列存放區壓縮的資料儲存
在資料行存放區索引的相關討論中，我們使用「資料列存放區」和「資料行存放區」等詞強調資料儲存格式。  資料行存放區索引會使用這兩種儲存類型。

 ![Clustered Columnstore Index](../../relational-databases/indexes/media/sql-server-pdw-columnstore-physicalstorage.gif "Clustered Columnstore Index")

- 「資料行存放區」是以邏輯方式組織成資料表的資料，其中包含資料列和資料行，並且會以資料行取向的資料格式實際儲存。
  
資料行存放區索引是以資料行存放區格式實際儲存大部分的資料。 在資料行存放區格式中，資料會以資料行的方式進行壓縮和解壓縮。 這樣就不需要解壓縮每個資料列中查詢未要求的其他值。 如此一來，便可快速掃描大型資料表的整個資料行。 

- 「資料列存放區」是以邏輯方式組織成資料表的資料，其中包含資料列和資料行，並且會以資料列取向的資料格式實際儲存。 這是傳統儲存關聯式資料表資料的方式，例如堆積或叢集 "BTree" 索引。

資料行存放區索引也會以資料列存放區格式實際儲存某些資料列，其稱為差異存放區。 差異存放區 (也稱為差異資料列群組) 是一種保存空間，用來保存數量太少而沒有資格壓縮到資料行存放區的資料列。 每個差異資料列群組都會實作為叢集 BTree 索引。 

- 「差異存放區」是一種保存空間，用來保存數量太少而無法壓縮到資料行存放區的資料列。 差異存放區是資料列存放區。 
  
## <a name="operations-are-performed-on-rowgroups-and-column-segments"></a>作業是在資料列群組和資料行區段上執行

資料行存放區索引會將資料列分組成可管理的單位。 每個單位稱為資料列群組。 為了達到最佳效能，資料列群組中的資料列數量必須多到足以改善壓縮率，並且少到足以獲益於記憶體內部作業。

* 「資料列群組」是一組資料列，資料行存放區索引將對其執行管理和壓縮作業。 

例如，資料行存放區索引會對資料列群組執行下列作業：

* 將資料列群組壓縮到資料行存放區。 對資料列群組內的每個資料行區段執行壓縮。
* 在 ALTER INDEX REORGANIZE 作業期間合併資料列群組。
* 在 ALTER INDEX REBUILD 作業期間建立新的資料列群組。
* 在動態管理檢視 (DMV) 中報告資料列群組健全狀況和片段。

差異存放區是由一個或多個資料列群組所組成，稱為差異資料列群組。 每個差異資料列群組都是叢集 BTree 索引，用來在資料列數量太少而不足以壓縮到資料行存放區時儲存資料列。  

* 「差異資料列群組」是叢集 BTree 索引，用來儲存少量載入和插入，直到資料列群組包含 1,048,576 個資料列或重建索引為止。  當差異資料列群組包含 1,048,576 個資料列時，它會標示為已關閉，並等候稱為 tuple-mover 的處理序將其壓縮到資料行存放區。 


在每個資料列群組中，每個資料行都有一些資料行值。 這些值稱為資料行區段。 當資料行存放區索引壓縮資料列群組時，它會個別壓縮每一個資料行區段。 若要解壓縮整個資料行，資料行存放區索引只需要解壓縮每個資料列群組中的一個資料行區段。

* 「資料行區段」是資料列群組中的資料行值部分。 每一個資料列群組會針對資料表中的每一個資料行包含一個資料行區段。 在每個資料列群組中，每個資料行都有一個資料行區段。| 
  
 ![Column segment](../../relational-databases/indexes/media/sql-server-pdw-columnstore-columnsegment.gif "Column segment")  
 
## <a name="small-loads-and-inserts-go-to-the-deltastore"></a>少量載入和插入會進入差異存放區
藉由一次至少將 102,400 個資料列壓縮到資料行存放區索引，資料行存放區索引可改善資料行存放區壓縮和效能。 為了大量壓縮資料列，資料行存放區索引會在差異存放區中累積少量載入和插入。 差異存放區作業將由幕後處理。 為了能傳回正確的查詢結果，叢集資料行存放區索引會結合資料行存放區和差異存放區兩方面的查詢結果。 

資料列會進入差異存放區的情況：
* 已使用 INSERT INTO VALUES 陳述式插入。
* 位於大量載入結尾，而且數量小於 102,400。
* 已更新。 每項更新的實作方式為刪除和插入。

差異存放區也會儲存已刪除資料列的識別碼清單，已刪除資料列是標示為已刪除，但尚未從資料行存放區中實際刪除的資料列。 

## <a name="when-delta-rowgroups-are-full-they-get-compressed-into-the-columnstore"></a>當差異資料列群組已滿時，即會壓縮到資料行存放區

叢集資料行存放區索引在將資料列群組壓縮到資料行存放區之前，在每個差異資料列群組中最多可收集 1,048,576 個資料列。 如此可改善資料行存放區索引的壓縮。 當差異資料列群組包含 1,048,576 個資料列時，資料行存放區索引會將資料列群組標示為已關閉。 稱為 *tuple-mover* 的背景處理序，會找到每個已關閉的資料列群組，並將其壓縮到資料行存放區中。 

您可以使用 [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) 強制將差異資料列群組壓縮到資料行存放區，以重建或重新組織索引。  請注意，如果在壓縮期間有記憶體不足的壓力，資料行存放區索引可能會減少已壓縮資料列群組中的資料列數量。

## <a name="each-table-partition-has-its-own-rowgroups-and-delta-rowgroups"></a>每個資料表資料分割都有自己的資料列群組和差異資料列群組

叢集索引、堆積和資料行存放區索引中的資料分割概念都相同。 分割資料表作業會根據一系列的資料行值，將資料表分割成較小的資料列群組。 這通常用於管理資料。 例如，您可以針對每一年的資料建立一個資料分割，然後使用資料分割切換將封存資料移至較便宜的儲存體。 資料分割切換適用於資料行存放區，可輕鬆地將資料的資料分割移至另一個位置。

資料列群組一律定義在資料表資料分割內。 當分割資料行存放區索引時，每個資料分割都有自己的壓縮資料列群組和差異資料列群組。

### <a name="each-partition-can-have-multiple-delta-rowgroups"></a>每個資料分割可以有多個差異資料列群組
每個資料分割可以有多個差異資料列群組。 當資料行存放區索引需要在差異資料列群組中新增資料，而差異資料列群組已鎖定時，資料行存放區索引會嘗試取得不同差異資料列群組的鎖定。 如果沒有任何可用的差異資料列群組，資料行存放區索引就會建立新的差異資料列群組。  例如，具有 10 個資料分割的資料表可以輕鬆擁有 20 多個差異資料列群組。 

  
## <a name="you-can-combine-columnstore-and-rowstore-indexes-on-the-same-table"></a>您可以合併相同資料表上的資料行存放區索引和資料列存放區索引
非叢集索引包含基礎資料表中部分或所有資料列和資料行的複本。 此索引會定義為資料表的一或多個資料行，並具有篩選資料列的選用條件。 

從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，您可以在資料列存放區資料表上建立可更新的非叢集資料行存放區索引。 資料行存放區索引會儲存資料的複本，因此您需要額外的儲存空間。 不過，資料行存放區索引中資料的壓縮大小比資料列存放區資料表所需大小還要小。  如此一來，您就可以同時在資料行存放區索引上執行分析，並在資料列存放區索引上執行交易。 當資料列存放區資料表中的資料變更時，會更新資料行存放區，讓兩個索引會針對相同的資料執行。  
  
 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]開始，您可以在資料行存放區索引上有一或多個非叢集資料列存放區索引。 如此一來，您就可以對基礎資料行存放區執行有效率的資料表搜尋。 其他選項現在也可以使用。 例如，您可以在資料列存放區資料表上使用 UNIQUE 條件約束，強制執行主索引鍵條件約束。 由於非唯一的值將無法插入資料列存放區資料表中，因此 SQL Server 無法將值插入資料行存放區中。  
 

## <a name="metadata"></a>中繼資料  
您可以使用這些中繼資料檢視來查看資料行存放區索引的屬性。 其中一些檢視內含其他架構資訊。

請注意，資料行存放區索引中的所有資料行都會儲存到中繼資料內作為內含資料行。 資料行存放區索引沒有索引鍵資料行。  
  
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
  
|  


## <a name="next-steps"></a>後續的步驟
 如需設計資料行存放區索引的指引，請參閱[資料行存放區索引 - 設計指引](../../relational-databases/indexes/columnstore-indexes-design-guidance.md)

