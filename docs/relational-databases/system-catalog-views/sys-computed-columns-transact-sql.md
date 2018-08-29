---
title: sys.computed_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.computed_columns_TSQL
- sys.computed_columns
- computed_columns_TSQL
- computed_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.computed_columns catalog view
ms.assetid: c962c619-e18f-4315-9251-8d9862462299
caps.latest.revision: 48
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f518ac42aa976b6ef99cdcdf91e5d6b7a92fbb4d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43097070"
---
# <a name="syscomputedcolumns-transact-sql"></a>sys.computed_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  包含一個資料列的每個資料行中找到**sys.columns**也就是計算資料行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承資料行 >**||**Sys.computed_columns**檢視會傳回所有資料行**sys.columns**檢視。 另外亦將傳回以下所述的其他資料行。 如需資料行的描述， **sys.computed_columns**檢視繼承自**sys.columns**，請參閱[sys.columns &#40;-&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)。 值**sys.computer_columns**資料行一律會設為 1 **sys.computed_columns**檢視。|  
|**定義**|**nvarchar(max)**|定義這個計算資料行的 SQL 文字。|  
|**uses_database_collation**|**bit**|1 = 資料行定義須依據資料庫的預設定序進行正確評估；否則為 0。 這種相依性可以防止資料庫預設定序變更。|  
|**is_persisted**|**bit**|計算資料行是保存計算資料行。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
