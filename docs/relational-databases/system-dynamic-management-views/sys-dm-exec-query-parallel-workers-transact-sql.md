---
title: sys.dm_exec_query_parallel_workers (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_parallel_workers_TSQL
- dm_exec_query_parallel_workers
- sys.dm_exec_query_parallel_workers_TSQL
- sys.dm_exec_query_parallel_workers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_parallel_workers dynamic management view
ms.assetid: 1d72cef1-22d8-4ae0-91db-6694fe918c9f
caps.latest.revision: 1
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f2bc4634a5e2fddb4a3c8eda009eb28019089596
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmexecqueryparallelworkers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  傳回背景工作每個節點的可用性資訊。  
  
|名稱|資料類型|Description|  
|----------|---------------|-----------------|  
|**node_id**|**int**|NUMA 節點識別碼。|  
|**scheduler_count**|**int**|在此節點上的排程器的數目。|  
|**max_worker_count**|**int**|平行查詢的背景工作的最大數目。|  
|**reserved_worker_count**|**int**|平行查詢，所保留的背景工作數目加上的所有要求所使用的主要背景工作數目。| 
|**free_worker_count**|**int**|背景工作提供給工作的數目。<br /><br />**注意：** 每個傳入要求會消耗至少 1 背景工作，會減去可用的背景工作計數。  很可能可用的背景工作計數可以是負數繁重的伺服器上。| 
|**used_worker_count**|**int**|使用平行查詢的背景工作數目。|  
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
 
## <a name="examples"></a>範例  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. 檢視目前的平行背景工作可用性  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_workers &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
