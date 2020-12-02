---
description: 索引
title: 索引 | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b8487f821b698974744fdc18453a2a5c8285d889
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88408004"
---
# <a name="indexes"></a>索引
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

## <a name="available-index-types"></a>可用的索引類型
下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用的索引類型，並提供其他資訊的連結。  
  
|索引類型|Description|其他資訊|  
|----------------|-----------------|----------------------------|  
|雜湊|有了雜湊索引，便會透過記憶體中的雜湊表來存取資料。 雜湊索引會耗用固定數量的記憶體，也就是值區計數的函數。|[使用記憶體最佳化資料表索引的方針](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)<br /><br /> [雜湊索引設計指導方針](../../relational-databases/sql-server-index-design-guide.md#hash_index)|  
|記憶體最佳化的非叢集|對於已完成記憶體最佳化的非叢集索引，記憶體耗用量是資料列計數和索引鍵資料行大小的函數|[使用記憶體最佳化資料表索引的方針](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)<br /><br /> [記憶體最佳化的非叢集索引設計指導方針](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)|  
|叢集|索引叢集根據叢集索引鍵的順序來排序和儲存資料表或檢視的資料列。 叢集索引將實作成 B 型樹狀索引結構，以根據它們的叢集索引鍵值快速地擷取資料列。|[叢集與非叢集索引說明](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [建立叢集索引](../../relational-databases/indexes/create-clustered-indexes.md)<br /><br /> [叢集索引設計指導方針](../../relational-databases/sql-server-index-design-guide.md#Clustered)|  
|非叢集|非叢集索引可在具有叢集索引的資料表或檢視中、或是堆積中定義。 非叢集索引中的每個索引資料列都含有非叢集鍵值與資料列定位器。 此定位器指向含有鍵值之叢集索引或堆積中的資料列。 索引中的資料列會依據索引鍵值的順序儲存，但除非叢集索引建立在資料表中，否則資料列不一定會依循任何特定的順序排列。|[叢集與非叢集索引說明](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [建立非叢集索引](../../relational-databases/indexes/create-nonclustered-indexes.md)<br /><br /> [非叢集索引設計指導方針](../../relational-databases/sql-server-index-design-guide.md#Nonclustered)|  
|唯一|唯一索引可確保索引鍵不含重複的值，因此資料表或檢視中的每個資料列就某方面而言都是唯一的。<br /><br /> 唯一性可以是叢集與非叢集索引的屬性。|[建立唯一索引](../../relational-databases/indexes/create-unique-indexes.md)<br /><br /> [唯一索引設計指導方針](../../relational-databases/sql-server-index-design-guide.md#Unique)|  
|columnstore|記憶體中的資料行存放區索引會使用資料行為基礎的資料儲存和資料行為基礎的查詢處理來儲存及管理資料。<br /><br /> 資料行存放區索引可在主要執行大量載入和唯讀查詢的資料倉儲工作負載中順利運作。 與傳統的資料列導向儲存相較之下，使用資料行存放區索引最高可達到 **10 倍查詢效能** 改善，與未壓縮資料大小相較之下，最高可達到 **7 倍資料壓縮** 。|[資料行存放區索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)<br /><br /> [資料行存放區索引設計指導方針](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)|  
|具有內含資料行的索引|除了索引鍵資料行以外，擴充為含有非索引鍵資料行的非叢集索引。|[建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)|  
|導出資料行的索引|從其他一個或多個資料行的值，或特定決定性輸入衍生的資料行索引。|[計算資料行的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)|  
|Filtered|最佳化的非叢集索引，特別適合涵蓋從妥善定義的資料子集進行選取的查詢。 篩選索引會使用篩選述詞對資料表中的部分資料列進行索引。 與完整資料表索引相較，設計良好的篩選索引可以提升查詢效能、降低索引維護成本，並降低索引儲存成本。|[建立篩選的索引](../../relational-databases/indexes/create-filtered-indexes.md)<br /><br /> [篩選索引設計指導方針](../../relational-databases/sql-server-index-design-guide.md#Filtered)|  
|空間|空間索引可以更有效率地在 **geometry** 資料類型之資料行的空間物件 (「空間資料」) 上執行特定作業。 空間索引會減少需要套用相當耗成本之空間作業的物件數目。|[空間索引概觀](../../relational-databases/spatial/spatial-indexes-overview.md)|  
|XML|在 **xml** 資料類型資料行中，一種細分且持續的 XML 二進位大型物件 (BLOB) 表示法。|[XML 索引 &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)|  
|全文檢索|一種特殊類型的 Token 式功能索引，由 Microsoft Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所建立與維護。 它可以有效地在字元字串資料中進行複雜字的搜尋。|[擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)|  
  
## <a name="related-content"></a>相關內容  
 [SQL Server 索引設計指南](../../relational-databases/sql-server-index-design-guide.md)      
 [索引的 SORT_IN_TEMPDB 選項](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)     
 [停用索引和條件約束](../../relational-databases/indexes/disable-indexes-and-constraints.md)     
 [啟用索引和條件約束](../../relational-databases/indexes/enable-indexes-and-constraints.md)    
 [重新命名索引](../../relational-databases/indexes/rename-indexes.md)     
 [設定索引選項](../../relational-databases/indexes/set-index-options.md)     
 [索引 DDL 作業的磁碟空間需求](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)     
 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)     
 [指定索引的填滿因素](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)     
 [分頁與範圍架構指南](../../relational-databases/pages-and-extents-architecture-guide.md)     
 [叢集與非叢集索引說明](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)     
  
