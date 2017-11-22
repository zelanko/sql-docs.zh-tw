---
title: "sys.dm_pdw_request_steps (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/01/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 846806609d926aef8bfc7f9c15238dfec069727c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留撰寫指定的要求，或查詢中的所有步驟的相關資訊[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 它會列出一個資料列，每個查詢步驟。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar （32)**|request_id 和 step_index 便會產生這份檢視的索引鍵。<br /><br /> 與要求相關聯的唯一數值識別碼。|請參閱中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|request_id 和 step_index 便會產生這份檢視的索引鍵。<br /><br /> 這個步驟中的要求所組成的步驟順序的位置。|0 到 (n-1) 代表 n 的要求。|  
|operation_type|**nvarchar(35)**|此步驟中所代表的作業類型。|**DMS 查詢計劃作業：** 'ReturnOperation'、 'PartitionMoveOperation'、 'MoveOperation'、 'BroadcastMoveOperation'、 'ShuffleMoveOperation'、 'TrimMoveOperation'、 'CopyOperation'、 'DistributeReplicatedTableMoveOperation'<br /><br /> **SQL 查詢計劃作業：** 'OnOperation'、 'RemoteOperation'<br /><br /> **其他的查詢計劃作業：** 'MetaDataCreateOperation'、 'RandomIDOperation'<br /><br /> **外部的讀取作業：** 'HadoopShuffleOperation'、 'HadoopRoundRobinOperation'、 'HadoopBroadcastOperation'<br /><br /> **外部 MapReduce 作業：** 'HadoopJobOperation'、 'HdfsDeleteOperation'<br /><br /> **外部寫入的作業：** 'ExternalExportDistributedOperation'、 'ExternalExportReplicatedOperation'、 'ExternalExportControlOperation'<br /><br /> 如需詳細資訊，請參閱 < > 的 < 了解查詢計畫中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。|  
|distribution_type|**nvarchar （32)**|將會進行此步驟的散發類型。|'AllNodes'、 'AllDistributions'、 'AllComputeNodes'、 'ComputeNode'、 'Distribution'、 'SubsetNodes'、 'SubsetDistributions'，'未指定'|  
|時間步驟 location_type|**nvarchar （32)**|其中正在執行的步驟。|' Compute'、 '控制項'，'DMS'|  
|status|**nvarchar （32)**|這個步驟的狀態。|暫止、 執行中、 完成、 失敗、 UndoFailed、 PendingCancel、 取消、 復原、 中止|  
|error_id|**nvarchar(36)**|如果有的話，這個步驟中，與相關的錯誤的唯一識別碼。|請參閱的 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). 如果沒有發生錯誤，則為 NULL。|  
|start_time|**datetime**|在步驟開始執行的時間。|較小或等於目前的時間，大於或等於 end_compile_time 這個步驟所屬的查詢。 如需有關查詢的詳細資訊，請參閱[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|end_time|**datetime**|在此步驟中完成執行、 已取消，或失敗的時間。|較小或等於目前的時間，大於或等於 start_time。 針對目前在執行中的步驟設定為 NULL，或是排入佇列。|  
|total_elapsed_time|**int**|已執行的查詢步驟，以毫秒為單位的時間總數量。|介於 0 到 end_time 和 start_time 之間的差異。 0 代表佇列的步驟。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 仍的最大值。 這種情況會產生警告的 「 已超過最大值 」。<br /><br /> 以毫秒為單位的最大值就相當於 24.8 天。|  
|row_count|**bigint**|這項要求所傳回或變更的資料列總數。|0，表示沒有變更或傳回資料的步驟。 否則，受影響的資料列數目。|  
|command|**nvarchar(4000)**|保存這個步驟的命令的完整文字。|步驟的任何有效的要求字串。 NULL 的型別 MetaDataCreateOperation 作業時。 如果超過 4000 個字元，截斷。|  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱 「 最小值和最大值 」 的系統檢視的最大值一節，在[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="see-also"></a>請參閱＜  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
