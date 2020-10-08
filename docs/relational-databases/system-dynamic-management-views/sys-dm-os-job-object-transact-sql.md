---
description: sys.dm_os_job_object (Azure SQL Database)
title: sys.dm_os_job_object (Azure SQL Database) Microsoft Docs
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
ms.openlocfilehash: c8ee9c4054a9bb39f7eebcd30aa0fa9c85d7bde7
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834075"
---
# <a name="sysdm_os_job_object-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

傳回單一資料列，描述管理 SQL Server 進程的工作物件設定，以及工作物件層級的特定資源耗用量統計資料。 如果 SQL Server 不是在工作物件中執行，則會傳回空的集合。

工作物件是在作業系統層級執行 CPU、記憶體和 IO 資源管理的 Windows 結構。 如需工作物件的詳細資訊，請參閱 [工作物件](/windows/desktop/ProcThread/job-objects)。
  
|資料行|資料類型|描述|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|指定 SQL Server 執行緒可在每個排程間隔期間使用的處理器迴圈部分。 此值會回報為10000週期排程間隔內可用迴圈的百分比，乘以邏輯 Cpu 的數目。 例如，在具有8個邏輯 Cpu 的 SQL Server 實例上，值800表示執行緒可以使用 Cpu 的完整容量。|
|cpu_affinity_mask|**bigint**|一種位元遮罩，描述 SQL Server 進程可在處理器群組內使用的邏輯處理器。 例如，cpu_affinity_mask 255 (1111 1111 in binary) 表示可以使用前八個邏輯處理器。 <br /><br />此資料行是為了回溯相容性而提供。 它不會報告處理器群組，且當處理器群組包含64個以上的邏輯處理器時，回報的值可能不正確。 請改用此資料 `process_physical_affinity` 行來判斷處理器親和性。|
|cpu_affinity_group|**int**|SQL Server 所使用的處理器群組數目。|
|memory_limit_mb|**bigint**|工作物件中所有進程（包括 SQL Server）的認可記憶體數量上限（以 MB 為單位）可以累積使用。| 
|process_memory_limit_mb |**bigint**|工作物件中的單一進程（例如 SQL Server）可以使用的認可記憶體數量上限（以 MB 為單位）。|
|workingset_limit_mb |**bigint**|SQL Server 工作集可使用的記憶體數量上限（以 MB 為單位）。|
|non_sos_mem_gap_mb|**bigint**|針對執行緒堆疊、Dll 和其他非 SOS 記憶體配置所設定的記憶體數量（以 MB 為單位）。 SOS 目標記憶體是與之間的 `process_memory_limit_mb` 差異 `non_sos_mem_gap_mb` 。| 
|low_mem_signal_threshold_mb|**bigint**|記憶體臨界值（以 MB 為單位）。 當工作物件的可用記憶體容量低於此臨界值時，就會將記憶體不足通知信號傳送到 SQL Server 進程。 |
|total_user_time|**bigint**|在工作物件建立後，工作物件中的執行緒在使用者模式下花費的 100 ns 滴答數總計。 |
|total_kernel_time |**bigint**|在工作物件建立後，工作物件內的執行緒在核心模式中花費的 100 ns 滴答數總計。 |
|write_operation_count |**bigint**|自從建立工作物件之後，SQL Server 所發出之本機磁片上的寫入 IO 作業總數。 |
|read_operation_count |**bigint**|自從建立工作物件之後，SQL Server 所發出之本機磁片上的讀取 IO 作業總數。 |
|peak_process_memory_used_mb|**bigint**|在工作物件建立之後，已使用工作物件中的單一進程（例如 SQL Server）的尖峰記憶體量（以 MB 為單位）。| 
|peak_job_memory_used_mb|**bigint**|工作物件中的所有進程在建立工作物件之後，已累積使用的記憶體尖峰數量（以 MB 為單位）。|
|process_physical_affinity|**Nvarchar (3072) **|位元遮罩，描述 SQL Server 進程可在每個處理器群組中使用的邏輯處理器。 此資料行中的值是由一或多個值組所組成，每個值組都以大括弧括住。 在每個配對中，第一個值是處理器群組編號，而第二個值是該處理器群組的親和性位元遮罩。 例如，此值 `{{0,a}{1,2}}` 表示處理器群組的親和性遮罩 `0` 會 `a` `1010` 以二進位 (，表示會使用處理器2和 4) ，而處理器群組的親和性遮罩 `1` 會 `2` (`10` 二進位，表示) 使用處理器2。|
  
## <a name="permissions"></a>權限  
在 SQL 受控執行個體上，需要 `VIEW SERVER STATE` 許可權。 在 SQL Database 上，資料庫需要 `VIEW DATABASE STATE` 權限。  
 
## <a name="see-also"></a>另請參閱  

如需受控實例的詳細資訊，請參閱 [SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance)。
