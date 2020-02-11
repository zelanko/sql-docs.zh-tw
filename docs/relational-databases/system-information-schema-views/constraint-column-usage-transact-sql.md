---
title: CONSTRAINT_COLUMN_USAGE （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e0936e74b3c48a2fe3298215107ae48d0c3b63cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67950780"
---
# <a name="constraint_column_usage-transact-sql"></a>CONSTRAINT_COLUMN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中定義了資料行條件約束的每個資料行，各傳回一個資料列。 這個資訊結構描述檢視會傳回目前使用者有權限的物件之相關資訊。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**Nvarchar （** 128 **）**|資料表限定詞。|  
|**TABLE_SCHEMA**|**Nvarchar （** 128 **）**|包含資料表擁有者之結構描述的名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**Nvarchar （** 128 **）**|資料表名稱。|  
|**COLUMN_NAME**|**Nvarchar （** 128 **）**|資料行名稱。|  
|**CONSTRAINT_CATALOG**|**Nvarchar （** 128 **）**|條件約束限定詞。|  
|**CONSTRAINT_SCHEMA**|**Nvarchar （** 128 **）**|包含條件約束之結構描述的名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**CONSTRAINT_NAME**|**Nvarchar （** 128 **）**|條件約束名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊架構視圖 &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [check_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [key_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [foreign_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
