---
title: sys.dm_os_tasks (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_tasks
- sys.dm_os_tasks_TSQL
- dm_os_tasks_TSQL
- dm_os_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_tasks dynamic management view
ms.assetid: 180a3c41-e71b-4670-819d-85ea7ef98bac
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8ed47fcd90e46fb0162b45acdc591f971e234627
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmostasks-transact-sql"></a>sys.dm_os_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的每一個作用中的工作，各傳回一個資料列。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_tasks**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|物件的記憶體位址。|  
|**task_state**|**nvarchar(60)**|工作的狀態。 這可以是下列項目之一：<br /><br /> PENDING；等待工作者執行緒。<br /><br /> RUNNABLE：可執行的，但等待接收配量。<br /><br /> RUNNING：目前在排程器上執行。<br /><br /> SUSPENDED：有工作者，但等待事件。<br /><br /> DONE：已完成。<br /><br /> SPINLOOP：卡在微調鎖定中。|  
|**context_switches_count**|**int**|這項工作已完成的排程器內容切換數目。|  
|**pending_io_count**|**int**|這項工作執行的實體 I/O 數目。|  
|**pending_io_byte_count**|**bigint**|這項工作執行之 I/O 的總位元組計數。|  
|**pending_io_byte_average**|**int**|這項工作執行之 I/O 的平均位元組計數。|  
|**scheduler_id**|**int**|父排程器的識別碼。 這是這項工作之排程器資訊的控制代碼。 如需詳細資訊，請參閱[sys.dm_os_schedulers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)。|  
|**session_id**|**smallint**|與這項工作相關聯的工作階段識別碼。|  
|**exec_context_id**|**int**|與這項工作相關聯的執行內容識別碼。|  
|**request_id**|**int**|工作的要求識別碼。 如需詳細資訊，請參閱[sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|**worker_address**|**varbinary(8)**|執行工作之工作者的記憶體位址。<br /><br /> NULL = 工作正等待工作者執行，或工作剛執行完畢。<br /><br /> 如需詳細資訊，請參閱[sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)。|  
|**host_address**|**varbinary(8)**|主機的記憶體位址。<br /><br /> 0 = 不會利用主控作業來建立工作。 這可幫助您識別用來建立這項工作的主機。<br /><br /> 如需詳細資訊，請參閱[s &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)。|  
|**parent_task_address**|**varbinary(8)**|做為物件之父系的工作記憶體位址。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="examples"></a>範例  
  
### <a name="a-monitoring-parallel-requests"></a>A. 監視平行要求  
 會平行執行的要求，您會看到相同組合的多個資料列 (\<**session_id**>， \< **request_id**>)。 使用下列查詢來尋找[設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)所有使用中要求。  
  
> [!NOTE]  
>  A **request_id**在工作階段內是唯一。  
  
```  
SELECT  
    task_address,  
    task_state,  
    context_switches_count,  
    pending_io_count,  
    pending_io_byte_count,  
    pending_io_byte_average,  
    scheduler_id,  
    session_id,  
    exec_context_id,  
    request_id,  
    worker_address,  
    host_address  
  FROM sys.dm_os_tasks  
  ORDER BY session_id, request_id;  
```  
  
### <a name="b-associating-session-ids-with-windows-threads"></a>B. 使工作階段識別碼與 Windows 執行緒產生關聯  
 您可以使用下列查詢讓工作階段識別碼與 Windows 執行緒識別碼產生關聯。 如此就可以在 Windows 效能監視器中監視執行緒的效能。 下列查詢不會傳回目前睡眠中的工作階段之資訊。  
  
```  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


