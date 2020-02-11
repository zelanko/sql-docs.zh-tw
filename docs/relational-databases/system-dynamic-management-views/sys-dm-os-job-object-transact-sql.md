---
title: sys. dm_os_job_object （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
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
ms.openlocfilehash: 43063bb56607d1b5a21ae04b40ee4c7a17825521
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900139"
---
# <a name="sysdm_os_job_object-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

傳回單一資料列，其中描述管理 SQL Server 進程之工作物件的設定，以及工作物件層級的特定資源耗用量統計資料。 如果 SQL Server 不是在工作物件中執行，則會傳回空的集合。 

工作物件是在作業系統層級執行 CPU、記憶體和 IO 資源管理的 Windows 結構。 如需工作物件的詳細資訊，請參閱[工作物件](/windows/desktop/ProcThread/job-objects)。 
  
|資料行|資料類型|描述|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|指定 SQL Server 執行緒可在每個排程間隔期間使用的處理器週期部分。 此值會回報為10000迴圈排程間隔內可用週期的百分比。 例如，值100表示執行緒可以使用 CPU 核心為其完整容量。|
|cpu_affinity_mask|**Bigint**|一個位元遮罩，用來描述 SQL Server 進程可在處理器群組內使用的邏輯處理器。 例如，cpu_affinity_mask 255 （二進位中的 1111 1111）表示可以使用前八個邏輯處理器。|
|cpu_affinity_group|**int**|SQL Server 使用的處理器組數。|
|memory_limit_mb|**Bigint**|工作物件中所有進程的認可記憶體數量上限（以 MB 為單位），包括 SQL Server，可以累積使用。| 
|process_memory_limit_mb |**Bigint**|工作物件中的單一進程（例如 SQL Server）可以使用的認可記憶體數量上限（以 MB 為單位）。|
|workingset_limit_mb |**Bigint**|SQL Server 工作集可以使用的記憶體數量上限（以 MB 為單位）。|
|non_sos_mem_gap_mb|**Bigint**|執行緒堆疊、Dll 和其他非 SOS 記憶體配置的記憶體數量（以 MB 為單位）。 SOS 目標記憶體是和`process_memory_limit_mb` `non_sos_mem_gap_mb`之間的差異。| 
|low_mem_signal_threshold_mb|**Bigint**|記憶體閾值（以 MB 為單位）。 當工作物件的可用記憶體數量低於此臨界值時，會將記憶體不足的通知信號傳送至 SQL Server 進程。 |
|total_user_time|**Bigint**|自工作物件建立後，工作物件中的執行緒在使用者模式中所花費的總 100 ns 滴答數。 |
|total_kernel_time |**Bigint**|自工作物件建立後，工作物件內線程在核心模式中所花費的總 100 ns 滴答數。 |
|write_operation_count |**Bigint**|自工作物件建立後，SQL Server 發出的本機磁片上的寫入 IO 作業總數。 |
|read_operation_count |**Bigint**|從建立工作物件以來，SQL Server 發出的本機磁片上的讀取 IO 作業總數。 |
|peak_process_memory_used_mb|**Bigint**|自工作物件建立後，工作物件中的單一進程（例如 SQL Server）所使用的尖峰記憶體數量（以 MB 為單位）。| 
|peak_job_memory_used_mb|**Bigint**|工作物件中的所有處理常式在工作物件建立後累積使用的尖峰記憶體數量（以 MB 為單位）。|
  
## <a name="permissions"></a>權限  
在 SQL Database 受控執行個體上， `VIEW SERVER STATE`需要許可權。 在 SQL Database 上，資料庫需要 `VIEW DATABASE STATE` 權限。  
 
## <a name="see-also"></a>另請參閱  

如需受控實例的詳細資訊，請參閱[SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。
  
