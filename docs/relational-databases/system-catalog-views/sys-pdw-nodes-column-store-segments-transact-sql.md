---
title: sys.pdw_nodes_column_store_segments (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/28/2018
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
author: hirokib
ms.author: elbutter
manager: jrj
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c98898560d4b2f523974065831f0d316a390f7b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682526"
---
# <a name="syspdwnodescolumnstoresegments-transact-sql"></a>sys.pdw_nodes_column_store_segments & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

包含資料行存放區索引中每個資料行的資料列。  

| 資料行名稱                 | 資料類型  | 描述                                                  |
| --------------------------- | ---------- | ------------------------------------------------------------ |
| **partition_id**            | **bigint** | 指出資料分割識別碼。 在資料庫中，這是唯一的。     |
| **hobt_id**                 | **bigint** | 具有此資料行存放區索引之資料表的堆積或 B 型樹狀目錄索引 (hobt) 的識別碼。 |
| **column_id**               | **int**    | 資料行存放區資料行的識別碼。                                |
| **segment_id**              | **int**    | 資料行區段的識別碼。 回溯相容性，資料行名稱會繼續可呼叫 segment_id，即使這是資料列群組識別碼。 可唯一識別區段，使用 < hobt_id，sys.partitions、 column_id >、 < segment_id >。 |
| **version**                 | **int**    | 資料行區段格式的版本。                        |
| **encoding_type**           | **int**    | 該區段所使用的編碼類型：<br /><br /> 1 = VALUE_BASED-非字串/二進位與沒有字典 （類似於一些內部的變化與 4）<br /><br /> 2 = VALUE_HASH_BASED-字典中的常見值的非字串/二進位資料行<br /><br /> 3 = STRING_HASH_BASED-字典中的常見值的二進位字串/資料行<br /><br /> 4 = STORE_BY_VALUE_BASED-非字串/二進位與沒有字典<br /><br /> 5 = STRING_STORE_BY_VALUE_BASED-字串/二進位檔使用沒有字典<br /><br /> 所有編碼方式的位元封裝執行長度編碼盡可能利用。 |
| **row_count**               | **int**    | 資料列群組中的列數。                             |
| **has_nulls**               | **int**    | 如果資料行區段具有 Null 值，則為 1。                     |
| **base_id**                 | **bigint** | 如果正在使用編碼類型 1 的基底值識別碼。  如果未使用編碼類型 1，base_id 設為 1。 |
| **大小**               | **float**  | 如果正在使用編碼類型 1 的範圍。  如果未使用編碼類型 1，範圍是設定為 1。 |
| **primary__dictionary_id**  | **int**    | 主要字典的識別碼。 為非零的值會指向本機字典中目前的區段 （也就是資料列群組） 此資料行。 -1 值表示沒有本機的字典，此區段。 |
| **secondary_dictionary_id** | **int**    | 次要字典的識別碼。 為非零的值會指向本機字典中目前的區段 （也就是資料列群組） 此資料行。 -1 值表示沒有本機的字典，此區段。 |
| **min_data_id**             | **bigint** | 在 資料行區段的最小資料識別碼。                       |
| **max_data_id**             | **bigint** | 資料行區段中的最大資料識別碼。                       |
| **null_value**              | **bigint** | 用來表示 Null 的值。                               |
| **on_disk_size**            | **bigint** | 區段大小 (以位元組為單位)。                                    |
| **pdw_node_id**             | **int**    | 唯一識別碼[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]節點。 |

## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

加入 sys.pdw_nodes_column_store_segments 與其他系統資料表，以判斷每個邏輯資料表的資料行存放區區段數目。 

```sql
SELECT  sm.name           as schema_nm
,       tb.name           as table_nm
,       nc.name           as col_nm
,       nc.column_id
,       COUNT(*)          as segment_count
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb                   ON  sm.[schema_id]          = tb.[schema_id]
JOIN    sys.[pdw_table_mappings] mp       ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt         ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[pdw_nodes_partitions] np     ON  np.[object_id]          = nt.[object_id]
                                          AND np.[pdw_node_id]        = nt.[pdw_node_id]
                                          AND np.[distribution_id]    = nt.[distribution_id]
JOIN    sys.[pdw_nodes_columns] nc        ON  np.[object_id]          = nc.[object_id]
                                          AND np.[pdw_node_id]        = nc.[pdw_node_id]
                                          AND np.[distribution_id]    = nc.[distribution_id]
JOIN    sys.[pdw_nodes_column_store_segments] rg  ON  rg.[partition_id]         = np.[partition_id]
                                                      AND rg.[pdw_node_id]      = np.[pdw_node_id]
                                                      AND rg.[distribution_id]  = np.[distribution_id]
                                                      AND rg.[column_id]        = nc.[column_id]
GROUP BY    sm.name
,           tb.name
,           nc.name
,           nc.column_id  
ORDER BY    table_nm
,           nc.column_id
,           sm.name
```

## <a name="permissions"></a>Permissions  
 需要 **VIEW SERVER STATE** 權限。  

## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [建立資料行存放區索引&#40;Transact SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)   
 [sys.pdw_nodes_column_store_dictionaries &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  

  

