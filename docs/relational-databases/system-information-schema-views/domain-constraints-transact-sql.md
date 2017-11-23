---
title: "DOMAIN_CONSTRAINTS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DOMAIN_CONSTRAINTS
- DOMAIN_CONSTRAINTS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.DOMAIN_CONSTRAINTS view
- DOMAIN_CONSTRAINTS view
ms.assetid: 436c4480-f1e3-403f-b2bd-de04539afe3c
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e39387eb33957487c57764152d9532c2acd8dde
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="domainconstraints-transact-sql"></a>DOMAIN_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中，每個具有其繫結規則，並且可由目前使用者存取的別名資料類型，各傳回一個資料列。  
  
 若要從這些檢視中擷取資訊，請指定完整的名稱**INFORMATION_SCHEMA。***view_name*。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (**128**)**|規則所在的資料庫。|  
|**CONSTRAINT_SCHEMA**|**nvarchar (**128**)**|包含條件約束之結構描述的名稱。<br /><br /> **\*\*重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**CONSTRAINT_NAME**|**sysname**|規則名稱。|  
|**DOMAIN_CATALOG**|**nvarchar (**128**)**|別名資料類型所在的資料庫。|  
|**DOMAIN_SCHEMA**|**nvarchar (**128**)**|包含別名資料類型之結構描述的名稱。<br /><br /> **\*\*重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷資料類型的結構描述。 尋找類型之結構描述的唯一可靠方式就是使用 TYPEPROPERTY 函數。|  
|**網域名稱**|**sysname**|別名資料類型。|  
|**IS_DEFERRABLE**|**varchar (**2**)**|指定條件約束檢查是否可以延後。 一律傳回 NO。|  
|**INITIALLY_DEFERRED**|**varchar (**2**)**|指定一開始時是否延遲條件約束檢查。 一律傳回 NO。|  
  
## <a name="see-also"></a>請參閱＜  
 [系統檢視 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視 &#40;TRANSACT-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
