---
title: 全文檢索搜尋 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server]
ms.assetid: a0ce315d-f96d-4e5d-b4eb-ff76811cab75
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 560761383a06bf9e3b319546011d58c7c1bdecb4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788640"
---
# <a name="full-text-search"></a>全文檢索搜尋
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中的全文檢索搜尋可讓使用者和應用程式針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中以字元為主的資料，執行全文檢索查詢。 資料庫管理員必須先在資料表上建立全文檢索索引，才能在此資料表上執行全文檢索查詢。 全文檢索索引包括資料表中一或多個以字元為基礎的資料行。 這些資料行可以具有下列任何資料類型：`char`、`varchar`、`nchar`、`nvarchar`、`text`、`ntext`、`image`、`xml` 或 `varbinary(max)` 和 FILESTREAM。 每個全文檢索索引都會為資料表中的一個或多個資料行建立索引，而且每個資料行都可以使用特定的語言。  
  
 全文檢索查詢會根據特定語言的規則 (例如英文或日文) 在單字與片語上運作，藉以針對全文檢索索引中的文字資料執行語言搜尋。 全文檢索查詢可以包含簡單的單字和片語，或者單字或片語的多種形式。 全文檢索查詢會傳回至少包含一個符合項目 (也稱為 *「叫用」*(Hit)) 的任何文件。 如果目標文件包含全文檢索查詢中指定的所有詞彙，而且符合其他搜尋條件 (例如相符詞彙之間的距離)，就會出現符合項目。  
  
> [!NOTE]  
>  全文檢索搜尋是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine 的選擇性元件。 如需詳細資訊，請參閱 <<c0> [ 安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)。  
  
##  <a name="benefits"></a> 我可以使用全文檢索搜尋來做什麼？  
 全文檢索搜尋是適用於各種商務案例，例如 e-企業-搜尋網站上的項目在法律資料儲存機制; 案例律師事務所搜尋公司的法律或人力資源部門符合工作描述與預存的履歷表。 不論商務案例為何，全文檢索搜尋的基本管理和開發工作都是相同的。 不過，在給定的商務案例中，可能會調整全文檢索索引和查詢來符合商務目標。 例如，對於電子商務而言，發揮最佳效能可能會比排序結果等級、重新叫用精確度 (全文檢索查詢實際傳回的現有相符項目數) 或支援多國語言更重要。 對於律師事務所而言，傳回每個可能的叫用 (資訊的 *「重新叫用總數」* (Total Recall)) 可能是最重要的考量。  
  
 [本主題內容](#top)  
  
###  <a name="queries"></a> 全文檢索搜尋查詢  
 將資料行加入至全文檢索索引之後，使用者和應用程式即可針對資料行中的文字執行全文檢索查詢。 這些查詢可以搜尋下列任何項目：  
  
-   一或多個特定的單字或片語 (*「不可分割的詞彙」*(Simple Term))  
  
-   以指定之文字開頭的單字或片語 (*「前置詞彙」*(Prefix Term))  
  
-   特定單字的字形變化 (*「衍生詞彙」*(Generation Term))  
  
-   靠近另一個單字或片語的單字或片語 (*「相近詞彙」*(Proximity Term))  
  
-   特定單字的同義字變化 (*「同義字」*(Thesaurus))  
  
-   使用加權值的單字或片語 (*「加權詞彙」*(Weighted Term))  
  
 全文檢索查詢不區分大小寫。 例如，搜尋 "Aluminum" 或 "aluminum" 都會傳回相同的結果。  
  
 全文檢索查詢會使用一小組 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 述詞 (CONTAINS 和 FREETEXT) 與函數 (CONTAINSTABLE 和 FREETEXTTABLE)。 不過，給定商務案例的搜尋目標會影響全文檢索查詢的結構。 例如：  
  
-   電子商務 - 搜尋網站上的產品：  
  
    ```  
    SELECT product_id   
    FROM products   
    WHERE CONTAINS(product_description, "Snap Happy 100EZ"  
        OR FORMSOF(THESAURUS,'Snap Happy')  
        OR '100EZ')   
    AND product_cost < 200 ;  
    ```  
  
-   人員招募案例 - 搜尋具有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用經驗的工作應徵者：  
  
    ```  
    SELECT candidate_name,SSN   
    FROM candidates   
    WHERE CONTAINS(candidate_resume,"SQL Server") AND candidate_division = 'DBA';  
    ```  
  
 如需詳細資訊，請參閱 [使用全文檢索搜尋查詢](query-with-full-text-search.md)。  
  
 [本主題內容](#top)  
  
###  <a name="like"></a> 比較 LIKE 與全文檢索搜尋  
 相較於全文檢索搜尋， [LIKE](/sql/t-sql/language-elements/like-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 述詞只能針對字元模式運作。 您也無法使用 LIKE 述詞來查詢格式化的二進位資料。 此外，針對大量非結構化文字資料執行 LIKE 查詢的速度會比針對相同資料執行對等全文檢索查詢的速度要慢很多。 對於數百萬列的資料，使用 LIKE 查詢時可能要好幾分鐘才能傳回搜尋結果，但是使用全文檢索查詢時可能只要幾秒鐘的時間 (視傳回的資料列數目而定)。  
  
 [本主題內容](#top)  
  
##  <a name="architecture"></a> 全文檢索搜尋元件和架構  
 全文檢索搜尋架構是由下列處理序所組成：  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 處理序 (sqlservr.exe)。  
  
-   篩選背景程式主機處理序 (fdhost.exe)。  
  
     基於安全性理由，篩選是由稱為篩選背景程式主機的個別處理序載入。 FDHOST 啟動器服務 (MSSQLFDLauncher) 會建立 fdhost.exe 處理序，而且這些處理序會在 FDHOST 啟動器服務帳戶的安全性認證底下執行。 因此，您必須執行 FDHOST 啟動器服務，才能讓全文檢索索引和全文檢索查詢運作。 如需設定此服務之服務帳戶的相關資訊，請參閱 [設定全文檢索篩選背景程式啟動器的服務帳戶](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)。  
  
 這兩個處理序包含全文檢索搜尋架構的元件。 下圖將摘要列出這些元件及其關聯性。 這些元件將在該圖之後描述。  
  
 ![全文檢索搜尋架構](../../database-engine/media/ifts-arch.gif "全文檢索搜尋架構")  
  
 [本主題內容](#top)  
  
###  <a name="sqlprocess"></a> SQL Server 處理序  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 處理序會使用全文檢索搜尋的下列元件：  
  
-   **使用者資料表。** 這些資料表包含要進行全文檢索索引的資料。  
  
-   **全文檢索收集程式。** 全文檢索收集程式會使用全文檢索搜耙執行緒。 此元件負責排程和驅動全文檢索索引母體擴展，以及監視全文檢索目錄。  
  
-   **同義字檔案。** 這些檔案包含搜尋詞彙的同義字。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的同義字檔案](configure-and-manage-thesaurus-files-for-full-text-search.md)。  
  
-   **停用字詞表物件。** 停用字詞表物件包含對搜尋沒有任何協助之常見單字的清單。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
-   **[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 查詢處理器。** 查詢處理器會編譯並執行 SQL 查詢。 如果某個 SQL 查詢包含全文檢索搜尋查詢，該查詢就會在編譯和執行期間傳送至全文檢索引擎。 系統會針對全文檢索索引比對查詢結果。  
  
-   **全文檢索引擎。** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的全文檢索引擎現在已經與查詢處理器完全整合了。 全文檢索引擎會編譯並執行全文檢索查詢。 在查詢執行期間，全文檢索引擎可能會收到來自同義字和停用字詞表的輸入。  
  
-   **索引寫入器 (索引子)。** 索引寫入器會建立用來儲存索引 Token 的結構。  
  
-   **篩選背景程式管理員。** 篩選背景程式管理員會負責監視全文檢索引擎篩選背景程式主機的狀態。  
  
 [本主題內容](#top)  
  
###  <a name="fdhostprocess"></a> 篩選背景程式主機處理序  
 篩選背景程式主機是全文檢索引擎所啟動的處理序。 它會執行下列全文檢索搜尋元件，而這些元件會負責存取、篩選和斷詞處理資料表的資料，以及斷詞處理和詞幹分析查詢輸入。  
  
 篩選背景程式主機的元件如下所示：  
  
-   **通訊協定處理常式。** 這個元件會從記憶體中提取資料以便進一步處理，而且會從指定之資料庫中的使用者資料表中存取資料。 其中一項責任就是從建立全文檢索索引的資料行中蒐集資料，並將資料傳遞給篩選背景程式主機，然後此處理序將會視需要套用篩選和斷詞工具。  
  
-   **篩選器。** 某些資料類型需要先篩選，然後才能針對文件中的資料建立全文檢索索引，包括 `varbinary`、`varbinary(max)`、`image` 或 `xml` 資料行中的資料。 用於給定文件的篩選會因其文件類型而不同。 例如，Microsoft Word (.doc) 文件、Microsoft Excel (.xls) 文件和 XML (.xml) 文件會使用不同的篩選。 然後，篩選會從文件中擷取文字區塊，並且移除內嵌的格式，並保留文字和文字位置的相關資訊。 其結果就是文字資訊的資料流。 如需詳細資訊，請參閱 [設定及管理搜尋的篩選](configure-and-manage-filters-for-search.md)。  
  
-   **斷詞工具和字幹分析器。** 斷詞工具是一項語言特有的元件，它會根據給定語言的語彙規則來尋找文字分界 (*「斷詞」*(Word Breaking))。 每個斷詞工具都與語言特有的字幹分析器元件相關聯，而且此元件會進行動詞變化和執行字形擴展。 建立索引時，篩選背景程式主機會使用斷詞工具和字幹分析器，針對來自給定資料表資料行的文字資料執行語言分析。 與全文檢索索引中資料表資料行相關聯的語言會決定哪些斷詞工具和字幹分析器要用於建立該資料行的索引。 如需詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
 [本主題內容](#top)  
  
##  <a name="processing"></a> 全文檢索搜尋處理  
 全文檢索搜尋是由全文檢索引擎所提供。 此全文檢索引擎扮演兩個角色：索引支援和查詢支援。  
  
###  <a name="indexing"></a> 全文檢索索引處理序  
 全文檢索擴展 (也就是搜耙) 起始時，全文檢索引擎會將大批的資料發送至記憶體中，並通知篩選背景程式主機。 此主機會針對資料進行篩選並斷詞，並且將轉換的資料轉換成反向字詞清單。 然後，全文檢索搜尋會從這些字詞清單中提取轉換的資料、處理資料以便移除停用字詞，並且將批次的字詞清單保存在一或多個反向索引中。  
  
 索引中儲存的資料時`varbinary(max)`或`image`資料行中，篩選器，它會實作**IFilter**介面，根據指定的檔案格式，該資料的擷取文字 (例如[!INCLUDE[msCoName](../../includes/msconame-md.md)]Word)。 在某些情況下，篩選元件必須`varbinary(max)`，或`image`寫出至 filterdata 資料夾，而不發送至記憶體的資料。  
  
 做為處理程序的一部分，收集的文字資料在經由文字分隔的處理之後，會分隔成 Token 或關鍵字。 用於 Token 化的語言是在資料行層級指定，也可由篩選元件在 `varbinary(max)`、`image` 或 `xml` 資料中識別。  
  
 您可以在停用字詞和 Token 儲存至全文檢索索引或索引片段前，進行額外的處理以移除停用字詞並將 Token 正規化。  
  
 完成母體擴展後會觸發最後的合併程序，將索引片段合併成一個主要的全文檢索索引。 如此可提升查詢的效能，因為只需要查詢一個主索引而不需查詢數個索引片段，而且可使用較佳的計分系統來排定關聯順序。  
  
 [本主題內容](#top)  
  
###  <a name="querying"></a> 全文檢索查詢處理序  
 查詢處理器會將查詢的全文檢索部分傳遞至全文檢索引擎，以便進行處理。 全文檢索引擎會執行斷詞並選擇性地執行同義字展開、詞幹分析和停用字詞 (非搜尋字) 處理。 然後，查詢的全文檢索部分會以 SQL 運算子的形式表示，主要表示成資料流資料表值函式 (STVF)。 在查詢執行期間，這些 STVF 會存取反向索引來擷取正確的結果。 接著，這些結果會在此時傳回用戶端，或在傳回用戶端之前進一步處理。  
  
 [本主題內容](#top)  
  
##  <a name="components"></a> 語言元件和語言支援的全文檢索搜尋  
 全文檢索搜尋幾乎支援 50 種不同的語言，例如英文、西班牙文、中文、日文、阿拉伯文、孟加拉文和印度文。 如需支援之全文檢索語言的完整清單，請參閱 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)。 全文檢索索引所包含的每個資料行都與 Microsoft Windows 地區設定識別碼 (LCID) 相關聯，而這個識別碼就等於全文檢索搜尋所支援的語言。 例如，LCID 1033 等於美式英文，而 LCID 2057 等於英式英文。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 針對每個支援的全文檢索語言提供了一些語言元件，可支援索引和查詢使用該語言所儲存的全文檢索資料。  
  
 語言特有的元件包含下列：  
  
-   **斷詞工具和字幹分析器。** 斷詞工具會根據給定語言的語彙規則來尋找文字分界 (*「斷詞」*(Word Breaking))。 每個斷詞工具都與針對相同語言進行動詞變化的字幹分析器相關聯。 如需詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
-   **停用字詞表。** 提供包含基本停用字詞 (也稱為非搜尋字) 集合的系統停用字詞表。 *「停用字詞」* (Stopword) 是指無助於搜尋而且全文檢索查詢會忽略的單字。 以英文地區設定為例，"a"、"and"、"is" 和 "the" 都會被視為停用字詞。 一般而言，您必須設定一個或多個同義字檔案和停用字詞表。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
-   **同義字檔案。** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 也會針對每個全文檢索語言安裝同義字檔案，以及全域同義字檔案。 已安裝的同義字 (Thesaurus) 檔案基本上是空白的，但是您可以編輯它們，以便定義特定語言或商務狀況的同義字 (Synonym)。 透過開發符合全文檢索資料的同義字，您可以有效地擴大針對該資料進行全文檢索查詢的範圍。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的同義字檔案](configure-and-manage-thesaurus-files-for-full-text-search.md)。  
  
-   **篩選 (iFilters)。**  在 `varbinary(max)`、`image` 或 `xml` 資料類型資料行中，索引文件需要執行額外處理的篩選。 此篩選必須是文件類型 (.doc、.pdf、.xls 和 .xml 等等) 特有的。 如需詳細資訊，請參閱 [設定及管理搜尋的篩選](configure-and-manage-filters-for-search.md)。  
  
 斷詞工具 (和字幹分析器) 與篩選會在篩選背景程式主機處理序 (fdhost.exe) 中執行。  
  
 [本主題內容](#top)  
  
##  <a name="reltasks"></a> 相關工作  
  
-   [全文檢索搜尋使用者入門](get-started-with-full-text-search.md)  
  
-   撰寫全文檢索查詢  
  
    -   [使用全文檢索搜尋查詢](query-with-full-text-search.md)  
  
    -   [使用 NEAR 搜尋接近另一個單字的字詞](search-for-words-close-to-another-word-with-near.md)  
  
    -   [使用 RANK 限制搜索結果](limit-search-results-with-rank.md)  
  
    -   [改善全文檢索查詢的效能](improve-the-performance-of-full-text-queries.md)  
  
    -   [使用搜索屬性清單搜索文件屬性](search-document-properties-with-search-property-lists.md)  
  
    -   [尋找搜尋屬性的屬性集 GUID 與屬性整數識別碼](find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
-   管理類別目錄和索引  
  
    -   [建立及管理全文檢索目錄](create-and-manage-full-text-catalogs.md)  
  
    -   [建立及管理全文檢索索引](create-and-manage-full-text-indexes.md)  
  
    -   [選擇建立全文檢索索引時的語言](choose-a-language-when-creating-a-full-text-index.md)  
  
    -   [擴展全文檢索索引](populate-full-text-indexes.md)  
  
    -   [管理全文檢索索引](../../database-engine/manage-full-text-indexes.md)  
  
    -   [改善全文檢索索引的效能](improve-the-performance-of-full-text-indexes.md)  
  
    -   [疑難排解全文檢索索引](troubleshoot-full-text-indexing.md)  
  
    -   [備份並還原全文檢索目錄與索引](back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   管理語言元件  
  
    -   [設定及管理搜尋的篩選](configure-and-manage-filters-for-search.md)  
  
    -   [設定及管理搜尋的斷詞工具與字幹分析器](configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
    -   [檢視或變更已註冊的篩選與斷詞工具](view-or-change-registered-filters-and-word-breakers.md)  
  
    -   [將搜索所使用的斷詞工具還原為舊版](revert-the-word-breakers-used-by-search-to-the-previous-version.md)  
  
    -   [變更用於美式英文與英式英文的斷詞工具](change-the-word-breaker-used-for-us-english-and-uk-english.md)  
  
    -   [使用自訂字典自訂斷詞工具行為](customize-the-behavior-of-word-breakers-with-a-custom-dictionary.md)  
  
    -   [設定及管理全文檢索搜尋的停用字詞與停用字詞表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
    -   [設定及管理全文檢索搜尋的同義字檔案](configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
-   管理全文檢索搜尋  
  
    -   [管理及監視伺服器執行個體的全文檢索搜尋](manage-and-monitor-full-text-search-for-a-server-instance.md)  
  
    -   [設定全文檢索篩選背景程式啟動器的服務帳戶](set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
  
-   [升級全文檢索搜尋](upgrade-full-text-search.md)  
  
 [本主題內容](#top)  
  
##  <a name="relcontent"></a> 相關內容  
  
-   [全文檢索搜尋 DDL、函數、預存程序與檢視](../views/views.md)  
  
 [本主題內容](#top)  
  
  
