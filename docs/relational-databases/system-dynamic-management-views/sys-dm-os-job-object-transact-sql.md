---
title: sys. dm_os_job_object （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 3fe2f22206d0882cafc8428d0fb9ccda22151ea2
ms.sourcegitcommit: dc6ea6665cd2fb58a940c722e86299396b329fec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84423425"
---
# <a name="sysdm_os_job_object-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

傳回單一資料列，其中描述管理 SQL Server 進程之工作物件的設定，以及工作物件層級的特定資源耗用量統計資料。 如果 SQL Server 不是在工作物件中執行，則會傳回空的集合。

工作物件是在作業系統層級執行 CPU、記憶體和 IO 資源管理的 Windows 結構。 如需工作物件的詳細資訊，請參閱[工作物件](/windows/desktop/ProcThread/job-objects)。
  
|資料行|資料類型|描述|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|指定 SQL Server 執行緒可在每個排程間隔期間使用的處理器週期部分。 此值會回報為10000迴圈排程間隔內可用週期的百分比，乘以邏輯 Cpu 的數目。 例如，值800在具有8個邏輯 Cpu 的 SQL Server 實例上，表示執行緒可以使用 Cpu 的完整容量。|
|cpu_affinity_mask|**bigint**|一個位元遮罩，用來描述 SQL Server 進程可在處理器群組內使用的邏輯處理器。 例如，cpu_affinity_mask 255 （二進位中的 1111 1111）表示可以使用前八個邏輯處理器。 <br /><br />此資料行是為了回溯相容性而提供。 它不會報告處理器群組，而當處理器群組包含超過64個邏輯處理器時，回報的值可能會不正確。 請改用資料 `process_physical_affinity` 行來判斷處理器親和性。|
|cpu_affinity_group|**int**|SQL Server 使用的處理器組數。|
|memory_limit_mb|**bigint**|工作物件中所有進程的認可記憶體數量上限（以 MB 為單位），包括 SQL Server，可以累積使用。| 
|process_memory_limit_mb |**bigint**|工作物件中的單一進程（例如 SQL Server）可以使用的認可記憶體數量上限（以 MB 為單位）。|
|workingset_limit_mb |**bigint**|SQL Server 工作集可以使用的記憶體數量上限（以 MB 為單位）。|
|non_sos_mem_gap_mb|**bigint**|執行緒堆疊、Dll 和其他非 SOS 記憶體配置的記憶體數量（以 MB 為單位）。 SOS 目標記憶體是和之間的 `process_memory_limit_mb` 差異 `non_sos_mem_gap_mb` 。| 
|low_mem_signal_threshold_mb|**bigint**|記憶體閾值（以 MB 為單位）。 當工作物件的可用記憶體數量低於此臨界值時，會將記憶體不足的通知信號傳送至 SQL Server 進程。 |
|total_user_time|**bigint**|自工作物件建立後，工作物件中的執行緒在使用者模式中所花費的總 100 ns 滴答數。 |
|total_kernel_time |**bigint**|自工作物件建立後，工作物件內線程在核心模式中所花費的總 100 ns 滴答數。 |
|write_operation_count |**bigint**|自工作物件建立後，SQL Server 發出的本機磁片上的寫入 IO 作業總數。 |
|read_operation_count |**bigint**|從建立工作物件以來，SQL Server 發出的本機磁片上的讀取 IO 作業總數。 |
|peak_process_memory_used_mb|**bigint**|自工作物件建立後，工作物件中的單一進程（例如 SQL Server）所使用的尖峰記憶體數量（以 MB 為單位）。| 
|peak_job_memory_used_mb|**bigint**|工作物件中的所有處理常式在工作物件建立後累積使用的尖峰記憶體數量（以 MB 為單位）。|
|process_physical_affinity|**Nvarchar （3072）**|位元遮罩，用來描述 SQL Server 進程可以在每個處理器群組中使用的邏輯處理器。 此資料行中的值是由一或多個值組所組成，每個都以大括弧括住。 在每個配對中，第一個值是處理器群組編號，而第二個值是該處理器群組的親和性位元遮罩。 例如，值 `{{0,a}{1,2}}` 表示處理器群組的親和性遮罩 `0` 是 `a` （ `1010` 二進位，表示使用處理器2和4），而處理器群組的親和性遮罩 `1` 是 `2` （ `10` 二進位，表示使用處理器2）。|
  
## <a name="permissions"></a>權限  
在 SQL Database 受控執行個體上，需要 `VIEW SERVER STATE` 許可權。 在 SQL Database 上，資料庫需要 `VIEW DATABASE STATE` 權限。  
 
## <a name="see-also"></a>另請參閱  

如需受控實例的詳細資訊，請參閱[SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。
  
