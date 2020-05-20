---
title: 全文檢索搜尋和語義搜尋預存程式（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], stored procedures
- full-text search [SQL Server], stored procedures
- full-text catalogs [SQL Server], stored procedures
- system stored procedures [SQL Server], full-text search
ms.assetid: 0d185a16-2b16-4958-884f-efe675e2e551
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9bfb3a2309b2e7d2d35f1b8f68c5caa9e9ac66c2
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820738"
---
# <a name="full-text-search-and-semantic-search-stored-procedures-transact-sql"></a>全文檢索搜尋和語意搜尋預存程序 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援下列用來執行和查詢全文檢索索引和語義索引的系統預存程式。  
  
## <a name="full-text-search-stored-procedures"></a>全文檢索搜尋預存程序  
 [sp_fulltext_catalog](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)  
 建立和卸除全文檢索目錄，以及啟動和停止目錄的索引動作。 每個資料庫都可以建立多個全文檢索目錄。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]請改用[CREATE 全文檢索目錄](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)、 [ALTER 全文檢索目錄](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)和[DROP 全文](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)檢索目錄。  
  
 [sp_fulltext_column](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)  
 指定資料表的特定資料行是否參與全文檢索索引。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[ALTER 全文檢索索引](../../t-sql/statements/alter-fulltext-index-transact-sql.md)。  
  
 [sp_fulltext_database](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)  
 對於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中的全文檢索目錄沒有任何影響，而且是為了回溯相容性才提供支援。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)  
 傳回檔識別碼（**DocId**s）和全文檢索索引鍵值之間的對應。  
  
 [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 從對應至 LCID 的已更新同義字檔案中剖析並載入資料，並且導致重新編譯使用此同義字的全文檢索查詢。  
  
 [sp_fulltext_pendingchanges](../../relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql.md)  
 針對使用變更追蹤的指定資料表，傳回未處理的變更 (例如，暫止插入、更新和刪除)。  
  
 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
 變更 SQL Server 全文檢索搜尋的伺服器屬性。  
  
 [sp_fulltext_table](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)  
 標示或取消標示全文檢索索引的資料表。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]請改用[CREATE 全文檢索索引](../../t-sql/statements/create-fulltext-index-transact-sql.md)、 [ALTER 全文檢索索引](../../t-sql/statements/alter-fulltext-index-transact-sql.md)和[DROP 全文檢索索引](../../t-sql/statements/drop-fulltext-index-transact-sql.md)。  
  
 [sp_help_fulltext_catalog_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql.md)  
 傳回目前資料庫中所有全文檢索目錄所用的所有元件 (篩選、斷詞工具和通訊協定處理常式) 的清單。  
  
 [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 [sp_help_fulltext_catalogs](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
 傳回指定全文檢索目錄之全文檢索索引資料表的識別碼、名稱、根目錄、狀態和數目。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[sys.databases fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)目錄檢視。  
  
 [sp_help_fulltext_catalogs_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)  
 利用資料指標來傳回指定全文檢索目錄之全文檢索索引資料表的識別碼、名稱、根目錄、狀態和數目。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[sys.databases fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)目錄檢視。  
  
 [sp_help_fulltext_columns](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)  
 傳回指定給全文檢索索引的資料行。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[sys.databases fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)目錄檢視。  
  
 [sp_help_fulltext_columns_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)  
 利用資料指標來傳回指定給全文檢索索引的資料行。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[sys.databases fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)目錄檢視。  
  
 [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
 傳回有關已註冊之斷詞工具、篩選和通訊協定處理常式的詳細資訊，以及資料庫識別碼的清單和已使用指定之元件的全文檢索目錄。  
  
 [sp_help_fulltext_tables](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)  
 傳回登錄了全文檢索索引的資料表清單。  
  
 [sp_help_fulltext_tables_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)  
 傳回登錄了全文檢索索引的資料表清單。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[sys.databases fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)目錄檢視。  
  
## <a name="semantic-search-stored-procedures"></a>語意搜尋預存程序  
 [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md)  
 在目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中註冊已預先擴展的語義語言統計資料庫。  
  
 [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md)  
 從目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中取消註冊現有的語義語言統計資料庫，並且刪除任何相關聯的中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的全文檢索搜尋和語義搜尋目錄檢視](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)   
 [全文檢索搜尋和語義搜尋動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)  
  
  
