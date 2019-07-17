---
title: sys.pdw_distributions (TRANSACT-SQL) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127545"
---
# <a name="syspdwdistributions-transact-sql"></a>sys.pdw_distributions & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留應用裝置上的散發套件的相關資訊。 它會列出每個設備散發的一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|distribution_id|**int**|與發佈相關聯的唯一數值識別碼。<br /><br /> 此檢視的索引鍵。|1 到乘以每個計算節點的發佈數目的設備中計算節點數目。|  
|pdw_node_id|**int**|這個分佈是在節點的識別碼。|請參閱中的 pdw_node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|name|**nvarchar(32)**|字串和分配，當做分散式資料表上的後置詞相關聯的識別碼。|字串組成的 'A-Z '、' a-z '、 ' 0-9'、 '_'、 '-'。|  
|position|**int**|節點分別為該節點上的其他散發套件中發佈的位置。|1 到每個節點的數目。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
