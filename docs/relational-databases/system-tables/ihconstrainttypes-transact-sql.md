---
title: "IHconstrainttypes (TRANSACT-SQL) |Microsoft 文件"
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
- IHconstrainttypes_TSQL
- IHconstrainttypes
dev_langs: TSQL
helpviewer_keywords: IHconstrainttypes system table
ms.assetid: 955d6fa9-0b31-4335-a3cd-e4c4d90ad308
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29a386aa784494fa46a7d7cd07c2ca3b302424c5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="ihconstrainttypes-transact-sql"></a>IHconstrainttypes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHconstrainttypes**系統資料表包含每一種支援的非 SQL Server 發行者的非 SQL Server 條件約束的一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**型別**|**nvarchar(255)**|支援的非 SQL Server 條件約束類型名稱。|  
  
## <a name="see-also"></a>請參閱＜  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
