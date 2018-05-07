---
title: sys.dm_pdw_node_status (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 873f83991cbc89ff3e552646c04e8657b005181b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>sys.dm_pdw_node_status (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存其他資訊 (透過[sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) 有關的效能和狀態的應用裝置的所有節點。 它會列出一個資料列，每個應用裝置中的節點。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。<br /><br /> 此檢視的索引鍵。|唯一的應用裝置，不論類型為何。|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|在此節點上的記憶體配置總計。||  
|available_memory|**bigint**|在此節點上的總可用記憶體。||  
|process_cpu_usage|**bigint**|總處理程序的 CPU 使用量，以刻度為單位。||  
|total_cpu_usage|**bigint**|總 CPU 使用量，以刻度為單位。||  
|thread_count|**bigint**|在此節點上的使用中的執行緒總數。||  
|handle_count|**bigint**|在此節點上的使用中的控制代碼總數。||  
|total_elapsed_time|**bigint**|系統啟動或重新啟動後，就會經過的總時間。|系統啟動或重新啟動後，就會經過的總時間。 如果 total_elapsed_time 超過整數 （以毫秒為單位的 24.8 天） 的最大值，它會導致具體化失敗，因為發生溢位。<br /><br /> 以毫秒為單位的最大值就相當於 24.8 天。|  
|is_available|**bit**|表示此節點是否可使用的旗標。||  
|sent_time|**datetime**|最後一次此節點已傳送的網路套件。||  
|received_time|**datetime**|最後一次此節點已收到網路套件。||  
|error_id|**nvarchar(36)**|在此節點上發生的最後一個錯誤的唯一識別碼。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
