---
title: "MSmerge_identity_range_allocations (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad5ad628c5f839c64d88c54e777aca7e0bc52b7e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="msmergeidentityrangeallocations-transact-sql"></a>MSmerge_identity_range_allocations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_identity_range_allocations**資料表用來追蹤指派識別範圍給發行者和訂閱者，針對發行之發行項的歷程記錄。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|發行者的識別碼。|  
|**publisher_db**|**nvarchar （128)**|發行集資料庫的名稱。|  
|**發行集**|**nvarchar （128)**|發行集的名稱。|  
|**發行項**|**nvarchar （128)**|發行項的名稱。|  
|**訂閱者**|**nvarchar （128)**|訂閱者的名稱。|  
|**subscriber_db**|**nvarchar （128)**|訂閱資料庫的名稱。|  
|**is_pub_range**|**bit**|列出識別範圍是否被指派給發行者。|  
|**ranges_allocated**|**tinyint**|指派的識別範圍數。|  
|**: range_begin**|**numeric(38)**|範圍的起始值。|  
|**range_end**|**numeric(38)**|範圍中的最後一值。|  
|**next_range_begin**|**numeric(38)**|要指派之下一個範圍的起始值。|  
|**next_range_end**|**numeric(38)**|要指派之下一個範圍的最後一個值。|  
|**max_used**|**numeric(38)**|所用的最高識別值。|  
|**time_of_allocation**|**datetime**|指派的時間。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
