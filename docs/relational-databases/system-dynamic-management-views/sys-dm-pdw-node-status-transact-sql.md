---
title: sys.databases dm_pdw_node_status （Transact-sql） |Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4cd8788d19b06329d0280efc43a13a9a218e056c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899363"
---
# <a name="sysdm_pdw_node_status-transact-sql"></a>sys.databases dm_pdw_node_status （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存有關所有設備節點的效能和狀態的其他資訊（透過[sys.databases dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)）。 它會針對設備中的每個節點列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|與節點相關聯的唯一數值識別碼。<br /><br /> 此視圖的索引鍵。|在設備上是唯一的，不論類型為何。|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**Bigint**|此節點上配置的記憶體總計。||  
|available_memory|**Bigint**|此節點上的可用記憶體總計。||  
|process_cpu_usage|**Bigint**|總處理常式 CPU 使用量（以刻度為單位）。||  
|total_cpu_usage|**Bigint**|總 CPU 使用量（以刻度為單位）。||  
|thread_count|**Bigint**|此節點上使用中的執行緒總數。||  
|handle_count|**Bigint**|此節點上使用中的控制碼總數。||  
|total_elapsed_time|**Bigint**|從系統啟動或重新開機以來經過的總時間。|從系統啟動或重新開機以來經過的總時間。 如果 total_elapsed_time 超過整數的最大值（以毫秒為單位的24.8 天），則會造成具體化失敗，因為溢位。<br /><br /> 最大值（以毫秒為單位）相當於24.8 天。|  
|is_available|**bit**|指出此節點是否可供使用的旗標。||  
|sent_time|**datetime**|上次此節點傳送網路封裝的時間。||  
|received_time|**datetime**|上次此節點收到網路套件的時間。||  
|error_id|**Nvarchar （36）**|此節點上發生之最後一個錯誤的唯一識別碼。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
