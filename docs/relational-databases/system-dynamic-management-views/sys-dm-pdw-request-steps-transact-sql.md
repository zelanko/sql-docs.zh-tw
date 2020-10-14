---
description: 'sys.dm_pdw_request_steps (Transact-sql) '
title: sys.dm_pdw_request_steps (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/28/2020
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
ms.openlocfilehash: 1d2672b9539770dd257b3db1bbce7af9c8a96c4e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035231"
---
# <a name="sysdm_pdw_request_steps-transact-sql"></a>sys.dm_pdw_request_steps (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存在中撰寫給定要求或查詢之所有步驟的相關資訊 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 它會針對每個查詢步驟列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id 並 step_index 組成此視圖的金鑰。<br /><br /> 與要求相關聯的唯一數值識別碼。|請參閱 [sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id。|  
|step_index|**int**|request_id 並 step_index 組成此視圖的金鑰。<br /><br /> 此步驟在提出要求的步驟順序中的位置。|0到 (n-1) 用於具有 n 個步驟的要求。|  
|plan_node_id|**int**|對應至執行計畫中該步驟之操作員識別碼的節點識別碼。|無|  
|operation_type|**nvarchar(35)**|此步驟所表示的作業類型。|**DMS 查詢計劃作業：** ' ReturnOperation '、' PartitionMoveOperation '、' MoveOperation '、' BroadcastMoveOperation '、' ShuffleMoveOperation '、' TrimMoveOperation '、' CopyOperation '、' DistributeReplicatedTableMoveOperation '<br /><br /> **SQL 查詢計劃作業：** ' OnOperation '、' RemoteOperation '<br /><br /> **其他查詢計劃作業：** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **讀取的外部作業：** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **MapReduce 的外部作業：** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **寫入的外部作業：** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> 如需詳細資訊，請參閱中的「瞭解查詢計劃」 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 。 <br /><br />  查詢計劃也可能會受到資料庫設定的影響。  查看 [ALTER DATABASE SET 選項](../../t-sql/statements/alter-database-transact-sql-set-options.md?bc=%252fazure%252fsql-data-warehouse%252fbreadcrumb%252ftoc.json&toc=%252fazure%252fsql-data-warehouse%252ftoc.json&view=azure-sqldw-latest) 以取得詳細資料。|  
|distribution_type|**nvarchar(32)**|此步驟將會進行的散發類型。|' >allnodes '、' AllDistributions '、' AllComputeNodes '、' ComputeNode '、' 散發 '、' SubsetNodes '、' SubsetDistributions '、' 未指定 '|  
|location_type|**nvarchar(32)**|步驟執行所在的位置。|「計算」、「控制」、「DMS」|  
|status|**nvarchar(32)**|此步驟的狀態。|暫止、執行中、完成、失敗、UndoFailed、PendingCancel、取消、復原、已中止|  
|error_id|**Nvarchar (36) **|與此步驟相關聯之錯誤的唯一識別碼（如果有的話）。|請參閱 [sys.dm_pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)的 error_id。 如果未發生任何錯誤，則為 Null。|  
|start_time|**datetime**|步驟開始執行的時間。|小於或等於目前的時間，而且大於或等於這個步驟所屬查詢的 end_compile_time。 如需查詢的詳細資訊，請參閱 [sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|end_time|**datetime**|此步驟完成執行、已取消或失敗的時間。|小於或等於目前時間，大於或等於 start_time。 針對目前執行中或已排入佇列的步驟，將設定為 Null。|  
|total_elapsed_time|**int**|查詢步驟執行的總時間量（以毫秒為單位）。|介於0和 end_time 與 start_time 之間的差異。 0表示已排入佇列的步驟。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 將會繼續成為最大值。 這種狀況會產生「已超過最大值」的警告。<br /><br /> 以毫秒為單位的最大值相當於24.8 天。|  
|row_count|**bigint**|此要求變更或傳回的資料列總數。|受此步驟影響的資料列數目。  大於或等於零，表示資料操作步驟。  -1 表示無法運算元據的步驟。|  
|estimated_rows|**bigint**|在查詢編譯期間計算的工作資料列總數。|步驟所估計的資料列數目。  大於或等於零，表示資料操作步驟。  -1 表示無法運算元據的步驟。|  
|命令|**nvarchar(4000)**|保存此步驟之命令的完整文字。|步驟的任何有效要求字串。 當作業的型別為 MetaDataCreateOperation 時，則為 Null。 如果超過4000個字元，則會截斷。|  
  
 如需此視圖所保留之最大資料列的詳細資訊，請參閱中的「最小值與最大值」一節中的最大系統檢視值區段 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
