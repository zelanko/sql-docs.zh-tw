---
description: 'sys. dm_fts_index_keywords_position_by_document (Transact-sql) '
title: sys. dm_fts_index_keywords_position_by_document (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 0b14ccbe7643ed56e18dc79b2a72e27867d63454
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474943"
---
# <a name="sysdm_fts_index_keywords_position_by_document-transact-sql"></a>sys. dm_fts_index_keywords_position_by_document (Transact-sql) 
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回已編制索引之檔中的關鍵字位置資訊。  
  
## <a name="syntax"></a>語法  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>引數  
 db_id ( '*database_name*' )   
 [DB_ID ( # B1](../../t-sql/functions/db-id-transact-sql.md)函數的呼叫。 此函數會接受資料庫名稱並傳回資料庫識別碼，而 sys. dm_fts_index_keywords_position_by_document 會使用此識別碼來尋找指定的資料庫。  
  
 object_id ( '*table_name*' )   
 [OBJECT_ID ( # B1](../../t-sql/functions/object-id-transact-sql.md)函數的呼叫。 此函數會接受資料表名稱並傳回資料表的資料表識別碼 (包含所要檢查的全文檢索索引)。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行|資料類型|描述|  
|------------|---------------|-----------------|  
|關鍵字 (keyword)|**varbinary(128)**|代表關鍵字的二進位字串。|  
|display_term|**nvarchar(4000)**|關鍵字的人們可讀取格式。 這個格式衍生自儲存在全文檢索索引中的內部格式。|  
|column_id|**int**|從中針對目前關鍵字進行全文檢索索引之資料行的識別碼。|  
|document_id|**bigint**|從中針對目前詞彙進行全文檢索索引之文件或資料列的識別碼。 這個識別碼會對應至該文件或資料列的全文檢索索引鍵值。|  
|position|**int**|檔中關鍵字的位置。|  
  
## <a name="remarks"></a>備註  
 使用 DMV 來識別索引檔中索引字組的位置。 當 **sys. dm_fts_index_keywords_by_document** 指出文字是在全文檢索索引中，但當您使用這些字組執行查詢時，這個 DMV 可以用來針對問題進行疑難排解，而且不會傳回檔。  
  
## <a name="permissions"></a>權限  
 需要全文檢索索引和 CREATE FULLTEXT CATALOG 權限所涵蓋之資料行的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從範例資料庫之資料表的全文檢索索引傳回關鍵字 `Production.Document` `AdventureWorks` 。  
  
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
  
 您可以在其他 columns_id 上新增述詞，如下列範例查詢所示，以進一步隔離位置。  
  
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
 [全文檢索搜尋和語義搜尋函數 &#40;Transact-sql&#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [&#40;Transact-sql&#41;的全文檢索搜尋和語義搜尋動態管理檢視和函數 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文檢索搜尋和語義搜尋預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [使用搜尋屬性清單搜尋文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
