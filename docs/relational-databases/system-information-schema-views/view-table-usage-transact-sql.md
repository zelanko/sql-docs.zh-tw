---
title: VIEW_TABLE_USAGE (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEW_TABLE_USAGE_TSQL
- VIEW_TABLE_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.VIEW_TABLE_USAGE view
- VIEW_TABLE_USAGE view
ms.assetid: 0aeefb3f-02ef-457e-8c42-84ddb26f1c88
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e691a52cebf3ca9de0454ca2ccd60b3f8daa43f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078367"
---
# <a name="viewtableusage-transact-sql"></a>VIEW_TABLE_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對檢視所用目前資料庫中的每份資料表，各傳回一個資料列。 這個資訊結構描述檢視會傳回目前使用者有權限的物件之相關資訊。  
  
 若要從這些檢視擷取資訊，請指定 完整格式的名稱**INFORMATION_SCHEMA。** _view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**VIEW_CATALOG**|**nvarchar(** 128 **)**|檢視限定詞。|  
|**VIEW_SCHEMA**|**nvarchar(** 128 **)**|包含檢視的結構描述名稱。<br /><br /> **&#42;&#42;重要&#42; &#42;** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**VIEW_NAME**|**sysname**|檢視名稱。|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|資料表限定詞。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|包含基底資料表之結構描述的名稱。<br /><br /> **&#42;&#42;重要&#42; &#42;** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**sysname**|作為檢視基礎的基底資料表。|  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_dependencies &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  
