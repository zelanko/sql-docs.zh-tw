---
title: VIEW_COLUMN_USAGE （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEW_COLUMN_USAGE
- VIEW_COLUMN_USAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.VIEW_COLUMN_USAGE view
- VIEW_COLUMN_USAGE view
ms.assetid: fc0b3608-a7e8-4532-8215-32235d6670f1
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d6fdb0c5be9b509c2f801ad5728d40467cd349c2
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670331"
---
# <a name="view_column_usage-transact-sql"></a>VIEW_COLUMN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對目前資料庫中用於檢視定義的每個資料行，各傳回一個資料列。 這個資訊結構描述檢視會傳回目前使用者有權限的物件之相關資訊。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**VIEW_CATALOG**|**Nvarchar （** 128 **）**|檢視限定詞。|  
|**VIEW_SCHEMA**|**Nvarchar （** 128 **）**|包含檢視的結構描述名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 只有可靠的方法可以尋找物件的架構，就是查詢 sys.databases 目錄檢視。|  
|**VIEW_NAME**|**sysname**|檢視名稱。|  
|**TABLE_CATALOG**|**Nvarchar （** 128 **）**|資料表限定詞。|  
|**TABLE_SCHEMA**|**Nvarchar （** 128 **）**|包含資料表的結構描述名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 只有可靠的方法可以尋找物件的架構，就是查詢 sys.databases 目錄檢視。|  
|**TABLE_NAME**|**sysname**|基底資料表。|  
|**COLUMN_NAME**|**sysname**|資料行名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊架構視圖 &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sql_dependencies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
