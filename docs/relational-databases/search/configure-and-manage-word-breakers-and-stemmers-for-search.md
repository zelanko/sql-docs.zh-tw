---
title: 設定及管理搜尋的文字分隔與詞幹分析器
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- full-text search [SQL Server], stemmers
- linguistic analysis [full-text search]
- full-text indexes [SQL Server], linguistic analysis
- full-text search [SQL Server], word breakers
- default full-text language option
- stemmers [full-text search]
- conjugating verbs [full-text search]
- word breakers [full-text search]
ms.assetid: d4bdd16b-a2db-4101-a946-583d1c674229
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 393b6e248962fa496dcdac9fe5def556b766a2bd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "74056265"
---
# <a name="configure--manage-word-breakers--stemmers-for-search-sql-server"></a>設定及管理搜尋的文字分隔與詞幹分析器 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
斷詞工具及字幹分析器，會在所有全文檢索索引資料上執行語文分析。 語言分析會執行下列兩項作業：

-   **尋找文字分界 (斷詞)** 。 「斷詞工具」  會根據語言的語彙規則，判斷文字分界存在的位置，藉以識別個別單字。 每個單字 (也稱為 *Token*) 都會使用壓縮表示來插入全文檢索索引中，以便減少其大小。

-   **結合動詞 (字幹分析)** 。 *「字幹分析器」* (Stemmer) 會根據該語言的規則來產生特定單字的字形變化 (例如，"running"、"ran" 和 "runner" 是 "run" 單字的不同形態)。

## <a name="word-breakers-and-stemmers-are-language-specific"></a>斷詞工具和字幹分析器依語言而異

斷詞工具與字幹分析器是語言特有的工具，而且語言分析的規則會因不同的語言而有所差異。 特定語言的斷詞工具可讓針對該語言產生的詞彙更正確。

您通常不需要採取任何動作，即可使用所有 SQL Server 支援語言所提供的斷詞工具和字幹分析器。

-   如果有語系的斷詞工具，但沒有特定次語言的斷詞工具，則會使用主要語言。 例如，處理加拿大法文時會使用法文文字分隔。
-   如果某種特定語文沒有文字分隔，則會使用中性文字分隔。 使用中性文字分隔時，會以中性字元來中斷文字，例如空白與標點符號。

## <a name="get-the-list-of-supported-languages"></a>取得支援語言的清單

若要查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文檢索搜尋所支援的語言清單，請使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 這份清單中出現的語言，表示該語言有註冊斷詞工具。 
  
```sql
SELECT * FROM sys.fulltext_languages
```

##  <a name="register"></a> 取得已註冊的斷詞工具清單

若要讓全文檢索搜尋使用語言的斷詞工具，必須先註冊斷詞工具。 若是已註冊的斷詞工具，全文檢索索引和查詢作業也可以使用相關聯的語言資源 (字幹分析器、非搜尋字 (停用字詞) 和同義字檔案)。

若要查看已註冊的斷詞工具元件清單，請使用下列陳述式。

```sql
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```

如需其他選項和詳細資訊，請參閱 [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)。
 
## <a name="if-you-add-or-remove-a-word-breaker"></a>如需新增或移除斷詞工具  
如果您加入、移除或更改了斷詞工具，就必須重新整理支援全文檢索索引和查詢的 Microsoft Windows 地區設定識別碼 (LCID) 清單。 如需詳細資訊，請參閱 [檢視或變更已註冊的篩選與斷詞工具](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)。  
  
##  <a name="default"></a> 設定預設全文檢索語言選項  
 若為當地語系化的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式就會將 **default full-text language** 選項設定為伺服器的語言 (如果有相符項目存在的話)。 若 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]為非當地語系化的版本時，則 **或** 選項會是英文。  
  
 建立或更改全文檢索索引時，您可以為每個全文檢索索引資料行指定不同的語言。 如果沒有為資料行指定語言，則預設值會是 [預設全文檢索語言]  組態選項的值。  
  
> [!NOTE]  
>  除非在查詢中指定 LANGUAGE 選項，否則列在單一全文檢索查詢函數子句的所有資料行都必須使用相同的語文。 查詢之全文檢索索引資料行所用的語言會決定要對全文檢索查詢述詞 ([CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)) 與函數 ([CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)) 之引數執行的語言分析。  
  
##  <a name="lang"></a> 選擇索引資料行的語言  
 建立全文檢索索引時，建議您針對每個索引資料行指定語言。 如果沒有為資料行指定語言，就會使用系統預設語言。 資料行的語言會決定哪些斷詞工具和字幹分析器要用於建立該資料行的索引。 此外，資料行的全文檢索查詢會使用該語言的同義字檔案。  
  
 在選擇資料行語言以建立全文檢索索引時，必須考慮一些事項。 這些考量與文字如何 Token 化，然後如何由全文檢索引擎編製索引有關。 如需詳細資訊，請參閱 [選擇建立全文檢索索引時的語言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  
  
若要檢視特定資料行的斷詞工具語言，請執行下列陳述式。
   
```sql 
SELECT language_id AS 'LCID' FROM sys.fulltext_index_columns;
```  

如需其他選項和詳細資訊，請參閱 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)。

##  <a name="tshoot"></a> 疑難排解斷詞逾時錯誤  
 斷詞逾時錯誤可能會在各種情況中發生。 如需這些情況以及如何回應每種情況的資訊，請參閱 [MSSQLSERVER_30053](../errors-events/mssqlserver-30053-database-engine-error.md)。

### <a name="info-about-the-mssqlserver_30053-error"></a>MSSQLSERVER_30053 錯誤的相關資訊
  
|屬性|值|
|-|-|
|產品名稱|SQL Server|  
|事件識別碼|30053|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|FTXT_QUERY_E_WORDBREAKINGTIMEOUT|  
|訊息文字|全文檢索查詢字串的斷詞工作逾時。 如果斷詞工具處理全文檢索查詢字串的時間太長，或伺服器上有大量查詢正在執行，就可能發生這個錯誤。 請嘗試在負載較輕時再執行一次查詢。|  
  
#### <a name="explanation"></a>說明  
 斷詞逾時錯誤可能會在下列情況中發生：  
  
-   查詢語言的斷詞工具設定不正確。例如，其登錄設定不正確。  
  
-   斷詞工具由於特定的查詢字串而無法運作。  
  
-   斷詞工具針對特定的查詢字串傳回太多資料。 資料過多會被系統視為可能的緩衝區滿溢攻擊，因而關閉主控斷詞服務的篩選背景程式處理序 (fdhost.exe)。  
  
-   篩選背景程式處理序的組態不正確。  
  
     最常見的組態問題是密碼逾期或讓篩選背景程式帳戶無法登入的網域原則。  
  
-   伺服器執行個體正在執行非常繁重的查詢工作負載。例如，斷詞工具處理全文檢索查詢字串的時間太長，或伺服器上有大量查詢正在執行。 請注意，這是可能性最低的原因。  
  
#### <a name="user-action"></a>使用者動作  
 請選取適用於逾時可能原因的使用者動作，如下所示：  
  
|可能的原因|使用者動作|  
|--------------------|-----------------|  
|查詢語言的斷詞工具設定不正確。|如果您正在使用協力廠商斷詞工具，可能是作業系統的註冊不正確。 在此情況下，請重新註冊斷詞工具。 如需詳細資訊，請參閱[將搜索所使用的斷詞工具還原為舊版](revert-the-word-breakers-used-by-search-to-the-previous-version.md)。|  
|斷詞工具由於特定的查詢字串而無法運作。|如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援斷詞工具，請連絡 Microsoft 客戶服務及支援中心。|  
|斷詞工具針對特定的查詢字串傳回太多資料。|如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援斷詞工具，請連絡 Microsoft 客戶服務及支援中心。|  
|篩選背景程式處理序的組態不正確。|請確定您使用最新的密碼，而且網域原則並未讓篩選背景程式帳戶無法登入。|  
|伺服器執行個體正在執行非常繁重的查詢工作負載。|請嘗試在負載較輕時再執行一次查詢。|  

##  <a name="impact"></a> 了解更新斷詞工具的影響  
 每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本一般都會包含新的斷詞工具，其語言規則比舊版斷詞工具更好而且更正確。 新斷詞工具的行為可能會與全文檢索索引內斷詞工具的行為稍有不同，而全文檢索索引是從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入。
 
如果全文檢索目錄是在將資料庫升級為目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本時匯入，則這點就很明顯。 全文檢索目錄中全文檢索索引所使用的一種或多種語言現在可能會與新的斷詞工具相關聯。 如需詳細資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
 
## <a name="see-also"></a>另請參閱  
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)    
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   

