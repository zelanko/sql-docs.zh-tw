---
title: "COLUMN_PRIVILEGES (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-information-schema-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMN_PRIVILEGES
- COLUMN_PRIVILEGES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMN_PRIVILEGES view
- INFORMATION_SCHEMA.COLUMN_PRIVILEGES view
ms.assetid: 8ae29a85-2b77-48db-a2b9-a1720287b271
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01df1be992fcebfe7b3f3df9dc52e66849b654ca
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="columnprivileges-transact-sql"></a>COLUMN_PRIVILEGES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  只要資料行具備授與目前資料庫中目前使用者的權限，或是被目前資料庫中目前使用者所授與的權限，則會針對每一個資料夾，各傳回一個資料列。  
  
 若要從這些檢視中擷取資訊，請指定完整的名稱**INFORMATION_SCHEMA。***view_name*。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**授與者**|**nvarchar (**128**)**|權限同意授權者。|  
|**被授與者**|**nvarchar (**128**)**|權限被授與者。|  
|**TABLE_CATALOG 排列**|**nvarchar (**128**)**|資料表限定詞。|  
|**TABLE_SCHEMA**|**nvarchar (**128**)**|包含資料表的結構描述名稱。<br /><br /> **\*\*重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**sysname**|資料表名稱。|  
|**COLUMN_NAME**|**sysname**|資料行名稱。|  
|**PRIVILEGE_TYPE**|**varchar (**10**)**|權限的類型。|  
|**IS_GRANTABLE**|**varchar (**3**)**|指定被授與者是否可以將權限授與其他人。|  
  
## <a name="see-also"></a>請參閱＜  
 [系統檢視 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視 &#40;TRANSACT-SQL &#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.database_permissions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [sys.server_permissions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
  
