---
description: sys.dm_exec_query_parallel_workers (Transact-SQL)
title: sys.dm_exec_query_parallel_workers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: pelopes
ms.author: pelopes
manager: ajayj
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 30ea6f1642da78754560b26a8772c33ab341d2b4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477239"
---
# <a name="sysdm_exec_query_parallel_workers-transact-sql"></a>sys.dm_exec_query_parallel_workers (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

  傳回每個節點的背景工作可用性資訊。  
  
|名稱|資料類型|描述|  
|----------|---------------|-----------------|  
|**node_id**|**int**|NUMA 節點識別碼。|  
|**scheduler_count**|**int**|此節點上的排程器數目。|  
|**max_worker_count**|**int**|平行查詢的背景工作數目上限。|  
|**reserved_worker_count**|**int**|平行查詢所保留的背景工作數目，以及所有要求所使用的主要背景工作數目。| 
|**free_worker_count**|**int**|工作可用的背景工作數目。<br /><br />**注意：** 每個連入要求都會耗用至少1個背景工作，而這會從免費的背景工作計數中扣除。  在負載過重的伺服器上，可用的背景工作數目可能是負數。| 
|**used_worker_count**|**int**|平行查詢所使用的背景工作數目。|  
  
## <a name="permissions"></a>權限  

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在 SQL Database Basic、S0 和 S1 服務目標上，以及針對彈性集區中的資料庫，則 `Server admin` `Azure Active Directory admin` 需要或帳戶。 在所有其他 SQL Database 服務目標上， `VIEW DATABASE STATE` 資料庫中都需要有許可權。   
 
## <a name="examples"></a>範例  
  
### <a name="a-viewing-current-parallel-worker-availability"></a>A. 查看目前的平行背景工作可用性  

```sql 
SELECT * FROM sys.dm_exec_query_parallel_workers;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關的動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_workers &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)
