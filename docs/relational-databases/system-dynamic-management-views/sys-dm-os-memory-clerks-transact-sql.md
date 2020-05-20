---
title: sys.databases dm_os_memory_clerks （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_clerks
- sys.dm_os_memory_clerks
- dm_os_memory_clerks_TSQL
- sys.dm_os_memory_clerks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_clerks dynamic management view
ms.assetid: 1d556c67-5c12-46d5-aa8c-7ec1bb858df7
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: feb07dbf92a68ec12a1c4c6ae8f509acc3320867
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829355"
---
# <a name="sysdm_os_memory_clerks-transact-sql"></a>sys.dm_os_memory_clerks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中所有目前作用中記憶體 Clerk 集。  
  
> [!NOTE]  
>  若要從或呼叫此 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，請使用**dm_pdw_nodes_os_memory_clerks**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**memory_clerk_address**|**varbinary(8)**|指定記憶體 Clerk 的唯一記憶體位址。 這是主索引鍵資料行。 不可為 Null。|  
|**type**|**nvarchar(60)**|指定記憶體 Clerk 的類型。 每一個 Clerk 都有特定類型，例如 CLR Clerks MEMORYCLERK_SQLCLR。 不可為 Null。|  
|**name**|**nvarchar(256)**|指定這個記憶體 Clerk 的內部指派名稱。 元件可以有特定類型的數個記憶體 Clerk。 元件可選擇使用特定名稱來識別相同類型的記憶體 Clerk。 不可為 Null。|  
|**memory_node_id**|**smallint**|指定記憶體節點的識別碼。 不可為 Null。|  
|**single_pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。|  
|**pages_kb**|**bigint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 指定這個記憶體 Clerk 的已配置分頁記憶體數量 (以 KB 為單位)。 不可為 Null。|  
|**multi_pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 已配置的多重頁面記憶體數量 (以 KB 為單位)。 這是使用記憶體節點之多重頁面配置器所配置的記憶體數量。 這個記憶體是配置在緩衝集區之外，並利用記憶體節點的虛擬配置器。 不可為 Null。|  
|**virtual_memory_reserved_kb**|**bigint**|指定記憶體 Clerk 所保留的虛擬記憶體數量。 不可為 Null。|  
|**virtual_memory_committed_kb**|**bigint**|指定記憶體 Clerk 所認可的虛擬記憶體數量。 已認可的記憶體數量一律小於已保留的記憶體數量。 不可為 Null。|  
|**awe_allocated_kb**|**bigint**|指定鎖定在實體記憶體中且未由作業系統移出分頁的記憶體數量 (KB)。 不可為 Null。|  
|**shared_memory_reserved_kb**|**bigint**|指定記憶體 Clerk 所保留的共用記憶體數量。 記憶體數量已保留給共用記憶體和檔案對應使用。 不可為 Null。|  
|**shared_memory_committed_kb**|**bigint**|指定記憶體 Clerk 認可的共用記憶體數量。 不可為 Null。|  
|**page_size_in_bytes**|**bigint**|指定這個記憶體 Clerk 的頁面配置資料粒度。 不可為 Null。|  
|**page_allocator_address**|**varbinary(8)**|指定頁面配置器的位址。 這個位址對記憶體人員而言是唯一的，而且可以在**sys.databases**中用來找出系結到這個職員的記憶體物件。 dm_os_memory_objects 不可為 Null。|  
|**host_address**|**varbinary(8)**|指定這個記憶體 Clerk 之主機的記憶體位址。 如需詳細資訊，請參閱[dm_os_hosts &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)。 元件（例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client）會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 透過主機介面來存取記憶體資源。<br /><br /> 0x00000000 = 記憶體 Clerk 屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br /> 不可為 Null。|  
|**pdw_node_id**|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="permissions"></a>權限 

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體管理員是由三層階層組成。 階層底端是記憶體節點。 中層級是由記憶體 Clerk、記憶體快取和記憶體集區所組成。 最上層是由記憶體物件組成。 這些物件通常用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體中配置記憶體。  
  
 記憶體節點為低階配置器提供介面和實作。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內，只有記憶體 Clerk 可存取記憶體節點。 記憶體 Clerk 存取記憶體節點介面來配置記憶體。 記憶體節點也追蹤使用 Clerk 配置的記憶體來進行診斷。 配置大量記憶體的每一個元件必須建立它自己的記憶體 Clerk，並使用 Clerk 介面來配置它的所有記憶體。 元件經常在啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時建立其對應的 Clerk。  
  
## <a name="see-also"></a>另請參閱  

 [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [dm_os_sys_info &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [dm_exec_query_memory_grants &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [dm_exec_requests &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [dm_exec_query_plan &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [dm_exec_sql_text &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
  
  


