---
title: sys.dm_pdw_diag_processing_stats (TRANSACT-SQL) |Microsoft 文件
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
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ef951e601b97b4f5de1ebf0675672fe1ff583439
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  顯示可能會併入診斷工作階段的系統管理員所定義的所有內部診斷事件的相關資訊。 查詢此檢視來了解的統計資料，背後的診斷和事件處理子系統該磁碟機的所有其他 Dmv 母體擴展。 有群組的每個節點上的每個處理序的佇列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|此記錄檔的來源應用裝置節點。|  
|**process_id**|**int**|執行 送出此統計資料之處理序識別碼。|  
|**target_name**|**nvarchar(255)**|佇列的名稱。|  
|**queue_size**|**int**|處理序佇列中的項目數目。 佇列大小通常是 0。 正數代表系統壓力下，且正在建置之事件的待處理項目。 其他資料行正計數表示系統已損毀該特定的佇列，以及任何相關的 Dmv。|  
|**lost_events_count**|**bigint**|遺失的事件數目。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
