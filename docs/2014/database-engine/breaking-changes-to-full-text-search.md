---
title: 全文檢索搜尋的重大變更 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- full-text catalogs [SQL Server], breaking changes
- breaking changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: c55a6748-e5d9-4fdb-9a1f-714475a419c5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 45b13c29af6a9c5e82533a4b66213d1cb1b9dd15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62787756"
---
# <a name="breaking-changes-to-full-text-search"></a>對全文檢索搜尋的重大變更
  本主題描述全文檢索搜尋的重大變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]為根據的應用程式、指令碼或功能。 當您升級時可能會遇到這些問題。 如需詳細資訊，請參閱＜ [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)＞。  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 全文檢索搜尋的重大變更  
 將於日後提供資訊。  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 全文檢索搜尋的重大變更  
  
### <a name="collation-changed-for-name-column-in-sysfulltext_languages"></a>sys.fulltext_languages 中之名稱資料行的定序已變更  
 目錄檢視 **sys.fulltext_languages &#40;Transact-SQL&#41;** 中的語言[名稱](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)資料行定序，已從資源資料庫的固定定序，變更為針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體選取的預設定序。 當您聯結 **sys.syslanguages &#40;Transact-SQL&#41;** 檢視與 [sys.fulltext_languages](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) 時，此項變更讓您可以比較**名稱**資料行中的值。 例如，您可以查詢預設全文檢索語言與預設資料庫語言不同的所有資料庫。  
  
## <a name="breaking-changes-in-full-text-search-in-sql-server-2008"></a>SQL Server 2008 全文檢索搜尋的重大變更  
 下列重大變更適用於 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 到 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 及更新版本的全文檢索搜尋。  
  
|功能|狀況|SQL Server 2005|SQL Server 2008 及更新版本|  
|-------------|--------------|---------------------|----------------------------------------|  
|具有使用者定義類型（Udt）的[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|全文檢索索引鍵是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用者定義型別，例如 `MyType = char(1)`。|傳回的索引鍵具有指派給使用者定義型別的型別。<br /><br /> 在此範例中，這會是**char （1）**。|傳回的索引鍵具有使用者定義型別。 在此範例中，這會是**MyType**。|  
|*top_n_by_rank*參數（CONTAINSTABLE 和[FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) [!INCLUDE[tsql](../includes/tsql-md.md)]語句的）|*top_n_by_rank*使用0做為參數的查詢。|發生失敗並傳回錯誤訊息，該訊息指出您必須使用大於零的值。|成功，傳回零個資料列。|  
|CONTAINSTABLE 和**ItemCount**|在基底資料表發送變更到 MSSearch 之前，從基底資料表中刪除資料列。|CONTAINSTABLE 會傳回準刪除記錄。 **ItemCount**不會變更。|CONTAINSTABLE 不會傳回任何準刪除記錄。|  
|**ItemCount**|資料表包含 Null 文件或類型資料行。|除了已編制索引的檔之外，也會在**ItemCount**值中計算 null 或具有 null 類型的檔。|只有已編制索引的檔會計算在**ItemCount**值中。|  
|目錄**ItemCount**|具有 NULL 延伸模組的 Blob 資料行。|它會在目錄的**ItemCount**中計算|它不會在目錄**ItemCount**中計算。|  
|**UniqueKeyCount**|從目錄中查詢唯一索引鍵計數，例如兩個資料表 (table1 和 table2)，每個資料表都有三個字：word1、word2 和 word3。|**UniqueKeyCount** = 9。 下表摘要列出如何達到這個值：<br /><br /> table1 = 3<br /><br /> table1 全文檢索索引的 EOF = 1<br /><br /> table2 = 3<br /><br /> table2 全文檢索索引的 EOF = 1<br /><br /> 全文檢索目錄 = 1|針對每個資料表， **UniqueKeyCount**是相異關鍵字 + 1 （0xff）的數目。  這不會將 > 1 檔中的相同單字視為新的唯一索引鍵。<br /><br /> 針對目錄， **UniqueKeyCount**是目錄下每個資料表的**UniqueKeyCount**總和。 不同資料表中的相同字會視為唯一索引鍵。 在此案例中，唯一索引鍵計數為 8。|  
|**預先計算次序**伺服器層級選項|FREETEXTTABLE 查詢的效能最佳化。|當選項設定為1時，使用*top_n_by_rank*所指定的 FREETEXTTABLE 查詢會使用儲存在全文檢索目錄中的預先計算 rank 資料。|不支援。|  
|更新索引鍵資料行時[sp_fulltext_pendingchanges](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql)|在 2 個資料列之資料表的其中一個資料列上更新全文檢索索引鍵資料行，並執行 sp_fulltext_pendingchanges。|兩個資料列都會出現。|只出現一個資料列。|  
|內嵌函數|具有全文檢索運算子的內嵌函數|傳回錯誤訊息。|傳回相關的資料列。|  
|[sp_fulltext_database](/sql/relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql)|使用 sp_fulltext_database 來啟用或停用全文檢索搜尋。|全文檢索查詢不會傳回任何結果。 如果此資料庫停用全文檢索，則不允許全文檢索作業。|傳回結果給全文檢索查詢，並允許全文檢索作業 (即使此資料庫停用全文檢索)。|  
|地區設定特性的停用字詞|查詢 inlocale 特定的父語言變體，例如比利時法文和加拿大法文。|查詢 inlocale 特定的變數會由其父語言的元件（斷詞工具、字幹分析器和停用字詞）處理。 例如，法文 (法國) 元件可用於剖析法文 (比利時)。|您必須明確針對每一個地區設定識別碼 (LCID) 加入停用字詞。 例如，您需要為比利時、加拿大和法國指定 LCID。|  
|同義字字幹處理|使用同義字和字形變化 (字幹)。|同義字會在擴充之後自動進行字幹處理。|如果您想要擴充的字幹形式，您需要明確加入字幹處理的形式。|  
|全文檢索目錄路徑和檔案群組|處理全文檢索目錄。|每一個全文檢索目錄都有實體路徑，而且會屬於某個檔案群組。 它會被視為資料庫檔案。|全文檢索目錄是虛擬物件，而且不屬於任何檔案群組。 全文檢索目錄是參考一組全文檢索索引的邏輯概念。<br /><br /> 注意： [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)]指定全文檢索目錄的 DDL 語句會正常運作。|  
|[sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)|使用此目錄檢視的路徑、data_space_id 和 file_id。|這些資料行會傳回特定的值。|這些資料行會傳回 NULL，因為此全文檢索目錄不再位於檔案系統中。|  
|[sys.sysfulltextcatalogs](/sql/relational-databases/system-compatibility-views/sys-sysfulltextcatalogs-transact-sql)|使用這個已被取代之系統資料表的路徑資料行。|傳回全文檢索目錄的檔案系統路徑。|傳回 NULL，因為此全文檢索目錄不再位於檔案系統中。|  
|[sp_help_fulltext_catalogs](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql)<br /><br /> [sp_help_fulltext_catalogs_cursor](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql)|使用這些已被取代之預存程序的 PATH 資料行。|傳回全文檢索目錄的檔案系統路徑。|傳回 NULL，因為此全文檢索目錄不再位於檔案系統中。|  
|[sp_help_fulltext_catalog_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql)|使用此預存程序的 sp_help_fulltext_catalog_components。|傳回目前資料庫中所有全文檢索目錄所用的所有元件 (篩選、斷詞工具和通訊協定處理常式) 的清單。|傳回空的資料列。|  
|[DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql)|使用**IsFullTextEnabled**屬性。|**IsFullTextEnabled**設定會指出是否在指定的資料庫中啟用全文檢索搜尋。|此資料行的值沒有任何作用。 使用者資料庫一定會啟用全文檢索搜尋。|  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋的行為變更](../relational-databases/search/full-text-search.md)   
 [全文檢索搜尋](../relational-databases/search/full-text-search.md)  
  
  
