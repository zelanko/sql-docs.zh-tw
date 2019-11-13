---
title: sys.databases dm_os_memory_nodes （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_nodes_TSQL
- sys.dm_os_memory_nodes
- sys.dm_os_memory_nodes_TSQL
- dm_os_memory_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_nodes dynamic management view
ms.assetid: bf4032fe-7db1-40e9-a62e-d69cebff4b44
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f68524b2713b9d662c9e9ed0950334ea0a94ece
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983127"
---
# <a name="sysdm_os_memory_nodes-transact-sql"></a>sys.dm_os_memory_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部的配置會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體管理員。 追蹤來自 sys.databases 的進程記憶體計數器之間的差異**dm_os_process_memory**和內部計數器，可以表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體空間中外部元件的記憶體使用量。  
  
 每個實體 NUMA 記憶體節點都會建立一些節點。 這些可能會與 sys.databases 中的 CPU 節點不同**dm_os_nodes**。  
  
 系統不會追蹤直接透過 Windows 記憶體配置常式完成的配置。 下表將提供僅使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體管理員介面所完成之記憶體配置的相關資訊。  
  
> [!NOTE]  
>  若要從 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 或 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]呼叫此，請使用**dm_pdw_nodes_os_memory_nodes**的名稱。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|指定記憶體節點的識別碼。 與**dm_os_memory_clerks**的**memory_node_id**相關。 不可為 Null。|  
|**virtual_address_space_reserved_kb**|**bigint**|指出未經認可也沒有對應至實體頁面的虛擬位址保留數目 (以 KB 為單位)。 不可為 Null。|  
|**virtual_address_space_committed_kb**|**bigint**|指定已經認可或對應至實體頁面的虛擬位址數量 (以 KB 為單位)。 不可為 Null。|  
|**locked_page_allocations_kb**|**bigint**|指定已經由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 鎖定的實體記憶體數量 (以 KB 為單位)。 不可為 Null。|  
|**single_pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 由這個節點上執行之執行緒使用單一頁面配置器所配置的認可記憶體數量 (以 KB 為單位)。 這個記憶體是從緩衝集區配置。 這個值會指出發生配置要求的節點，而非滿足配置要求的實體位置。|  
|**pages_kb**|**bigint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 指定由 Memory Manager 頁面配置器從這個 NUMA 節點所配置的認可記憶體數量 (以 KB 為單位)。 不可為 Null。|  
|**multi_pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 由這個節點上執行之執行緒使用多頁配置器所配置的認可記憶體數量 (以 KB 為單位)。 這個記憶體是在緩衝集區外部配置。 這個值會指出發生配置要求的節點，而非滿足配置要求的實體位置。|  
|**shared_memory_reserved_kb**|**bigint**|指定已經從這個節點保留的共用記憶體數量 (以 KB 為單位)。 不可為 Null。|  
|**shared_memory_committed_kb**|**bigint**|指定已經在這個節點上認可的共用記憶體數量 (以 KB 為單位)。 不可為 Null。|  
|**cpu_affinity_mask**|**bigint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 僅供內部使用。 不可為 Null。|  
|**online_scheduler_mask**|**bigint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 僅供內部使用。 不可為 Null。|  
|**processor_group**|**smallint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 僅供內部使用。 不可為 Null。|  
|**foreign_committed_kb**|**bigint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 指定來自其他記憶體節點的認可記憶體數量 (以 KB 為單位)。 不可為 Null。|  
|**target_kb** |**bigint** |**適用于**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 和更新版本，[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 指定記憶體節點的記憶體目標（以 KB 為單位）。 |   
|**pdw_node_id**|**int**|**適用于**： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="permissions"></a>Permissions

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上，需要 `VIEW SERVER STATE` 許可權。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高階層級上，需要資料庫中的 `VIEW DATABASE STATE` 許可權。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準和基本層上，需要**伺服器管理員**或 Azure Active Directory 的系統**管理員**帳戶。   

## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理 Views &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


