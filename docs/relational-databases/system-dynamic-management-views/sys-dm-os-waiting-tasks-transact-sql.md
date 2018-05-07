---
title: sys.dm_os_waiting_tasks (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a44e9fe9e42f415ac7f859c25be95800ff0b1393
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmoswaitingtasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回有關等候某項資源的工作等候佇列資訊。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_waiting_tasks**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|等候工作的位址。|  
|**session_id**|**smallint**|與這項工作相關聯的工作階段識別碼。|  
|**exec_context_id**|**int**|與這項工作相關聯的執行內容識別碼。|  
|**wait_duration_ms**|**bigint**|這個等候類型的總等候時間 (以毫秒為單位)。 此時間**signal_wait_time**。|  
|**wait_type**|**nvarchar(60)**|等候類型的名稱。|  
|**resource_address**|**varbinary(8)**|工作在等候的資源位址。|  
|**blocking_task_address**|**varbinary(8)**|目前保留這項資源的工作。|  
|**blocking_session_id**|**smallint**|封鎖要求之工作階段的識別碼。 如果這個資料行是 NULL，表示要求沒有被封鎖，或者封鎖工作階段的工作階段資訊無法使用 (或無法識別)。<br /><br /> -2 = 封鎖資源是由被遺棄的分散式交易所擁有。<br /><br /> -3 = 封鎖資源是由延遲的復原交易所擁有。<br /><br /> -4 = 由於內部閂鎖狀態轉換，而無法判斷封鎖閂鎖擁有者的工作階段識別碼。|  
|**blocking_exec_context_id**|**int**|封鎖工作的執行內容識別碼。|  
|**resource_description**|**nvarchar(3072)**|正在耗用的資源描述。 如需詳細資訊，請參閱以下清單。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="resourcedescription-column"></a>resource_description 資料行  
 Resource_description 資料行有下列可能的值。  
  
 **執行緒集區資源擁有者：**  
  
-   執行緒集區識別碼 = 排程器\<十六進位位址 >  
  
 **平行查詢資源擁有者：**  
  
-   exchangeEvent id = {通訊埠 |管道}\<十六進位位址 > WaitType =\<exchange 等候類型 > nodeId =\<exchange 節點識別碼 >  
  
 **Exchange 等候類型：**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **鎖定資源擁有者：**  
  
-   \<型別特定描述 > id = 鎖定\<鎖定 hex 位址 > 模式 =\<模式 > associatedObjectId =\<相關聯 obj 識別碼 >  
  
     **\<型別特定描述 > 可以是：**  
  
    -   Database: Databaselock subresource =\<databaselock subresource > dbid =\<db 識別碼 >  
  
    -   檔案： Filelock fileid =\<檔案識別碼 > subresource =\<filelock subresource > dbid =\<db 識別碼 >  
  
    -   物件： Objectlock lockPartition =\<鎖定資料分割識別碼 > objid =\<obj 識別碼 > subresource =\<objectlock subresource > dbid =\<db 識別碼 >  
  
    -   對於 PAGE: Pagelock fileid =\<檔案識別碼 > pageid =\<頁面識別碼 > dbid =\<db 識別碼 > subresource =\<pagelock s >  
  
    -   對於 Key: Keylock hobtid =\<hobt 識別碼 > dbid =\<db 識別碼 >  
  
    -   對於 EXTENT: Extentlock fileid =\<檔案識別碼 > pageid =\<頁面識別碼 > dbid =\<db 識別碼 >  
  
    -   對於 RID: Ridlock fileid =\<檔案識別碼 > pageid =\<頁面識別碼 > dbid =\<db 識別碼 >  
  
    -   對於應用程式： Applicationlock 雜湊 =\<雜湊 > databasePrincipalId =\<角色識別碼 > dbid =\<db 識別碼 >  
  
    -   對於 METADATA: Metadatalock subresource =\<中繼資料 subresource > classid =\<metadatalock 描述 > dbid =\<db 識別碼 >  
  
    -   對於 HOBT: Hobtlock hobtid =\<hobt 識別碼 > subresource =\<hobt subresource > dbid =\<db 識別碼 >  
  
    -   對於 ALLOCATION_UNIT: Allocunitlock hobtid =\<hobt 識別碼 > subresource =\<配置單位-d subresource > dbid =\<db 識別碼 >  
  
     **\<模式 > 可以是：**  
  
     Sch-S、Sch-M、S、U、X、IS、IU、IX、SIU、SIX、UIX、BU、RangeS-S、RangeS-U、RangeI-N、RangeI-S、RangeI-U、RangeI-X、RangeX-、RangeX-U、RangeX-X  
  
 **外部資源擁有者：**  
  
-   外部 ExternalResource =\<等候類型 >  
  
 **一般資源擁有者：**  
  
-   工作區中 TransactionInfo TransactionMutex =\<工作區識別碼 >  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **閂鎖資源擁有者：**  
  
-   \<資料庫識別碼 >:\<檔案識別碼 >:\<分頁中檔案 >  
  
-   \<GUID &GT;  
  
-   \<閂鎖類別 > (\<閂鎖位址 >)  
  
## <a name="permissions"></a>Permissions

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
 
## <a name="example"></a>範例
這個範例會識別已封鎖工作階段。  執行[!INCLUDE[tsql](../../includes/tsql-md.md)]以查詢[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>另請參閱  
  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


