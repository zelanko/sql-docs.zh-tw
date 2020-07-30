---
title: sys.databases dm_pdw_diag_processing_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a765e591e3b55bb4be2e2b6d7431873702910f6f
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394350"
---
# <a name="sysdm_pdw_diag_processing_stats-transact-sql"></a>sys.databases dm_pdw_diag_processing_stats （Transact-sql）
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  顯示所有內部診斷事件的相關資訊，這些事件可以併入系統管理員定義的診斷會話中。 查詢此視圖，以瞭解診斷和事件子系統背後的統計資料，以驅動所有其他 Dmv 的人口。 每個節點上的每個處理常式都有一組佇列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|此記錄檔來源的設備節點。|  
|**process_id**|**int**|正在提交此統計資料之進程的識別碼。|  
|**target_name**|**nvarchar(255)**|佇列的名稱。|  
|**queue_size**|**int**|進程佇列中的專案數。 佇列大小通常是0。 正數表示系統正在承受壓力，而且正在建立事件的待處理專案（backlog）。 其他資料行中的正計數表示系統已損毀該特定佇列和任何相關的 Dmv。|  
|**lost_events_count**|**bigint**|遺失的事件數目。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
