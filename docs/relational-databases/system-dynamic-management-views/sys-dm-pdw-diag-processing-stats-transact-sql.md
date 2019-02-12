---
title: sys.dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f96dd7be6de1415abb8a71425b083c58e7012d9d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023989"
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  顯示可能會併入診斷工作階段，系統管理員定義的所有內部診斷事件的相關資訊。 查詢此檢視來了解背後的診斷和事件處理子系統的統計資料的所有其他 Dmv 母體擴展該磁碟機。 有一群的每個節點上的每個處理序的佇列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|此記錄檔的來源應用裝置節點。|  
|**process_id**|**int**|執行 送出這項統計資料的處理序識別碼。|  
|**target_name**|**nvarchar(255)**|佇列的名稱。|  
|**queue_size**|**int**|在處理佇列中的項目數目。 佇列大小通常是 0。 正數代表系統在壓力下，而且正在建置之事件的待處理項目。 在其他資料行正計數表示系統已損毀的該特定的佇列，以及任何相關的 Dmv。|  
|**lost_events_count**|**bigint**|遺失的事件數目。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
