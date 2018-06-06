---
title: semantickeyphrasetable (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- semantickeyphrasetable
- semantickeyphrasetable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semantickeyphrasetable function
ms.assetid: d33b973a-2724-4d4b-aaf7-67675929c392
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 98d837abe05cf99051230e24fd0d418e1263aa4f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="semantickeyphrasetable-transact-sql"></a>semantickeyphrasetable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  為關聯至指定資料表之資料行的主要片語，傳回包含零個、一個或多個資料列的資料表。  
  
 您可以在 SELECT 陳述式的 FROM 子句中參考這個資料列集函數，就像是一般資料表名稱一樣。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
SEMANTICKEYPHRASETABLE  
    (  
    table,  
    { column | (column_list) | * }  
     [ , source_key ]  
    )  
```  
  
##  <a name="Arguments"></a> 引數  
 **table**  
 這是已啟用全文檢索和語意索引之資料表的名稱。  
  
 這個名稱可以是一到四個部分名稱，但不允許遠端伺服器名稱。  
  
 **column**  
 應傳回結果之索引資料行的名稱。 資料行必須啟用語意索引。  
  
 **column_list**  
 指定以逗號分隔並括以括號的數個資料行。 所有資料行皆必須啟用語意索引。  
  
 **\***  
 指定已包含所有啟用語意索引的資料行。  
  
 **source_key**  
 資料列的唯一索引鍵，可以用於要求特定資料列的結果。  
  
 在可能的情況下，此索引鍵會隱含轉換成來源資料表中的全文檢索唯一索引鍵類型。 索引鍵可以指定成常數或變數，但不可以是運算式或純量子查詢的結果。 如果省略 source_key，將會傳回所有資料列的結果。  
  
## <a name="table-returned"></a>傳回的資料表  
 下表說明此資料列集函式傳回的主要片語相關資訊。  
  
|Column_name|型別|Description|  
|------------------|----------|-----------------|  
|**column_id**|**int**|從中擷取及索引目前主要片語之資料行的識別碼。<br /><br /> 如需如何從 column_id 擷取資料行名稱 (反之亦然) 的詳細資料，請參閱 COL_NAME 及 COLUMNPROPERTY 函數。|  
|**document_key**|**\***<br /><br /> 此索引鍵與來源資料表中的唯一索引鍵類型相同。|要從中索引目前主要片語之文件或資料列的唯一索引鍵值。|  
|**keyphrase**|**NVARCHAR**|在 column_id 所指定之資料行中所找到，關聯至 document_key 指定之文件的主要片語。|  
|**score**|**REAL**|此主要片語與索引資料行的相同文件中所有其他主要片語之間關聯性的相對值。<br /><br /> 此值是 [0.0, 1.0] 範圍內的小數值，分數愈高表示權重愈高。1.0 為滿分。|  
  
## <a name="general-remarks"></a>一般備註  
 如需詳細資訊，請參閱[使用語意搜尋的文件中尋找主要片語](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)。  
  
## <a name="metadata"></a>中繼資料  
 如需有關語意關鍵片語擷取和母體擴展的詳細資訊和狀態，請查詢下列動態管理檢視：  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要建立全文檢索和語意索引之基底資料表的 SELECT 權限。  
  
## <a name="examples"></a>範例  
  
###  <a name="HowToTopPhrases"></a>範例 1： 在特定文件中尋找前的主要片語  
 下列範例會從 AdventureWorks 範例資料庫之 Production.Document 資料表 Document 資料行 @DocumentId 變數所指定的文件中，擷取前 10 個主要片語。 @DocumentId 變數是指來自全文檢索索引之索引鍵資料行的值。 **SEMANTICKEYPHRASETABLE** 函數會使用索引搜尋有效率地擷取這些結果，而不會使用資料表掃描。 此範例假設已針對全文檢索與語意索引配置資料行。  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
  
```  
  
###  <a name="HowToTopDocuments"></a>範例 2： 尋找包含特定主要片語的最上層文件  
 下列範例會從 AdventureWorks 範例資料庫之 Production.Document 資料表的 Document 資料行中，擷取前 25 份包含主要片語的 "Bracket" 的文件。 此範例假設已針對全文檢索與語意索引配置資料行。  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
  
```  
  
  
