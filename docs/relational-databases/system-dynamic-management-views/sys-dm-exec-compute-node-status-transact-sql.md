---
title: sys.dm_exec_compute_node_status & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODE_STATUS_TSQL
- DM_EXEC_COMPUTE_NODE_STATUS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_compute_node_status
- sys.dm_exec_compute_node_status management view
ms.assetid: b606f91f-3a08-4a4f-bb57-32ae155b3738
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55023b301b1c6bae53f890e273f5a415fde42355
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51671057"
---
# <a name="sysdmexeccomputenodestatus-transact-sql"></a>sys.dm_exec_compute_node_status & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  保留所有的 PolyBase 節點的狀態與效能相關的其他資訊。 列出每個節點的一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|與節點相關聯的唯一數值識別碼。|跨相應放大叢集，無論何種類型是唯一的。|  
|process_id|**int**|||  
|process_name|**nvarchar(255)**|節點的邏輯名稱。|任何適當的長度的字串。|  
|allocated_memory|**bigint**|在這個節點上的記憶體配置總計。||  
|available_memory|**bigint**|在這個節點上的總可用記憶體。||  
|process_cpu_usage|**bigint**|總處理序 CPU 使用量，以刻度為單位。||  
|total_cpu_usage|**bigint**|總 CPU 使用量，以刻度為單位。||  
|thread_count|**bigint**|在這個節點上的使用中的執行緒總數。||  
|handle_count|**bigint**|在這個節點上的使用中的控制代碼的總數。||  
|total_elapsed_time|**bigint**|自系統啟動或重新啟動後經過的時間總計。|自系統啟動或重新啟動後經過的時間總計。 如果 total_elapsed_time 超過整數 （以毫秒為單位的 24.8 天） 的最大值，它會具體化失敗，因為溢位。以毫秒為單位的最大值相當於 24.8 天。|  
|is_available|**bit**|指出是否可使用此節點的旗標。||  
|sent_time|**datetime**|上次由此傳送網路套件||  
|received_time|**datetime**|上次，此節點所傳送的網路套件。||  
|error_id|**nvarchar(36)**|在這個節點發生的最後一個錯誤的唯一識別碼。||  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase 疑難排解動態管理檢視](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
