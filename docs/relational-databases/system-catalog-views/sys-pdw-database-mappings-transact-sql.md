---
title: sys.databases pdw_database_mappings （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4ae2c71e-dd56-41ea-a16b-64936175b459
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 013a6bcbba5e7647db1bec04204f8e8fec710c16
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396085"
---
# <a name="syspdw_database_mappings-transact-sql"></a>sys.databases pdw_database_mappings （Transact-sql）
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  將資料庫的**database_id**對應到計算節點上所使用的機構名稱，並提供系統上資料庫擁有**者的主體識別碼**。 將**sys. pdw_database_mappings**加入**sys.databases**和 sys.databases。 **pdw_nodes_pdw_physical_databases**。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**Nvarchar （36）**|計算節點上資料庫的機構名稱。<br /><br /> **physical_name**和**database_id**形成此視圖的索引鍵。||  
|database_id|**int**|資料庫的物件識別碼。 請參閱[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。<br /><br /> **physical_name**和**database_id**形成此視圖的索引鍵。||  
  
## <a name="examples-sspdw"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會將 pdw_database_mappings sys.databases 聯結至其他系統資料表，以顯示資料庫的對應方式。  
  
```  
SELECT DB.database_id, DB.name, Map.*, Phys.*   
FROM sys.databases AS DB  
JOIN sys.pdw_database_mappings AS Map  
    ON DB.database_id = Map.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS Phys  
    ON Map.physical_name = Phys.physical_name  
ORDER BY DB.database_id, Phys.pdw_node_id;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [pdw_index_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [pdw_table_mappings &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [pdw_nodes_pdw_physical_databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
  

