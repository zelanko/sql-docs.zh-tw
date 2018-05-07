---
title: sys.dm_exec_external_work (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d44d36f478e28518df525356c5fef3e4475bc0ff
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecexternalwork-transact-sql"></a>sys.dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  傳回每個計算節點上每個背景工作，工作負載的相關資訊。  
  
 若要識別工作查詢 sys.dm_exec_external_work 調整大小與外部資料來源 （例如 Hadoop 或外部的 SQL Server） 進行通訊。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|相關聯的 PolyBase 查詢的唯一識別碼。|請參閱*request_ID*中[sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|step_index|**int**|這個背景工作正在執行要求。|請參閱*step_index*中[sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|dms_step_index|**int**|這個背景工作正在執行的 DMS 計劃中的步驟。|請參閱[sys.dm_exec_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)。|  
|compute_node_id|**int**|背景工作的節點上執行。|請參閱[sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|型別|**nvarchar(60)**|外部工作類型。|' File 分割 '|  
|work_id|**int**|實際的分割線的識別碼。|大於或等於 0。|  
|input_name|**nvarchar(4000)**|要讀取輸入的名稱|使用 Hadoop 時的檔案名稱。|  
|read_location|**bigint**|位移或讀取位置。|要讀取的檔案的位移。|  
|bytes_processed|**bigint**|這個工作者所處理的位元組總數。|大於或等於 0。|  
|長度|**bigint**|分割或發生 Hadoop HDFS 區塊的長度|使用者可定義。 預設值是 64 M|  
|status|**nvarchar(32)**|背景工作的狀態|暫止，處理、 完成、 失敗、 已中止|  
|start_time|**datetime**|開始的工作||  
|end_time|**datetime**|工作的結尾||  
|total_elapsed_time|**int**|以毫秒為單位的總時間||  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase，疑難排解動態管理檢視](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
