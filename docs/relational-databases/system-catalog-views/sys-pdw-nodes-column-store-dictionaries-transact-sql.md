---
title: sys.databases pdw_nodes_column_store_dictionaries （Transact-sql） |Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.custom: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 7ae1c2e4-45c0-4880-a692-1f299fbcfd19
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 618a92cfd0f1602753b9fcfd61ac232eff5cecd4
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305190"
---
# <a name="syspdw_nodes_column_store_dictionaries-transact-sql"></a>sys.databases pdw_nodes_column_store_dictionaries （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  針對資料行存放區索引中使用的每個字典，各包含一個資料列。 字典是用於編碼部分的資料類型而非全部，因此資料行存放區索引中並非所有資料行都有字典。 字典存在的形式可能是主要字典 (適用所有區段)，且或許另有其他次要字典用於資料行各區段的特定子集。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|指出資料分割識別碼。 在資料庫中，這是唯一的。|  
|**hobt_id**|**bigint**|具有此資料行存放區索引之資料表的堆積或 B 型樹狀目錄索引（HoBT）識別碼。|  
|**column_id**|**int**|資料行存放區資料行的識別碼。|  
|**dictionary_id**|**int**|字典的識別碼。|  
|**version**|**int**|字典格式的版本。|  
|**型別**|**int**|字典類型：<br /><br /> 1-包含**int**值的雜湊字典<br /><br /> 2-未使用<br /><br /> 3-包含字串值的雜湊字典<br /><br /> 4-包含**浮點**值的雜湊字典|  
|**last_id**|**int**|字典中的最後一個資料識別碼。|  
|**entry_count**|**bigint**|字典中的項目數。|  
|**on_disc_size**|**bigint**|字典的大小 (以位元組為單位)。|  
|**pdw_node_id**|**int**|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 節點的唯一識別碼。|  
  
## <a name="permissions"></a>Permissions  
 需要 `VIEW SERVER STATE` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 建立資料行存放區[ &#40;索引&#41; transact-sql](../../t-sql/statements/create-columnstore-index-transact-sql.md)   
 [pdw_nodes_column_store_segments &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)   
 [sys. pdw_nodes_column_store_row_groups &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
  
