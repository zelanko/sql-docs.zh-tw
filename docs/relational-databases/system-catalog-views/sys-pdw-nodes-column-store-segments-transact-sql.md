---
title: sys.pdw_nodes_column_store_segments (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5982fa99effc211d23c7e92557d96e20d131ad4
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>sys.pdw_nodes_column_store_segments (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含資料行存放區索引中每個資料行的資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|指出資料分割識別碼。 在資料庫中，這是唯一的。|  
|**hobt_id**|**bigint**|具有此資料行存放區索引之資料表的堆積或 B 型樹狀目錄索引 (hobt) 的識別碼。|  
|**column_id**|**int**|資料行存放區資料行的識別碼。|  
|**segment_id**|**int**|資料行區段的識別碼。|  
|**version**|**int**|資料行區段格式的版本。|  
|**encoding_type**|**int**|該區段所使用的編碼類型。|  
|**row_count**|**int**|資料列群組中的列數。|  
|**has_nulls**|**int**|如果資料行區段具有 Null 值，則為 1。|  
|**base_id**|**bigint**|如果使用編碼類型 1 的基底值識別碼。  如果沒有使用編碼類型 1，base_id 是設為 1。|  
|**magnitude**|**float**|如果正在使用編碼類型 1 的範圍。  如果沒有使用編碼類型 1，magnitude 是設為 1。|  
|**primary__dictionary_id**|**int**|主要字典的識別碼。|  
|**secondary_dictionary_id**|**int**|次要字典的識別碼。 如果沒有次要字典，會傳回 -1。|  
|**min_data_id**|**bigint**|資料行區段中的最小資料識別碼。|  
|**max_data_id**|**bigint**|資料行區段中的最大資料識別碼。|  
|**null_value**|**bigint**|用來表示 Null 的值。|  
|**on_disk_size**|**bigint**|區段大小 (以位元組為單位)。|  
|**pdw_node_id**|**int**|唯一識別項[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]附註。|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列查詢會傳回資料行存放區索引之區段的相關資訊。  
  
```sql  
SELECT i.name, p.object_id, p.index_id, i.type_desc,   
    COUNT(*) AS number_of_segments  
FROM sys.column_store_segments AS s   
INNER JOIN sys.partitions AS p   
    ON s.hobt_id = p.hobt_id   
INNER JOIN sys.indexes AS i   
    ON p.object_id = i.object_id  
WHERE i.type = 6  
GROUP BY i.name, p.object_id, p.index_id, i.type_desc ;  
```  
  
 聯結 sys.pdw_nodes_column_store_segments 與其他系統資料表，來判斷資料列計數和磁碟上的區段大小。  
  
```  
SELECT o.name, css.hobt_id, css. column_id, css.pdw_node_id, css.row_count, css.on_disk_size  
FROM sys.pdw_nodes_column_store_segments AS css  
JOIN sys.pdw_nodes_partitions AS pnp  
    ON css.partition_id = pnp.partition_id  
JOIN sys.pdw_nodes_tables AS part  
    ON pnp.object_id = part.object_id   
    AND pnp.pdw_node_id = part.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON part.name = TMap.physical_name  
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
ORDER BY css.hobt_id, css.column_id;  
```  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW SERVER STATE**權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [建立資料行存放區索引 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
  

