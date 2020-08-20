---
description: sys.fulltext_index_columns (Transact-SQL)
title: sys. fulltext_index_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1c1dbd0b4885ef9c1320a505eba17b21b5c8964c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460648"
---
# <a name="sysfulltext_index_columns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  屬於全文檢索索引一部分的每個資料行各有一個資料列。    
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**int**|所屬物件的識別碼。|  
|**column_id**|**int**|屬於全文檢索索引一部份的資料行識別碼。|  
|**type_column_id**|**int**|在指定的資料列中，儲存使用者提供的檔副檔名的類型資料行識別碼-".doc"、".xls" 等等。 只有在全文檢索索引時需要篩選資料的資料行，才能指定這個類型資料行。 如果不適用，則傳回 NULL。 如需詳細資訊，請參閱 [設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)。|  
|**language_id**|**int**|用於檢索這個全文檢索資料行之斷詞工具的語言識別碼。<br /><br /> 0 = 中性語言。<br /><br /> 如需詳細資訊，請參閱 [sys. fulltext_languages &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。|  
|**statistical_semantics**|**int**|1 = 這個資料行除了啟用全文檢索索引以外，也啟用了統計語意。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
