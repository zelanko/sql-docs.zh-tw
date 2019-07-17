---
title: sys.pdw_loader_backup_run_details (TRANSACT-SQL) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127651"
---
# <a name="syspdwloaderbackuprundetails-transact-sql"></a>sys.pdw_loader_backup_run_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含進一步的詳細的資訊，而不在資訊[sys.pdw_loader_backup_runs &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)、 進行中和已完成備份和還原作業中的相關[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]以及進行中並完成備份、 還原及載入作業中的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 此資訊在系統重新啟動之後會持續存留。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定的備份或還原執行的唯一識別碼。<br /><br /> run_id 和 pdw_node_id 形成這個檢視的索引鍵。||  
|pdw_node_id|**int**|此記錄表格包含詳細資料的應用裝置節點的唯一識別碼。<br /><br /> run_id 和 pdw_node_id 形成這個檢視的索引鍵。|請參閱中的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|status|**nvarchar(16)**|執行目前的狀態。|'已取消'，' 已完成 '，'FAILED'、 '佇列更新'、 'RUNNING'|  
|start_time|**datetime**|在這個特定的節點作業開始時間。||  
|end_time|**datetime**|作業結束時間在這個特定的節點，如果有的話。||  
|total_elapsed_time|**int**|在這個特定的節點執行作業的總時間。|如果 total_elapsed_time 超過整數 （以毫秒為單位的 24.8 天） 的最大值，它會具體化失敗，因為溢位。<br /><br /> 以毫秒為單位的最大值相當於 24.8 天。|  
|進度|**int**|以百分比表示作業的進度。|0 到 100 之間|  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
