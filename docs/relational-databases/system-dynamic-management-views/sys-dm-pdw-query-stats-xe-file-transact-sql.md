---
title: "sys.dm_pdw_query_stats_xe_file (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.reviewer: 
ms.service: 
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: e0cd402f-04d0-4a5b-b725-88b31bb7862e
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 76e5f9a846dce839f176999118594e8951fb48cc
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwquerystatsxefile-transact-sql"></a>sys.dm_pdw_query_stats_xe_file (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  此 DMV 已被取代，未來版本將移除。 在此版本中，它會傳回 0 個資料列。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|event|**nvarchar （60)**|此檢視的索引鍵。||  
|data|**xml**|||  
|pdw_node_id|**int**|這個 Xevent 執行個體執行所在的節點。||  
  
## <a name="see-also"></a>請參閱＜  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
