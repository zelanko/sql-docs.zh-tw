---
title: sys.databases pdw_loader_backup_run_details （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: dead5962987f7fb132f21bb4e3517f7cc9249601
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127651"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>sys.databases pdw_loader_backup_run_details （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  除了 sys.databases 中的資訊之外，還包含[pdw_loader_backup_runs &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)中的詳細資訊，以及中的進行中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和已完成的備份和還原作業，以及關於中[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]的持續性和已完成的備份、還原和載入作業。 此資訊在系統重新啟動之後會持續存留。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定備份或還原執行的唯一識別碼。<br /><br /> run_id 和 pdw_node_id 形成此視圖的索引鍵。||  
|pdw_node_id|**int**|此記錄保留詳細資料之應用裝置節點的唯一識別碼。<br /><br /> run_id 和 pdw_node_id 形成此視圖的索引鍵。|請參閱[dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 node_id。|  
|status|**Nvarchar （16）**|執行的目前狀態。|「已取消」、「已完成」、「失敗」、「已排入佇列」、「執行中」|  
|start_time|**datetime**|在這個特定節點上開始作業的時間。||  
|end_time|**datetime**|此特定節點上作業結束的時間（如果有的話）。||  
|total_elapsed_time|**int**|此特定節點上作業已執行的總時間。|如果 total_elapsed_time 超過整數的最大值（以毫秒為單位的24.8 天），則會造成具體化失敗，因為溢位。<br /><br /> 最大值（以毫秒為單位）相當於24.8 天。|  
|progress|**int**|以百分比表示的作業進度。|0 到 100|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
