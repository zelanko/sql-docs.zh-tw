---
title: sys.databases dm_os_waiting_tasks （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0a89a48fa960812ee955cd3b7ecb30069161f61
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2019
ms.locfileid: "72260386"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回有關等候某項資源的工作等候佇列資訊。 如需有關工作的詳細資訊，請參閱[執行緒和工作架構指南](../../relational-databases/thread-and-task-architecture-guide.md)。
   
> [!NOTE]  
>  若要從 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 或 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]呼叫此，請使用**dm_pdw_nodes_os_waiting_tasks**的名稱。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**Varbinary （8）**|等候工作的位址。|  
|**session_id**|**smallint**|與這項工作相關聯的工作階段識別碼。|  
|**exec_coNtext_id**|**int**|與這項工作相關聯的執行內容識別碼。|  
|**wait_duration_ms**|**bigint**|這個等候類型的總等候時間 (以毫秒為單位)。 這一段時間包含**signal_wait_time**。|  
|**wait_type**|**nvarchar(60)**|等候類型的名稱。|  
|**resource_address**|**Varbinary （8）**|工作在等候的資源位址。|  
|**blocking_task_address**|**Varbinary （8）**|目前保留這項資源的工作。|  
|**blocking_session_id**|**smallint**|封鎖要求之工作階段的識別碼。 如果這個資料行是 NULL，表示要求沒有被封鎖，或者封鎖工作階段的工作階段資訊無法使用 (或無法識別)。<br /><br /> -2 = 封鎖資源是由被遺棄的分散式交易所擁有。<br /><br /> -3 = 封鎖資源是由延遲的復原交易所擁有。<br /><br /> -4 = 由於內部閂鎖狀態轉換，而無法判斷封鎖閂鎖擁有者的工作階段識別碼。|  
|**blocking_exec_coNtext_id**|**int**|封鎖工作的執行內容識別碼。|  
|**resource_description**|**Nvarchar （3072）**|正在耗用的資源描述。 如需詳細資訊，請參閱以下清單。|  
|**pdw_node_id**|**int**|**適用于**： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="resource_description-column"></a>resource_description 資料行  
 Resource_description 資料行具有下列可能的值。  
  
 **執行緒集區資源擁有者：**  
  
-   threadpool id = 排程器\<十六進位位址 >  
  
 **平行查詢資源擁有者：**  
  
-   exchangeEvent id = {Port |管道}\<十六進位位址 > WaitType =\<交換-等候類型 > 節點識別碼 =\<exchange 節點 id >  
  
 **Exchange-等候類型：**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **鎖定資源擁有者：**  
  
-   \<類型特定-描述 > 識別碼 = 鎖定\<鎖定-十六進位-位址 > 模式 =\<模式 > associatedObjectId =\<關聯的 obj id >  
  
     **\<類型特有的描述 > 可以是：**  
  
    -   針對資料庫： databaselock subresource =\<databaselock-subresource > dbid =\<db 識別碼 >  
  
    -   針對 FILE： k fileid =\<檔案識別碼 > subresource =\<k-subresource > dbid =\<db-id >  
  
    -   針對 OBJECT： objectlock lockPartition =\<lock-partition-id > objid =\<obj-id > subresource =\<objectlock-subresource > dbid =\<db-id >  
  
    -   針對 PAGE： pagelock fileid =\<檔案識別碼 > pageid =\<頁面識別碼 > dbid =\<db-id > subresource =\<pagelock-subresource >  
  
    -   針對索引鍵：機碼 hobtid =\<hobt-id > dbid =\<db 識別碼 >  
  
    -   針對範圍： extentlock fileid =\<檔案識別碼 > pageid =\<頁面識別碼 > dbid =\<db-id >  
  
    -   針對 RID： ridlock fileid =\<檔案識別碼 > pageid =\<頁面識別碼 > dbid =\<db-id >  
  
    -   針對應用程式： applicationlock hash =\<hash > databasePrincipalId =\<role-id > dbid =\<db-id >  
  
    -   針對中繼資料： metadatalock subresource =\<中繼資料-subresource > classid =\<metadatalock-description > dbid =\<db-id >  
  
    -   針對 HOBT： hobtlock hobtid =\<HOBT-id > subresource =\<HOBT-subresource > dbid =\<db-id >  
  
    -   針對 ALLOCATION_UNIT： allocunitlock hobtid =\<hobt-id > subresource =\<配置-UNIT-subresource > dbid =\<db-id >  
  
     **\<模式 > 可以是：**  
  
     Sch-S、Sch-M、S、U、X、IS、IU、IX、SIU、SIX、UIX、BU、RangeS-S、RangeS-U、RangeI-N、RangeI-S、RangeI-U、RangeI-X、RangeX-、RangeX-U、RangeX-X  
  
 **外部資源擁有者：**  
  
-   External ExternalResource =\<wait 類型 >  
  
 **一般資源擁有者：**  
  
-   TransactionMutex TransactionInfo Workspace =\<工作區識別碼 >  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **閂鎖資源擁有者：**  
  
-   \<db 識別碼 >：\<的檔案識別碼 >：\<分頁檔 >  
  
-   \<GUID >  
  
-   \<閂鎖-類別 > （\<閂鎖-位址 >）  
  
## <a name="permissions"></a>Permissions

在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上，需要 `VIEW SERVER STATE` 許可權。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高階層級上，需要資料庫中的 `VIEW DATABASE STATE` 許可權。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準和基本層上，需要**伺服器管理員**或 Azure Active Directory 的系統**管理員**帳戶。   
 
## <a name="example"></a>範例
這個範例會識別已封鎖的會話。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢。

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>另請參閱  
[SQL Server 作業系統相關的動態管理 Views &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[執行緒和工作架構指南](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
