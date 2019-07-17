---
title: sys.dm_os_memory_objects (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ca3a6a8891e74bd795f15e9a374194650e70b197
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265746"
---
# <a name="sysdmosmemoryobjects-transact-sql"></a>sys.dm_os_memory_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回目前所配置的記憶體物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以使用**sys.dm_os_memory_objects**來分析記憶體使用以及識別可能的記憶體遺漏。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**memory_object_address**|**varbinary(8)**|記憶體物件的位址。 不可為 Null。|  
|**parent_address**|**varbinary(8)**|父記憶體物件的位址。 可為 Null。|  
|**pages_allocated_count**|**int**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 這個物件所配置的頁數。 不可為 Null。|  
|**pages_in_bytes**|**bigint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 這個記憶體物件執行個體所配置的記憶體數量 (以位元組為單位)。 不可為 Null。|  
|**creation_options**|**int**|僅供內部使用。 可為 Null。|  
|**bytes_used**|**bigint**|僅供內部使用。 可為 Null。|  
|**type**|**nvarchar(60)**|記憶體物件的類型。<br /><br /> 這表示這個記憶體物件所屬的某個元件，或是記憶體物件的函數。 可為 Null。|  
|**name**|**varchar(128)**|僅供內部使用。 可為 Null。|  
|**memory_node_id**|**smallint**|這個記憶體物件正在使用之記憶體節點的識別碼。 不可為 Null。|  
|**creation_time**|**datetime**|僅供內部使用。 可為 Null。|  
|**max_pages_allocated_count**|**int**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 這個記憶體物件所配置的最大頁數。 不可為 Null。|  
|**page_size_in_bytes**|**int**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 這個物件所配置的頁面大小 (以位元組為單位)。 不可為 Null。|  
|**max_pages_in_bytes**|**bigint**|這個記憶體物件所使用的最大記憶體數量。 不可為 Null。|  
|**page_allocator_address**|**varbinary(8)**|頁面配置器的記憶體位址。 不可為 Null。 如需詳細資訊，請參閱 < [sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)。|  
|**creation_stack_address**|**varbinary(8)**|僅供內部使用。 可為 Null。|  
|**sequence_num**|**int**|僅供內部使用。 可為 Null。|  
|**partition_type**|**int**|磁碟分割類型：<br /><br /> 0-非可分割記憶體物件<br /><br /> 1-可分割記憶體物件，目前未分割<br /><br /> 2-可分割記憶體物件，依 NUMA 節點分割。 具有單一 NUMA 節點的環境中這相當於 1。<br /><br /> 3-可分割記憶體物件，依 CPU 進行分割。|  
|**contention_factor**|**real**|值，指定這個記憶體物件上的爭用，0 表示沒有爭用的情況。 每當指定的數目的記憶體配置進行反射的爭用情況，在該期間內，將更新的值。 僅適用於安全執行緒記憶體物件。|  
|**waiting_tasks_count**|**bigint**|這個記憶體物件上的等候次數。 此計數器會遞增，每當從這個記憶體物件配置記憶體。 的增量是目前等候這個記憶體物件的存取權的工作數目。 僅適用於安全執行緒記憶體物件。 這是最佳的投入時間值，不保證正確性。|  
|**exclusive_access_count**|**bigint**|指定這個記憶體物件頻率以獨佔方式存取。 僅適用於安全執行緒記憶體物件。  這是最佳的投入時間值，不保證正確性。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 這個分佈是在節點的識別碼。|  
  
 **partition_type**， **contention_factor**， **waiting_tasks_count**，和**exclusive_access_count**尚未實作中[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
## <a name="permissions"></a>Permissions

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，則需要**伺服器系統管理員**該**Azure Active Directory 管理員**帳戶。   

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
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)  
  
  


