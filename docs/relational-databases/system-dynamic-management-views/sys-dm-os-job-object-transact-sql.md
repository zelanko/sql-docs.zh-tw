---
title: sys.dm_os_job_object (Azure SQL Database) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 074981f19f0eb74a7e7c7d4e82466957f0ff98b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63047037"
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

傳回單一資料列描述管理 SQL Server 處理序，以及特定作業物件層級的資源耗用量統計資料的工作物件的組態。 如果 SQL Server 未執行中工作物件，則傳回空集合。 

工作物件是一種 Windows 建構，會實作在作業系統層級的 CPU、 記憶體和 IO 資源管理。 如需工作物件的詳細資訊，請參閱[工作物件](/windows/desktop/ProcThread/job-objects)。 
  
|[資料行]|資料類型|描述|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|指定 SQL Server 執行緒可以使用每個排程的間隔期間的處理器循環的部分。 報告的值是 10000 週期排程的間隔內可用的循環的百分比。 例如，執行緒可以使用 CPU 核心值 100 表示是其完整的容量。|
|cpu_affinity_mask|**bigint**|描述的邏輯處理器的位元遮罩處理器群組中可以使用的 SQL Server 處理序。 比方說，cpu_affinity_mask 255 (1111 1111 二進位檔中) 表示，前八個可用的邏輯處理器。|
|cpu_affinity_group|**int**|SQL server 所使用的處理器群組數目。|
|memory_limit_mb|**bigint**|認可的記憶體，以 mb 為單位的工作物件，包括 SQL Server 中的所有處理序都可以使用最大數量。| 
|process_memory_limit_mb |**bigint**|認可的記憶體，以 mb 為單位，可以使用工作物件，例如 SQL Server 中的單一處理序最大數量。|
|workingset_limit_mb |**bigint**|以 mb 為單位的 SQL Server 工作集可以使用的記憶體最大數量。|
|non_sos_mem_gap_mb|**bigint**|以 mb 為單位的記憶體數量會保留為執行緒堆疊、 Dll 以及其他非 SOS 記憶體配置。 SOS 目標記憶體是之間的差異`process_memory_limit_mb`和`non_sos_mem_gap_mb`。| 
|low_mem_signal_threshold_mb|**bigint**|記憶體臨界值，以 mb 為單位。 當工作物件的可用記憶體數量低於此臨界值時，則會將低記憶體通知訊號傳送至 SQL Server 處理序。 |
|total_user_time|**bigint**|工作物件中的執行緒花費在使用者模式中，因為建立工作物件的 100 ns 刻度總數。 |
|total_kernel_time |**bigint**|工作物件中的執行緒花費在核心模式中，因為建立工作物件的 100 ns 刻度總數。 |
|write_operation_count |**bigint**|總數寫入之後建立的工作物件，SQL Server 所發出的本機磁碟上的 IO 作業。 |
|read_operation_count |**bigint**|在建立工作物件之後，SQL Server 所發出的本機磁碟上的讀取 IO 作業總數。 |
|peak_process_memory_used_mb|**bigint**|建立工作物件之後，已使用之記憶體尖峰數量，以 mb 為單位的工作物件，例如 SQL Server 中的單一處理。| 
|peak_job_memory_used_mb|**bigint**|已建立之記憶體尖峰數量，以 mb 為單位，因為工作物件累積使用工作物件中的所有處理程序。|
  
## <a name="permissions"></a>Permissions  
SQL Database 受控執行個體，需要`VIEW SERVER STATE`權限。 在 SQL Database 上需要`VIEW DATABASE STATE`資料庫的權限。  
 
## <a name="see-also"></a>另請參閱  

如需受控執行個體的資訊，請參閱[SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。
  
