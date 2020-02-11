---
title: 管理及監視語意搜尋 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 94f8edc0fe8b2505adc36705200e299f36b2dbf9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011124"
---
# <a name="manage-and-monitor-semantic-search"></a>管理及監視語意搜尋
  描述語意索引的程序，以及與管理及監視索引相關的工作。  
  
##  <a name="HowToMonitorStatus"></a>如何：檢查語義索引的狀態  
 **語意索引的第一個階段是否已完成？**  
 查詢動態管理檢視 [sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)**status** 和 **status_description** 資料行。  
  
 索引的第一個階段包括擴展全文檢索關鍵字索引和語意主要片語索引，以及擷取文件相似度資料。  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
 **語意索引的第二個階段是否已完成？**  
 查詢動態管理檢視 [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)**status** 和 **status_description** 資料行。  
  
 索引的第二個階段包括擴展語意文件相似度索引。  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a>如何：檢查語義索引的大小  
 **語意主要片語索引或語意文件相似度索引的邏輯大小為何？**  
 查詢動態管理檢視 [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)。  
  
 邏輯大小會以索引頁面的數目表示。  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
 **全文檢索目錄的全文檢索索引與語意索引的總大小為何？**  
 查詢 **FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;** 中繼資料函數的 [IndexSize](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql) 屬性。  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
 **全文檢索目錄的全文檢索索引和語意索引中建立了多少項目的索引？**  
 查詢 **FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;** 中繼資料函數的 [ItemCount](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql) 屬性。  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a>如何：強制填入語義索引  
 您可以強制全文檢索索引和語意索引的母體擴展，其方式是使用 START/STOP/PAUSE 或 RESUME POPULATION 子句搭配全文檢索索引所描述的相同語法和行為。 如需詳細資訊，請參閱 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql) 和[擴展全文檢索索引](../indexes/indexes.md)。  
  
 因為語意索引會依據全文檢索索引，所以只有當關聯的全文檢索索引已擴展時，才會擴展語意索引。  
  
 **範例：開始全文檢索索引與語意索引的完整母體擴展**  
  
 下列範例會改變 AdventureWorks2012 範例資料庫中 **Production.Document** 資料表上現有的全文檢索索引，以便開始完整擴展全文檢索索引與語意索引。  
  
```vb  
USE AdventureWorks2012  
GO  
  
ALTER FULLTEXT INDEX ON Production.Document  
    START FULL POPULATION  
GO  
```  
  
##  <a name="HowToDisableIndexing"></a>如何：停用或重新啟用語義索引編制  
 您可以啟用或停用全文檢索索引或語意索引，其方式是使用 ENABLE/DISABLE 子句搭配全文檢索索引所描述的相同語法與行為。 如需詳細資訊，請參閱 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)。  
  
 當語意索引已停用且暫停時，語意資料的查詢會持續順利運作，並傳回之前的索引資料。 此行為與全文檢索搜尋的行為不一致。  
  
```sql  
-- To disable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name DISABLE  
GO  
  
-- To re-enable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name ENABLE  
GO  
```  
  
##  <a name="SemanticIndexing"></a>語義索引的階段  
 語意搜尋會針對其啟用所在的每一個資料行，建立兩種資料的索引：  
  
1.  **關鍵片語**  
  
2.  **文件相似度**  
  
 語意索引會連同全文檢索索引發生在兩個階段：  
  
1.  **階段 1**. 全文檢索關鍵字索引和語意主要片語索引會以平行方式同時擴展。 此時也會擷取建立文件相似度索引所需的資料。  
  
2.  **階段 2**： 然後會擴展語意文件相似度索引。 此索引取決於上一個階段中已擴展的兩個索引。  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a>問題：未填入語義索引  
 **是否已擴展關聯的全文檢索索引？**  
 因為語意索引會依據全文檢索索引，所以只有當關聯的全文檢索索引已擴展時，才會擴展語意索引。  
  
 **是否已正確安裝及設定全文檢索搜尋及語意搜尋？**  
 如需詳細資訊，請參閱 [安裝及設定語意搜尋](install-and-configure-semantic-search.md)。  
  
 **FDHOST 服務是否無法使用，或是有另一個狀況導致全文檢索索引失敗？**  
 如需相關資訊，請參閱 [疑難排解全文檢索索引](troubleshoot-full-text-indexing.md)。  
  
  
