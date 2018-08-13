---
title: sys.dm_db_xtp_hash_index_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_hash_index_stats
- sys.dm_db_xtp_hash_index_stats_TSQL
- dm_db_xtp_hash_index_stats
- dm_db_xtp_hash_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_hash_index_stats (dynamic management view)
ms.assetid: 45969884-cd61-48e8-aee5-c725c78e3e4c
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 668dc3ab34159b80f7227bf088b3261a1dad44b7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555528"
---
# <a name="sysdmdbxtphashindexstats-transact-sql"></a>sys.dm_db_xtp_hash_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  這些統計資料有助於了解及調整值區計數。 另外還可用於偵測索引鍵擁有太多重複項目的情況。  
  
 大型平均鏈結長度代表有許多資料列會雜湊處理至相同貯體內。 發生這種情況可能是因為：  
  
-   如果空貯體的數目較低或平均和最大鏈結長度類似，總值區計數就可能過低。 這樣會導致將許多不同的索引鍵雜湊處理至相同貯體。  
  
-   如果空貯體的數目較高或最大鏈結長度相對於平均鏈結長度而言較高，則可能有許多資料列包含重複的索引鍵值，或是索引鍵值扭曲。 所有具有相同索引鍵值的資料列都會雜湊處理為相同貯體，因此該貯體會擁有很長的鏈結長度。  
  
較長的鏈結長度可能對個別資料列上所有 DML 作業的效能造成相當大的影響，包括 SELECT 和 INSERT。 鏈結長度較短且空的值區計數較高時，表示 bucket_count 太高。 這樣會降低索引掃描的效能。  
  
> [!WARNING]
> **sys.dm_db_xtp_hash_index_stats**掃描整個資料表。 因此，如果在資料庫中，有大型資料表**sys.dm_db_xtp_hash_index_stats**可能需要很長時間執行。  
  
如需詳細資訊，請參閱 <<c0> [ 記憶體最佳化資料表的雜湊索引](../../relational-databases/sql-server-index-design-guide.md#hash_index)。  
  
|資料行名稱|類型|描述|  
|-----------------|----------|-----------------|  
|object_id|**int**|父資料表的物件識別碼。|  
|xtp_object_id|**bigint**|記憶體最佳化資料表的識別碼。|  
|index_id|**int**|索引識別碼。|  
|total_bucket_count|**bigint**|索引中雜湊值區的總數。|  
|empty_bucket_count|**bigint**|索引中空雜湊值區的數目。|  
|avg_chain_length|**bigint**|索引中所有雜湊值區的平均資料列鏈結長度。|  
|max_chain_length|**bigint**|雜湊值區中資料列鏈結的最大長度。|  
|xtp_object_id|**bigint**|記憶體中 OLTP 物件識別碼對應到記憶體最佳化的資料表。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW DATABASE STATE 權限。  

## <a name="examples"></a>範例  
  
### <a name="a-troubleshooting-hash-index-bucket-count"></a>A. 疑難排解雜湊索引值區計數

下列查詢可用來針對現有的資料表的雜湊索引值區計數進行疑難排解。 查詢會傳回空值區和所有的雜湊索引的鏈結長度的百分比的統計資料，使用者資料表上。

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
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
``` 

如需有關如何解譯此查詢的結果的詳細資訊，請參閱 <<c0> [ 疑難排解記憶體最佳化資料表的雜湊索引](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)。  

### <a name="b-hash-index-statistics-for-internal-tables"></a>B. 內部資料表的雜湊索引統計資料

某些功能會使用利用雜湊索引，例如記憶體最佳化資料表上的資料行存放區索引的內部資料表。 下列查詢會傳回連結至使用者資料表的內部資料表上的雜湊索引的統計資料。

```sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [user_table],
    ia.type_desc as [internal_table_type],
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM sys.dm_db_xtp_hash_index_stats as h   
  INNER JOIN sys.indexes as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    INNER JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    INNER JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type!=1
  ORDER BY [user_table], [internal_table_type], [index]; 
```

請注意，無法變更內部資料表上索引的 BUCKET_COUNT，因此這個查詢的輸出應該僅被視為具有資訊價值。 您不需要執行任何動作。  

此查詢不會傳回任何資料列，除非您使用會利用內部的資料表上的雜湊索引的功能。 下列為記憶體最佳化的資料表包含資料行存放區索引。 建立此資料表之後, 您會看到上內部資料表的雜湊索引。

```sql
  CREATE TABLE dbo.table_columnstore
  (
    c1 INT NOT NULL PRIMARY KEY NONCLUSTERED,
    INDEX ix_columnstore CLUSTERED COLUMNSTORE
  ) WITH (MEMORY_OPTIMIZED=ON)
```

## <a name="see-also"></a>另請參閱  
 [記憶體最佳化的資料表動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
