---
title: sys.dm_clr_tasks (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_tasks
- sys.dm_clr_tasks_TSQL
- dm_clr_tasks
- dm_clr_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_tasks dynamic management view
ms.assetid: 462b9061-09fa-4858-9707-03d6cc19c769
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5ae63389310a8100c75e008e6d4e508d55800424
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmclrtasks-transact-sql"></a>sys.dm_clr_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回目前執行之所有 Common Language Runtime (CLR) 工作的資料列。 包含 CLR 常式之參考的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次會建立個別工作，來執行該批次內所有 Managed 程式碼。 批次中需要執行 Managed 程式碼的多個陳述式使用相同的 CLR 工作。 CLR 工作負責維護關於 Managed 程式碼執行的物件和狀態，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體和 Common Language Runtime 之間的轉換。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|CLR 工作的位址。|  
|**sos_task_address**|**varbinary(8)**|基礎 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次工作的位址。|  
|**appdomain_address**|**varbinary(8)**|執行這項工作的應用程式網域的位址。|  
|**狀態**|**nvarchar(128)**|工作的目前狀態。|  
|**abort_state**|**nvarchar(128)**|中止目前的狀態 (如果已取消工作)。中止工作時有多個相關的狀態。|  
|**type**|**nvarchar(128)**|工作類型。|  
|**affinity_count**|**int**|工作的相似性。|  
|**forced_yield_count**|**int**|強制產生工作的次數。|  
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Common Language Runtime 相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  

