---
title: "MSdistribution_status (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSdistribution_status_TSQL
- MSdistribution_status
dev_langs: TSQL
helpviewer_keywords: MSdistribution_status view
ms.assetid: 90d447de-3a4a-4f3e-aeab-e8fff6348361
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f6f18aa6d26fca65d26fd7d6dda39ee1ca54b2a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="msdistributionstatus-transact-sql"></a>MSdistribution_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdistribution_status**檢視會顯示散發資料庫中狀態命令的其他資訊。 這份檢視儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|識別發行項。|  
|**agent_id**|**int**|識別複寫代理程式。|  
|**UndelivCmdsInDistDB**|**int**|暫止傳遞給訂閱者的命令數。|  
|**DelivCmdsInDistDB**|**int**|傳遞給訂閱者的命令數。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
