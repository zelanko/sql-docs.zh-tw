---
title: 全文檢索搜尋的行為變更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- behavior changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: 573444e8-51bc-4f3d-9813-0037d2e13b8f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 0d3bf42ec031415d16ea45bc8241c85c6d937c35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62813191"
---
# <a name="behavior-changes-to-full-text-search"></a>全文檢索搜尋的行為變更
  本主題描述全文檢索搜尋的行為變更。 行為變更會影響 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 功能的運作或互動方式 (相較於舊版的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])。  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 全文檢索搜尋的行為變更  
 將於日後提供資訊。  
  
## <a name="behavior-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 全文檢索搜尋的行為變更  
 
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 會安裝美式英文 (LCID 1033) 和英式英文 (LCID 2057) 的新版斷詞工具和字幹分析器。 不過，如果您要保留舊版的行為，可以切換到這些元件的舊版。 如需詳細資訊，請參閱[變更用於美式英文與英式英文的斷詞工具](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)。  
  
### <a name="new-word-breakers-and-stemmers-installed"></a>已安裝新的斷詞工具和字幹分析器  
 
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 更新全文檢索搜尋和語意搜尋使用的所有斷詞工具和字幹分析器。 建議您重新擴展現有的全文檢索索引，以取得索引內容和查詢結果的一致性。  
  
1.  目前有英文的新斷詞工具。 如果您必須保留舊版的行為，請參閱[變更用於美式英文與英式英文的斷詞工具](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)。  
  
2.  舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 隨附之丹麥文、波蘭文及土耳其文的協力廠商斷詞工具已取代為 [!INCLUDE[msCoName](../includes/msconame-md.md)] 元件。 預設會啟用新元件。  
  
3.  目前有捷克文和希臘文的新斷詞工具。 舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 全文檢索搜尋不支援這兩種語言。  
  
### <a name="behavior-changes-of-new-word-breakers-and-stemmers"></a>新斷詞工具和字幹分析器的行為變更  
 當您擴展及查詢全文檢索索引時，新元件可能會傳回與舊元件不同的結果。 下表示範英文結果中一些可預期的差異。  
  
 如果您必須保留舊版斷詞工具和字幹分析器的行為，請參閱以下主題：  
  
-   [Change the Word Breaker Used for US English and UK English](../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
-   [將搜索所使用的斷詞工具還原為舊版](../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
 在某些情況下，新元件會傳回「更多」** 結果：  
  
|**詞彙**|**舊版斷詞工具和字幹分析器的結果**|**新版斷詞工具和字幹分析器的結果**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|cat-dog|cat<br /><br /> dog|cat<br /><br /> cat-dog<br /><br /> dog|  
|cat@dog.com|cat<br /><br /> com<br /><br /> dog|cat<br /><br /> cat@dog.com<br /><br /> com<br /><br /> dog|  
|12/11/2011<br /><br /> *(其中詞彙是日期)*|12/11/2011<br /><br /> dd20111211|11<br /><br /> 12<br /><br /> 12/11/2011<br /><br /> 2011<br /><br /> dd20111211|  
  
 在某些情況下，新元件會傳回「類似」** 的結果：  
  
|**詞彙**|**舊版斷詞工具和字幹分析器的結果**|**新版斷詞工具和字幹分析器的結果**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|100$|100$<br /><br /> nn100$|100$<br /><br /> nn100usd|  
|022|022<br /><br /> nn022|022<br /><br /> nn22|  
|10:49AM<br /><br /> *(其中詞彙是時間)*|10:49AM<br /><br /> tt1049|10:49AM<br /><br /> tt24104900|  
  
 在某些情況下，新元件會傳回「較少」** 結果或應用程式可能未預期的結果：  
  
|**詞彙**|**舊版斷詞工具和字幹分析器的結果**|**新版斷詞工具和字幹分析器的結果**|  
|--------------|--------------------------------------------------------|---------------------------------------------------|  
|jěˊÿｑℭžl<br /><br /> *(其中詞彙不是有效的英文字元)*|'jěˊÿｑℭžl'|je yq zl|  
|table's|table's<br /><br /> 資料表|table's|  
|cat-|cat<br /><br /> cat-|cat|  
|v-z (其中 v 和 z 是非搜尋字)**|*（沒有結果）*|v-z|  
|$100 000 USD|$100<br /><br /> 000<br /><br /> nn000<br /><br /> nn100$<br /><br /> usd|$100 000 USD<br /><br /> nn100000usd|  
|beautiful U.S land|beautiful<br /><br /> land<br /><br /> u.s<br /><br /> us|beautiful<br /><br /> land|  
|Mt. Kent and Mt Challenger|challenger<br /><br /> kent<br /><br /> mt<br /><br /> Mt.|mt<br /><br /> kent<br /><br /> challenger|  
  
## <a name="behavior-changes-in-full-text-search-in-sql-server-2008"></a>SQL Server 2008 中全文檢索搜尋的行為變更  
 在[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]和更新的版本中，全文檢索引擎會以資料庫服務的形式整合至關係資料庫中，成為伺服器查詢和儲存引擎基礎結構的一部分。 新的全文檢索搜尋架構可達成下列目標：  
  
-   整合式儲存與管理-全文檢索搜尋現在直接與的固有儲存體和管理功能整合[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，而 MSFTESQL 服務已不存在。  
  
    -   全文檢索索引會儲存在資料庫檔案群組內部，而非儲存在檔案系統中。 資料庫的管理作業 (例如建立備份) 會自動影響其全文檢索索引。  
  
    -   全文檢索目錄現在是不屬於任何檔案群組的虛擬物件。它是參考一組全文檢索索引的邏輯概念。 因此，許多目錄管理功能都已經被取代，而且這項取代已經針對某些功能建立重大變更。 如需詳細資訊，請參閱[SQL Server 2014 中的已淘汰資料庫引擎功能](deprecated-database-engine-features-in-sql-server-2016.md)和[全文檢索搜尋的重大變更](breaking-changes-to-full-text-search.md)。  
  
        > [!NOTE]  
        >  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)][!INCLUDE[tsql](../includes/tsql-md.md)]指定全文檢索目錄正常運作的 DDL 語句。  
  
-   整合式查詢處理-新的全文檢索搜尋查詢處理器是資料庫引擎的一部分，而且已與 SQL Server 查詢處理器完全整合。 這表示，查詢最佳化工具會辨識全文檢索查詢述詞並且盡可能有效率地自動執行它們。  
  
-   增強式管理和疑難排解-整合的全文檢索搜尋提供的工具可協助您分析搜尋結構，例如全文檢索索引、給定斷詞工具的輸出、停用字詞設定等等。  
  
-   停用字詞和停用字詞表已經取代了非搜尋字和非搜尋字檔案。 停用字詞表是一個資料庫物件，可加快停用字詞管理工作的速度並且改善不同伺服器執行個體與環境之間的完整性。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
-   
  [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和更新的版本包含 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 中許多語言的新斷詞工具。 只有英文、韓文、泰文和中文 (所有形式) 的斷詞工具維持原狀。 對於其他語言，如果全文檢索目錄是在[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]資料庫升級為[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]或更新版本時匯入，則全文檢索目錄中的全文檢索索引所使用的一或多個語言現在可能會與新的斷詞工具相關聯，其行為可能與匯入的斷詞工具有些許不同。 如需有關如何確保查詢與全文檢索索引內容之間一致性的詳細資訊，請參閱[升級全文檢索搜尋](../relational-databases/search/upgrade-full-text-search.md)。  
  
-   加入了新的 FDHOST Launcher (MSSQLFDLauncher) 服務。 如需詳細資訊，請參閱[開始使用全文檢索搜尋](../relational-databases/search/get-started-with-full-text-search.md)。  
  
-   全文檢索索引的運作方式與[FILESTREAM](../relational-databases/blob/filestream-sql-server.md)資料行相同，方法與資料`varbinary(max)`行相同。 FILESTREAM 資料表必須有一個資料行包含每一個 FILESTREAM BLOB 的副檔名。 如需詳細資訊，請參閱[使用全文檢索搜尋進行查詢](../relational-databases/search/query-with-full-text-search.md)、[設定及管理搜尋的篩選](../relational-databases/search/configure-and-manage-filters-for-search.md)，以及[fulltext_document_types &#40;transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql)。  
  
     全文檢索引擎會針對 FILESTREAM BLOB 的內容建立索引。 為檔案 (如影像) 建立索引可能不會很實用。 當更新 FILESTREAM BLOB 時，會為它重新建立索引。  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋](../relational-databases/search/full-text-search.md)   
 [全文檢索搜尋回溯相容性](../../2014/database-engine/full-text-search-backward-compatibility.md)   
 [升級全文檢索搜尋](../relational-databases/search/upgrade-full-text-search.md)   
 [全文檢索搜尋使用者入門](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
