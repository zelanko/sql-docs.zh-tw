---
description: VIEW_TABLE_USAGE (Transact-SQL)
title: VIEW_TABLE_USAGE (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ab6d2bb6b1abff0eb2d6a4d30e29464bf7485f8
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753550"
---
# <a name="view_table_usage-transact-sql"></a>VIEW_TABLE_USAGE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  針對檢視所用目前資料庫中的每份資料表，各傳回一個資料列。 這個資訊結構描述檢視會傳回目前使用者有權限的物件之相關資訊。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**VIEW_CATALOG**|**Nvarchar (** 128 **) **|檢視限定詞。|  
|**VIEW_SCHEMA**|**Nvarchar (** 128 **) **|包含檢視的結構描述名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;**  只有可靠的方法可尋找物件的架構，就是查詢 sys. objects 目錄檢視。|  
|**VIEW_NAME**|**sysname**|檢視名稱。|  
|**TABLE_CATALOG**|**Nvarchar (** 128 **) **|資料表限定詞。|  
|**TABLE_SCHEMA**|**Nvarchar (** 128 **) **|包含基底資料表之結構描述的名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;**  只有可靠的方法可尋找物件的架構，就是查詢 sys. objects 目錄檢視。|  
|**TABLE_NAME**|**sysname**|作為檢視基礎的基底資料表。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](../../t-sql/language-reference.md)   
 [&#40;Transact-sql&#41;的資訊架構視圖 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_dependencies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
