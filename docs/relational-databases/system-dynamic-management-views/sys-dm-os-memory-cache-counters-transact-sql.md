---
title: sys.dm_os_memory_cache_counters (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d16da7e5bbc38b7017da1f94741d4c4955e3485d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosmemorycachecounters-transact-sql"></a>sys.dm_os_memory_cache_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中傳回快取健全狀況的快照集。 **sys.dm_os_memory_cache_counters**提供有關配置的快取項目執行階段資訊、 其使用情形和之記憶體來源的快取項目。  
  
> **注意：**呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_memory_cache_counters**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|指出與特定快取相關聯之計數器的位址 (主索引鍵)。 不可為 Null。|  
|**name**|**nvarchar(256)**|指定快取的名稱。 不可為 Null。|  
|**type**|**nvarchar(60)**|表示此項目相關聯的快取類型。 不可為 Null。|  
|**single_pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 配置的單一頁面記憶體數量 (以 KB 為單位)。 這是使用單一頁面配置器所配置的記憶體數量。 這是指直接從這個快取緩衝集區取得的 8KB 頁面。 不可為 Null。|  
|**pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定快取中配置的記憶體數量 (以 KB 為單位)。 不可為 Null。|  
|**multi_pages_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 配置的多重頁面記憶體數量 (以 KB 為單位)。 這是使用記憶體節點之多重頁面配置器所配置的記憶體數量。 這個記憶體是配置在緩衝集區之外，並利用記憶體節點的虛擬配置器。 不可為 Null。|  
|**pages_in_use_kb**|**bigint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指定快取中配置且使用中的記憶體數量 (以 KB 為單位)。 可為 Null。  不追蹤 `USERSTORE_<*>` 類型物件的值。  對這些物件回報 NULL。|  
|**single_pages_in_use_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 使用的單一頁面記憶體數量 (以 KB 為單位)。 可為 Null。 這項資訊不會追蹤 USERSTORE_< 類型的物件\<* >，這些值會是 NULL。|  
|**multi_pages_in_use_kb**|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。<br /><br /> 使用的多重頁面記憶體數量 (以 KB 為單位)。 NULLABLE。 這項資訊不會追蹤 USERSTORE_< 類型的物件\<* >，而且這些值會是 NULL。|  
|**entries_count**|**bigint**|指出快取中的項目數目。 不可為 Null。|  
|**entries_in_use_count**|**bigint**|指出使用之快取的項目數。 不可為 Null。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions 

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


