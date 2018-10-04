---
title: sys.fulltext_index_columns & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 08279891640407371c19884d4384fabb61786b54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47857146"
---
# <a name="sysfulltextindexcolumns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  屬於全文檢索索引一部分的每個資料行各有一個資料列。    
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|所屬物件的識別碼。|  
|**column_id**|**int**|屬於全文檢索索引一部份的資料行識別碼。|  
|**type_column_id**|**int**|這個類型資料行識別碼會針對給定資料列中的文件，儲存使用者提供的文件副檔名 (".doc"、".xls" 等等)。 只有在全文檢索索引時需要篩選資料的資料行，才能指定這個類型資料行。 如果不適用，則傳回 NULL。 如需詳細資訊，請參閱 [設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)。|  
|**language_id**|**int**|用於檢索這個全文檢索資料行之斷詞工具的語言識別碼。<br /><br /> 0 = 中性語言。<br /><br /> 如需詳細資訊，請參閱 < [sys.fulltext_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。|  
|**statistical_semantics**|**int**|1 = 這個資料行除了啟用全文檢索索引以外，也啟用了統計語意。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
