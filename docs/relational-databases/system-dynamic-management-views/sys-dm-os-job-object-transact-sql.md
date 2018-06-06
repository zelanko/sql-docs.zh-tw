---
title: sys.dm_os_job_object (Azure SQL Database) |Microsoft 文件
ms.custom: ''
ms.date: 04/17/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 8ab408179388ca10821ad79e855e39fd3ec7eb01
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmosjobobject-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

傳回單一資料列描述管理 SQL Server 處理序，以及特定作業的物件層級的資源耗用量統計資料的工作物件的設定。 如果 SQL Server 未執行中工作物件會傳回空集合。 

工作物件是 Windows 建構，可實作作業系統層級的 CPU、 記憶體和 IO 資源管理。 如需工作物件的詳細資訊，請參閱[工作物件](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)。 

> [!NOTE]
> Sys.dm_os_job_object DMV 目前可能顯示為 sys.dm_job_object。 這是暫時性：`sys.dm_os_job_object`將會永久這個 DMV 的名稱。 
  
|資料行|資料類型|Description|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|指定的 SQL Server 執行緒可以在每個排程的間隔期間使用的處理器循環的部分。 報告的值是 10000 循環排程的間隔內可用的循環的百分比。 例如，執行緒可以使用 CPU 核心數的值 100 表示是其完整的容量。|
|cpu_affinity_mask|**bigint**|描述邏輯處理器的位元遮罩的 SQL Server 程序可以使用處理器群組中。 例如，cpu_affinity_mask 255 (1111 1111 二進位) 表示，前八位可用的邏輯處理器。|
|cpu_affinity_group|**int**|SQL Server 使用的處理器群組數目。|
|memory_limit_mb|**bigint**|已認可的記憶體，以 mb 為單位的工作物件，包括 SQL Server 中的所有處理程序可以使用累積的數量上限。| 
|process_memory_limit_mb |**bigint**|已認可的記憶體，以 mb 為單位的工作物件，例如 SQL Server 中的單一處理序可以使用最大數量。|
|workingset_limit_mb |**bigint**|以 mb 為單位的 SQL Server 的工作集可以使用的記憶體數量上限。|
|non_sos_mem_gap_mb|**bigint**|以 mb 為單位的記憶體數量為設定的執行緒堆疊、 Dll 以及其他非 SOS 記憶體配置。 SOS 目標記憶體是之間的差異`process_memory_limit_mb`和`non_sos_mem_gap_mb`。| 
|low_mem_signal_threshold_mb|**bigint**|記憶體臨界值，以 mb 為單位。 當工作物件的可用記憶體數量低於此臨界值時，記憶體不足的通知訊號傳送至 SQL Server 處理序。 |
|total_user_time|**bigint**|工作物件中的執行緒所在使用者模式中，自工作物件建立之後的 100 ns 刻度的總數。 |
|total_kernel_time |**bigint**|工作物件中的執行緒所核心模式中的工作物件建立之後的 100 ns 刻度的總數。 |
|write_operation_count |**bigint**|總數的寫入 IO 發出 SQL Server 所建立的工作物件的本機磁碟上的作業。 |
|read_operation_count |**bigint**|發出 SQL Server 所建立的工作物件的本機磁碟上的讀取 IO 作業總數。 |
|peak_process_memory_used_mb|**bigint**|工作物件建立以來，已使用之記憶體尖峰數量，以 mb 為單位的工作物件，例如 SQL Server 中的單一處理。| 
|peak_job_memory_used_mb|**bigint**|已建立之記憶體尖峰數量，以 mb 為單位，因為工作物件累積使用工作物件中的所有處理程序。|
  
## <a name="permissions"></a>Permissions  
SQL 資料庫 Managed 執行個體上，需要`VIEW SERVER STATE`權限。 SQL 資料庫上需要`VIEW DATABASE STATE`資料庫的權限。  
 
## <a name="see-also"></a>另請參閱  

受管理的執行個體上的資訊，請參閱[SQL 資料庫 Managed 執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。
  
