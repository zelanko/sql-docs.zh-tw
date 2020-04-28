---
title: 描述的資料行存放區索引 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
author: mikeraymsft
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6220d6650d2be81cad3f38862ba74213219a28a0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175923"
---
# <a name="columnstore-indexes-described"></a>Columnstore Indexes Described
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] *記憶體*內部資料行存放區索引會使用以資料行為基礎的資料儲存和資料行為基礎的查詢處理來儲存和管理資料。 資料行存放區索引可在主要執行大量載入和唯讀查詢的資料倉儲工作負載中順利運作。 與傳統的資料列導向儲存相較之下，使用資料行存放區索引最高可達到 **10 倍查詢效能** 改善，與未壓縮資料大小相較之下，最高可達到 **7 倍資料壓縮** 。

> [!NOTE]
>  我們將叢集資料行存放區索引視為儲存大型資料倉儲事實資料表的標準，並期望它能廣泛用於資料倉儲案例中。 由於叢集資料行存放區索引可更新，工作負載可以執行大量的插入、更新和刪除作業。

## <a name="contents"></a>內容

-   [基本概念](#basics)

-   [載入資料](#dataload)

-   [效能秘訣](#performance)

-   [相關工作和主題](#related)

##  <a name="basics"></a><a name="basics"></a>操作
 *columnstore index* 是使用單欄式資料格式 (稱為「資料行存放區」) 來儲存、擷取及管理資料的一項技術。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 同時支援叢集和非叢集資料行存放區索引。 此兩者所用記憶體中的資料行存放區技術相同，但在用途和支援的功能上有所差異。

###  <a name="benefits"></a><a name="benefits"></a>各種
 資料行存放區索引可在大部分對大型資料集執行分析的唯讀查詢中順利運作。 這一類通常是資料倉儲工作負載所使用的查詢。 資料行存放區索引對於使用完整資料表掃描的查詢可帶來極高的效能增益，但若查詢是要查找資料搜尋特定的值則不適用。

 資料行存放區索引的優點：

-   資料行經常擁有類似的資料，而導致高壓縮率。

-   高壓縮率會透過使用較小的記憶體中耗用量改善查詢效能。 而查詢效能可獲得改善是因為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 能夠執行更多記憶體中查詢及資料作業。

-   SQL Server 加入了新的查詢執行機制，稱為批次模式執行，能夠大量地降低 CPU 使用率。 批次模式執行已針對資料行存放區儲存格式最佳化並與其密切整合。 批次模式執行有時又稱為向量式或向量化執行。

-   查詢通常只會選取資料表中的少數資料行，如此可降低讀取實體媒體的總 I/O 量。

### <a name="columnstore-versions"></a>資料行存放區版本
 SQL Server 2012、SQL Server 2012 Parallel Data Warehouse 和 SQL Server 2014 都是使用資料行存放區索引以加速常用的資料倉儲查詢。 SQL Server 2012 導入了兩項新功能：非叢集資料行存放區索引，還有以所謂的「批次」為單位來處理資料的向量式查詢執行功能。 SQL Server 2014 除了有 SQL Server 2012 的功能外，另又導入可更新的叢集資料行存放區索引。

### <a name="key-characteristics"></a>主要特性

||
|-|
|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。|

 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，叢集資料行存放區索引：

-   由 Enterprise、Developer 及 Evaluation Edition 提供。

-   可更新。

-   是整個資料表的主要儲存方法。

-   沒有索引鍵資料行。 所有資料行都是內含資料行。

-   這是資料表上唯一的索引。 不可與任何其他索引合併。

-   可設定為使用資料行存放區或資料行存放區封存壓縮。

-   不會實際以排序順序儲存資料行。 而是儲存資料以改善壓縮和效能。

||
|-|
|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。|

 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，非叢集資料行存放區索引：

-   可對叢集索引或堆積中的資料行子集建立索引。 例如，可以對常用的資料行建立索引。

-   需要額外的儲存體將資料行的副本儲存到索引中。

-   會藉由重建索引或將資料分割切換入和移出來進行更新。它無法使用 DML 作業（例如 insert、update 和 delete）進行更新。

-   可與資料表上的其他索引合併。

-   可設定為使用資料行存放區或資料行存放區封存壓縮。

-   不會實際以排序順序儲存資料行。 而是儲存資料以改善壓縮和效能。 建立資料行存放區索引之前不需要預先排序資料，但可改善資料行存放區壓縮。

###  <a name="key-concepts-and-terms"></a><a name="Concepts"></a>重要概念和詞彙
 以下是與資料行存放區索引相關聯的主要詞彙和概念。

 資料行存放區索引資料行存放區*索引*是一項技術，可使用單欄式資料格式（稱為「資料行存放區」）來儲存、抓取和管理 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 同時支援叢集和非叢集資料行存放區索引。 此兩者所用記憶體中的資料行存放區技術相同，但在用途和支援的功能上有所差異。

 資料行存放*區是以*邏輯方式組織成具有資料列和資料行的資料表，並實際儲存成資料行取向的資料格式。

 rowstore *rowstore*是以邏輯方式組織成具有資料列和資料行的資料表，然後實際儲存為數據列取向資料格式的資料。 這是傳統儲存關聯式資料表資料的方式。

 資料列群組和資料行區段：若要取得高效能和高壓縮率，資料行存放區索引會將資料表配量為數據列群組（稱為資料列群組），然後以資料行取向的方式壓縮每個資料列群組。 資料列群組中的資料列數目必須多到足以改善壓縮率，並且少到足以獲益於記憶體中作業。

 資料列群組*a 資料*列群組是一組會同時壓縮成資料行存放區格式的資料列。

 資料行區段：資料*行區段*是資料列群組內的資料行。

-   資料列群組通常包含了每一資料列群組的資料列數目上限，即 1,048,576 個資料列。

-   每一個資料列群組會針對資料表中的每一個資料行包含一個資料行區段。

-   每個資料行區段會各自壓縮成一體並且儲存到實體媒體上。

 ![資料行區段](../../database-engine/media/sql-server-pdw-columnstore-columnsegment.gif "資料行區段")

 非叢集資料行存放區索引：非叢集資料行存放區*索引*是在現有叢集索引或堆積資料表上建立的唯讀索引。 其包含了資料行子集的副本，截至包括資料表中的所有資料行。 當資料表包含非叢集資料行存放區索引時，這是唯讀的。

 非叢集資料行存放區索引讓您單憑資料行存放區索引既可執行分析查詢，同時又能對原始資料表執行唯讀作業。

 ![非叢集資料行存放區索引](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage-nonclustered.gif "非叢集資料行存放區索引")

 叢集資料行存放區索引叢集資料行存放區*索引*是整個資料表的實體儲存體，而且是資料表的唯一索引。 叢集索引可更新。 您可以對索引執行插入、刪除和更新作業，還可將資料大量載入索引。

 ![叢集資料行存放區索引](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage.gif "叢集資料行存放區索引")

 為了減少資料行區段的片段化情況並改善效能，資料行存放區索引可能會暫時將一些資料儲存到資料列存放區資料表 (稱為差異存放區)，加上 B 型樹狀目錄含有已刪除之資料列的識別碼。 差異存放區作業將由幕後處理。 為了能傳回正確的查詢結果，叢集資料行存放區索引會結合資料行存放區和差異存放區兩方面的查詢結果。

 差異存放區僅搭配叢集資料行存放區索引使用，*差異存放區*是儲存資料列的 rowstore 資料表，直到資料列數目夠大，才能移入資料行存放區。 差異存放區搭配叢集資料行存放區索引使用，可改善載入作業及其他 DML 作業的效能。

 在大規模的大量載入過程中，大多數資料列會直接進入資料行存放區，而不經過差異存放區。 大量載入結束時，某些資料列可能因為數量太少，而不符合資料列群組 102,400 個資料列的大小下限。 發生這種情況時，最後這些資料列就會進入差異存放區，而不是資料行存放區。 若是少於 102,400 個資料列的小規模大量載入，則所有資料列都將直接進入差異存放區。

 差異存放區一旦達到資料列數目上限，就會隨即關閉。 Tuple 移動處理序將檢查是否有資料列群組已關閉。 只要一發現已關閉的資料列群組，處理序便會予以壓縮並儲存至資料行存放區。

##  <a name="loading-data"></a><a name="dataload"></a>載入資料

###  <a name="loading-data-into-a-nonclustered-columnstore-index"></a><a name="dataload_nci"></a>將資料載入非叢集資料行存放區索引
 若要將資料載入非叢集資料行存放區索引，請先將資料載入至儲存為堆積或叢集索引的傳統 rowstore 資料表，然後再建立具有 Create 資料行存放區索引[&#40;transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)的非叢集資料行存放區索引。

 ![將資料載入資料行存放區索引](../../database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "將資料載入資料行存放區索引")

 凡是具有非叢集資料行存放區索引的資料表，直到卸除或停用索引之前都是唯讀的。 若要更新資料表和非叢集資料行存放區索引，您可以將資料分割切換入和移出。您也可以停用索引、更新資料表，然後重建索引。

 如需詳細資訊，請參閱＜ [Using Nonclustered Columnstore Indexes](indexes.md)＞。

###  <a name="loading-data-into-a-clustered-columnstore-index"></a><a name="dataload_cci"></a>將資料載入叢集資料行存放區索引
 ![載入叢集資料行存放區索引](../../database-engine/media/sql-server-pdw-columnstore-loadprocess.gif "載入叢集資料行存放區索引")

 如圖中所示，若要將資料載入叢集資料行存放區索引中， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：

1.  將最大大小的資料列群組直接插入資料行存放區中。 資料載入時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會依先到先處理的順序將資料列指派至開放的資料列群組中。

2.  每個資料列群組達到其大小的上限後， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：

    1.  將資料列群組標示為 CLOSED。

    2.  略過差異存放區。

    3.  利用資料行存放區壓縮對每個含有資料列群組的資料行區段進行壓縮。

    4.  實際將每個壓縮的資料行區段儲存到資料行存放區。

3.  將其餘資料列插入資料行存放區或差異存放區，如下所示：

    1.  如果資料列數符合每個資料列群組的資料列數下限需求，則會將資料列加入至資料行存放區。

    2.  如果資料列數低於每個資料列群組的資料列數下限，則會將資料列加入至差異存放區。

 如需有關差異存放區各項工作和程序的詳細資訊，請參閱＜ [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md)＞。

##  <a name="performance-tips"></a><a name="performance"></a>效能秘訣

### <a name="plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>規劃足夠的記憶體以平行建立資料行存放區索引
 除非記憶體受到限制，資料行存放區索引的建立預設都是平行作業。 平行建立索引比循序建立索引需要更多的記憶體。 在記憶體很寬裕的情況下，建立資料行存放區索引花費的時間大約是根據相同的資料行建構 B 型樹狀目錄的 1.5 倍。

 建立資料行存放區索引所需的記憶體取決於資料行數目、字串資料行的數目、平行處理原則的程度 (DOP) 和資料的特性。 例如，假設您的資料表少於一百萬個資料列，SQL Server 便只會使用單一執行緒來建立資料行存放區索引。

 如果資料表的資料列數目超過一百萬個，但是 SQL Server 無法取得足夠的記憶體授權可使用 MAXDOP 建立索引，SQL Server 則會視需要自動降低 MAXDOP 以符合所提供的記憶體授權。  在某些情況下若記憶體受到限制，DOP 就必須降至 1 才能建立索引。

##  <a name="related-tasks-and-topics"></a><a name="related"></a>相關工作與主題

### <a name="nonclustered-columnstore-indexes"></a>非叢集資料行存放區索引
 如需相關的一般工作，請參閱＜ [Using Nonclustered Columnstore Indexes](../../database-engine/using-nonclustered-columnstore-indexes.md)＞。

-   [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)

-   [ALTER INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/alter-index-transact-sql) with REBUILD。

-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)

### <a name="clustered-columnstore-indexes"></a>叢集資料行存放區索引
 如需相關的一般工作，請參閱＜ [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md)＞。

-   [建立叢集資料行存放區索引 &#40;Transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)

-   [ALTER INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/alter-index-transact-sql) with REBUILD 或重新組織。

-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)

-   [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)

-   [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)

-   [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)

### <a name="metadata"></a>中繼資料
 資料行存放區索引中的所有資料行都將儲存於中繼資料內成為內含資料行。 資料行存放區索引沒有索引鍵資料行。

-   [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)

-   [sys.index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)

-   [sys.partitions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql)

-   [sys.column_store_segments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-segments-transact-sql)

-   [sys.column_store_dictionaries &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql)

-   [sys.column_store_row_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql)


