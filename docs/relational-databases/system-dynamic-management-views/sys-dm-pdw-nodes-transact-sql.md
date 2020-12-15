---
description: 'sys.dm_pdw_nodes (Transact-sql) '
title: sys.dm_pdw_nodes (Transact-sql) |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 28c2f14eebfecd386cc49678a1429b678a428239
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440773"
---
# <a name="sysdm_pdw_nodes-transact-sql"></a>sys.dm_pdw_nodes (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存中所有節點的相關資訊 [!INCLUDE[ssAPS](../../includes/ssaps-md.md)] 。 它會針對設備中的每個節點列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。<br /><br /> 此視圖的索引鍵。|無論何種類型，在設備間都是唯一的。|  
|類型|**nvarchar(32)**|節點的類型。|「計算」、「控制」、「管理」|  
|NAME|**nvarchar(32)**|節點的邏輯名稱。|適當長度的任何字串。|  
|address|**nvarchar(32)**|此節點的 IP 位址。|格式為 [0-255]。[0-255]。[0-255]。[0-255]。|  
|is_passive|**int**|指出執行節點的虛擬機器是否正在指派的伺服器上執行，或已容錯移轉至待命伺服器。|0-節點 VM 正在源伺服器上執行。<br /><br /> 1-節點 VM 正在待命伺服器上執行。|  
|region|**nvarchar(32)**|節點執行所在的區域。|' PDW '、' HDINSIGHT '|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
