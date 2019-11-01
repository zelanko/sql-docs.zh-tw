---
title: _pdw_request_steps （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 260b822d111f94fc567704cd908cb5632e3bdcaf
ms.sourcegitcommit: 27c267bf2a3cfaf2abcb5f3777534803bf4cffe5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2019
ms.locfileid: "73240781"
---
# <a name="sysdm_pdw_request_steps-transact-sql"></a>sys.databases _pdw_request_steps （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]中撰寫給定要求或查詢之所有步驟的相關資訊。 它會針對每個查詢步驟列出一個資料列。  
  
|[狀態]|資料類型|[描述]|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id 和 step_index 組成此視圖的索引鍵。<br /><br /> 與要求相關聯的唯一數值識別碼。|請參閱[_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id。|  
|step_index|**整數**|request_id 和 step_index 組成此視圖的索引鍵。<br /><br /> 此步驟在組成要求的步驟順序中的位置。|0到（n-1），代表具有 n 個步驟的要求。|  
|operation_type|**nvarchar(35)**|此步驟所表示的作業類型。|**DMS 查詢計劃作業：** ' ReturnOperation '、' PartitionMoveOperation '、' MoveOperation '、' BroadcastMoveOperation '、' ShuffleMoveOperation '、' TrimMoveOperation '、' CopyOperation '、' DistributeReplicatedTableMoveOperation '<br /><br /> **SQL 查詢計劃作業：** ' OnOperation '、' RemoteOperation '<br /><br /> **其他查詢計劃作業：** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **讀取的外部作業：** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **MapReduce 的外部作業：** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **寫入的外部作業：** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> 如需詳細資訊，請參閱 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中的「瞭解查詢計劃」。 <br /><br />  查詢計劃也可能受到資料庫設定的影響。  如需詳細資料，請參閱[ALTER DATABASE SET 選項](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-set-options?toc=/azure/sql-data-warehouse/toc.json&bc=/azure/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest)。|  
|distribution_type|**nvarchar(32)**|此步驟將會進行的散發類型。|' AllNodes '、' AllDistributions '、' AllComputeNodes '、' ComputeNode '、' 散發 '、' SubsetNodes '、' SubsetDistributions '、' 未指定 '|  
|location_type|**nvarchar(32)**|步驟執行所在的位置。|「計算」、「控制項」、「DMS」|  
|status|**nvarchar(32)**|此步驟的狀態。|暫止、執行中、完成、失敗、UndoFailed、PendingCancel、取消、復原、中止|  
|error_id|**Nvarchar （36）**|與此步驟相關聯之錯誤的唯一識別碼（如果有的話）。|請參閱 error_id 的[_pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)。 如果未發生錯誤，則為 Null。|  
|start_time|**datetime**|步驟開始執行的時間。|小於或等於目前的時間，或是大於或等於此步驟所屬查詢的 end_compile_time。 如需查詢的詳細資訊，請參閱[sys.databases _pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|end_time|**datetime**|此步驟完成執行、已取消或失敗的時間。|小於或等於目前時間且大於或等於 start_time。 針對目前執行中或已排入佇列的步驟，將設為 Null。|  
|total_elapsed_time|**整數**|查詢步驟已執行的總時間量（以毫秒為單位）。|介於0和 end_time 與 start_time 之間的差異。 0表示已排入佇列的步驟。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 將會繼續成為最大值。 此狀況會產生「已超過最大值」的警告。<br /><br /> 最大值（以毫秒為單位）相當於24.8 天。|  
|row_count|**bigint**|此要求變更或傳回的總數據列數。|0適用于未變更或傳回資料的步驟。 否則，受影響的資料列數目。|  
|command|**nvarchar(4000)**|保存此步驟之命令的完整文字。|步驟的任何有效要求字串。 當作業的型別為 MetaDataCreateOperation 時，則為 Null。 如果超過4000個字元，則會截斷。|  
  
 如需此視圖所保留之最大資料列的詳細資訊，請參閱 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]中「最小值和最大值」一節的最大系統檢視值一節。  
  
## <a name="see-also"></a>請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理&#40;Views transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
