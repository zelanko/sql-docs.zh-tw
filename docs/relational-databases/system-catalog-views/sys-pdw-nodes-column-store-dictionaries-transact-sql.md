---
title: sys.pdw_nodes_column_store_dictionaries (TRANSACT-SQL) |Microsoft 文件
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 7ae1c2e4-45c0-4880-a692-1f299fbcfd19
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: bc7104fedccb7f8937e99e47496e3ce25aac2c8c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="syspdwnodescolumnstoredictionaries-transact-sql"></a>sys.pdw_nodes_column_store_dictionaries (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含使用資料行存放區索引中每個字典的資料列。 字典是用於編碼部分的資料類型而非全部，因此資料行存放區索引中並非所有資料行都有字典。 字典存在的形式可能是主要字典 (適用所有區段)，且或許另有其他次要字典用於資料行各區段的特定子集。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|指出資料分割識別碼。 在資料庫中，這是唯一的。|  
|**hobt_id**|**bigint**|具有此資料行存放區索引之資料表的堆積或 B 型樹狀目錄索引 (hobt) 的識別碼。|  
|**column_id**|**int**|資料行存放區資料行的識別碼。|  
|**dictionary_id**|**int**|字典的識別碼。|  
|**version**|**int**|字典格式的版本。|  
|**type**|**int**|字典類型：<br /><br /> 1 – 雜湊字典包含**int**值<br /><br /> 2 – 未使用<br /><br /> 3 – 包含字串值的雜湊字典<br /><br /> 4 – 雜湊字典包含**float**值|  
|**last_id**|**int**|字典中的最後一個資料識別碼。|  
|**entry_count**|**bigint**|字典中的項目數。|  
|**on_disc_size**|**bigint**|字典的大小 (以位元組為單位)。|  
|**pdw_node_id**|**int**|唯一識別項[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]節點。|  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [建立資料行存放區索引&#40;Transact SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [sys.pdw_nodes_column_store_segments &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
  
