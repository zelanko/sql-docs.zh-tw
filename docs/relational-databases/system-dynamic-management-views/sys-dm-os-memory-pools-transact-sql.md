---
title: sys.dm_os_memory_pools (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_pools_TSQL
- dm_os_memory_pools
- dm_os_memory_pools_TSQL
- sys.dm_os_memory_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_pools dynamic management view
ms.assetid: 1ef053f3-c6f3-456e-82b6-26e4bd630d46
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0de67bd53b568f77a16fd10903a5d0c3fddfce4c
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmosmemorypools-transact-sql"></a>sys.dm_os_memory_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的每一個物件存放區，各傳回一個資料列。 您可以利用這份檢視，來監視快取記憶體的使用情形，並且識別不當的快取行為。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_memory_pools**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**memory_pool_address**|**varbinary(8)**|代表記憶體集區之項目的記憶體位址。 不可為 Null。|  
|**pool_id**|**int**|一組集區中某個特定集區的識別碼。 不可為 Null。|  
|**type**|**nvarchar(60)**|物件集區的類型。 不可為 Null。 如需詳細資訊，請參閱[sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)。|  
|**name**|**nvarchar(256)**|這個記憶體物件之系統指派的名稱。 不可為 Null。|  
|**max_free_entries_count**|**bigint**|集區最多所能容納的可用項目數。 不可為 Null。|  
|**free_entries_count**|**bigint**|目前在集區中的可用項目數。 不可為 Null。|  
|**removed_in_all_rounds_count**|**bigint**|自  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體啟動之後，從集區移除的項目數。 不可為 Null。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件有時會使用一個共用集區架構，來快取異質、非靜態類型的資料。 集區架構比快取架構更簡單。 集區中所有的項目都視為相同。 集區在內部相當於記憶體 Clerk，可以取代記憶體 Clerk 使用。  
  
## <a name="see-also"></a>另請參閱  
 
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


