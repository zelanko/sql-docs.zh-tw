---
title: sys.databases dm_os_memory_objects （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_objects
- sys.dm_os_memory_objects
- sys.dm_os_memory_objects_TSQL
- dm_os_memory_objects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_objects dynamic management view
ms.assetid: 5688bcf8-5da9-4ff9-960b-742b671d7096
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eece83b3c1fcde0d33a515c85eeb2cdac0a72cf4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827874"
---
# <a name="sysdm_os_memory_objects-transact-sql"></a>sys.dm_os_memory_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回目前所配置的記憶體物件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以使用**dm_os_memory_objects sys.databases**來分析記憶體使用量，並找出可能的記憶體流失。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary(8)**|記憶體物件的位址。 不可為 Null。|  
|**parent_address**|**varbinary(8)**|父記憶體物件的位址。 可為 Null。|  
|**pages_allocated_count**|**int**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 這個物件所配置的頁數。 不可為 Null。|  
|**pages_in_bytes**|**bigint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 這個記憶體物件執行個體所配置的記憶體數量 (以位元組為單位)。 不可為 Null。|  
|**creation_options**|**int**|僅供內部使用。 可為 Null。|  
|**bytes_used**|**bigint**|僅供內部使用。 可為 Null。|  
|**type**|**nvarchar(60)**|記憶體物件的類型。<br /><br /> 這表示這個記憶體物件所屬的某個元件，或是記憶體物件的函數。 可為 Null。|  
|**name**|**varchar(128)**|僅供內部使用。 可為 Null。|  
|**memory_node_id**|**smallint**|這個記憶體物件正在使用之記憶體節點的識別碼。 不可為 Null。|  
|**creation_time**|**datetime**|僅供內部使用。 可為 Null。|  
|**max_pages_allocated_count**|**int**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 這個記憶體物件所配置的最大頁數。 不可為 Null。|  
|**page_size_in_bytes**|**int**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 這個物件所配置的頁面大小 (以位元組為單位)。 不可為 Null。|  
|**max_pages_in_bytes**|**bigint**|這個記憶體物件所使用的最大記憶體數量。 不可為 Null。|  
|**page_allocator_address**|**varbinary(8)**|頁面配置器的記憶體位址。 不可為 Null。 如需詳細資訊，請參閱[dm_os_memory_clerks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)。|  
|**creation_stack_address**|**varbinary(8)**|僅供內部使用。 可為 Null。|  
|**sequence_num**|**int**|僅供內部使用。 可為 Null。|  
|**partition_type**|**int**|資料分割的類型：<br /><br /> 0-非可分割記憶體物件<br /><br /> 1-可分割記憶體物件，目前未分割<br /><br /> 2-可分割 memory 物件，依 NUMA 節點進行分割。 在具有單一 NUMA 節點的環境中，這相當於1。<br /><br /> 3-可分割 memory 物件，依 CPU 分割。|  
|**contention_factor**|**real**|值，指定此記憶體物件上的爭用，0表示沒有爭用。 每當指定的記憶體配置數目反映該期間內的爭用時，就會更新此值。 僅適用于安全線程的記憶體物件。|  
|**waiting_tasks_count**|**bigint**|此記憶體物件的等候次數。 每當從這個記憶體物件配置記憶體時，這個計數器就會遞增。 增量是目前正在等待存取此記憶體物件的工作數目。 僅適用于安全線程的記憶體物件。 這是不具有正確性保證的最佳工作價值。|  
|**exclusive_access_count**|**bigint**|指定以獨佔方式存取此記憶體物件的頻率。 僅適用于安全線程的記憶體物件。  這是不具有正確性保證的最佳工作價值。|  
|**pdw_node_id**|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
 **partition_type**、 **contention_factor**、 **waiting_tasks_count**和**exclusive_access_count**尚未在中執行 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 。  
  
## <a name="permissions"></a>權限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="remarks"></a>備註  
 記憶體物件是堆積。 它們提供的配置比記憶體 Clerk 所提供的配置資料粒度更細。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件會使用記憶體物件來取代記憶體 Clerk。 記憶體物件使用記憶體 Clerk 頁面配置器介面來配置頁面。 記憶體物件不使用虛擬或共用記憶體介面。 隨著配置模式的不同，元件可以建立不同類型的記憶體物件，來配置任意大小的頁面。  
  
 記憶體物件一般的頁面大小是 8 KB。 然而，累加記憶體物件的頁面大小範圍從 512 位元組到 8 KB 不等。  
  
> [!NOTE]  
>  頁面大小不是最大配置。 相對的，頁面大小是頁面配置器支援、記憶體 Clerk 實作的配置資料粒度。 您可以從記憶體物件要求大於 8 KB 的配置。  
  
## <a name="examples"></a>範例  
 下列範例會傳回各記憶體物件類型配置的記憶體數量。  
  
```  
SELECT SUM (pages_in_bytes) as 'Bytes Used', type   
FROM sys.dm_os_memory_objects  
GROUP BY type   
ORDER BY 'Bytes Used' DESC;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [dm_os_memory_clerks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


