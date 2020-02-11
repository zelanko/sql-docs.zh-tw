---
title: sys.databases pdw_distributions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 572b5187-9753-4063-adf8-65dea87d11f8
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7deddb57cdc02410fe161728f45190492ac18a16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127545"
---
# <a name="syspdw_distributions-transact-sql"></a>sys.databases pdw_distributions （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存設備上散發套件的相關資訊。 它會針對每個設備散發列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|與散發相關聯的唯一數值識別碼。<br /><br /> 此視圖的索引鍵。|1到設備中的計算節點數目乘以每個計算節點的散發數目。|  
|pdw_node_id|**int**|此散發所在節點的識別碼。|請參閱[dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 pdw_node_id。|  
|NAME|**Nvarchar （32）**|與散發相關聯的字串識別碼，用來做為分散式資料表的尾碼。|由 ' a-z '、' a-z '、' 0-9 '、' _ '、'-' 組成的字串。|  
|position|**int**|相對於該節點上其他散發的節點內的分佈位置。|1到每個節點的散發數目。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
