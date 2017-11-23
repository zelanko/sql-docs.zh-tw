---
title: "Y (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MStracer_history
- MStracer_history_TSQL
dev_langs: TSQL
helpviewer_keywords: MStracer_history system table
ms.assetid: 97237a0c-d574-4b17-8a94-1a8730b31d98
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 59673833f8862368296e6803805a3f2c99ef1b8a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mstracerhistory-transact-sql"></a>MStracer_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MStracer_history**資料表會維護所有已在訂閱者端接收的追蹤 token 記錄。 這份資料表儲存在散發資料庫中，並且由複寫用來監視效能之用。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**parent_tracer_id**|**int**|唯一識別追蹤 Token。|  
|**agent_id**|**int**|識別處理追蹤 Token 記錄的代理程式。|  
|**subscriber_commit**|**datetime**|在訂閱者端認可追蹤 Token 記錄的日期和時間。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
