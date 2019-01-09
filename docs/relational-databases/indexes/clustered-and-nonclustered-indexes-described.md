---
title: 叢集與非叢集索引說明 | Microsoft 文件
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- query optimizer [SQL Server], index usage
- index concepts [SQL Server]
ms.assetid: b7d6b323-728d-4763-a987-92e6292f6f7a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1ce02d6d6c177eec37a8a2279931f454368f3e54
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210687"
---
# <a name="clustered-and-nonclustered-indexes-described"></a>叢集與非叢集索引說明
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  索引是一種與資料表或檢視有關的磁碟內存結構，它會加快從該資料表或檢視中擷取資料列的速度。 索引中包含從資料表或檢視中一或多個資料行建出的索引鍵。 這些索引鍵儲存在結構中 (B 型樹狀目錄)，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以快速有效地找到與索引鍵值相關的一或多個資料列。  
  
 資料表或檢視可包含下列類型的索引：  
  
-   叢集  
  
    -   叢集索引將資料表或檢視中的資料列依其索引鍵值排序與儲存。 這些就是索引定義中包含的資料行。 因為資料列本身只能以一種順序排序，所以每個資料表只能有一個叢集索引。  
  
    -   只有當資料表包含叢集索引時，資料表中的資料列才會以排序順序儲存。 當資料表有叢集索引時，資料表又稱為叢集資料表。 如果資料表沒有任何叢集索引，它的資料列就儲存在未排序的結構中，這個結構稱為堆積。  
  
-   非叢集  
  
    -   非叢集索引有一個與資料列完全分開的結構。 非叢集索引包含非叢集索引鍵值，而每個索引鍵值項目都有一個指標，指向包含索引鍵值的資料列。  
  
    -   從非叢集索引中的索引列指向資料列的指標被稱為資料列定位器。 資料列定位器的結構須視資料頁儲存在堆積或叢集資料表而定。 若是堆積，資料列定位器是指向資料列的指標。 若是叢集資料表，資料列定位器就是叢集索引鍵。  
  
    -   您可以將非索引鍵之資料行新增至非叢集索引的分葉層級中，以規避現有索引鍵的限制，並執行完全涵蓋的索引查詢。 如需詳細資訊，請參閱 [建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。 如需索引碼限制的詳細資料，請參閱 [SQL Server 的最大容量規格](../../sql-server/maximum-capacity-specifications-for-sql-server.md)。 
  
 叢集與非叢集索引都可以是唯一的。 這表示任何兩個資料列不得以相同的值做為索引鍵。 否則，索引就不是唯一的，那麼多個資料列就可以共用同一個索引鍵值。 如需詳細資訊，請參閱 [建立唯一索引](../../relational-databases/indexes/create-unique-indexes.md)。  
  
 每當修改資料表的資料時，就會自動維護資料表或檢視的索引。  
  
 如需其他類型的特殊用途索引，請參閱 [索引](../../relational-databases/indexes/indexes.md) 。  
  
## <a name="indexes-and-constraints"></a>索引與條件約束  
 在資料表的資料行上定義 PRIMARY KEY 與 UNIQUE 條件約束時，會自動建立索引。 例如，當您建立資料表和識別特定資料行做為主索引鍵時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會自動為該資料行建立 PRIMARY KEY 條件約束與索引。 如需相關資訊，請參閱 [建立主索引鍵](../../relational-databases/tables/create-primary-keys.md) 及 [建立唯一的條件約束](../../relational-databases/tables/create-unique-constraints.md)。  
  
## <a name="how-indexes-are-used-by-the-query-optimizer"></a>查詢最佳化工具用索引  
 設計精良的索引可以降低磁碟 I/O 作業並耗用較少的系統資源，因此可改善查詢效能。 索引對於包含 SELECT、UPDATE、DELETE 或 MERGE 陳述式的各種查詢非常有用。 請考慮在 `SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250` 資料庫中的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 查詢。 當執行此查詢時，查詢最佳化工具會評估每個擷取資料的可用方法，並選取最有效的方法。 該方法可以是資料表掃描，或是掃描一或多個索引 (如果存在的話)。  
  
 當執行資料表掃描時，查詢最佳化工具可以讀取資料表中的所有資料列，並擷取符合查詢條件的資料列。 資料表掃描將產生許多磁碟 I/O 作業，而且可能需要大量資源。 不過例如，如果查詢的結果集有很高的百分比是源自於資料表的資料列，則資料表掃描可能是最有效率的方法。  
  
 當查詢最佳化工具使用索引時，它會搜尋索引鍵資料行、尋找查詢所需的資料列之儲存位置，並從該位置擷取符合的資料列。 一般而言，搜尋索引會比搜尋資料表更快，因為與資料表不同的是，索引的每個資料列通常包含非常少的資料行，而且資料列為排序的順序。  
  
 查詢最佳化工具在執行查詢時通常會選取最有效率的方法。 不過，如果沒有可用的索引，則查詢最佳化工具就必須使用資料表掃描。 您的工作是設計和建立最符合您環境的索引，因此查詢最佳化工具將會從要選取的索引中選取最有效率的索引。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) 協助您分析資料庫環境並選取適當的索引。  
  
> [!IMPORTANT] 
> 如需索引設計指導方針和本質的詳細資訊，請參閱 [SQL Server 索引設計指南](../../relational-databases/sql-server-index-design-guide.md)。

## <a name="related-content"></a>相關內容  
 [SQL Server 索引設計指南](../../relational-databases/sql-server-index-design-guide.md)     
 [建立叢集索引](../../relational-databases/indexes/create-clustered-indexes.md)  
 [建立非叢集索引](../../relational-databases/indexes/create-nonclustered-indexes.md)  
  
  
