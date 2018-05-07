---
title: sys.dm_exec_query_resource_semaphores (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_query_resource_semaphores_TSQL
- dm_exec_query_resource_semaphores_TSQL
- sys.dm_exec_query_resource_semaphores
- dm_exec_query_resource_semaphores
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_resource_semaphores dynamic management view
ms.assetid: e43a2aa9-dd52-4c89-911e-1a7d05f7ffbb
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 63173aa03cdd8d95326a145a081c9702b033b05b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecqueryresourcesemaphores-transact-sql"></a>sys.dm_exec_query_resource_semaphores (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中目前查詢資源信號狀態的相關資訊。 **sys.dm_exec_query_resource_semaphores**提供一般查詢執行記憶體狀態，而且可讓您判斷系統是否可以存取足夠的記憶體。 這個檢視可以補充從取得的記憶體資訊[sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)提供完整的伺服器記憶體狀態。 **sys.dm_exec_query_resource_semaphores**傳回一般資源信號的一個資料列，並為小型查詢資源信號的另一個資料列。 有兩個為小型查詢號誌的需求：  
  
-   應小於 5 MB 記憶體授權要求。  
  
-   查詢成本應該小於 3 個成本單位  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_exec_query_resource_semaphores**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**resource_semaphore_id**|**smallint**|資源信號的非唯一識別碼。 一般資源信號為 0，而小型查詢資源信號則為 1。|  
|**target_memory_kb**|**bigint**|授與使用目標 (以 KB 為單位)。|  
|**max_target_memory_kb**|**bigint**|最大的可能目標 (以 KB 為單位)。 小型查詢資源信號為 NULL。|  
|**total_memory_kb**|**bigint**|資源信號擁有的記憶體 (以 KB 為單位)。 如果系統有記憶體壓力，或如果強制最小記憶體為經常授與，這個值可以是大於**target_memory_kb**或**max_target_memory_kb**值。 總記憶體是可用記憶體和授與記憶體的總和。|  
|**available_memory_kb**|**bigint**|新授與的可用記憶體 (以 KB 為單位)。|  
|**granted_memory_kb**|**bigint**|授與的總記憶體 (以 KB 為單位)。|  
|**used_memory_kb**|**bigint**|授與記憶體的實際使用部分 (以 KB 為單位)。|  
|**grantee_count**|**int**|已滿足其授與的使用中查詢數目。|  
|**waiter_count**|**int**|等候要滿足授與的查詢數目。|  
|**timeout_error_count**|**bigint**|伺服器啟動後逾時錯誤的總數。 小型查詢資源信號為 NULL。|  
|**forced_grant_count**|**bigint**|伺服器啟動後強制最小記憶體授與的總數。 小型查詢資源信號為 NULL。|  
|**pool_id**|**int**|這個資源信號所屬資源集區的識別碼。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="remarks"></a>備註  
 使用包含 ORDER BY 或彙總之動態管理檢視的查詢，有可能會增加記憶體耗用量，但也因此可協助它們正在進行疑難排解的問題。  
  
 使用**sys.dm_exec_query_resource_semaphores**進行疑難排解，但不要將使用的未來版本的應用程式中包含[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 資源管理員功能可讓資料庫管理員在資源集區間散發伺服器資源，最多可達 64 個集區。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本中，每個集區的行為都像是一個小型的獨立伺服器執行個體，而且需要 2 個信號。  
  
## <a name="see-also"></a>另請參閱  
 [執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
  


