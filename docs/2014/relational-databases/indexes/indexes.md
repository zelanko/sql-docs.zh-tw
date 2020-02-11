---
title: 索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58d4d71189598a6fd101e6db0a40b8c8b0a3b903
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63161868"
---
# <a name="indexes"></a>索引
  下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用的索引類型，並提供其他資訊的連結。  
  
|索引類型|描述|其他資訊|  
|----------------|-----------------|----------------------------|  
|雜湊|有了雜湊索引，便會透過記憶體中的雜湊表來存取資料。 雜湊索引會耗用固定數量的記憶體，也就是值區計數的函數。|[使用記憶體最佳化資料表索引的方針](../in-memory-oltp/memory-optimized-tables.md)|  
|記憶體最佳化的非叢集索引|對於已完成記憶體最佳化的非叢集索引，記憶體耗用量是資料列計數和索引鍵資料行大小的函數|[使用記憶體最佳化資料表索引的方針](../in-memory-oltp/memory-optimized-tables.md)|  
|叢集|索引叢集根據叢集索引鍵的順序來排序和儲存資料表或檢視的資料列。 叢集索引將實作成 B 型樹狀索引結構，以根據它們的叢集索引鍵值快速地擷取資料列。|[叢集與非叢集索引說明](clustered-and-nonclustered-indexes-described.md)<br /><br /> [建立叢集索引](create-clustered-indexes.md)|  
|非叢集|非叢集索引可在具有叢集索引的資料表或檢視中、或是堆積中定義。 非叢集索引中的每個索引資料列都含有非叢集鍵值與資料列定位器。 此定位器指向含有鍵值之叢集索引或堆積中的資料列。 索引中的資料列會依據索引鍵值的順序儲存，但除非叢集索引建立在資料表中，否則資料列不一定會依循任何特定的順序排列。|[叢集與非叢集索引說明](clustered-and-nonclustered-indexes-described.md)<br /><br /> [建立非叢集索引](create-nonclustered-indexes.md)|  
|唯一|唯一索引可確保索引鍵不含重複的值，因此資料表或檢視中的每個資料列就某方面而言都是唯一的。<br /><br /> 唯一性可以是叢集與非叢集索引的屬性。|[建立唯一索引](create-unique-indexes.md)|  
|columnstore|記憶體中的資料行存放區索引會使用資料行為基礎的資料儲存和資料行為基礎的查詢處理來儲存及管理資料。<br /><br /> 資料行存放區索引可在主要執行大量載入和唯讀查詢的資料倉儲工作負載中順利運作。 與傳統的資料列導向儲存相較之下，使用資料行存放區索引最高可達到 **10 倍查詢效能** 改善，與未壓縮資料大小相較之下，最高可達到 **7 倍資料壓縮** 。|[Columnstore Indexes Described](columnstore-indexes-described.md)<br /><br /> [使用非叢集資料行存放區索引](../../database-engine/using-nonclustered-columnstore-indexes.md)<br /><br /> [使用叢集資料行存放區索引](../../database-engine/using-clustered-columnstore-indexes.md)|  
|具有內含資料行的索引|除了索引鍵資料行以外，擴充為含有非索引鍵資料行的非叢集索引。|[建立內含資料行的索引](create-indexes-with-included-columns.md)|  
|導出資料行的索引|從其他一個或多個資料行的值，或特定決定性輸入衍生的資料行索引。|[計算資料行的索引](indexes-on-computed-columns.md)|  
|Filtered|最佳化的非叢集索引，特別適合涵蓋從妥善定義的資料子集進行選取的查詢。 篩選索引會使用篩選述詞對資料表中的部分資料列進行索引。 與完整資料表索引相較，設計良好的篩選索引可以提升查詢效能、降低索引維護成本，並降低索引儲存成本。|[建立篩選的索引](create-filtered-indexes.md)|  
|空間|空間索引可以更有效率地在 *geometry* 資料類型之資料行的空間物件 (「空間資料」****) 上執行特定作業。 空間索引會減少需要套用相當耗成本之空間作業的物件數目。|[空間索引概觀](../spatial/spatial-indexes-overview.md)|  
|XML|在 `xml` 資料類型資料行中，一種細分且持續的 XML 二進位大型物件 (BLOB) 表示法。|[XML 索引 &#40;SQL Server&#41;](../xml/xml-indexes-sql-server.md)|  
|全文檢索|一種特殊類型的 Token 式功能索引，由 Microsoft Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所建立與維護。 它可以有效地在字元字串資料中進行複雜字的搜尋。|[擴展全文檢索索引](../search/populate-full-text-indexes.md)|  
  
## <a name="related-tasks"></a>相關工作  
  
## <a name="related-content"></a>相關內容  
 [索引的 SORT_IN_TEMPDB 選項](sort-in-tempdb-option-for-indexes.md)  
  
 [停用索引和條件約束](disable-indexes-and-constraints.md)  
  
 [啟用索引和條件約束](enable-indexes-and-constraints.md)  
  
 [重新命名索引](rename-indexes.md)  
  
 [設定索引選項](set-index-options.md)  
  
 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)  
  
 [重新組織與重建索引](reorganize-and-rebuild-indexes.md)  
  
 [指定索引的填滿因素](specify-fill-factor-for-an-index.md)  
  
## <a name="see-also"></a>另請參閱  
 [叢集與非叢集索引說明](clustered-and-nonclustered-indexes-described.md)  
  
  
