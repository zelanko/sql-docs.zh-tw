---
description: sys.pdw_replicated_table_cache_state (Transact-SQL)
title: sys.pdw_replicated_table_cache_state (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 76b5f9ec684b4733934a8cdd703942f12cf1b541
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404450"
---
# <a name="syspdw_replicated_table_cache_state-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  藉由 **object_id**，傳回與複寫資料表相關聯的快取狀態。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|資料表的物件識別碼。 請參閱 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。<br /><br /> **object_id** 是此視圖的索引鍵。||  
|state|**nvarchar(40)**|此資料表的複寫資料表快取狀態。|' NotReady '、' Ready '|  
  
## <a name="example"></a>範例
此範例會聯結 sys.pdw_replicated_table_cache_state 與 sys. 資料表，以抓取資料表名稱和複寫資料表快取的狀態。

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>後續步驟  
 如需 Azure Synapse Analytics 和平行處理資料倉儲的所有目錄檢視清單，請參閱 [Azure Synapse Analytics 和平行處理資料倉儲目錄的觀點](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。   
  
