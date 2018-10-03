---
title: sys.fulltext_index_catalog_usages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_catalog_usages
- sys.fulltext_index_catalog_usages_TSQL
- fulltext_index_catalog_usages
- fulltext_index_catalog_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_index_catalog_usages catalog view
ms.assetid: d095ab62-270b-484b-a541-9f9e7c951cf0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d9714230ff13588e490ecdbb502c98bb8c2223d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617876"
---
# <a name="sysfulltextindexcatalogusages-transact-sql"></a>sys.fulltext_index_catalog_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對通往全文檢索索引參考的每個全文檢索目錄，各傳回一個資料列。    
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|全文檢索索引資料表的識別碼。 在資料庫中，這是唯一的。|  
|**index_id**|**int**|全文檢索索引的識別碼。|  
|**fulltext_catalog_id**|**int**|全文檢索目錄的識別碼。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [資料空間&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
  
