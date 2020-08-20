---
description: 'sys. dm_pdw_os_threads (Transact-sql) '
title: sys. dm_pdw_os_threads (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ddc12f05-edeb-4848-b6d7-e851684cf044
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 13b2d0ec8bfebb03efd0b2ea4305994bdc8e1609
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474710"
---
# <a name="sysdm_pdw_os_threads-transact-sql"></a>sys. dm_pdw_os_threads (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|受影響節點的識別碼。<br /><br /> pdw_node_id 並 thread_id 形成此視圖的索引鍵。|請參閱 [sys. dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 node_id。|  
|thread_id|**int**|pdw_node_id 並 thread_id 形成此視圖的索引鍵。||  
|process_id|**int**|||  
|NAME|**nvarchar(255)**|||  
|priority|**int**|||  
|start_time|**datetime**|||  
|狀態|**nvarchar(32)**|||  
|wait_reason|**nvarchar(32)**|||  
|total_processor_elapsed_time|**bigint**|執行緒使用的核心時間總計。||  
|total_user_elapsed_time|**bigint**|執行緒使用的總使用者時間||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
