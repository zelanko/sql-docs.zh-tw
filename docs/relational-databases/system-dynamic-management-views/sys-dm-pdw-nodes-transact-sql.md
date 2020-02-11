---
title: sys.databases dm_pdw_nodes （Transact-sql） |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 61593522e09ed86ec10f08a6ad8ff7a941a2e10e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899350"
---
# <a name="sysdm_pdw_nodes-transact-sql"></a>sys.databases dm_pdw_nodes （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存中[!INCLUDE[ssAPS](../../includes/ssaps-md.md)]所有節點的相關資訊。 它會針對設備中的每個節點列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。<br /><br /> 此視圖的索引鍵。|在設備上是唯一的，不論類型為何。|  
|type|**Nvarchar （32）**|節點的類型。|「計算」、「控制項」、「管理」|  
|NAME|**Nvarchar （32）**|節點的邏輯名稱。|適當長度的任何字串。|  
|address|**Nvarchar （32）**|此節點的 IP 位址。|格式為 [0-255]。[0-255]。[0-255]。[0-255]。|  
|is_passive|**int**|指出執行節點的虛擬機器是否正在指派的伺服器上執行，或已故障切換至待命伺服器。|0-節點 VM 正在源伺服器上執行。<br /><br /> 1-節點 VM 正在待命伺服器上執行。|  
|region|**Nvarchar （32）**|節點正在執行的區域。|' PDW '、' HDINSIGHT '|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
