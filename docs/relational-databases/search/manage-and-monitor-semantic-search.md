---
title: "管理及監視語意搜尋 | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6749d7f7db6e6e76cd940c166180a7ccd206aaf9
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="manage-and-monitor-semantic-search"></a>管理及監視語意搜尋
  描述語意索引的程序，以及與管理及監視索引相關的工作。  
  
##  <a name="HowToMonitorStatus"></a>檢查語意索引的狀態  
### <a name="is-the-first-phase-of-semantic-indexing-complete"></a>語意索引的第一個階段是否已完成？
 查詢動態管理檢視 [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md) **status** 和 **status_description** 資料行。  
  
 索引的第一個階段包括擴展全文檢索關鍵字索引和語意主要片語索引，以及擷取文件相似度資料。  
  
```tsql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="is-the-second-phase-of-semantic-indexing-complete"></a>語意索引的第二個階段是否已完成？
 查詢動態管理檢視 [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md) **status** 和 **status_description** 資料行。  
  
 索引的第二個階段包括擴展語意文件相似度索引。  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a>檢查語意索引的大小  
### <a name="what-is-the-logical-size-of-a-semantic-key-phrase-index-or-a-semantic-document-similarity-index"></a>語意主要片語索引或語意文件相似度索引的邏輯大小為何？
 查詢動態管理檢視 [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)。  
  
 邏輯大小會以索引頁面的數目表示。  
  
```tsql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="what-is-the-total-size-of-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>全文檢索目錄的全文檢索索引與語意索引的總大小為何？  
 查詢 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md) 中繼資料函數的 **IndexSize** 屬性。  
  
```tsql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
### <a name="how-many-items-are-indexed-in-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>全文檢索目錄的全文檢索索引和語意索引中建立了多少項目的索引？  
 查詢 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md) 中繼資料函數的 **ItemCount** 屬性。  
  
```tsql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a>強制擴展語意索引  
 您可以強制全文檢索索引和語意索引的母體擴展，其方式是使用 START/STOP/PAUSE 或 RESUME POPULATION 子句搭配全文檢索索引所描述的相同語法和行為。 如需詳細資訊，請參閱 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md) 和[擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
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
  
##  <a name="HowToDisableIndexing"></a>停用或重新啟用語意索引  
 您可以啟用或停用全文檢索索引或語意索引，其方式是使用 ENABLE/DISABLE 子句搭配全文檢索索引所描述的相同語法與行為。 如需詳細資訊，請參閱 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)。  
  
 當語意索引已停用且暫停時，語意資料的查詢會持續順利運作，並傳回之前的索引資料。 此行為與全文檢索搜尋的行為不一致。  
  
```tsql  
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
  
##  <a name="SemanticIndexing"></a>關於語意索引的階段  
 語意搜尋會針對其啟用所在的每一個資料行，建立兩種資料的索引：  
  
1.  **主要片語**  
  
2.  **文件相似度**  
  
 語意索引會連同全文檢索索引發生在兩個階段：  
  
1.  **階段 1**. 全文檢索關鍵字索引和語意主要片語索引會以平行方式同時擴展。 此時也會擷取建立文件相似度索引所需的資料。  
  
2.  **階段 2**： 然後會擴展語意文件相似度索引。 此索引取決於上一個階段中已擴展的兩個索引。  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a>問題：未擴展語意索引  
### <a name="are-the-associated-full-text-indexes-populated"></a>是否已擴展關聯的全文檢索索引？  
 因為語意索引會依據全文檢索索引，所以只有當關聯的全文檢索索引已擴展時，才會擴展語意索引。  
  
### <a name="are-full-text-search-and-semantic-search-properly-installed-and-configured"></a>是否已正確安裝及設定全文檢索搜尋及語意搜尋？  
 如需詳細資訊，請參閱 [安裝及設定語意搜尋](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
### <a name="is-the-fdhost-service-not-available-or-is-there-another-condition-that-would-cause-full-text-indexing-to-fail"></a>FDHOST 服務是否無法使用，或是有另一個狀況導致全文檢索索引失敗？  
 如需相關資訊，請參閱 [疑難排解全文檢索索引](../../relational-databases/search/troubleshoot-full-text-indexing.md)。  
  
  

