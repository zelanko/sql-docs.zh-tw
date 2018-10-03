---
title: sys.dm_os_memory_cache_entries (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_cache_entries
- sys.dm_os_memory_cache_entries
- dm_os_memory_cache_entries_TSQL
- sys.dm_os_memory_cache_entries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_entries dynamic management view
ms.assetid: dd32be6b-10d1-4059-b4fd-0bf817f40d54
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d00a5e39057f6c1410cb170095bc9c0d5f322fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763176"
---
# <a name="sysdmosmemorycacheentries-transact-sql"></a>sys.dm_os_memory_cache_entries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中傳回有關快取中所有項目的資訊。 使用這份檢視來追蹤其相關聯物件的快取項目。 您也可以使用這份檢視來取得快取項目的統計資料。  
  
> [!NOTE]  
>  若要呼叫這個屬性從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_memory_cache_entries**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|快取的位址。 不可為 Null。|  
|**name**|**nvarchar(256)**|快取的名稱。 不可為 Null。|  
|**type**|**varchar(60)**|快取的類型。 不可為 Null。|  
|**entry_address**|**varbinary(8)**|快取項目的描述項位址。 不可為 Null。|  
|**entry_data_address**|**varbinary(8)**|快取項目的使用者資料位址。<br /><br /> 0x00000000 = 項目資料位址無法使用。<br /><br /> 不可為 Null。|  
|**in_use_count**|**int**|這個快取項目的並行使用者數目。 不可為 Null。|  
|**is_dirty**|**bit**|指出此快取項目是否已標記為要移除。 1 = 標示為移除。 不可為 Null。|  
|**disk_ios_count**|**int**|建立這個項目時產生的 I/O 數。 不可為 Null。|  
|**context_switches_count**|**int**|建立這個項目時產生的內容切換數目。 不可為 Null。|  
|**original_cost**|**int**|項目的原始成本。 這個值是產生的 I/O 數、CPU 指示成本和各項目耗用記憶體數量的近似值。 成本愈大，從快取中移除項目的機會愈小。 不可為 Null。|  
|**current_cost**|**int**|快取項目的目前成本。 在項目清除處理期間，會更新這個值。 當項目重複使用時，目前成本會重設為其原始值。 不可為 Null。|  
|**memory_object_address**|**varbinary(8)**|相關聯記憶體物件的位址。 可為 Null。|  
|**pages_allocated_count**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 用來儲存這個快取項目的 8KB 頁數。 不可為 Null。|  
|**pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 此快取項目所使用的記憶體數量 (以 KB 為單位)。  不可為 Null。|  
|**entry_data**|**nvarchar(2048)**|快取項目的序列化表示法。 這項資訊視快取存放區而定。 可為 Null。|  
|**pool_id**|**int**|**適用於**： [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 與項目相關聯的資源集區識別碼。 可為 Null。<br /><br /> 不是 katmai|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 這個分佈是在節點的識別碼。|  
  
## <a name="permissions"></a>Permissions 

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="see-also"></a>另請參閱  
 
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


