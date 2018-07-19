---
title: CONSTRAINT_COLUMN_USAGE (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_COLUMN_USAGE_TSQL
- CONSTRAINT_COLUMN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE view
- CONSTRAINT_COLUMN_USAGE view
ms.assetid: 0f3ae521-6b19-43ad-b2c4-3822adb19591
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ac38fb841a2027c1f616333b50c320aa9a3317ad
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33232553"
---
# <a name="constraintcolumnusage-transact-sql"></a>CONSTRAINT_COLUMN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中定義了資料行條件約束的每個資料行，各傳回一個資料列。 這個資訊結構描述檢視會傳回目前使用者有權限的物件之相關資訊。  
  
 若要從這些檢視中擷取資訊，請指定完整的名稱 **INFORMATION_SCHEMA。 * * * view_name*。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG 排列**|**nvarchar(** 128 **)**|資料表限定詞。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|包含資料表擁有者之結構描述的名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|資料表名稱。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|資料行名稱。|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|條件約束限定詞。|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|包含條件約束之結構描述的名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**CONSTRAINT_NAME**|**nvarchar(** 128 **)**|條件約束名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [sys.check_constraints &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.key_constraints &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.foreign_keys &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
