---
title: 全文檢索和語意搜尋動態管理檢視函數 |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dynamic management objects [SQL Server], full-text search
- full-text search [SQL Server], dynamic management views
ms.assetid: 199dbd5a-29f6-4ef0-8e65-86e32c0aaa3a
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b8a3c8db692e5ac0755291ff7116868c23bf58cd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="full-text-and-semantic-search-dynamic-management-views---functions"></a>全文檢索和語意搜尋動態管理檢視函式
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本節包含與全文檢索搜尋和語意搜尋相關的下列動態管理檢視和函數。  
  
## <a name="full-text-search-dynamic-management-views-and-functions"></a>全文檢索搜尋動態管理檢視和函數  
 [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
 傳回全文檢索目錄的相關資訊，這些目錄正在伺服器上進行某個母體擴展活動。  
  
 [sys.dm_fts_fdhosts](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
 傳回伺服器執行個體上篩選背景程式主機之目前活動的相關資訊。  
  
 [sys.dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
 針對指定的資料表傳回全文檢索索引之內容的相關資訊。  
  
 [sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
 針對指定的資料表傳回全文檢索索引之文件層級內容的相關資訊。 給定的關鍵字可能會出現在許多份文件中。  
  
 [sys.dm_fts_index_keywords_by_property](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
 傳回給定資料表之全文檢索索引中的所有屬性相關內容。 這包括與該全文檢索索引相關聯的搜尋屬性清單所註冊之任何屬性的一切所屬資料。  
  
 sys.dm_fts_index_keywords_position_by_document  
 傳回文件中的關鍵字的位置。  
  
 [sys.dm_fts_index_population](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
 傳回有關目前進行中之全文檢索索引母體擴展的資訊。  
  
 [sys.dm_fts_memory_buffers](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
 傳回屬於特定記憶體集區之記憶體緩衝區的相關資訊，這些緩衝區會做為全文檢索搜耙的一部分或全文檢索搜耙範圍使用。  
  
 [sys.dm_fts_memory_pools](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
 針對全文檢索搜耙或全文檢索搜耙範圍，傳回可供「全文檢索收集程式」元件使用之共用記憶體集區的相關資訊。  
  
 [sys.dm_fts_outstanding_batches](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
 傳回有關每個全文檢索索引批次的資訊。  
  
 [sys.dm_fts_parser](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
 傳回將給定斷詞工具、同義字和停用字詞表組合套用至查詢字串輸入之後的最終 Token 化結果。 此輸出就相當於將指定之給定查詢字串發給全文檢索引擎的輸出。  
  
 [sys.dm_fts_population_ranges](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
 傳回與目前正在進行的全文檢索索引擴展相關之特定範圍的資訊。  
  
## <a name="semantic-search-dynamic-management-views-and-functions"></a>語意搜尋動態管理檢視和函數  
 [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
 傳回一個資料列，其中包含每個有相關語意索引的資料表中每個相似度索引之文件相似度索引母體擴展的狀態資訊。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
