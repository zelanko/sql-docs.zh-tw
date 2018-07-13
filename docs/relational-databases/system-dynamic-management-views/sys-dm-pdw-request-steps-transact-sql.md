---
title: sys.dm_pdw_request_steps (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5a6fbf843d3a9aca9172a5ab6ea828a0c0b0a40a
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926839"
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>sys.dm_pdw_request_steps & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留的撰寫指定的要求，或查詢中的所有步驟的相關資訊[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 它會列出每個查詢步驟的一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id 和 step_index 組成此檢視的索引鍵。<br /><br /> 與要求相關聯的唯一數值識別碼。|請參閱中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|request_id 和 step_index 組成此檢視的索引鍵。<br /><br /> 此步驟中的要求，以進行的步驟順序的位置。|0 到 (n-1) 代表 n 的要求。|  
|operation_type|**nvarchar(35)**|此步驟中所代表的作業類型。|**DMS 查詢計劃作業：** '3a:onoperation、remoteoperation、returnoperation'、 'PartitionMoveOperation'、 '執行'、 'BroadcastMoveOperation'、 'ShuffleMoveOperation'、 '下列'、 'CopyOperation'、 'DistributeReplicatedTableMoveOperation'<br /><br /> **SQL 查詢計劃作業：** '下列'、 '執行'<br /><br /> **其他的查詢計劃作業：** 'MetaDataCreateOperation'、 'RandomIDOperation'<br /><br /> **外部作業讀取：** 'HadoopShuffleOperation'、 'HadoopRoundRobinOperation'、 'HadoopBroadcastOperation'<br /><br /> **外部 MapReduce 作業：** 'HadoopJobOperation'、 'HdfsDeleteOperation'<br /><br /> **外部作業寫入：** 'ExternalExportDistributedOperation'、 'ExternalExportReplicatedOperation'、 'ExternalExportControlOperation'<br /><br /> 如需詳細資訊，請參閱 「 了解查詢計劃 」，在[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。|  
|distribution_type|**nvarchar(32)**|此步驟中將會進行的分佈的類型。|'AllNodes'、 'AllDistributions'、 'AllComputeNodes'、 'ComputeNode'、 'Distribution'、 'SubsetNodes'、 'SubsetDistributions'，'未指定'|  
|location_type|**nvarchar(32)**|步驟執行。|' Compute'、 'Control'，'DMS'|  
|status|**nvarchar(32)**|此步驟的狀態。|暫止、 執行中、 完成、 失敗、 UndoFailed PendingCancel，已取消、 復原、 已中止|  
|error_id|**nvarchar(36)**|如果有的話，此步驟中，與相關的錯誤的唯一識別碼。|請參閱的 error_id [sys.dm_pdw_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)。 如果未不發生任何錯誤，則為 NULL。|  
|start_time|**datetime**|步驟開始執行的時間。|較小或等於目前的時間和大於或等於 end_compile_time 屬於此步驟中的查詢。 如需有關查詢的詳細資訊，請參閱 < [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|end_time|**datetime**|在此步驟中完成執行、 已取消，或失敗的時間。|較小或等於目前的時間和大於或等於 start_time。 如需目前在執行中的步驟設定為 NULL 或已排入佇列。|  
|total_elapsed_time|**int**|已執行的查詢步驟，以毫秒為單位的時間總量。|介於 0 到 end_time 和 start_time 之間的差異。 0 代表已排入佇列的步驟。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 仍是最大值。 這種情況會產生警告 」 的最大值已超過 」。<br /><br /> 以毫秒為單位的最大值相當於 24.8 天。|  
|row_count|**bigint**|資料列總數會變更，或這項要求所傳回。|0 表示未變更或傳回資料的步驟。 受影響的資料列數目，否則為。|  
|command|**nvarchar(4000)**|保留此步驟的命令的完整文字。|步驟的任何有效的要求字串。 NULL 的型別 MetaDataCreateOperation 作業時。 如果超過 4000 個字元，就會截斷。|  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱 「 最小值與最大值 」 的系統檢視的最大值一節，在[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
