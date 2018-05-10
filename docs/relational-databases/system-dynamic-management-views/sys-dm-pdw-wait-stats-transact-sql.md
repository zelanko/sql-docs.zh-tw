---
title: sys.dm_pdw_wait_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: cf297c6cdbff7c2a79e8adbdeec05f4d0232314d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwwaitstats-transact-sql"></a>sys.dm_pdw_wait_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存的相關資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]OS 狀態與不同的節點上執行的執行個體相關。 如需等候的類型以及其描述的清單，請參閱[sys.dm_os_wait_stats](http://msdn.microsoft.com/en-us/library/ms179984\(v=sql.120\).aspx)。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|此項目是指的節點的識別碼。||  
|**wait_name**|**nvarchar(255)**|等候類型的名稱。||  
|**max_wait_time**|**bigint**|這種等候類型的最長等待時間。||  
|**request_count**|**bigint**|這個等候次數等候未處理的類型。||  
|**signal_time**|**bigint**|從等候執行緒接獲訊號到開始執行的時間。||  
|**completed_count**|**bigint**|重新啟動後的最後一個伺服器完成此類型的等候的總數目。||  
|**wait_time**|**bigint**|這種等候類型 millisecons 中的總等候時間。 內含的 signal_time。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_waits &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
