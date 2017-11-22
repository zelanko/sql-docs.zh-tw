---
title: "索引 DDL 作業的磁碟空間需求 | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- temporary disk space [SQL Server]
ms.assetid: 35930826-c870-44c1-a966-a6a4638f62ef
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddf19430350de7403cc3c9d46416cbc6cfa409c1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="disk-space-requirements-for-index-ddl-operations"></a>索引 DDL 作業的磁碟空間需求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  當您建立、重建或卸除索引時，磁碟空間是一個重要的考量。 不足的磁碟空間會降低效能，甚至導致索引作業失敗。 此主題提供了一般資訊，可協助您判斷索引資料定義語言 (DDL) 作業所需的磁碟空間數量。  
  
## <a name="index-operations-that-require-no-additional-disk-space"></a>不需要額外磁碟空間的索引作業  
 下列是不需要額外磁碟空間的索引作業：  
  
-   ALTER INDEX REORGANIZE，但是需要記錄檔空間。  
  
-   DROP INDEX，卸除非叢集索引時。  
  
-   DROP INDEX，離線卸除叢集索引，而不指定 MOVE TO 子句且非叢集索引不存在時。  
  
-   CREATE TABLE (PRIMARY KEY 或 UNIQUE 條件約束)  
  
## <a name="index-operations-that-require-additional-disk-space"></a>需要額外磁碟空間的索引作業  
 所有其他索引 DDL 作業在作業期間都需要使用額外的磁碟空間，並需要永久磁碟空間來儲存新的索引結構。  
  
 當建立新的索引結構時，舊 (來源) 和新 (目標) 結構在適當的檔案和檔案群組中需要用到磁碟空間。 舊結構要到索引建立交易認可時才會取消配置。  
  
 下列索引 DDL 作業會建立新的索引結構，並需要額外的磁碟空間：  
  
-   CREATE INDEX  
  
-   CREATE INDEX WITH DROP_EXISTING  
  
-   ALTER INDEX REBUILD  
  
-   ALTER TABLE ADD CONSTRAINT (PRIMARY KEY 或 UNIQUE)  
  
-   ALTER TABLE DROP CONSTRAINT (PRIMARY KEY 或 UNIQUE) (當條件約束是以叢集索引為基礎時)  
  
-   DROP INDEX MOVE TO (僅適用於叢集索引)。  
  
## <a name="temporary-disk-space-for-sorting"></a>用於排序的暫存磁碟空間  
 除了來源和目標結構需要磁碟空間之外，排序時也需要暫存磁碟空間，除非查詢最佳化工具找到不需要排序的執行計畫。  
  
 如果需要排序，一次只會對一個新索引進行排序。 例如，當您在單一陳述式內重建叢集索引和相關聯的非叢集索引時，會逐一排序索引。 因此，排序所需的額外暫存磁碟空間必須和作業中最大的索引一樣大。 這幾乎都是叢集索引。  
  
 如果 SORT_IN_TEMPDB 選項設為 ON，則最大的索引必須符合 **tempdb**。 雖然此選項會增加建立索引所使用的暫存磁碟空間數量，但只要 **tempdb** 所在的磁碟集與使用者資料庫不同，就可減少建立索引所需的時間。  
  
 如果 SORT_IN_TEMPDB 設為 OFF (預設值)，則每個索引 (包括資料分割索引) 會在其目的地磁碟空間中排序；而且只需要建立新索引結構的磁碟空間。  
  
 如需計算磁碟空間的範例，請參閱＜ [Index Disk Space Example](../../relational-databases/indexes/index-disk-space-example.md)＞。  
  
## <a name="temporary-disk-space-for-online-index-operations"></a>線上索引作業的暫存磁碟空間  
 在線上執行索引作業時，需要額外的暫存磁碟空間。  
  
 如果在線上建立、重建或卸除叢集索引，會建立暫存非叢集索引，以便將舊書籤對應至新書籤。 如果 SORT_IN_TEMPDB 選項設為 ON，則會在 **tempdb**中建立此暫存索引。 如果 SORT_IN_TEMPDB 設為 OFF，會使用與目標索引相同的檔案群組或資料分割結構描述。 暫存對應索引為資料表中的每個資料列都包含一筆記錄，而且其內容結合了舊的和新的書籤資料行，包括唯一識別碼和記錄識別碼，並只包括用於這兩個書籤中之所有資料行的單一副本。 如需線上索引作業的詳細資訊，請參閱 [線上執行索引作業](../../relational-databases/indexes/perform-index-operations-online.md)。  
  
> [!NOTE]  
>  無法對 DROP INDEX 陳述式設定 SORT_IN_TEMPDB 選項。 永遠會在與目標索引相同的檔案群組或資料分割結構描述中，建立暫存對應索引。  
  
 線上索引作業會使用資料列版本設定來隔離索引作業與其他交易所進行的修改影響。 這樣可避免在已讀取的資料列上要求共用鎖定。 線上索引作業期間進行的並行使用者更新和刪除作業，將需要一些空間在 **tempdb**中產生版本記錄。 如需詳細資訊，請參閱 [線上執行索引作業](../../relational-databases/indexes/perform-index-operations-online.md) 。  
  
## <a name="related-tasks"></a>相關工作  
 [Index Disk Space Example](../../relational-databases/indexes/index-disk-space-example.md)  
  
 [索引作業的交易記錄磁碟空間](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
 [估計資料表的大小](../../relational-databases/databases/estimate-the-size-of-a-table.md)  
  
 [估計叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)  
  
 [估計非叢集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
 [估計堆積的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)  
  
## <a name="related-content"></a>相關內容  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 [指定索引的填滿因素](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
  
