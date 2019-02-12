---
title: sys.dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a5df628a6b37c8d89843506c5b7f4c5050157158
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027390"
---
# <a name="sysdmpdwnodes-transact-sql"></a>sys.dm_pdw_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留的所有節點中的相關資訊[!INCLUDE[ssAPS](../../includes/ssaps-md.md)]。 它會列出每個設備中的節點的一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。<br /><br /> 此檢視的索引鍵。|跨設備，無論何種類型是唯一的。|  
|型別|**nvarchar(32)**|節點型別。|' COMPUTE'、 'CONTROL'，[管理]|  
|NAME|**nvarchar(32)**|節點的邏輯名稱。|任何適當的長度的字串。|  
|address|**nvarchar(32)**|此節點的 IP 位址。|在 [0-255] 格式。[0-255]。[0-255]。[0-255]。|  
|is_passive|**int**|指出執行節點的虛擬機器指派的伺服器上執行或已容錯移轉到備援伺服器。|0-節點 VM 會在原始伺服器上執行。<br /><br /> 1-節點 VM 會在備用的伺服器上執行。|  
|區域|**nvarchar(32)**|節點正在執行的所在區域。|' PDW'，'HDINSIGHT'|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
