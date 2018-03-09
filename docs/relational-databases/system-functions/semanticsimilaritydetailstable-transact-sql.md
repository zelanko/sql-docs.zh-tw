---
title: "semanticsimilaritydetailstable (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69d13d3b16d1b58062cd93dc18e2f20f3fd01b42
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  會傳回零個、一個或多個主要片語的資料列，而這些主要片語對於兩個內容語意類似之文件 (來源文件與比對文件) 來說是共同的主要片語。  
  
 此資料列集函式可以參考 SELECT 陳述式的 FROM 子句中 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
SEMANTICSIMILARITYDETAILSTABLE  
    (  
    table,  
    source_column,  
    source_key,  
    matched_column,  
    matched_key  
    )  
```  
  
##  <a name="Arguments"></a> 引數  
 **table**  
 這是已啟用全文檢索和語意索引之資料表的名稱。  
  
 這個名稱可以是一到四個部分名稱，但不允許遠端伺服器名稱。  
  
 **source_column**  
 內含要比對相似度之內容的來源資料列中資料行的名稱。  
  
 **source_key**  
 代表來源文件資料列的獨特索引鍵。  
  
 在可能的情況下，這個索引鍵會隱含轉換成來源資料表中全文檢索之唯一索引鍵的類型。 索引鍵可以指定成常數或變數，但不可以是運算式或純量子查詢的結果。 如果指定的索引鍵無效，則不會傳回資料列。  
  
 **matched_column**  
 內含要比對相似度之內容的比對資料列中資料行的名稱。  
  
 **matched_key**  
 代表比對文件的資料列之唯一索引鍵。  
  
 在可能的情況下，這個索引鍵會隱含轉換成來源資料表中全文檢索之唯一索引鍵的類型。 索引鍵可以指定成常數或變數，但不可以是運算式或純量子查詢的結果。  
  
## <a name="table-returned"></a>傳回的資料表  
 下表說明此資料列集函式傳回的主要片語相關資訊。  
  
|Column_name|型別|Description|  
|------------------|----------|-----------------|  
|**keyphrase**|**NVARCHAR**|來源文件與比對文件中出現類似度的主要片語。|  
|**score**|**實數**|此主要片語與兩份文件中所有其他類似片語之關聯性的相對值。<br /><br /> 此值是 [0.0, 1.0] 範圍內的小數值，分數愈高表示權重愈高。1.0 為滿分。|  
  
## <a name="general-remarks"></a>一般備註  
 如需詳細資訊，請參閱[尋找相似及相關文件使用語意搜尋](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)。  
  
## <a name="metadata"></a>中繼資料  
 如需有關語意相似度擷取和母體擴展的詳細資訊和狀態，請查詢下列動態管理檢視：  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要建立全文檢索和語意索引之基底資料表的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會擷取所指定候選人之間相似度分數最高的 5 個主要片語**HumanResources.JobCandidate** AdventureWorks2012 範例資料庫的資料表。 @CandidateId和@MatchedID變數代表來自全文檢索索引之索引鍵資料行的值。  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROMSEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
