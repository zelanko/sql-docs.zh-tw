---
title: COLUMN_PRIVILEGES （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 703d7cb0b225bf12e7ccd91bdf34251c3044230b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67950846"
---
# <a name="column_privileges-transact-sql"></a>COLUMN_PRIVILEGES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  只要資料行具備授與目前資料庫中目前使用者的權限，或是被目前資料庫中目前使用者所授與的權限，則會針對每一個資料夾，各傳回一個資料列。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**授權**|**Nvarchar （** 128 **）**|權限同意授權者。|  
|**GRANTEE**|**Nvarchar （** 128 **）**|權限被授與者。|  
|**TABLE_CATALOG**|**Nvarchar （** 128 **）**|資料表限定詞。|  
|**TABLE_SCHEMA**|**Nvarchar （** 128 **）**|包含資料表的結構描述名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**sysname**|資料表名稱。|  
|**COLUMN_NAME**|**sysname**|資料行名稱。|  
|**PRIVILEGE_TYPE**|**Varchar （** 10 **）**|權限的類型。|  
|**IS_GRANTABLE**|**Varchar （** 3 **）**|指定被授與者是否可以將權限授與其他人。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊架構視圖 &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sql_modules &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [server_permissions &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
  
