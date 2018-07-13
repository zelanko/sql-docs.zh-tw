---
title: sys.pdw_replicated_table_cache_state (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 8d78a537bb2de2ee880551afd3667f308b49ce83
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926049"
---
# <a name="syspdwreplicatedtablecachestate-transact-sql"></a>sys.pdw_replicated_table_cache_state & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  傳回與所複寫的資料表相關聯的快取的狀態**object_id**。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|資料表的物件識別碼。 請參閱[j &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **object_id**是此檢視的索引鍵。||  
|state|**nvarchar(40)**|這個資料表的複寫的資料表快取狀態。|'NotReady','Ready'|  
  
## <a name="example"></a>範例
此範例會聯結 sys.pdw_replicated_table_cache_state 與 sys.tables 來擷取資料表名稱和複寫的資料表快取的狀態。

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>後續的步驟  
 如需所有 SQL 資料倉儲和平行資料倉儲的目錄檢視的清單，請參閱 < [SQL 資料倉儲和平行資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。   
  
