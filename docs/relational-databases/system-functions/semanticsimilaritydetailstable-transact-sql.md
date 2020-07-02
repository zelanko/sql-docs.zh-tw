---
title: semanticsimilaritydetailstable （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4b264f5276ad9d9f411fcdd14550130eb412a1b0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771561"
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  會傳回零個、一個或多個主要片語的資料列，而這些主要片語對於兩個內容語意類似之文件 (來源文件與比對文件) 來說是共同的主要片語。  
  
 此資料列集函數可在 SELECT 語句的 FROM 子句中參考 
  
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
  
##  <a name="arguments"></a><a name="Arguments"></a>參量  
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
  
|Column_name|類型|描述|  
|------------------|----------|-----------------|  
|**keyphrase**|**NVARCHAR**|來源文件與比對文件中出現類似度的主要片語。|  
|**成績**|**即時**|此主要片語與兩份文件中所有其他類似片語之關聯性的相對值。<br /><br /> 此值是 [0.0, 1.0] 範圍內的小數值，分數愈高表示權重愈高。1.0 為滿分。|  
  
## <a name="general-remarks"></a>一般備註  
 如需詳細資訊，請參閱[使用語義搜尋尋找相似及相關的檔](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)。  
  
## <a name="metadata"></a>中繼資料  
 如需有關語意相似度擷取和母體擴展的詳細資訊和狀態，請查詢下列動態管理檢視：  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要建立全文檢索和語意索引之基底資料表的 SELECT 權限。  
  
## <a name="examples"></a>範例  
 下列範例會抓取5個主要片語，其在 AdventureWorks2012 範例資料庫的**HumanResources humanresources.jobcandidate**資料表中的指定候選項目之間具有最高的相似性分數。 @CandidateId和 @MatchedID 變數代表全文檢索索引之索引鍵資料行中的值。  
  
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
  
  
