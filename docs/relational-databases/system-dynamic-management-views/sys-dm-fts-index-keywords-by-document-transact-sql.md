---
title: sys.dm_fts_index_keywords_by_document (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_by_document_TSQL
- dm_fts_index_keywords_by_document_TSQL
- sys.dm_fts_index_keywords_by_document
- dm_fts_index_keywords_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- sys.dm_fts_index_keywords_by_document dynamic management function
- full-text search [SQL Server], viewing keywords
ms.assetid: 793b978b-c8a1-428c-90c2-a3e49d81b5c9
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 68cb399b6b32285340e2099e15c9bad316032e4a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmftsindexkeywordsbydocument-transact-sql"></a>sys.dm_fts_index_keywords_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  傳回與指定資料表相關聯之全文檢索索引之文件層級內容的相關資訊。  
  
 sys.dm_fts_index_keywords_by_document 是動態管理函數。  
  
 **若要檢視較高層級的全文檢索索引資訊**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
 **若要檢視屬性層級內容的相關資訊與相關文件屬性**  
  
-   [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.dm_fts_index_keywords_by_document  
(   
    DB_ID('database_name'),     OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>引數  
 db_id('*database_name*')  
 呼叫[db_id （)](../../t-sql/functions/db-id-transact-sql.md)函式。 這個函數會接受資料庫名稱並傳回資料庫識別碼，然後 sys.dm_fts_index_keywords_by_document 就會使用此識別碼來尋找指定的資料庫。 如果省略 *database_name*，則會傳回目前的資料庫識別碼。  
  
 object_id('*table_name*')  
 呼叫[object_id （)](../../t-sql/functions/object-id-transact-sql.md)函式。 此函數會接受資料表名稱並傳回資料表的資料表識別碼 (包含所要檢查的全文檢索索引)。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行|資料類型|Description|  
|------------|---------------|-----------------|  
|關鍵字 (keyword)|**nvarchar(4000)**|儲存在全文檢索索引內部之關鍵字的十六進位表示法。<br /><br /> 注意： OxFF 代表指出檔案或資料集的結尾的特殊字元。|  
|display_term|**nvarchar(4000)**|關鍵字的人們可讀取格式。 這個格式衍生自儲存在全文檢索索引中的內部格式。<br /><br /> 注意： OxFF 代表指出檔案或資料集的結尾的特殊字元。|  
|column_id|**int**|從中針對目前關鍵字進行全文檢索索引之資料行的識別碼。|  
|document_id|**int**|從中針對目前詞彙進行全文檢索索引之文件或資料列的識別碼。 這個識別碼會對應至該文件或資料列的全文檢索索引鍵值。|  
|occurrence_count|**int**|目前關鍵字在文件或資料列所指出的次數**document_id**。 當 '*search_property_name*' 指定，則 occurrence_count 文件或資料列內指定之搜尋屬性中顯示的項目之目前的關鍵字數目。|  
  
## <a name="remarks"></a>備註  
 此外，sys.dm_fts_index_keywords_by_document 所傳回的資訊可用於了解下列項目：  
  
-   全文檢索索引包含之關鍵字的總數。  
  
-   關鍵字是否屬於給定文件或資料列的一部分。  
  
-   關鍵字出現在整個全文檢索索引中的次數，亦即：  
  
     ([總和](../../t-sql/functions/sum-transact-sql.md)(**occurrence_count**) 其中**關鍵字**=*keyword_value* )  
  
-   關鍵字出現在給定文件或資料列中的次數。  
  
-   給定文件或資料列所包含的關鍵字數目。  
  
 而且，您也可以使用 sys.dm_fts_index_keywords_by_document 所提供的資訊來擷取屬於給定文件或資料列的所有關鍵字。  
  
 當全文檢索索引鍵資料行為整數資料類型時，建議您將 document_id 直接對應到基底資料表內的全文檢索索引鍵值。  
  
 相反地，當全文檢索索引鍵資料行使用非整數資料類型時，document_id 就不表示基底資料表內的全文檢索索引鍵。 在此情況下，若要識別 dm_fts_index_keywords_by_document 所傳回的基底資料表中的資料列，您需要聯結此檢視與所傳回的結果[sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)。 在您可以聯結之前，必須先將預存程序的輸出儲存到暫存資料表。 然後您可以將 dm_fts_index_keywords_by_document 的 document_id 資料行聯結到此預存程序所傳回的 DocId 資料行。 請注意，**時間戳記**資料行無法接收值在插入時，因為它們是由自動產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 因此，**時間戳記**資料行必須轉換成**varbinary （8)** 資料行。 下列範例會示範這些步驟。 在此範例中， *table_id*是您的資料表識別碼*database_name*是您的資料庫名稱和*table_name*是資料表的名稱。  
  
```  
USE database_name;  
GO  
CREATE TABLE #MyTempTable   
   (  
      docid INT PRIMARY KEY ,  
      [key] INT NOT NULL  
   );  
DECLARE @db_id int = db_id(N'database_name');  
DECLARE @table_id int = OBJECT_ID(N'table_name');  
INSERT INTO #MyTempTable EXEC sp_fulltext_keymappings @table_id;  
SELECT * FROM sys.dm_fts_index_keywords_by_document   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Permissions  
 需要全文檢索索引和 CREATE FULLTEXT CATALOG 權限所涵蓋之資料行的 SELECT 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-full-text-index-content-at-the-document-level"></a>A. 顯示位於文件層級的全文檢索索引內容  
 下列範例會在 `HumanResources.JobCandidate` 範例資料庫的 `AdventureWorks2012` 資料表中顯示位於文件層級之全文檢索索引的內容。  
  
> [!NOTE]  
>  您可以藉由執行所提供的範例來建立這個索引`HumanResources.JobCandidate`資料表中[CREATE FULLTEXT INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)。  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_by_document(db_id('AdventureWorks'),   
object_id('HumanResources.JobCandidate'));  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋和語意搜尋動態管理檢視與函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [sp_fulltext_keymappings &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [改善全文檢索索引的效能](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
  
