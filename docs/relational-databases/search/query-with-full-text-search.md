---
title: 使用全文檢索搜尋進行查詢 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 92b2a975fbee89249850e4acfdf23f7f47e5bd23
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47652626"
---
# <a name="query-with-full-text-search"></a>Query with Full-Text Search
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
使用述詞 **CONTAINS** 和 **FREETEXT** 以及具有 **SELECT** 陳述式的資料列集值函式 **CONTAINSTABLE** 和 **FREETEXTTABLE**，以撰寫全文檢索查詢。 本文提供每個述詞和函式的範例，並協助您選擇最適合的來使用。

-   若要比對單字和片語，請使用 **CONTAINS** 和 **CONTAINSTABLE**。
-   若要比對意義，而不是確切的用字，請使用 **FREETEXT** 和 **FREETEXTTABLE**。

## <a name="examples_simple"></a> 每個述詞和函式的範例

下列範例使用 AdventureWorks 範例資料庫。 如需 AdventureWorks 的最終版本，請參閱 [SQL Server 2016 CTP3 的 AdventureWorks 資料庫與指令碼](https://www.microsoft.com/download/details.aspx?id=49502)。 若要執行範例查詢，您也必須設定全文檢索搜尋。 如需詳細資訊，請參閱[開始使用全文檢索搜尋](get-started-with-full-text-search.md)。 

### <a name="example---contains"></a>範例 - CONTAINS  
下列範例會尋找所有價格是 `$80.99`，且含有 `"Mountain"` 這個單字的產品：
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
### <a name="example---freetext"></a>範例 - FREETEXT 
 下列範例會搜尋包含 `vital safety components` 相關單字的所有文件：
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```

### <a name="example---containstable"></a>範例 - CONTAINSTABLE  
 下列範例會傳回 **Description** 資料行在 "light" 或 "lightweight" 單字附近包含 "aluminum" 單字之所有產品的描述識別碼和描述。 只會傳回排名大於或等於 2 的資料列。  
  
```sql
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
  
### <a name="example---freetexttable"></a>範例 - FREETEXTTABLE  
 下列範例將擴充 FREETEXTTABLE 查詢，以便先傳回最高等級的資料列，並將每個資料列的等級加至選取清單。 若要撰寫類似查詢，您必須知道 **ProductDescriptionID** 是 **ProductDescription** 資料表的唯一索引鍵資料行。  
  
```sql 
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
  
下面是相同查詢的擴充，其只傳回排名大於或等於 10 的資料列：  
  
```sql  
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

## <a name="match-words-or-match-meaning"></a>比對單字或比對意義

`CONTAINS`/`CONTAINSTABLE` 和 `FREETEXT`/`FREETEXTTABLE` 適用於不同類型的比對。 下列資訊協助您選擇查詢的最佳述詞或函式：

### <a name="containscontainstable"></a>CONTAINS/CONTAINSTABLE

-   使用精確或模糊 (較不精確) 的比對，來比對單字和片語。
-   您也可以執行下列動作：
    -   指定單字彼此在一定距離內。
    -   傳回加權相符項目。
    -   結合搜尋條件與邏輯運算子。 如需詳細資訊，請參閱本文中後續的[使用布林運算子 (AND、OR 和 NOT)](#Using_Boolean_Operators)。

### <a name="freetextfreetexttable"></a>FREETEXT/FREETEXTTABLE

-   比對指定之單字、片語或句子 (「Freetext 字串」) 的意義，而不是確切的用字。
-   如果在指定之資料行的全文檢索索引中找到任何詞彙或任何形式的詞彙，就會產生相符項目。

## <a name="compare-predicates-and-functions"></a>比較述詞和函式

述詞 `CONTAINS`/`FREETEXT` 與資料列集值函式 `CONTAINSTABLE`/`FREETEXTTABLE` 的語法和選項不同。 下列資訊協助您選擇查詢的最佳述詞或函式：

### <a name="predicates-contains-and-freetext"></a>述詞 CONTAINS 和 FREETEXT

**使用方式**。 在 SELECT 陳述式的 WHERE 或 HAVING 子句中，使用全文檢索**述詞** CONTAINS 和 FREETEXT。

**結果**。 CONTAINS 和 FREETEXT 述詞會傳回 TRUE 或 FALSE 值，指出給定資料列是否符合全文檢索查詢。 符合的資料列就會傳回結果集中。

**其他選項**。 您可以將述詞與任何其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 述詞合併使用，例如 LIKE 和 BETWEEN。

您可以指定要搜尋資料表中的單一資料行、資料行清單或所有資料行。

此外，您可以針對斷詞和詞幹分析、同義字查閱及非搜尋字移除，指定全文檢索查詢使用其資源的語言。

您可以在 CONTAINS 或 FREETEXT 述詞中使用四部分名稱，以便在連結的伺服器上查詢目標資料表的全文檢索索引資料行。 若要準備遠端伺服器來接收全文檢索查詢，請針對遠端伺服器上的目標資料表與資料行建立全文檢索索引，然後加入遠端伺服器成為連結的伺服器。

**其他資訊**。 如需這些述詞的語法和引數詳細資訊，請參閱 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)。

### <a name="rowset-valued-functions-containstable-and-freetexttable"></a>資料列集值函式 CONTAINSTABLE 和 FREETEXTTABLE

**使用方式**。 使用全文檢索**函式** CONTAINSTABLE 和 FREETEXTTABLE 函式，就像 SELECT 陳述式之 FROM 子句中的一般資料表名稱。

您必須指定要在使用其中一個函式時所要搜尋的基底資料表。 至於述詞，您可以指定要搜尋之資料表中的單一資料行、資料行清單或所有資料行，且可選擇性地指定全文檢索查詢使用其資源的語言。

一般而言，您必須聯結 CONTAINSTABLE 或 FREETEXTTABLE 的結果與基底資料表。 若要加入資料表，您必須知道唯一索引鍵資料行名稱。 這個資料行 (出現在每個啟用全文檢索的資料表中) 用來強制資料表的唯一資料列 (*unique**key column*)。 如需索引鍵資料行的詳細資訊，請參閱[建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)。

**結果**。 這些函式會傳回符合全文檢索查詢之零、一或多個資料列的資料表。 傳回的資料表僅包含基底資料表的資料列，而這些資料列符合函式之全文檢索搜尋條件中指定的選取準則。

使用其中一個函式的查詢也會針對每個傳回的資料列傳回一個相關排名值 (RANK) 和全文檢索索引鍵 (KEY)，如下所示：

-   **KEY** 資料行。 KEY 資料行會傳回所傳回之資料列的唯一值。 KEY 資料行可用來指定選取準則。
-   **RANK** 資料行。 RANK 資料行會傳回每個資料列的「等級值」(Rank Value)，表示資料列與選取準則的符合程度。 資料列中文字或文件的等級值越高，該資料列與給定全文檢索查詢的關聯性就越大。 不同的資料列可能會以完全相同的方式排名。 您可以透過指定選擇性 *top_n_by_rank* 參數，限制要傳回的相符項目數。 如需詳細資訊，請參閱 [限制 RANK 的搜索結果](../../relational-databases/search/limit-search-results-with-rank.md)。

**其他資訊**。 如需這些函式的語法和引數詳細資訊，請參閱[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)。

## <a name="examples_specific"></a> 特定的搜尋類型

###  <a name="Simple_Term"></a> 搜尋特定單字或片語 (簡單詞彙)  
 您可以使用 [CONTAINS](../../t-sql/queries/contains-transact-sql.md)、[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)、[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 或 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 來搜尋資料表中的特定單字或片語。 例如，如果您要搜尋 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中的 **ProductReview** 資料表，以尋找某產品具有 "learning curve" 片語的所有註解，可依照下列方式使用 CONTAINS 述詞：  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
搜尋條件 (在此範例中是 "learning curve") 有時候可能很複雜，且由一或多個詞彙組成。

#### <a name="more-info-about-simple-term-searches"></a>簡單字詞搜尋的詳細資訊

在全文檢索搜尋中，「單字」 (或 Token) 是一種字串，其邊界是由適當的斷詞工具所識別，後面緊接著指定之語言的語言規則。 有效的「片語」是由多個單字所組成 (不論單字之間是否有標點符號)。

例如，"croissant" 是一個單字，而 "café au lait" 則是一個片語。 這類字詞與片語稱為簡單詞彙。

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 會尋找完全相符的片語。 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 會將片語分解成個別的字詞。

###  <a name="Prefix_Term"></a> 搜尋具有前置詞的單字 (前置詞彙)  
 您可以使用 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 或 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 來搜尋具有指定之前置詞的字詞或片語。 傳回資料行內包含以指定之前置詞開頭之文字的所有項目。 例如，若要搜尋包含 `top`- 前置詞的所有資料列，如同在 `top``ple`、 `top``ping`和 `top`中。 查詢看起來會像下列範例：  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 傳回的項目是與星號 (*) 前指定之文字相符的所有文字。 如果文字及星號未以雙引號 (") 分隔，例如 `CONTAINS (DESCRIPTION, 'top*')`，則全文檢索搜尋就不會將星號視為萬用字元。  
  
 若前置詞彙為片語，每個組成片語的 Token 都會被視為個別的前置項目。 傳回的資料列均包含以前置詞彙開頭的單字。 例如，"light bread\*" 這個前置詞彙找到的是包含 "light breaded"、"lightly breaded" 或 "light bread" 文字的資料列，而不會傳回如 "lightly toasted bread" 的資料列。

#### <a name="more-info-about-prefix-searches"></a>前置詞搜尋的詳細資訊

「前置詞彙」是指附加至單字前面以便產生衍生字或字形變化的字串。

-   對於單一前置詞彙而言，任何以指定之詞彙為開頭的單字都會成為結果集的一部分。 例如，"auto*" 詞彙與 "automatic"、"automobile" 等字相符。

-   對於片語而言，片語中的每個單字都會被視為前置詞彙。 例如，"auto tran\*" 詞彙符合 "automatic transmission" 及 "automobile transducer"，但不符合 "automatic motor transmission"。

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)支持前置詞搜尋。
  
###  <a name="Inflectional_Generation_Term"></a> 搜尋特定單字的字形變化 (衍生詞彙)  
您可以使用 [CONTAINS](../../t-sql/queries/contains-transact-sql.md)、 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)、 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)或 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 搜尋動詞的所有不同時態和變化或名詞的單複數形式 (變化形式搜尋)，或是特定字詞的同義字形式 (同義字搜尋)。  
  
下列範例會在 `Comments` 資料庫中 `ProductReview` 資料表的 `AdventureWorks` 資料行內，搜尋任何形式的 "foot" ("foot"、"feet" 等)： 
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
全文檢索搜尋會使用字幹分析器，此工具可讓您搜尋動詞的不同時態和變化或是名詞的單複數形式。 如需字幹分析器的詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  

#### <a name="more-info-about-generation-term-searches"></a>衍生詞彙搜尋的詳細資訊

「字形變化」是指動詞的不同時態和變化或是名詞的單複數。

例如，搜尋 "drive" 單字的字形變化。 如果資料表的不同資料列中包括 "drive"、"drives"、"drove"、"driving" 及 "driven" 等字，因為這些單字全都從 "drive" 這個字變化而來，所以都會出現在結果集中。

[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 預設會尋找所有指定之單字的變化詞彙。 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 支援選擇性 `INFLECTIONAL` 引數。

### <a name="search-for-synonyms-of-a-specific-word"></a>搜尋特定單字的同義字

「同義字」會針對詞彙定義使用者指定的同義字。 如需同義字檔案的詳細資訊，請參閱[設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)。

例如，如果 "{car, automobile, truck, van}" 項目新增到同義字中，您就可以搜尋 "car" 這個字的同義字變化。 由於 "automobile"、"truck"、"van" 或 "car" 這些字都是屬於內含 "car" 這個字的同義字擴充集，因此所查詢的資料表中，所有包含這些字的資料列都會出現在結果集。

[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 預設會使用同義字。 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 支援選擇性 `THESAURUS` 引數。

### <a name="search-for-a-word-near-another-word"></a>搜尋一個單字的「接近」單字

「近接字詞」表示彼此相近的單字或片語。 您也可以指定分隔第一個和最後一個搜尋詞彙之非搜尋詞彙的數目上限。 此外，您可以依任何順序或是您所指定的順序來搜尋字詞或片語。

例如，您要尋找其中有 "ice" 單字接近 "hockey" 單字，或 "ice skating" 片語接近 "ice hockey" 片語的資料列。 

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)

如需鄰近搜尋的詳細資訊，請參閱[使用 NEAR 搜尋靠近另一個單字的字詞](search-for-words-close-to-another-word-with-near.md)。

###  <a name="Weighted_Term"></a> 使用加權值來搜尋單字或片語 (加權詞彙)  
您可以使用 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 來搜尋字詞或片語，並指定加權值。 加權值是介於 0.0 到 1.0 之間的數字，用來指示每個字詞與片語在一組字詞與片語中的重要程度。 最小的加權值是 0.0，最大則為 1.0。  
  
下列範例顯示的查詢會搜尋所有客戶的地址，並使用加權值，找出以 "Bay" 字串開頭並含有 "Street" 或 "View" 的所有文字。 資料列中包含越多指定的字詞，結果就會為該資料列指定越高的等級。  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*,"   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 加權詞彙可以搭配任何不可分割的詞彙、前置詞彙、衍生詞彙或相近詞彙一起使用。

#### <a name="more-info-about-weighted-term-searches"></a>加權字詞搜尋的詳細資訊

在加權字詞搜尋中，「加權值」是表示每個單字與片語在一組單字與片語中的重要程度。 最小的加權值是 0.0，最大則為 1.0。

例如，在搜尋多個詞彙的查詢中，您可以指派每個搜尋單字的加權值，以指出它與搜尋條件中之其他單字的相對重要性。 這類型之查詢的結果會根據您指派給搜尋單字的相對加權，先傳回最相關的資料列。 結果集包含具有任何指定之詞彙的文件或資料列 (或它們之間的內容)。不過，因為與不同搜尋詞彙相關聯的加權值具有變化，所以某些結果會被視為比其他結果更相關。

[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 支援加權字詞搜尋。

##  <a name="Using_Boolean_Operators"></a> 使用 AND、OR 和 NOT (布林運算子)
 
CONTAINS 述詞與 CONTAINSTABLE 函數會使用相同的搜尋條件。 這兩個項目都支援使用布林運算子 (AND、OR 和 NOT) 來結合許多搜尋詞彙，以便執行邏輯作業。 例如，您可以使用 AND 來尋找同時包含 "latte" 和 "New York-style bagel" 的資料列。 例如，您可以使用 AND NOT 來尋找包含 "bagel" 但不包含 "cream cheese" 的資料列。  
  
相較之下，FREETEXT 和 FREETEXTTABLE 會將布林詞彙視為要搜尋的單字。  
  
 如需結合 CONTAINS 與使用邏輯運算子 AND、OR 和 NOT 之其他述詞的詳細資訊，請參閱[搜尋條件 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)。  
  
### <a name="example"></a>範例  
 下列範例使用 CONTAINS 述詞來搜尋描述識別碼不等於 5，而且描述同時包含 "Aluminum" 與 "spindle" 這兩個單字的描述。 搜尋條件會使用 AND 布林運算子。 這個範例使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的 ProductDescription 資料表。
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
##  <a name="Additional_Considerations"></a> 大小寫、停用字詞、語言和同義字

 當您撰寫全文檢索查詢時，也可以指定下列選項：
  
-   **區分大小寫**。 全文檢索搜尋查詢是不分大小寫的。 但在日文中，有多種發音拼字法，它的拼音正規化概念就類似不區分大小寫 (例如，kana = insensitivity)。 這類拼字法正規化並未支援。  

-   **停用字詞**。 定義全文檢索查詢時，全文檢索引擎會從搜尋準則中捨棄停用字詞 (也稱為非搜尋字)。 停用字詞是指 "a"、"and"、"is" 或 "the" 等字，這些字雖然經常出現，但通常對搜尋特定文字並無幫助。 停用字詞會列於停用字詞表中。 每個全文檢索索引都會與特定停用字詞表相關聯，以便判斷哪些停用字詞會在建立索引時，從查詢或索引中省略。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  

-   [語言]，含 **LANGUAGE** 選項。 許多查詢詞彙主要取決於斷詞工具行為。 若要確保您使用正確的斷詞工具 (和字幹分析器) 和同義字檔案，我們建議您指定 LANGUAGE 選項。 如需詳細資訊，請參閱 [選擇建立全文檢索索引時的語言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  
  
-   **同義字**. FREETEXT 和 FREETEXTTABLE 查詢預設會使用同義字。 CONTAINS 和 CONTAINSTABLE 支援選擇性 THESAURUS 引數。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的同義字檔案](configure-and-manage-thesaurus-files-for-full-text-search.md)。
  
##  <a name="tokens"></a> 檢查 Token 化結果

在查詢中套用指定的文字分隔、同義字和停用字詞表組合之後，您就可以使用 **sys.dm_fts_parser** 動態管理檢視來查看全文檢索搜尋如何將結化成 Token。 如需詳細資訊，請參閱 [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [建立全文檢索搜尋查詢 &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [改善全文檢索查詢的效能](../../relational-databases/search/improve-the-performance-of-full-text-queries.md)
 
