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
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8b880820ac633402d1d3cdd679b16a54d1be358e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899534"
---
# <a name="sysdm_pdw_diag_processing_stats-transact-sql"></a>sys.databases dm_pdw_diag_processing_stats （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  顯示所有內部診斷事件的相關資訊，這些事件可以併入系統管理員定義的診斷會話中。 查詢此視圖，以瞭解診斷和事件子系統背後的統計資料，以驅動所有其他 Dmv 的人口。 每個節點上的每個處理常式都有一組佇列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|此記錄檔來源的設備節點。|  
|**process_id**|**int**|正在提交此統計資料之進程的識別碼。|  
|**target_name**|**nvarchar(255)**|佇列的名稱。|  
|**queue_size**|**int**|進程佇列中的專案數。 佇列大小通常是0。 正數表示系統正在承受壓力，而且正在建立事件的待處理專案（backlog）。 其他資料行中的正計數表示系統已損毀該特定佇列和任何相關的 Dmv。|  
|**lost_events_count**|**Bigint**|遺失的事件數目。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
