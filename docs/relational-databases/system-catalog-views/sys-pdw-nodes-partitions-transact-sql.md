---
title: pdw_nodes_partitions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 32c64ad5faab1ef262cd754201cac40e4a076619
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197354"
---
# <a name="syspdw_nodes_partitions-transact-sql"></a>pdw_nodes_partitions (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  針對所有資料表的每個分割區，以及資料庫中的大部分索引類型，各包含一個 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 資料列。 所有資料表和索引都至少包含一個資料分割，不論它們是否已明確分割。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|資料分割的識別碼。 在資料庫中，這是唯一的。|  
|object_id|**int**|此資料分割所屬物件的識別碼。 每份資料表或檢視表至少都是由一個資料分割組成。|  
|index_id|**int**|此資料分割所屬物件內的索引識別碼。|  
|partition_number|**int**|在作為擁有索引或堆積內，以 1 為底的資料分割編號。 若為 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ，則此資料行的值為1。|  
|hobt_id|**bigint**|資料堆積或 B 型樹狀目錄的識別碼， (HoBT) ，其中包含此分割區的資料列。|  
|rows|**bigint**|這個資料分割中的近似資料列數。 |  
|data_compression|**int**|表示每個資料分割的壓縮狀態：<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE<br /><br /> 3 = COLUMNSTORE|  
|data_compression_desc|**nvarchar(60)**|表示每個資料分割的壓縮狀態。 可能的值是 NONE、ROW 和 PAGE。|  
|pdw_node_id|**int**|節點的唯一識別碼 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。|  
  
## <a name="permissions"></a>權限  
 需要 `CONTROL SERVER` 權限。  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>範例 A：顯示每個散發中每個資料分割內的資料列 

**適用于：** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
若要顯示每個散發中每個分割區的資料列數，請使用[DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW) ](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md) 。

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>範例 B：使用系統檢視來查看資料表之每個散發的每個資料分割中的資料列

**適用對象：** [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
此查詢會傳回資料表中每個散發的每個資料分割中的資料列數目 `myTable` 。  
 
```sql  
SELECT o.name, pnp.index_id, pnp.partition_id, pnp.rows,   
    pnp.data_compression_desc, pnp.pdw_node_id  
FROM sys.pdw_nodes_partitions AS pnp  
JOIN sys.pdw_nodes_tables AS NTables  
    ON pnp.object_id = NTables.object_id  
AND pnp.pdw_node_id = NTables.pdw_node_id  
JOIN sys.pdw_table_mappings AS TMap  
    ON NTables.name = TMap.physical_name 
    AND substring(TMap.physical_name,40, 10) = pnp.distribution_id 
JOIN sys.objects AS o  
    ON TMap.object_id = o.object_id  
WHERE o.name = 'myTable'  
ORDER BY o.name, pnp.index_id, pnp.partition_id;  
```    
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

