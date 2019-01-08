---
title: 語意搜尋 DDL、函式、預存程序及檢視 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76ced95f53b50c0fc0402051cff35329d39ce9f0
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530735"
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>語意搜尋 DDL、函數、預存程序及檢視
  列出支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中統計語意搜尋的 Transact-SQL 陳述式和資料庫物件。  
  
 如需支援全文檢索搜尋之陳述式和資料庫物件的清單，請參閱 [全文檢索搜尋 DDL、函數、預存程序與檢視](../views/views.md)。  
  
##  <a name="ddl"></a> Transact-SQL 資料定義語言 (DDL) 陳述式  
  
|Object|[詳細資訊]|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)|[在資料表和資料行上啟用語意搜尋](enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)|[在資料表和資料行上啟用語意搜尋](enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="func"></a> 系統函數  
  
|Object|[詳細資訊]|  
|------------|----------------------|  
|[semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql)|[使用語意搜尋在文件中尋找主要片語](find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)|[使用語意搜尋尋找相似及相關的文件](find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)|[使用語意搜尋尋找相似及相關的文件](find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="meta"></a> 系統中繼資料函數  
  
|Object|[詳細資訊]|  
|------------|----------------------|  
|[COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)|[在資料表和資料行上啟用語意搜尋](enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql)|[在資料表和資料行上啟用語意搜尋](enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|[管理及監視語意搜尋](manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)|[管理及監視語意搜尋](manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|[在資料表和資料行上啟用語意搜尋](enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|[安裝及設定語意搜尋](install-and-configure-semantic-search.md)|  
  
##  <a name="sproc"></a> 系統預存程序  
  
|Object|[詳細資訊]|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql)|[安裝及設定語意搜尋](install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql)|[安裝及設定語意搜尋](install-and-configure-semantic-search.md)|  
  
##  <a name="cv"></a> 系統檢視表 - 目錄檢視  
  
|Object|[詳細資訊]|  
|------------|----------------------|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|[管理及監視語意搜尋](manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql)|[安裝及設定語意搜尋](install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)|[安裝及設定語意搜尋](install-and-configure-semantic-search.md)|  
  
##  <a name="dmv"></a> 系統檢視表 - 動態管理檢視  
  
|Object|[詳細資訊]|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)|[管理及監視語意搜尋](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|[管理及監視語意搜尋](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)|[管理及監視語意搜尋](manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>另請參閱  
 [管理及監視語意搜尋](manage-and-monitor-semantic-search.md)  
  
  
