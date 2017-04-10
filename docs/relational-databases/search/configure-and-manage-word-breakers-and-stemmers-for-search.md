---
title: "設定及管理搜尋的斷詞工具與字幹分析器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "語言 [全文檢索搜尋]"
  - "全文檢索搜尋 [SQL Server], 詞幹分析器"
  - "語言分析 [全文檢索搜尋]"
  - "全文檢索索引 [SQL Server], 語言分析"
  - "全文檢索搜尋 [SQL Server], 斷詞工具"
  - "預設全文檢索語言選項"
  - "字幹分析器 [全文檢索搜尋]"
  - "動詞變化 [全文檢索搜尋]"
  - "斷詞工具 [全文檢索搜尋]"
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
caps.latest.revision: 89
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 88
---
# 設定及管理搜尋的斷詞工具與字幹分析器
  斷詞工具及字幹分析器，會在所有全文檢索索引資料上執行語文分析。 語文分析包括找出文字分界 (斷詞) 以及動詞變化 (字根處理)。 斷詞工具與字幹分析器是語言特有的工具，而且語言分析的規則會因不同的語言而有所差異。 對於給定的語言而言，*「斷詞工具」*(Word Breaker) 會根據語言的語彙規則，判斷文字分界存在的位置，藉以識別個別單字。 每個單字 (也稱為 *Token*) 都會使用壓縮表示來插入全文檢索索引中，以便減少其大小。 *「字幹分析器」*(Stemmer) 會根據該語言的規則來產生特定單字的字形變化 (例如，"running"、"ran" 和 "runner" 是 "run" 單字的不同形態)。  
  
 使用語言特有的斷詞工具會使得針對該語言產生的詞彙更正確。 如果有語系的斷詞工具，但沒有特定次語言的斷詞工具，則會使用主要語言。 例如，處理加拿大法文時會使用法文文字分隔。 如果某種特定語文沒有文字分隔，則會使用中性文字分隔。 使用中性文字分隔時，會以中性字元來中斷文字，例如空白與標點符號。  
  
##  <a name="register"></a> 註冊斷詞工具  
 若要使用某種語言的斷詞工具，您必須註冊它們。 對於已註冊的斷詞工具而言，相關聯的語言資源 (字幹分析器、非搜尋字 (停用字詞) 和同義字檔案) 也會成為可供全文檢索索引和查詢作業使用。 若要檢視目前已向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊之斷詞工具的語言清單，請使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
 SELECT * FROM sys.fulltext_languages  
  
 如果您加入、移除或更改了斷詞工具，就必須重新整理支援全文檢索索引和查詢的 Microsoft Windows 地區設定識別碼 (LCID) 清單。 如需詳細資訊，請參閱 [View or Change Registered Filters and Word Breakers](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)。  
  
##  <a name="default"></a> 設定預設全文檢索語言選項  
 若為當地語系化的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式就會將 [預設全文檢索語言] 選項設定為伺服器的語言 (如果有相符項目存在的話)。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為非當地語系化的版本時，則 [預設全文檢索語言] 選項會是英文。  
  
 建立或更改全文檢索索引時，您可以為每個全文檢索索引資料行指定不同的語言。 如果沒有為資料行指定語言，則預設值會是 [預設全文檢索語言] 組態選項的值。  
  
> [!NOTE]  
>  除非在查詢中指定 LANGUAGE 選項，否則列在單一全文檢索查詢函數子句的所有資料行都必須使用相同的語文。 查詢之全文檢索索引資料行所用的語言會決定要對全文檢索查詢述詞 ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) 與函數 ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)) 之引數執行的語言分析。  
  
##  <a name="lang"></a> 選擇索引資料行的語言  
 建立全文檢索索引時，建議您針對每個索引資料行指定語言。 如果沒有為資料行指定語言，就會使用系統預設語言。 資料行的語言會決定哪些斷詞工具和字幹分析器要用於建立該資料行的索引。 此外，資料行的全文檢索查詢會使用該語言的同義字檔案。  
  
 在選擇資料行語言以建立全文檢索索引時，必須考慮一些事項。 這些考量與文字如何 Token 化，然後如何由全文檢索引擎編製索引有關。 如需詳細資訊，請參閱[選擇建立全文檢索索引時的語言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  
  
 **檢視資料行的斷詞工具語言**  
  
-   [管理全文檢索索引](../Topic/Manage%20Full-Text%20Indexes.md)  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
    ```  
    SELECT 'language_id' AS "LCID" FROM sys.fulltext_index_columns;  
    ```  
  
##  <a name="info"></a> 取得斷詞工具的相關資訊  
 **檢視斷詞工具、同義字和停用字詞表組合的 Token 化結果**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).  
  
 **傳回已註冊斷詞工具的相關資訊**  
  
-   [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
  
##  <a name="tshoot"></a> 疑難排解斷詞逾時錯誤  
 斷詞逾時錯誤可能會在各種情況中發生。 如需這些情況以及每種情況中之回應方式的相關資訊，請參閱 [MSSQLSERVER_30053](../Topic/MSSQLSERVER_30053.md)。  
  
##  <a name="impact"></a> 了解新斷詞工具的影響  
 每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本一般都會包含新的斷詞工具，其語言規則比舊版斷詞工具更好而且更正確。 新斷詞工具的行為可能會與全文檢索索引內斷詞工具的行為稍有不同，而全文檢索索引是從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入。 如果全文檢索目錄是在將資料庫升級為目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本時匯入，則這點就很明顯。 全文檢索目錄中全文檢索索引所使用的一種或多種語言現在可能會與新的斷詞工具相關聯。 如需詳細資訊，請參閱[升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
 如需所有斷詞工具的完整清單，請參閱 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。  
  
## 另請參閱  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)   
 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)  
  
  