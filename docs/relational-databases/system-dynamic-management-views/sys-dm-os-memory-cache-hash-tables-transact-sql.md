---
title: sys.dm_os_memory_cache_hash_tables (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_hash_tables_TSQL
- sys.dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables
- dm_os_memory_cache_hash_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_hash_tables dynamic management view
ms.assetid: 68b94f35-8f80-4d2b-bcde-7a21934219af
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d053c47cbe51026e6c3ee71a523cadf176d6ff1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899955"
---
# <a name="sysdmosmemorycachehashtables-transact-sql"></a>sys.dm_os_memory_cache_hash_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的每一個作用中快取，各傳回一個資料列。  
  
> [!NOTE]  
>  若要呼叫這個屬性從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_memory_cache_hash_tables**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|快取項目的位址 (主索引鍵)。 不可為 Null。|  
|**name**|**nvarchar(256)**|快取的名稱。 不可為 Null。|  
|**type**|**nvarchar(60)**|快取的類型。 不可為 Null。|  
|**table_level**|**int**|雜湊資料表號碼。 一個特定快取可以有多個雜湊資料表對應到不同的雜湊函數。 不可為 Null。|  
|**buckets_count**|**int**|雜湊資料表中的值區數。 不可為 Null。|  
|**buckets_in_use_count**|**int**|目前使用的值區數。 不可為 Null。|  
|**buckets_min_length**|**int**|值區的最小快取項目數。 不可為 Null。|  
|**buckets_max_length**|**int**|值區的最大快取項目數。 不可為 Null。|  
|**buckets_avg_length**|**int**|每一個值區的平均快取項目數。 不可為 Null。|  
|**buckets_max_length_ever**|**int**|自從伺服器啟動之後，這份雜湊資料表之雜湊值區的最大快取項目數。 不可為 Null。|  
|**hits_count**|**bigint**|快取叫用數。 不可為 Null。|  
|**misses_count**|**bigint**|快速遺漏數。 不可為 Null。|  
|**buckets_avg_scan_hit_length**|**int**|在找到搜尋的項目之前，值區的平均檢查項目數。 不可為 Null。|  
|**buckets_avg_scan_miss_length**|**int**|在搜尋未成功結束之前，值區的平均檢查項目數。 不可為 Null。|  
|**pdw_node_id**|**int**|這個分佈是在節點的識別碼。<br /><br /> **適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissions 

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 上，需要資料庫中的 `VIEW DATABASE STATE` 權限。   

## <a name="see-also"></a>另請參閱  
 
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


