---
title: sys.dm_exec_compute_nodes & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODES_TSQL
- DM_EXEC_COMPUTE_NODES
- SYS.DM_EXEC_COMPUTE_NODES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_nodes management view
- PolyBase, views
- PolyBase management views
- dm_exec_compute_nodes management view
ms.assetid: 0de4b7a4-401f-4e2d-9ab0-c54587e05154
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e09741600a63596d9b486ebf2d36a808e7981a87
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753116"
---
# <a name="sysdmexeccomputenodes-transact-sql"></a>sys.dm_exec_compute_nodes & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  含有 PolyBase 的資料管理搭配使用的節點相關資訊。 它會列出每個節點的一個資料列。  
  
 您可以使用此 DMV，查看與他們的角色、 名稱和 IP 位址向外延展叢集中所有節點的清單。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|與節點相關聯的唯一數值識別碼。 此檢視的索引鍵。|跨相應放大叢集，無論何種類型是唯一的。|  
|型別|**nvarchar(32)**|節點型別。|' COMPUTE'、 'HEAD'|  
|NAME|**nvarchar(32)**|節點的邏輯名稱。|任何適當的長度的字串。|  
|address|**nvarchar(32)**|此節點的 P 位址。|IP 位址範圍|  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase 疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
