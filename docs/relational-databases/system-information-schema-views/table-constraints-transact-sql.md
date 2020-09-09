---
description: TABLE_CONSTRAINTS (Transact-SQL)
title: TABLE_CONSTRAINTS (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- TABLE_CONSTRAINTS
- TABLE_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.TABLE_CONSTRAINTS view
- TABLE_CONSTRAINTS view
ms.assetid: 687f3284-2849-4853-8a5c-fc936deceae0
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c44e41086b436e046745da2cde86918b383c9eba
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542089"
---
# <a name="table_constraints-transact-sql"></a>TABLE_CONSTRAINTS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  針對目前資料庫中的每個資料表條件約束，各傳回一個資料列。 這個資訊結構描述檢視會傳回目前使用者有權限的物件之相關資訊。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**Nvarchar (** 128 **) **|條件約束限定詞。|  
|**CONSTRAINT_SCHEMA**|**Nvarchar (** 128 **) **|包含條件約束之結構描述的名稱。<br /><br /> 重要的是，若要尋找物件的架構，唯一的可靠方式就是查詢 sys. objects 目錄檢視。 <strong> \* \* \* \* </strong>|  
|**CONSTRAINT_NAME**|**sysname**|條件約束名稱。|  
|**TABLE_CATALOG**|**Nvarchar (** 128 **) **|資料表限定詞。|  
|**TABLE_SCHEMA**|**Nvarchar (** 128 **) **|包含資料表的結構描述名稱。<br /><br /> 重要的是，若要尋找物件的架構，唯一的可靠方式就是查詢 sys. objects 目錄檢視。 <strong> \* \* \* \* </strong>|  
|**TABLE_NAME**|**sysname**|資料表名稱。|  
|**CONSTRAINT_TYPE**|**Varchar (** 11 **) **|條件約束的類型：<br /><br /> CHECK<br /><br /> UNIQUE<br /><br /> PRIMARY KEY<br /><br /> FOREIGN KEY|  
|**IS_DEFERRABLE**|**Varchar (** 2 **) **|指定條件約束檢查是否可以延後。 一律傳回 NO。|  
|**INITIALLY_DEFERRED**|**Varchar (** 2 **) **|指定一開始時是否延遲條件約束檢查。 一律傳回 NO。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [&#40;Transact-sql&#41;的資訊架構視圖 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. key_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys. check_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
  
