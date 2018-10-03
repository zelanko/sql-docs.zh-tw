---
title: sys.dm_broker_activated_tasks (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_activated_tasks
- sys.dm_broker_activated_tasks_TSQL
- dm_broker_activated_tasks
- dm_broker_activated_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_activated_tasks dynamic management view
ms.assetid: 17e6f87f-8f56-489d-9aed-216afc8ef310
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf3910b432d803ce74e0bf24d83a974072028f33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704871"
---
# <a name="sysdmbrokeractivatedtasks-transact-sql"></a>sys.dm_broker_activated_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對 Service Broker 所啟動的每個預存程序，各傳回一個資料列。  
 

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**spid**|**int**|啟動的預存程序之工作階段識別碼。 NULLABLE。|  
|**database_id**|**smallint**|佇列定義所在的資料庫識別碼。 NULLABLE。|  
|**queue_id**|**int**|啟動的預存程序所針對之佇列的物件識別碼。 NULLABLE。|  
|**procedure_name**|**nvarchar(650)**|啟動的預存程序名稱。 NULLABLE。|  
|**execute_as**|**int**|預存程序執行身分的使用者識別碼。 NULLABLE。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="physical-joins"></a>實體聯結  
 ![Sys.dm_broker_activated_tasks 的聯結](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-activated-tasks-1.gif "sys.dm_broker_activated_tasks 的聯結")  
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|關聯性|  
|----------|--------|------------------|  
|dm_broker_activated_tasks.spid|dm_exec_sessions.session_id|一對一|  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 相關的動態管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

