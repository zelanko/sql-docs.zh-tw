---
title: dbo.sysoperators (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysoperators
- dbo.sysoperators
- dbo.sysoperators_TSQL
- sysoperators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoperators system table
ms.assetid: c2afa20c-b15f-46ca-ae74-2eb65909409e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3796714cbdfb55900447bf23904136ac5abefa9c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470653"
---
# <a name="dbosysoperators-transact-sql"></a>dbo.sysoperators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 操作員，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|操作員的識別碼。|  
|**name**|**sysname**|操作員的名稱。|  
|**enabled**|**tinyint**|警示通知的狀態 (布林)。 如果**1**，發生警示時，這位操作員可以收到通知。|  
|**email_address**|**nvarchar(100)**|這位操作員的電子郵件地址。|  
|**last_email_date**|**int**|這位操作員前次收到電子郵件警示通知的日期。|  
|**last_email_time**|**int**|這位操作員前次收到電子郵件警示通知的日期時間。|  
|**pager_address**|**nvarchar(100)**|這位操作員的呼叫器號碼。|  
|**last_pager_date**|**int**|這位操作員前次收到呼叫器警示通知的日期。|  
|**last_pager_time**|**int**|這位操作員前次收到呼叫器警示通知的日期時間。|  
|**weekday_pager_start_time**|**int**|這是一週工作日期 (週一至週五) 的時間，過了這個日期時間之後，這位操作員便能夠收到呼叫器警示通知。|  
|**weekday_pager_end_time**|**int**|這是一週工作日期 (週一至週五) 的時間，過了這個日期時間之後，這位操作員便無法收到呼叫器警示通知。|  
|**saturday_pager_start_time**|**int**|這是一個週六的時間，過了這個時間之後，這位操作員便能夠收到呼叫器警示通知。|  
|**saturday_pager_end_time**|**int**|這是一個週六的時間，過了這個時間之後，這位操作員便無法收到呼叫器警示通知。|  
|**sunday_pager_start_time**|**int**|這是一個週日的時間，過了這個時間之後，這位操作員便能夠收到呼叫器警示通知。|  
|**sunday_pager_end_time**|**int**|這是一個週日的時間，過了這個時間之後，這位操作員便無法收到呼叫器警示通知。|  
|**pager_days**|**tinyint**|這是一個位元遮罩，代表這位操作員能夠收到呼叫器警示通知之每週的日期。|  
|**netsend_address**|**nvarchar(100)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**last_netsend_date**|**int**|這是最近的網路訊息前次傳給指定操作員識別碼的日期。|  
|**last_netsend_time**|**int**|這是最近的網路訊息前次傳給指定操作員識別碼的時間。|  
|**category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
