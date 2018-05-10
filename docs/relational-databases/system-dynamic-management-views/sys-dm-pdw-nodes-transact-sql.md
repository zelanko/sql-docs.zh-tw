---
title: sys.dm_pdw_nodes (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: e609a3e5d6963a5e643df86a61588586984baf20
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留的所有節點中的相關資訊[!INCLUDE[ssAPS](../../includes/ssaps-md.md)]。 它會列出一個資料列，每個應用裝置中的節點。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。<br /><br /> 此檢視的索引鍵。|唯一的應用裝置，不論類型為何。|  
|型別|**nvarchar(32)**|節點的類型。|' COMPUTE'，「 控制項 」、 「 管理 」|  
|name|**nvarchar(32)**|節點的邏輯名稱。|任何適當的長度的字串。|  
|address|**nvarchar(32)**|此節點的 IP 位址。|在 [0-255] 格式。[0-255]。[0-255]。[0-255]。|  
|is_passive|**int**|指出執行節點的虛擬機器指派的伺服器上執行或已容錯移轉至備援的伺服器。|0 – 節點 VM 正在執行原始的伺服器上。<br /><br /> 1 – 節點 VM 備用的伺服器上執行。|  
|區域|**nvarchar(32)**|節點正在執行所在的區域。|' PDW'，'HDINSIGHT'|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
