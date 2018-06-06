---
title: sys.dm_pdw_sys_info (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: eddd759f3dfa1447a441350583a6ce66e2ac14ab
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  提供一組應用裝置層級的計數器會反映應用裝置上的整體活動。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|目前在系統中的工作階段數目。|0 表示 max_active_sessions （請參閱下文）。|  
|idle_sessions|**int**|目前閒置的工作階段數目。||  
|active_requests|**int**|目前執行中的作用中要求數目。||  
|queued_requests|**int**|目前佇列的要求數目。||  
|active_loads|**int**|載入系統中目前執行的數目。||  
|queued_loads|**int**|佇列等待執行的載入數目。||  
|active_backups|**int**|目前正在執行的備份數目。||  
|active_restores|**int**|目前正在執行的備份還原的數目。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
