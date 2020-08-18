---
description: 'sys. pdw_loader_backup_run_details (Transact-sql) '
title: sys. pdw_loader_backup_run_details (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: d42094beb9b29cc620007bb1d590a6fa8dc33987
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400524"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>sys. pdw_loader_backup_run_details (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  除了 [sys. pdw_loader_backup_runs ](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)中的資訊之外，還包含更詳細的資訊，&#40;transact-sql&#41;、中的進行中和已完成的備份和還原作業， [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 以及中的進行中和已完成的備份、還原和載入作業 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。 此資訊在系統重新啟動之後會持續存留。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定備份或還原執行的唯一識別碼。<br /><br /> run_id 並 pdw_node_id 形成此視圖的索引鍵。||  
|pdw_node_id|**int**|此記錄包含詳細資料之設備節點的唯一識別碼。<br /><br /> run_id 並 pdw_node_id 形成此視圖的索引鍵。|請參閱 [sys. dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 node_id。|  
|status|**Nvarchar (16) **|執行的目前狀態。|「已取消」、「已完成」、「失敗」、「已排入佇列」、「正在執行」|  
|start_time|**datetime**|此特定節點上的作業開始時間。||  
|end_time|**datetime**|此特定節點上作業結束的時間（如果有的話）。||  
|total_elapsed_time|**int**|此特定節點上的作業執行的總時間。|如果 total_elapsed_time 超過整數 (24.8 天（以毫秒為單位）的最大值) ，則會造成具體化失敗，因為溢位。<br /><br /> 以毫秒為單位的最大值相當於24.8 天。|  
|progress|**int**|作業的進度（以百分比表示）。|0 到 100|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
