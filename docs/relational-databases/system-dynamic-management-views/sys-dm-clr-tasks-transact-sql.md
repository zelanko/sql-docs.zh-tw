---
title: "sys.dm_clr_tasks (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a3c99ffd172c97c5738ed2dd19bc8b07f303470
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
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
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要在伺服器上的 VIEW SERVER STATE 權限。  
  
 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]Premium 層需要資料庫的 VIEW DATABASE STATE 權限。 在[!INCLUDE[ssSDS](../../includes/sssds-md.md)]標準和基本層需要[!INCLUDE[ssSDS](../../includes/sssds-md.md)]系統管理員帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Common Language Runtime 相關動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  

