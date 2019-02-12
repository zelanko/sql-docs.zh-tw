---
title: sys.dm_pdw_node_status (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6c56d169e8aa55e83b86713e1b9fa476bc213ae3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014142"
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>sys.dm_pdw_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存其他資訊 (透過[sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) 相關的效能和應用裝置的所有節點的狀態。 它會列出每個設備中的節點的一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。<br /><br /> 此檢視的索引鍵。|跨設備，無論何種類型是唯一的。|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|在這個節點上的記憶體配置總計。||  
|available_memory|**bigint**|在這個節點上的總可用記憶體。||  
|process_cpu_usage|**bigint**|總處理序 CPU 使用量，以刻度為單位。||  
|total_cpu_usage|**bigint**|總 CPU 使用量，以刻度為單位。||  
|thread_count|**bigint**|在這個節點上的使用中的執行緒總數。||  
|handle_count|**bigint**|在這個節點上的使用中的控制代碼的總數。||  
|total_elapsed_time|**bigint**|自系統啟動或重新啟動後經過的時間總計。|自系統啟動或重新啟動後經過的時間總計。 如果 total_elapsed_time 超過整數 （以毫秒為單位的 24.8 天） 的最大值，它會具體化失敗，因為溢位。<br /><br /> 以毫秒為單位的最大值相當於 24.8 天。|  
|is_available|**bit**|指出是否可使用此節點的旗標。||  
|sent_time|**datetime**|上次，此節點所傳送的網路套件。||  
|received_time|**datetime**|最後一次此節點已收到網路套件。||  
|error_id|**nvarchar(36)**|在這個節點發生的最後一個錯誤的唯一識別碼。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
