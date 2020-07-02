---
title: sys.databases dm_os_memory_cache_counters （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 20bda8c759d17443d56c2ce046f6c7d279e76f5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754121"
---
# <a name="sysdm_os_memory_cache_counters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中傳回快取健全狀況的快照集。 **dm_os_memory_cache_counters**提供有關已配置的快取專案、其使用，以及快取專案的記憶體來源的執行時間資訊。  
  
> **注意：** 若要從或呼叫此 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，請使用**dm_pdw_nodes_os_memory_cache_counters**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|指出與特定快取相關聯之計數器的位址 (主索引鍵)。 不可為 Null。|  
|**name**|**nvarchar(256)**|指定快取的名稱。 不可為 Null。|  
|**type**|**nvarchar(60)**|表示此項目相關聯的快取類型。 不可為 Null。|  
|**single_pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 配置的單一頁面記憶體數量 (以 KB 為單位)。 這是使用單一頁面配置器所配置的記憶體數量。 這是指直接從這個快取緩衝集區取得的 8KB 頁面。 不可為 Null。|  
|**pages_kb**|**bigint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 指定快取中配置的記憶體數量 (以 KB 為單位)。 不可為 Null。|  
|**multi_pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 配置的多重頁面記憶體數量 (以 KB 為單位)。 這是使用記憶體節點之多重頁面配置器所配置的記憶體數量。 這個記憶體是配置在緩衝集區之外，並利用記憶體節點的虛擬配置器。 不可為 Null。|  
|**pages_in_use_kb**|**bigint**|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 指定快取中配置且使用中的記憶體數量 (以 KB 為單位)。 可為 Null。  不追蹤 `USERSTORE_<*>` 類型物件的值。  對這些物件回報 NULL。|  
|**single_pages_in_use_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 使用的單一頁面記憶體數量 (以 KB 為單位)。 可為 Null。 USERSTORE_ 類型的物件不會追蹤這項資訊 \<*> ，這些值將會是 Null。|  
|**multi_pages_in_use_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 使用的多重頁面記憶體數量 (以 KB 為單位)。 NULLABLE。 這項資訊不會針對 USERSTORE_ 類型的物件進行追蹤 \<*> ，而且這些值會是 Null。|  
|**entries_count**|**bigint**|指出快取中的項目數目。 不可為 Null。|  
|**entries_in_use_count**|**bigint**|指出使用之快取的項目數。 不可為 Null。|  
|**pdw_node_id**|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="permissions"></a>權限 

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


