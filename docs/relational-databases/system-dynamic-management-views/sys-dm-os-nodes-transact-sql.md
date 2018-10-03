---
title: sys.dm_os_nodes & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dec718bfea5748db1baa4bb5d9be8c01b85ace26
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643486"
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

名為 SQLOS 的內部元件會建立模擬硬體處理器位置的節點結構。 使用也可以變更這些結構[軟體式 NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md)建立自訂節點配置。  

> [!NOTE]
> 開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，則[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]會自動使用軟體 NUMA 的特定硬體設定。 如需詳細資訊，請參閱 <<c0> [ 自動軟體式 NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa)。
  
下表提供有關這些節點的資訊。  
  
> [!NOTE]
> 若要呼叫從這個 DMV[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_nodes**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|節點的識別碼。|  
|node_state_desc|**nvarchar(256)**|節點狀態的描述。 系統會先顯示互斥的值，然後再顯示可結合的值。 例如：<br /> Online, Thread Resources Low, Lazy Preemptive<br /><br />有四個互斥的 node_state_desc 值。 它們會列出以下及其描述。<br /><ul><li>節點已連線的連線：<li>離線： 節點已離線<li>閒置： 節點沒有任何暫止的工作要求，而且已進入閒置狀態。<li>IDLE_READY： 節點沒有任何暫止工作要求，並已準備好進入閒置狀態。</li></ul><br />有三個可結合的 node_state_desc 值，如下所示及其描述。<br /><ul><li>DAC： 此節點保留供[專用管理連接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。<li>THREAD_RESOURCES_LOW： 任何新的執行緒上不建立此節點由於記憶體不足的狀況。<li>熱新增： 表示已加入節點，以回應 hot add CPU 事件。</li></ul>|  
|memory_object_address|**varbinary(8)**|與這個節點相關聯之記憶體物件的位址。 一對一關聯性[sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).memory_object_address。|  
|memory_clerk_address|**varbinary(8)**|與這個節點相關聯之記憶體 Clerk 的位址。 一對一關聯性[sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).memory_clerk_address。|  
|io_completion_worker_address|**varbinary(8)**|指派給這個節點之 IO 完成的工作者位址。 一對一關聯性[sys.dm_os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).worker_address。|  
|memory_node_id|**smallint**|這個節點所屬之記憶體節點的識別碼。 多對一關聯性[sys.dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md).memory_node_id。|  
|cpu_affinity_mask|**bigint**|識別與這個節點相關之 CPU 的點陣圖。|  
|online_scheduler_count|**smallint**|此節點所管理之線上排程器的數目。|  
|idle_scheduler_count|**smallint**|沒有使用中工作者之線上排程器的數目。|  
|active_worker_count|**int**|在這個節點所管理之所有排程器上使用中的工作者數目。|  
|avg_load_balance|**int**|這個節點上每個排程器的平均工作數目。|  
|timer_task_affinity_mask|**bigint**|識別可指派計時器工作給本身之排程器的點陣圖。|  
|permanent_task_affinity_mask|**bigint**|識別可指派永久工作給本身之排程器的點陣圖。|  
|resource_monitor_state|**bit**|每個節點都具有一個指派給本身的資源監視器。 資源監視器可能是執行中或閒置。 值 1 是表示執行中，而值 0 則表示閒置。|  
|online_scheduler_mask|**bigint**|識別這個節點的處理序相似性遮罩。|  
|processor_group|**smallint**|識別這個節點的處理器群組。|  
|cpu_count |**int** |適用於此節點的 Cpu 數目。 |
|pdw_node_id|**int**|這個分佈是在節點的識別碼。<br /><br /> **適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissions

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="see-also"></a>另請參閱    
 [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [軟體 NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
