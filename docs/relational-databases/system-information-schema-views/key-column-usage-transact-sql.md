---
title: KEY_COLUMN_USAGE (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- KEY_COLUMN_USAGE_TSQL
- KEY_COLUMN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.KEY_COLUMN_USAGE view
- KEY_COLUMN_USAGE view
ms.assetid: ec1e18c2-63a1-4d2b-ba9a-c13857403782
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 002bb09d82a8f636d6216ed9a5a82182bb1415fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848326"
---
# <a name="keycolumnusage-transact-sql"></a>KEY_COLUMN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中被限制為索引鍵的每個資料行，各傳回一個資料列。 這個資訊結構描述檢視會傳回目前使用者有權限的物件之相關資訊。  
  
 若要從這些檢視擷取資訊，請指定 完整格式的名稱 **INFORMATION_SCHEMA。 * * * view_name*。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|條件約束限定詞。|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|包含條件約束之結構描述的名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**CONSTRAINT_NAME**|**nvarchar(** 128 **)**|條件約束名稱。|  
|**TABLE_CATALOG 排列**|**nvarchar(** 128 **)**|資料表限定詞。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|包含資料表的結構描述名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|資料表名稱。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|資料行名稱。|  
|**ORDINAL_POSITION**|**int**|資料行序數位置。|  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.foreign_keys &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)   
 [sys.key_constraints &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)  
  
  
