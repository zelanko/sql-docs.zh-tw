---
title: sys.databases pdw_nodes_column_store_segments （Transact-sql）
ms.custom: seo-dt-2019
ms.date: 03/28/2018
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e2fdf8e9-1b74-4682-b2d4-c62aca053d7f
author: julieMSFT
ms.author: jrasnick
manager: jrj
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: bea8e0d51b2918d7280f4afdb8b9d02f6b757827
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401675"
---
# <a name="syspdw_nodes_column_store_segments-transact-sql"></a>sys.databases pdw_nodes_column_store_segments （Transact-sql）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

包含資料行存放區索引中每個資料行的資料列。

| 資料行名稱                 | 資料類型  | 描述                                                  |
| :-------------------------- | :--------- | :----------------------------------------------------------- |
| **partition_id**            | **Bigint** | 指出資料分割識別碼。 在資料庫中，這是唯一的。     |
| **hobt_id**                 | **Bigint** | 具有此資料行存放區索引之資料表的堆積或 B 型樹狀目錄索引 (hobt) 的識別碼。 |
| **column_id**               | **int**    | 資料行存放區資料行的識別碼。                                |
| **segment_id**              | **int**    | 資料行區段的識別碼。 為了回溯相容性，即使這是資料列群組識別碼，仍會繼續呼叫資料行名稱 segment_id。 您可以使用 <hobt_id、partition_id、column_id> <segment_id> 來唯一識別區段。 |
| **版本**                 | **int**    | 資料行區段格式的版本。                        |
| **encoding_type**           | **int**    | 用於該區段的編碼類型：<br /><br /> 1 = VALUE_BASED-不含字典的非字串/二進位（類似于4，有一些內部變體）<br /><br /> 2 = VALUE_HASH_BASED-字典中具有通用值的非字串/二進位資料行<br /><br /> 3 = 具有字典中通用值的 STRING_HASH_BASED 字串/二進位資料行<br /><br /> 4 = STORE_BY_VALUE_BASED-不含字典的非字串/二進位<br /><br /> 5 = 不含字典的 STRING_STORE_BY_VALUE_BASED 字串/二進位檔<br /><br /> 所有編碼會盡可能利用位封裝和執行長度編碼。 |
| **row_count**               | **int**    | 資料列群組中的列數。                             |
| **has_nulls**               | **int**    | 如果資料行區段具有 Null 值，則為 1。                     |
| **base_id**                 | **Bigint** | 如果正在使用編碼類型1，則為基底值識別碼。  如果未使用編碼類型1，base_id 會設定為1。 |
| **magnitude**               | **float**  | 如果正在使用編碼類型1，則為大小。  如果未使用編碼類型1，則會將 [大小] 設定為1。 |
| **primary__dictionary_id**  | **int**    | 主要字典的識別碼。 非零值指向目前區段中這個資料行的本機字典（也就是資料列群組）。 值為-1 表示沒有此區段的本機字典。 |
| **secondary_dictionary_id** | **int**    | 次要字典的識別碼。 非零值指向目前區段中這個資料行的本機字典（也就是資料列群組）。 值為-1 表示沒有此區段的本機字典。 |
| **min_data_id**             | **Bigint** | 資料行區段中的最小資料識別碼。                       |
| **max_data_id**             | **Bigint** | 資料行區段中的最大資料識別碼。                       |
| **null_value**              | **Bigint** | 用來表示 Null 的值。                               |
| **on_disk_size**            | **Bigint** | 區段大小 (以位元組為單位)。                                    |
| **pdw_node_id**             | **int**    | [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]節點的唯一識別碼。 |
| &nbsp; | &nbsp; | &nbsp; |

## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

將 pdw_nodes_column_store_segments sys.databases 與其他系統資料表聯結，以判斷每個邏輯資料表的資料行存放區區段數目。

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
,           sm.name ;
```

## <a name="permissions"></a>權限

需要**VIEW SERVER STATE**許可權。

## <a name="see-also"></a>另請參閱

[SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
[建立資料行存放區索引 &#40;Transact-sql&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)  
[pdw_nodes_column_store_row_groups &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
[pdw_nodes_column_store_dictionaries &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)
