---
title: sys.pdw_nodes_partitions (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b4216752-4813-4b2c-b259-7d8ffc6cc190
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 94f7ab8cb379c2147446b67d9865e8ad415dcf84
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="syspdwnodespartitions-transact-sql"></a>sys.pdw_nodes_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含每個資料分割的所有資料表和索引中的大部分類型的資料列[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]資料庫。 所有資料表和索引都包含至少一個資料分割，不論是否明確地進行資料分割。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|partition_id|`bigint`|資料分割識別碼。 在資料庫中，這是唯一的。|  
|object_id|`int`|此資料分割所屬物件的識別碼。 每份資料表或檢視表至少都是由一個資料分割組成。|  
|index_id|`int`|此資料分割所屬的物件內的索引識別碼。|  
|partition_number|`int`|在作為擁有索引或堆積內，以 1 為底的資料分割編號。 如[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，此資料行的值為 1。|  
|hobt_id|`bigint`|包含這個資料分割的資料列之資料堆積或 B 型樹狀目錄的識別碼。|  
|rows|`bigint`|這個資料分割中的近似資料列數。 |  
|data_compression|`int`|表示每個資料分割的壓縮狀態：<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE<br /><br /> 3 = COLUMNSTORE|  
|data_compression_desc|`nvarchar(60)`|表示每個資料分割的壓縮狀態。 可能的值是 NONE、ROW 和 PAGE。|  
|pdw_node_id|`int`|唯一識別項[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]節點。|  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  

### <a name="example-a-display-rows-in-each-partition-within-each-distribution"></a>範例 a： 顯示資料列中每個發佈中的每個資料分割 

適用於：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
 
若要顯示每個發佈中的每個資料分割的資料列數目，使用[DBCC PDW_SHOWPARTITIONSTATS (SQL Server PDW)](../../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md) 。

### <a name="example-b-uses-system-views-to-view-rows-in-each-partition-of-each-distribution-of-a-table"></a>若要檢視每個資料分割中之資料表的每個發佈的資料列的範例 b： 使用系統檢視表

適用於：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
 
此查詢傳回的資料列數目，每個資料分割中之資料表的每個發佈`myTable`。  
 
```  
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
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  

