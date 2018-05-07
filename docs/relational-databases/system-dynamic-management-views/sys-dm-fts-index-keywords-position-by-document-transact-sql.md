---
title: sys.dm_fts_index_keywords_position_by_document (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document
- sys.dm_fts_index_keywords_position_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords_position_by_document dynamic management view
ms.assetid: 0d70184f-baa2-411b-a32d-a4c5af890edd
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76d7a58ba785964f240cccb6d68cdff897cd6a77
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmftsindexkeywordspositionbydocument-transact-sql"></a>sys.dm_fts_index_keywords_position_by_document (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回索引的文件中的關鍵字的位置資訊。  
  
## <a name="syntax"></a>語法  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>引數  
 db_id('*database_name*')  
 呼叫[db_id （)](../../t-sql/functions/db-id-transact-sql.md)函式。 此函式會接受資料庫名稱，並傳回資料庫識別碼，哪些 sys.dm_fts_index_keywords_position_by_document 用來尋找指定的資料庫。  
  
 object_id('*table_name*')  
 呼叫[object_id （)](../../t-sql/functions/object-id-transact-sql.md)函式。 此函數會接受資料表名稱並傳回資料表的資料表識別碼 (包含所要檢查的全文檢索索引)。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行|資料類型|Description|  
|------------|---------------|-----------------|  
|關鍵字 (keyword)|**varbinary(128)**|二進位字串關鍵字。|  
|display_term|**nvarchar(4000)**|關鍵字的人們可讀取格式。 這個格式衍生自儲存在全文檢索索引中的內部格式。|  
|column_id|**int**|從中針對目前關鍵字進行全文檢索索引之資料行的識別碼。|  
|document_id|**bigint**|從中針對目前詞彙進行全文檢索索引之文件或資料列的識別碼。 這個識別碼會對應至該文件或資料列的全文檢索索引鍵值。|  
|position|**int**|文件中關鍵字的位置。|  
  
## <a name="remarks"></a>備註  
 您可以使用 DMV 來識別索引的文字，在索引之文件中的位置。 此 DMV 可用來疑難排解問題時**sys.dm_fts_index_keywords_by_document**表示的文字並在全文檢索索引中，但當您執行查詢，使用這些字時，不會傳回文件。  
  
## <a name="permissions"></a>Permissions  
 需要全文檢索索引和 CREATE FULLTEXT CATALOG 權限所涵蓋之資料行的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回從全文檢索索引的關鍵字`Production.Document`資料表`AdventureWorks`範例資料庫。  
  
```  
USE AdventureWorks2012;  
GO   
  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
);   
GO  
```  
  
 您可以在其他 columns_id 如同下列範例查詢中，若要進一步找出的位置上加入述詞。  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [改善全文檢索索引的效能](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [全文檢索搜尋和語意搜尋函數&#40;Transact SQL&#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [全文檢索搜尋和語意搜尋動態管理檢視與函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文檢索搜尋和語意搜尋預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
