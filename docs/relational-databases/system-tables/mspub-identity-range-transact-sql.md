---
title: "MSpub_identity_range (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
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
- MSpub_identity_range_TSQL
- MSpub_identity_range
dev_langs: TSQL
helpviewer_keywords: MSpub_identity_range system table
ms.assetid: 68746eef-32e1-42bc-aff0-9798cd0e88b8
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dcf00bab09fb47969439740d4b93b40fd89bf42e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mspubidentityrange-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpub_identity_range**資料表提供識別範圍管理支援。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|具有複寫所管理的識別欄位之資料表的識別碼。|  
|**範圍**|**bigint**|控制將在調整時，在訂閱進行指派的連續識別值的範圍大小。|  
|**sp_changearticle**|**bigint**|控制將在調整時，在發行集進行指派的連續識別值的範圍大小。|  
|**current_pub_range**|**bigint**|發行集所用的目前範圍。 可能會不同於*sp_changearticle*如果變更之後檢視**sp_changearticle**並在下次調整範圍之前。|  
|**臨界值**|**int**|用來控制散發代理程式指派新識別範圍之時機的百分比值。 當指定的百分比值中*閾值*是使用，散發代理程式會建立新的識別範圍。|  
|**last_seed**|**bigint**|目前範圍的下限。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
