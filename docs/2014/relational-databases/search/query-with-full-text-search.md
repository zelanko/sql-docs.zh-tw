---
title: 使用全文檢索搜尋進行查詢 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 244161359910896533a1d7179f2ce80b5cb03d86
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749422"
---
# <a name="query-with-full-text-search"></a>Query with Full-Text Search
  為了定義全文檢索搜尋，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文檢索查詢會使用全文檢索述詞 (CONTAINS 和 FREETEXT) 與函數 (CONTAINSTABLE 和 FREETEXTTABLE)。 這些項目支援豐富的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法，而這種語法支援各種形式的查詢詞彙。 若要撰寫全文檢索查詢，您必須了解使用這些述詞與函數的時機和方式。  
  
##  <a name="OV_ft_predicates"></a> 概觀全文檢索述詞 （CONTAINS 和 FREETEXT）  
 CONTAINS 和 FREETEXT 述詞會傳回 TRUE 或 FALSE 值。 它們只能用來指定選取準則，以便判斷給定的資料列是否符合全文檢索查詢。 符合的資料列就會傳回結果集中。 CONTAINS 和 FREETEXT 都是在 SELECT 陳述式的 WHERE 或 HAVING 子句中指定的。 它們可與任何其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 述詞結合，例如 LIKE 和 BETWEEN。  
  
> [!NOTE]  
>  如需語法和引數，這些述詞的詳細資訊，請參閱[CONTAINS &#40;TRANSACT-SQL&#41; ](/sql/t-sql/queries/contains-transact-sql)和[FREETEXT &#40;-&#41;](/sql/t-sql/queries/freetext-transact-sql)。  
  
 使用 CONTAINS 或 FREETEXT 時，您可以指定要搜尋資料表中的單一資料行、資料行清單或所有資料行。 此外，您可以針對斷詞和詞幹分析、同義字查閱以及非搜尋字移除，指定給定全文檢索查詢將使用之資源的語言。  
  
 CONTAINS 和 FREETEXT 適用於不同種類的比對，如下所示：  
  
-   使用 CONTAINS (或 CONTAINSTABLE) 以進行下列各種比對：單字和片語的精確或模糊 (較不精確) 比對、單字彼此在一定距離之間的接近度，或加權相符。 使用 CONTAINS 時，您至少必須指定一個指定您要搜尋之文字的搜尋條件，以及判斷是否相符的條件。  
  
     您可以在搜尋條件之間使用邏輯作業。 如需詳細資訊，請參閱 <<c0> [ 使用布林運算子-AND、 OR、 AND NOT （在 CONTAINS 和 CONTAINSTABLE 中）](#Using_Boolean_Operators)稍後在本主題中。  
  
-   使用 FREETEXT (或 FREETEXTTABLE) 來比對指定之單字、片語或句子 (「Freetext 字串」(Freetext String)) 的意義，但不比對確切的用字。 如果在指定之資料行的全文檢索索引中找到任何詞彙或任何形式的詞彙，就會產生相符項目。  
  
 您可以在 CONTAINS 或 FREETEXT 述詞中使用四部分名稱，以便在連結的伺服器上查詢目標資料表的全文檢索索引資料行。 若要準備遠端伺服器來接收全文檢索查詢，請針對遠端伺服器上的目標資料表與資料行建立全文檢索索引，然後加入遠端伺服器成為連結的伺服器。  
  
> [!NOTE]  
>  當資料庫相容性層級設定為 100 時， [OUTPUT 子句](/sql/t-sql/queries/output-clause-transact-sql) 中不允許全文檢索述詞。  
  
 
  
### <a name="examples"></a>範例  
  
#### <a name="a-using-contains-with-simpleterm"></a>A. 搭配使用 CONTAINS 與 <simple_term>  
 下列範例會尋找所有價格是 `$80.99`，且含有 `"Mountain"` 這個單字的產品。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
#### <a name="b-using-freetext-to-search-for-words-containing-specified-character-values"></a>B. 使用 FREETEXT 搜尋含有所指定字元值的單字  
 下列範例會搜尋包含 vital、safety 和 components 相關單字的所有文件。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```  
  
 
  
##  <a name="OV_ft_functions_CONTAINSTABLE_FREETEXTTABLE"></a> 全文檢索函數 （CONTAINSTABLE 和 FREETEXTTABLE） 的概觀  
 CONTAINSTABLE 和 FREETEXTTABLE 函數的參考方式就如同 SELECT 陳述式之 FROM 子句中的一般資料表名稱。 它們會傳回符合全文檢索查詢之零、一或多個資料列的資料表。 傳回的資料表僅包含基底資料表的資料列，而這些資料列符合函數之全文檢索搜尋條件中指定的選取準則。  
  
> [!NOTE]  
>  如需語法和引數，這些函式的資訊，請參閱[CONTAINSTABLE &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-functions/containstable-transact-sql)和[FREETEXTTABLE &#40;-&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)。  
  
 使用其中一個函數的查詢會針對每個資料列傳回一個相關次序值 (RANK) 和全文檢索索引鍵 (KEY)，如下所示：  
  
-   KEY 資料行  
  
     KEY 資料行會傳回所傳回之資料列的唯一值。 KEY 資料行可用來指定選取準則。  
  
-   RANK 資料行  
  
     RANK 資料行會傳回每個資料列的「等級值」(Rank Value)，表示資料列與選取準則的符合程度。 資料列中文字或文件的等級值越高，該資料列與給定全文檢索查詢的關聯性就越大。 請注意，不同的資料列可能會以完全相同的方式排序等級。 您可以透過指定選擇性 *top_n_by_rank* 參數，限制要傳回的相符項目數。 如需詳細資訊，請參閱 [限制 RANK 的搜索結果](limit-search-results-with-rank.md)。  
  
 使用其中一個函數時，您必須指定要進行全文檢索搜尋的基底資料表。 與述詞一樣，您可以指定要搜尋資料表中的單一資料行、資料行清單或所有資料行，而且可以選擇性地指定給定全文檢索查詢將使用之資源的語言。  
  
 CONTAINSTABLE 適用的比對種類與 CONTAINS 相同，而 FREETEXTTABLE 適用的比對種類則與 FREETEXT 相同。 如需詳細資訊，請參閱本主題前面的 [全文檢索述詞 (CONTAINS 和 FREETEXT) 的概觀](#OV_ft_predicates)。 執行使用 CONTAINSTABLE 與 FREETEXTTABLE 函數的查詢時，您必須明確聯結傳回的資料列與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基底資料表中的資料列。  
  
 一般而言，CONTAINSTABLE 或 FREETEXTTABLE 的結果必須與基底資料表聯結。 在這種情況下，您必須知道唯一索引鍵資料行名稱。 這個資料行 (出現在每個啟用全文檢索的資料表中) 用來強制資料表的唯一資料列 (*unique**key column*)。 如需詳細資訊，請參閱 [管理全文檢索索引](../indexes/indexes.md)。  
  
 
  
### <a name="examples"></a>範例  
  
#### <a name="a-using-containstable"></a>A. 使用 CONTAINSTABLE  
 下列範例會傳回 **Description** 資料行在 "light" 或 "lightweight" 字附近包含 "aluminum" 這個字之所有產品的描述識別碼和描述。 只會傳回排名值大於或等於 2 的資料列。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
#### <a name="b-using-freetexttable"></a>B. 使用 FREETEXTTABLE  
 下列範例將擴充 FREETEXTTABLE 查詢，以便先傳回最高等級的資料列，並將每個資料列的等級加至選取清單。 若要指定查詢，您必須知道**ProductDescriptionID**是唯一的索引鍵資料行的`ProductDescription`資料表。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 下面是相同查詢的擴充，它只傳回等級值大於或等於 10 的資料列：  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 
  
##  <a name="Using_Boolean_Operators"></a> 使用布林運算子-，OR，而不要-在 CONTAINS 和 CONTAINSTABLE  
 CONTAINS 述詞與 CONTAINSTABLE 函數會使用相同的搜尋條件。 兩者都支援的結合許多搜尋詞彙使用布林運算子-AND、 OR 和 NOT-以便執行邏輯作業。 例如，您可以使用 AND 來尋找同時包含 "latte" 和 "New York-style bagel" 的資料列。 例如，您可以使用 AND NOT 來尋找包含 "bagel" 但不包含 "cream cheese" 的資料列。  
  
> [!NOTE]  
>  相較之下，FREETEXT 和 FREETEXTTABLE 會將布林詞彙視為要搜尋的單字。  
  
 如需結合 CONTAINS 與使用邏輯運算子 AND、OR 和 NOT 之其他述詞的詳細資訊，請參閱[搜尋條件 &#40;Transact-SQL&#41;](/sql/t-sql/queries/search-condition-transact-sql)。  
  
### <a name="example"></a>範例  
 下列範例會使用 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 資料庫的 ProductDescription 資料表。 此查詢會使用 CONTAINS 述詞來搜尋描述識別碼不等於 5，而且描述同時包含 "Aluminum" 與 "spindle" 這兩個單字的描述。 搜尋條件會使用 AND 布林運算子。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
 
  
##  <a name="Additional_Considerations"></a> 全文檢索查詢的其他考量  
 撰寫全文檢索查詢時，請同時考量下列事項：  
  
-   LANGUAGE 選項  
  
     許多查詢詞彙主要取決於斷詞工具行為。 若要確保您使用正確的斷詞工具 (和字幹分析器) 和同義字檔案，我們建議您指定 LANGUAGE 選項。 如需詳細資訊，請參閱 [選擇建立全文檢索索引時的語言](choose-a-language-when-creating-a-full-text-index.md)。  
  
-   停用字詞  
  
     定義全文檢索查詢時，全文檢索引擎會從搜尋準則中捨棄停用字詞 (也稱為非搜尋字)。 停用字詞是指 "a"、"and"、"is" 或 "the" 等字，這些字雖然經常出現，但通常對搜尋特定文字並無幫助。 停用字詞會列於停用字詞表中。 每個全文檢索索引都會與特定停用字詞表相關聯，以便判斷哪些停用字詞會在建立索引時，從查詢或索引中省略。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](full-text-search.md)。  
  
-   同義字  
  
     FREETEXT 和 FREETEXTTABLE 查詢預設會使用同義字。 CONTAINS 和 CONTAINSTABLE 支援選擇性 THESAURUS 引數。  
  
-   區分大小寫  
  
     全文檢索搜尋查詢是不分大小寫的。 但在日文中，有多種發音拼字法，它的拼音正規化概念就類似不區分大小寫 (例如，kana = insensitivity)。 這類拼字法正規化並未支援。  
  

  
##  <a name="varbinary"></a> 查詢 varbinary （max） 和 xml 資料行  
 如果已建立 `varbinary(max)`、`varbinary` 或 `xml` 資料行的全文檢索索引，您就可以使用全文檢索述詞 (CONTAINS 和 FREETEXT) 與函數 (CONTAINSTABLE 和 FREETEXTTABLE) 來查詢它，就像查詢任何其他全文檢索索引資料行一樣。  
  
> [!IMPORTANT]  
>  全文檢索搜尋也會處理 image 資料行。 不過，`image` 資料類型將在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未來版本中移除。 請避免在新的開發作業中使用此資料類型，並且計畫修改目前使用此資料類型的應用程式。 請改用 `varbinary(max)` 資料類型。  
  
### <a name="varbinarymax-or-varbinary-data"></a>varbinary(max) 或 varbinary 資料  
 單一 `varbinary(max)` 或 `varbinary` 資料行可以儲存多種類型的文件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援已在作業系統中安裝並提供篩選的任何文件類型。 每份文件的文件類型都是由文件的副檔名所識別。 例如，全文檢索搜尋會針對 .doc 副檔名使用支援 Microsoft Word 文件的篩選。 如需可用文件類型的清單，請查詢 [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) 目錄檢視。  
  
 請注意，全文檢索引擎可以運用安裝在作業系統中的現有篩選。 您必須先將作業系統篩選、斷詞工具和字幹分析器載入伺服器執行個體中，然後才能使用它們，如下所示：  
  
```  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
 若要針對 `varbinary(max)` 資料行建立全文檢索索引，全文檢索引擎需要 `varbinary(max)` 資料行中文件副檔名的存取權。 這項資訊必須儲存在稱為類型資料行的資料表資料行中，而此資料行必須與全文檢索索引中的 `varbinary(max)` 資料行相關聯。 建立文件的索引時，全文檢索引擎會使用類型資料行中的副檔名來識別要使用的篩選。  
  
 
  
### <a name="xml-data"></a>xml 資料  
 `xml` 資料類型資料行只會儲存 XML 文件和片段，而且只有 XML 篩選會用於這些文件。 因此，類型資料行是不必要的。 在 `xml` 資料行上，全文檢索索引會建立 XML 元素內容的索引，但忽略 XML 標記。 屬性值是全文檢索索引的值 (除非它們是數值)。 元素標記會當做 Token 界限來使用。 系統支援包含多種語言且格式正確的 XML 或 HTML 文件和片段。  
  
 如需查詢的詳細資訊`xml`資料行，請參閱 <<c2> [ 使用 XML 資料行全文檢索搜尋](../xml/use-full-text-search-with-xml-columns.md)。  
  
 
  
##  <a name="supported"></a> 支援的查詢詞彙形式  
 本節摘要說明全文檢索述詞和資料列集值函數針對每一種查詢形式所提供的支援。  
  
> [!NOTE]  
>  如果是有提供查詢詞彙的語法，請按下表 **支援者** 列中的對應連結。  
  
|查詢詞彙形式|描述|支援者|  
|----------------------|-----------------|------------------|  
|一或多個特定的單字或片語 (「不可分割的詞彙」(Simple Term))|在全文檢索搜尋中，字詞 (或 *token*) 是一種字串，其邊界是由適當的斷詞工具所識別，後面緊接著指定之語言的語言規則。 有效的片語是由多個字詞所組成 (不論字詞之間是否有標點符號)。<br /><br /> 例如，"可頌麵包 」 是 word 和 「 外 」 au lait 」 這個詞彙。 這類字詞與片語稱為簡單詞彙。<br /><br /> 如需詳細資訊，請參閱本主題稍後的 [搜尋特定字詞或片語 (簡單詞彙)](#Simple_Term)。|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 會尋找完全相符的片語。<br /><br /> [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) 和 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) 會將片語分解成個別的字詞。|  
|以指定之文字開頭的單字或片語 (「前置詞彙」(Prefix Term))|前置詞彙是指附加至單字前面以便產生衍生字或字形變化的字串。<br /><br /> 對於單一前置詞彙而言，任何以指定之詞彙為開頭的單字都會成為結果集的一部分。 例如，詞彙 "auto*" 與 "automatic"、"automobile" 等字相符。<br /><br /> 對於片語而言，片語中的每個單字都會被視為前置詞彙。 例如，"auto tran\*" 詞彙符合 "automatic transmission" 及 "automobile transducer"，但不符合 "automatic motor transmission"。<br /><br /> 如需詳細資訊，請參閱本主題稍後的 [執行前置詞搜尋 (前置詞彙)](#Prefix_Term)。|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|特定單字的字形變化 (*詞彙-變化產生*)|變化形式是指動詞的不同時態和變化或是名詞的單複數。 例如，搜尋 "drive" 單字的變化形式。 如果資料表的不同資料列中包括 "drive"、"drives"、"drove"、"driving" 及 "driven" 等字，因為所有這些單字都是從 "drive" 這個字所變化產生，所以它們都會出現在結果集中。<br /><br /> 如需詳細資訊，請參閱本主題稍後的 [搜尋特定單字的變化形式 (衍生詞彙)](#Inflectional_Generation_Term)。|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) 和 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) 預設會尋找所有指定之單字的變化詞彙。<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 支援選擇性 INFLECTIONAL 引數。|  
|特定單字的同義字形式 (*產生詞彙-同義字*)|同義字 (Thesaurus) 會針對詞彙定義使用者指定的同義字 (Synonym)。 例如，如果將 "{car, automobile, truck, van}" 這個項目加入同義字中，則您可搜尋 "car" 這個字的同義字變化。 由於 "automobile"、"truck"、"van" 或 "car" 這些字都是屬於內含 "car" 這個字的同義字展開集，因此所查詢之資料表中含有這些字的所有資料列都會出現在結果集中。<br /><br /> 如需同義字檔案的結構詳細資訊，請參閱 [設定及管理全文檢索搜尋的同義字檔案](configure-and-manage-thesaurus-files-for-full-text-search.md)。|[FREETEXT](/sql/t-sql/queries/freetext-transact-sql) 和 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) 預設會使用同義字。<br /><br /> [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 支援選擇性 THESAURUS 引數。|  
|靠近另一個單字或片語的單字或片語 (「相近詞彙」(Proximity Term))|相近詞彙表示彼此互相靠近的字詞或片語。您也可以指定分隔第一個和最後一個搜尋詞彙的非搜尋詞彙數目上限。 此外，您可以依任何順序或是您所指定的順序來搜尋字詞或片語。<br /><br /> 例如，您要尋找 "ice" 單字接近 "hockey" 單字或 "ice skating" 片語接近 "ice hockey" 片語的資料列。<br /><br /> 如需詳細資訊，請參閱 [使用 NEAR 搜尋靠近另一個單字的字詞](search-for-words-close-to-another-word-with-near.md).|[CONTAINS](/sql/t-sql/queries/contains-transact-sql) 和 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
|使用加權值的單字或片語 (「加權詞彙」)|加權值是表示每個字詞與片語在一組字詞與片語中的重要程度。 最小的加權值是 0.0，最大則為 1.0。<br /><br /> 例如，在搜尋多個詞彙的查詢中，您可以指派每個搜尋單字的加權值，以指出它與搜尋條件中之其他單字的相對重要性。 這類型之查詢的結果會根據您指派給搜尋單字的相對加權，先傳回最相關的資料列。 結果集包含具有任何指定之詞彙的文件或資料列 (或它們之間的內容)。不過，因為與不同搜尋詞彙相關聯的加權值具有變化，所以某些結果會被視為比其他結果更相關。<br /><br /> 如需詳細資訊，請參閱本主題稍後的 [使用加權值來搜尋字詞或片語 (加權詞彙)](#Weighted_Term)。|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)|  
  

  
###  <a name="Simple_Term"></a> 搜尋特定單字或片語 （簡單詞彙）  
 您可以使用 [CONTAINS](/sql/t-sql/queries/contains-transact-sql)、 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)、 [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)或 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) 來搜尋資料表中的特定片語。 例如，如果您要搜尋 [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 資料庫中的 `ProductReview` 資料表，以尋找具有 "learning curve" 片語之產品的所有註解，可依照下列方式使用 CONTAINS 述詞：  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 搜尋條件 (在此範例中是 "learning curve") 有時候可能相當複雜，且由一個或多個詞彙組成。  
  
 
  
###  <a name="Prefix_Term"></a> 執行前置詞搜尋 （前置詞彙）  
 您可以使用 [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 或 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 來搜尋具有指定之前置詞的字詞或片語。 傳回資料行內包含以指定之前置詞開頭之文字的所有項目。 例如，若要搜尋包含 `top`- 前置詞的所有資料列，如同在 `top``ple`、 `top``ping`和 `top`中。 查詢內容如下所示：  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 傳回的項目是與星號 (*) 前指定之文字相符的所有文字。 如果文字及星號未以雙引號 (") 分隔，例如 `CONTAINS (DESCRIPTION, 'top*')`，則全文檢索搜尋就不會將星號視為萬用字元。  
  
 若前置詞彙為片語，每個組成片語的 Token 都會被視為個別的前置項目。 傳回的資料列均包含以前置詞彙開頭的單字。 例如，"light bread*" 這個前置詞彙找到的是包含 "light breaded"、"lightly breaded" 或 "light bread" 文字的資料列，而不會傳回如 "lightly toasted bread" 的資料列。  
  
 
  
###  <a name="Inflectional_Generation_Term"></a> 搜尋特定單字 （衍生詞彙） 的變化形式  
 您可以使用 [CONTAINS](/sql/t-sql/queries/contains-transact-sql)、 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql)、 [FREETEXT](/sql/t-sql/queries/freetext-transact-sql)或 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) 搜尋動詞的所有不同時態和變化或名詞的單複數形式 (變化形式搜尋)，或是特定字詞的同義字形式 (同義字搜尋)。  
  
 下列範例會在 `Comments` 資料庫中 `ProductReview` 資料表的 `AdventureWorks` 資料行內，搜尋任何形式的 "foot" ("foot"、"feet" 等)。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
> [!NOTE]  
>  全文檢索搜尋會使用字幹分析器，此工具可讓您搜尋動詞的不同時態和變化或是名詞的單複數形式。 如需字幹分析器的詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  

  
###  <a name="Weighted_Term"></a> 搜尋字詞或片語使用加權值 （加權詞彙）  
 您可以使用 [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 來搜尋字詞或片語，並指定加權值。 加權值是介於 0.0 到 1.0 之間的數字，用來指示每個字詞與片語在一組字詞與片語中的重要程度。 最小的加權值是 0.0，最大則為 1.0。  
  
 下列範例顯示一項查詢，此查詢會搜尋所有客戶的地址，並使用加權值，找出以 "Bay" 字串開頭且連接 "Street" 或 "View" 的所有文字。 資料列中包含越多指定的字詞，結果就會為該資料列指定越高的等級。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*",   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 加權詞彙可以搭配任何不可分割的詞彙、前置詞彙、衍生詞彙或相近詞彙一起使用。  
  

  
##  <a name="tokens"></a> 檢視斷詞工具、 同義字和停用字詞表組合的 token 化結果  
 將指定的斷詞工具、同義字和停用字詞表組合套用至查詢字串輸入之後，您就可以使用 **sys.dm_fts_parser** 動態管理檢視來檢視 Token 化結果。 如需詳細資訊，請參閱 [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)。  
  
 
  
## <a name="see-also"></a>另請參閱  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [建立全文檢索搜尋查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)   
 [改善全文檢索查詢的效能](improve-the-performance-of-full-text-queries.md)  
  
  
