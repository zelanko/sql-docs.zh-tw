---
title: sys.databases computed_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 883469cb57a9735ccfc27ecaafa85fedd41cf9b3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821911"
---
# <a name="syscomputed_columns-transact-sql"></a>sys.computed_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對在**sys.databases**中找到的每個資料行，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承的資料行>**||[ **Sys.databases] computed_columns**視圖會傳回 [ **sys.databases** ] 視圖中的所有資料行。 另外亦將傳回以下所述的其他資料行。 如需**sys. computed_columns** view 繼承自**sys.databases**之資料行的描述，請參閱[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)。 在 [ **computed_columns** ] 視圖中， **is_computed**資料行的值一律會設定為1。|  
|**definition**|**nvarchar(max)**|定義這個計算資料行的 SQL 文字。|  
|**uses_database_collation**|**bit**|1 = 資料行定義須依據資料庫的預設定序進行正確評估；否則為 0。 這種相依性可以防止資料庫預設定序變更。|  
|**is_persisted**|**bit**|計算資料行是保存計算資料行。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
