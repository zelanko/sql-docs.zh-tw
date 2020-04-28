---
title: sys.databases dm_os_hosts （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
author: stevestein
ms.author: sstein
ms.openlocfilehash: e4ff3e25accf5c499afb5e306a0eec206f6b3f82
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "73982547"
---
# <a name="sysdm_os_hosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回所有目前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體登錄的主機。 這份檢視也會傳回這些主機所用的資源。  
  
> [!NOTE]  
>  若要從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]呼叫此，請使用**dm_pdw_nodes_os_hosts**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary(8)**|主物件的內部記憶體位址。|  
|**type**|**nvarchar(60)**|主控的元件類型。 例如，<br /><br /> SOSHOST_CLIENTID_SERVERSNI= SQL Server Native Interface<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB 提供者<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft Data Access Run Time|  
|**name**|**nvarchar(32)**|主機的名稱。|  
|**enqueued_tasks_count**|**int**|這個主機置於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中之佇列的工作總數。|  
|**active_tasks_count**|**int**|這個主機置於佇列中而目前正在執行的工作總數。|  
|**completed_ios_count**|**int**|透過這個主機發出和完成的 I/O 總數。|  
|**completed_ios_in_bytes**|**bigint**|透過這個主機完成的 I/O 總位元組計數。|  
|**active_ios_count**|**int**|與這個主機相關而目前在等待完成的 I/O 要求總數。|  
|**default_memory_clerk_address**|**varbinary(8)**|與這個主機相關聯之記憶體 Clerk 物件的記憶體位址。 如需詳細資訊，請參閱[dm_os_memory_clerks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)。|  
|**pdw_node_id**|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="permissions"></a>權限

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高階層級上， `VIEW DATABASE STATE`需要資料庫的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許不屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可執行檔一部分的元件 (例如 OLE DB 提供者) 配置記憶體，以及參與非先佔式排程。 這些元件會由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主控，並且這些元件所配置的所有資源都會進行追蹤。 主控可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更有效地管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可執行檔之外部元件所使用的資源。  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|從|至|關聯性|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|一對一|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|一對一|  
  
## <a name="examples"></a>範例  
 下列範例會判斷由主控元件認可的記憶體總數。  
  
||  
|-|  
|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>另請參閱  

 [dm_os_memory_clerks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


