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
ms.openlocfilehash: 64c8fc3b51cbf6c96b25218a3ea53be4eac12f21
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48122398"
---
# <a name="breaking-changes-to-full-text-search"></a>對全文檢索搜尋的重大變更
  本主題描述全文檢索搜尋的重大變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]為根據的應用程式、指令碼或功能。 當您升級時可能會遇到這些問題。 如需詳細資訊，請參閱＜ [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)＞。  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>全文檢索搜尋的突破性變更 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 將於日後提供資訊。  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>全文檢索搜尋的突破性變更 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="collation-changed-for-name-column-in-sysfulltextlanguages"></a>sys.fulltext_languages 中之名稱資料行的定序已變更  
 目錄檢視 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql) 中的語言**名稱**資料行定序，已從資源資料庫的固定定序，變更為針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體選取的預設定序。 當您聯結 [sys.syslanguages &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) 檢視與 **sys.fulltext_languages** 時，此項變更讓您可以比較**名稱**資料行中的值。 例如，您可以查詢預設全文檢索語言與預設資料庫語言不同的所有資料庫。  
  
## <a name="breaking-changes-in-full-text-search-in-sql-server-2008"></a>SQL Server 2008 全文檢索搜尋的重大變更  
 下列重大變更適用於 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 到 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 及更新版本的全文檢索搜尋。  
  
|功能|狀況|SQL Server 2005|SQL Server 2008 及更新版本|  
|-------------|--------------|---------------------|----------------------------------------|  
|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)與使用者定義型別 (Udt)|全文檢索索引鍵是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用者定義型別，例如 `MyType = char(1)`。|傳回的索引鍵具有指派給使用者定義型別的型別。<br /><br /> 在此範例中，這會是**char(1)**。|傳回的索引鍵具有使用者定義型別。 在此範例中，這會是**MyType**。|  
|*top_n_by_rank*參數 (的 CONTAINSTABLE 和[FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) [!INCLUDE[tsql](../includes/tsql-md.md)]陳述式)|*top_n_by_rank*使用 0 做為參數的查詢。|發生失敗並傳回錯誤訊息，該訊息指出您必須使用大於零的值。|成功，傳回零個資料列。|  
|CONTAINSTABLE 和**ItemCount**|在基底資料表發送變更到 MSSearch 之前，從基底資料表中刪除資料列。|CONTAINSTABLE 會傳回準刪除記錄。 **ItemCount**則不會變更。|CONTAINSTABLE 不會傳回任何準刪除記錄。|  
|**ItemCount**|資料表包含 Null 文件或類型資料行。|除了索引文件，文件，都是 null 或具有 null 的型別會算入**ItemCount**值。|只有索引文件中計算**ItemCount**值。|  
|目錄**ItemCount**|具有 NULL 延伸模組的 Blob 資料行。|它會計算**ItemCount**的類別目錄|它不會計入**ItemCount**的目錄。|  
|**UniqueKeyCount**|從目錄中查詢唯一索引鍵計數，例如兩個資料表 (table1 和 table2)，每個資料表都有三個字：word1、word2 和 word3。|**UniqueKeyCount** = 9。 下表摘要列出如何達到這個值：<br /><br /> table1 = 3<br /><br /> table1 全文檢索索引的 EOF = 1<br /><br /> table2 = 3<br /><br /> table2 全文檢索索引的 EOF = 1<br /><br /> 全文檢索目錄 = 1|每個資料表**UniqueKeyCount**是不同的關鍵字 + 1 的數字 (0xFF)。  這並不會將 > 1 份文件中的相同字視為新的唯一索引鍵。<br /><br /> 類別目錄中， **UniqueKeyCount**的總和**UniqueKeyCount**的每個目錄下的資料表。 不同資料表中的相同字會視為唯一索引鍵。 在此案例中，唯一索引鍵計數為 8。|  
|**預先計算陣序規範**伺服器層級選項|FREETEXTTABLE 查詢的效能最佳化。|當此選項設為 1 時，使用指定的 FREETEXTTABLE 查詢*top_n_by_rank*使用預先計算陣序的資料儲存在全文檢索目錄中。|不支援。|  
|[sp_fulltext_pendingchanges](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql)更新索引鍵資料行時|在 2 個資料列之資料表的其中一個資料列上更新全文檢索索引鍵資料行，並執行 sp_fulltext_pendingchanges。|兩個資料列都會出現。|只出現一個資料列。|  
|內嵌函數|具有全文檢索運算子的內嵌函數|傳回錯誤訊息。|傳回相關的資料列。|  
|[sp_fulltext_database](/sql/relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql)|使用 sp_fulltext_database 來啟用或停用全文檢索搜尋。|全文檢索查詢不會傳回任何結果。 如果此資料庫停用全文檢索，則不允許全文檢索作業。|傳回結果給全文檢索查詢，並允許全文檢索作業 (即使此資料庫停用全文檢索)。|  
|地區設定特性的停用字詞|查詢上層語言，例如比利時法文和加拿大法文 inlocale 特性的變化。|查詢 inlocale 特性變化會由其母語的元件 （斷詞工具、 字幹分析器和停用字詞） 處理。 例如，法文 (法國) 元件可用於剖析法文 (比利時)。|您必須明確針對每一個地區設定識別碼 (LCID) 加入停用字詞。 例如，您需要為比利時、加拿大和法國指定 LCID。|  
|同義字字幹處理|使用同義字和字形變化 (字幹)。|同義字會在擴充之後自動進行字幹處理。|如果您想要擴充的字幹形式，您需要明確加入字幹處理的形式。|  
|全文檢索目錄路徑和檔案群組|處理全文檢索目錄。|每一個全文檢索目錄都有實體路徑，而且會屬於某個檔案群組。 它會被視為資料庫檔案。|全文檢索目錄是虛擬物件，而且不屬於任何檔案群組。 全文檢索目錄是參考一組全文檢索索引的邏輯概念。<br /><br /> 注意︰ [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] DDL 陳述式，指定全文檢索目錄正常運作。|  
|[sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)|使用此目錄檢視的路徑、data_space_id 和 file_id。|這些資料行會傳回特定的值。|這些資料行會傳回 NULL，因為此全文檢索目錄不再位於檔案系統中。|  
|[sys.sysfulltextcatalogs](/sql/relational-databases/system-compatibility-views/sys-sysfulltextcatalogs-transact-sql)|使用這個已被取代之系統資料表的路徑資料行。|傳回全文檢索目錄的檔案系統路徑。|傳回 NULL，因為此全文檢索目錄不再位於檔案系統中。|  
|[sp_help_fulltext_catalogs](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql)<br /><br /> [sp_help_fulltext_catalogs_cursor](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql)|使用這些已被取代之預存程序的 PATH 資料行。|傳回全文檢索目錄的檔案系統路徑。|傳回 NULL，因為此全文檢索目錄不再位於檔案系統中。|  
|[sp_help_fulltext_catalog_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql)|使用此預存程序的 sp_help_fulltext_catalog_components。|傳回目前資料庫中所有全文檢索目錄所用的所有元件 (篩選、斷詞工具和通訊協定處理常式) 的清單。|傳回空的資料列。|  
|[DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql)|使用**IsFullTextEnabled**屬性。|**IsFullTextEnabled**設定指出是否啟用全文檢索搜尋指定的資料庫中。|此資料行的值沒有任何作用。 使用者資料庫一定會啟用全文檢索搜尋。|  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋的行為變更](../relational-databases/search/full-text-search.md)   
 [全文檢索搜尋] ((../ relational-databases/search/full-text-search.md)  
  
  
