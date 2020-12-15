---
description: 'sys.dm_pdw_query_stats_xe (Transact-sql) '
title: sys.dm_pdw_query_stats_xe (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d551241-db35-4958-b60f-55e996f95c1f
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 9208823cd17c5638b759e3608280773ea60c454a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440730"
---
# <a name="sysdm_pdw_query_stats_xe-transact-sql"></a>sys.dm_pdw_query_stats_xe (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  此 DMV 已被取代，並將在未來的版本中移除。 在此版本中，它會傳回0個數據列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|event|**nvarchar(60)**|此視圖的索引鍵。||  
|event_id|**Nvarchar (36)**|||  
|create_time|**datetime**|||  
|session_id|**int**|會話的識別碼。|請參閱 [sys.dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)中的 session_id。|  
|cpu|**int**|||  
|reads|**int**|自事件開始之後的邏輯讀取數。||  
|writes|**int**|自事件開始之後的邏輯寫入數。||  
|sql_text|**nvarchar(4000)**|||  
|client_app_name|**nvarchar(255)**|||  
|tsql_stack|**nvarchar(255)**|||  
|pdw_node_id|**int**|此 Xevent 實例正在其上執行的節點。|  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
