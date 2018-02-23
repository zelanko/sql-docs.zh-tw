---
title: "使用全文檢索搜尋進行查詢 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3eb62bf156079250cc129ab1b07aa3411381e211
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="query-with-full-text-search"></a>Query with Full-Text Search
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
使用全文檢索述詞 **CONTAINS** 和 **FREETEXT** 以及具有 **SELECT** 陳述式的資料列集值函式 **CONTAINSTABLE** 和 **FREETEXTTABLE**，以撰寫全文檢索查詢。 本文提供每個述詞和函式的範例，並協助您選擇最適合的來使用。

-   使用 **CONTAINS** 和 **CONTAINSTABLE**，以比對單字和片語。
-   使用 **FREETEXT** 和 **FREETEXTTABLE** 比對意義，而不是確切的用字。

## <a name="examples_simple"></a> 每個述詞和函式的簡單範例

### <a name="example---contains"></a>範例 - CONTAINS  
 下列範例會尋找所有價格是 `$80.99` ，且含有 `"Mountain"`這個單字的產品。  
  
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
 下列範例會搜尋包含 vital、safety 和 components 相關單字的所有文件。  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```

### <a name="example---containstable"></a>範例 - CONTAINSTABLE  
 下列範例會傳回 **Description** 資料行在 "light" 或 "lightweight" 單字附近包含 "aluminum" 單字之所有產品的描述識別碼和描述。 只會傳回排名值大於或等於 2 的資料列。  
  
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
  
### <a name="example--freetexttable"></a>範例- FREETEXTTABLE  
 下列範例將擴充 FREETEXTTABLE 查詢，以便先傳回最高等級的資料列，並將每個資料列的等級加至選取清單。 若要指定查詢，您必須知道 **ProductDescriptionID** 是 **ProductDescription** 資料表的唯一索引鍵資料行。  
  
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
  
下面是相同查詢的擴充，它只傳回等級值大於或等於 10 的資料列：  
  
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

## <a name="pick-the-best-predicate-or-function"></a>選擇最佳述詞或函式

`CONTAINS`/`CONTAINSTABLE` 和 `FREETEXT`/`FREETEXTTABLE` 適用於不同類型的比對。 下表協助您選擇查詢的最佳述詞或函式。

如需範例，請參閱[每個述詞和函式的簡單範例](#examples_simple)和[特定搜尋類型的範例](#examples_specific)。 另請參閱[可搜尋的內容](#supported)。

| |CONTAINS/CONTAINSTABLE|FREETEXT/FREETEXTTABLE|
|---|---|---|
|**查詢類型**|使用精確或模糊 (較不精確) 的比對，來比對單字和片語。|比對指定之單字、片語或句子 (「Freetext 字串」) 的意義，而不是確切的用字。<br/><br/>如果在指定之資料行的全文檢索索引中找到任何詞彙或任何形式的詞彙，就會產生相符項目。|
|**其他查詢選項**|您可以指定單字彼此在一定距離內。<br/><br/>您可以傳回加權相符項目。<br/><br/>您可以使用邏輯作業來合併多個搜尋條件。 如需詳細資訊，請參閱本文中後續的[使用布林運算子 (AND、OR 和 NOT)](#Using_Boolean_Operators)。|N/a|

## <a name="compare-predicates-and-functions"></a>比較述詞和函式

述詞 `CONTAINS`/`FREETEXT` 與資料列集值函式 `CONTAINSTABLE`/`FREETEXTTABLE` 的語法和選項不同。 下表協助您選擇查詢的最佳述詞或函式。

如需範例，請參閱[每個述詞和函式的簡單範例](#examples_simple)和[特定搜尋類型的範例](#examples_specific)。 另請參閱[可搜尋的內容](#supported)。

| |述詞<br/>CONTAINS/FREETEXT|函數<br/>CONTAINSTABLE/FREETEXTTABLE|
|---|---|---|
|**使用方式**|在 SELECT 陳述式的 WHERE 或 HAVING 子句中，使用全文檢索**述詞** CONTAINS 和 FREETEXT。|使用全文檢索**函式** CONTAINSTABLE 和 FREETEXTTABLE 函式，就像 SELECT 陳述式之 FROM 子句中的一般資料表名稱。|
|**其他查詢選項**|您可以將它們與任何其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 述詞合併使用，例如 LIKE 和 BETWEEN。<br/><br/>您可以指定要搜尋資料表中的單一資料行、資料行清單或所有資料行。<br/><br/>此外，您可以針對斷詞和詞幹分析、同義字查閱及非搜尋字移除，指定全文檢索查詢使用其資源的語言。|您必須指定要在使用其中一個函式時所要搜尋的基底資料表。 至於述詞，您可以指定要搜尋之資料表中的單一資料行、資料行清單或所有資料行，且可選擇性地指定全文檢索查詢使用其資源的語言。<br/><br/>一般而言，您必須聯結 CONTAINSTABLE 或 FREETEXTTABLE 的結果與基底資料表。 若要這麼做，您必須知道唯一索引鍵資料行名稱。 這個資料行 (出現在每個啟用全文檢索的資料表中) 用來強制資料表的唯一資料列 (*unique**key column*)。 如需索引鍵資料行的詳細資訊，請參閱[建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)。|
|**結果**|CONTAINS 和 FREETEXT 述詞會傳回 TRUE 或 FALSE 值，指出給定資料列是否符合全文檢索查詢。 符合的資料列就會傳回結果集中。|這些函式會傳回符合全文檢索查詢之零、一或多個資料列的資料表。 傳回的資料表僅包含基底資料表的資料列，而這些資料列符合函式之全文檢索搜尋條件中指定的選取準則。<br/><br/>使用其中一個函式的查詢也會針對每個傳回的資料列傳回一個相關次序值 (RANK) 和全文檢索索引鍵 (KEY)，如下所示：<br/><ul><li>**KEY** 資料行。 KEY 資料行會傳回所傳回之資料列的唯一值。 KEY 資料行可用來指定選取準則。</li><li>**RANK** 資料行。 RANK 資料行會傳回每個資料列的「等級值」(Rank Value)，表示資料列與選取準則的符合程度。 資料列中文字或文件的等級值越高，該資料列與給定全文檢索查詢的關聯性就越大。 請注意，不同的資料列可能會以完全相同的方式排序等級。 您可以透過指定選擇性 *top_n_by_rank* 參數，限制要傳回的相符項目數。 如需詳細資訊，請參閱 [限制 RANK 的搜索結果](../../relational-databases/search/limit-search-results-with-rank.md)。</li></ul>|
|**其他選項**|您可以在 CONTAINS 或 FREETEXT 述詞中使用四部分名稱，以便在連結的伺服器上查詢目標資料表的全文檢索索引資料行。 若要準備遠端伺服器來接收全文檢索查詢，請針對遠端伺服器上的目標資料表與資料行建立全文檢索索引，然後加入遠端伺服器成為連結的伺服器。|N/a|
|**其他資訊**|如需這些述詞的語法和引數詳細資訊，請參閱 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)。|如需這些函式的語法和引數詳細資訊，請參閱[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)。|

##  <a name="supported"></a> 可搜尋的內容

下表描述您可搜尋的單字和片語類型。
  
|查詢詞彙形式|描述|支援者|  
|----------------------|-----------------|------------------|  
|一或多個特定的單字或片語<br/>(「簡單詞彙」)|例如，"croissant" 是一個單字，而 "café au lait" 則是一個片語。 這類字詞與片語稱為簡單詞彙。<br /><br /> 在全文檢索搜尋中，「單字」 (或 Token) 是一種字串，其邊界是由適當的斷詞工具所識別，後面緊接著指定之語言的語言規則。 有效的「片語」是由多個單字所組成 (不論單字之間是否有標點符號)。<br /><br /> 如需詳細資訊，請參閱本文中後續的[搜尋特定單字或片語 (簡單詞彙)](#Simple_Term)。|[CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 會尋找完全相符的片語。<br /><br /> [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 會將片語分解成個別的字詞。|  
|以指定之文字開頭的單字或片語<br/>(「前置詞彙」)|對於單一前置詞彙而言，任何以指定之詞彙為開頭的單字都會成為結果集的一部分。 例如，詞彙 "auto*" 與 "automatic"、"automobile" 等字相符。<br /><br /> 對於片語而言，片語中的每個單字都會被視為前置詞彙。 例如，"auto tran\*" 詞彙符合 "automatic transmission" 及 "automobile transducer"，但不符合 "automatic motor transmission"。<br /><br /> 「前置詞彙」是指附加至單字前面以便產生衍生字或字形變化的字串。<br /><br /> 如需詳細資訊，請參閱本文中稍後的[執行前置詞搜尋 (前置字詞)](#Prefix_Term)。|[CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)|  
|特定單字的字形變化<br/>(「衍生詞彙 - 字形變化」)|例如，搜尋 "drive" 單字的變化形式。 如果資料表的不同資料列中包括 "drive"、"drives"、"drove"、"driving" 及 "driven" 等字，因為所有這些單字都是從 "drive" 這個字所變化產生，所以它們都會出現在結果集中。<br /><br /> 「字形變化」是指動詞的不同時態和變化或是名詞的單複數。 <br /><br /> 如需詳細資訊，請參閱本文中稍後的[搜尋特定單字的屈折形式 (產生字詞)](#Inflectional_Generation_Term)。|[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 預設會尋找所有指定之單字的變化詞彙。<br /><br /> [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 支援選擇性 INFLECTIONAL 引數。|  
|特定單字的同義字變化<br/>(「衍生詞彙 - 同義字」)|例如，如果將 "{car, automobile, truck, van}" 這個項目加入同義字中，則您可搜尋 "car" 這個字的同義字變化。 由於 "automobile"、"truck"、"van" 或 "car" 這些字都是屬於內含 "car" 這個字的同義字展開集，因此所查詢之資料表中含有這些字的所有資料列都會出現在結果集中。<br /><br />「同義字」會針對詞彙定義使用者指定的同義字。<br /><br />  如需同義字檔案的結構詳細資訊，請參閱 [設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)。|[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 和 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 預設會使用同義字。<br /><br /> [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 支援選擇性 THESAURUS 引數。|  
|靠近另一個單字或片語的單字或片語<br/>(「相近詞彙」)|例如，您要尋找 "ice" 單字接近 "hockey" 單字或 "ice skating" 片語接近 "ice hockey" 片語的資料列。<br /><br /> 「近接字詞」表示彼此相近的單字或片語。 您也可以指定分隔第一個和最後一個搜尋詞彙之非搜尋詞彙的數目上限。 此外，您可以依任何順序或是您所指定的順序來搜尋字詞或片語。<br /><br /> 如需詳細資訊，請參閱 [使用 NEAR 搜尋靠近另一個單字的字詞](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md).|[CONTAINS](../../t-sql/queries/contains-transact-sql.md) 和 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)|  
|使用加權值的單字或片語<br/>(「加權詞彙」)|例如，在搜尋多個詞彙的查詢中，您可以指派每個搜尋單字的加權值，以指出它與搜尋條件中之其他單字的相對重要性。 這類型之查詢的結果會根據您指派給搜尋單字的相對加權，先傳回最相關的資料列。 結果集包含具有任何指定之詞彙的文件或資料列 (或它們之間的內容)。不過，因為與不同搜尋詞彙相關聯的加權值具有變化，所以某些結果會被視為比其他結果更相關。<br /><br /> 「加權值」是表示每個單字與片語在一組單字與片語中的重要程度。 最小的加權值是 0.0，最大則為 1.0。<br /><br /> 如需詳細資訊，請參閱本文中稍後的[使用加權值搜尋單字或片語 (加權字詞)](#Weighted_Term)。|[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)|  

## <a name="examples_specific"></a> 特定搜尋類型的範例

###  <a name="Simple_Term"></a> 搜尋特定單字或片語 (簡單詞彙)  
 您可以使用 [CONTAINS](../../t-sql/queries/contains-transact-sql.md)、 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)、 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)或 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 來搜尋資料表中的特定片語。 例如，如果您要搜尋 **資料庫中的** ProductReview [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料表，以尋找具有 "learning curve" 片語之產品的所有註解，可依照下列方式使用 CONTAINS 述詞：  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
 搜尋條件 (在此範例中是 "learning curve") 有時候可能相當複雜，且由一或多個詞彙組成。  
  
###  <a name="Prefix_Term"></a> 搜尋具有前置詞的單字 (前置詞彙)  
 您可以使用 [CONTAINS](../../t-sql/queries/contains-transact-sql.md) 或 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 來搜尋具有指定之前置詞的字詞或片語。 傳回資料行內包含以指定之前置詞開頭之文字的所有項目。 例如，若要搜尋包含 `top`- 前置詞的所有資料列，如同在 `top``ple`、 `top``ping`和 `top`中。 查詢內容如下所示：  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 傳回的項目是與星號 (*) 前指定之文字相符的所有文字。 如果文字及星號未以雙引號 (") 分隔，例如 `CONTAINS (DESCRIPTION, 'top*')`，則全文檢索搜尋就不會將星號視為萬用字元。  
  
 若前置詞彙為片語，每個組成片語的 Token 都會被視為個別的前置項目。 傳回的資料列均包含以前置詞彙開頭的單字。 例如，"light bread*" 這個前置詞彙找到的是包含 "light breaded"、"lightly breaded" 或 "light bread" 文字的資料列，而不會傳回如 "lightly toasted bread" 的資料列。  
  
###  <a name="Inflectional_Generation_Term"></a> 搜尋特定單字的字形變化 (衍生詞彙)  
您可以使用 [CONTAINS](../../t-sql/queries/contains-transact-sql.md)、 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)、 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)或 [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) 搜尋動詞的所有不同時態和變化或名詞的單複數形式 (變化形式搜尋)，或是特定字詞的同義字形式 (同義字搜尋)。  
  
下列範例會在 `Comments` 資料庫中 `ProductReview` 資料表的 `AdventureWorks` 資料行內，搜尋任何形式的 "foot" ("foot"、"feet" 等)。  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
全文檢索搜尋會使用字幹分析器，此工具可讓您搜尋動詞的不同時態和變化或是名詞的單複數形式。 如需字幹分析器的詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
   
###  <a name="Weighted_Term"></a> 使用加權值來搜尋單字或片語 (加權詞彙)  
您可以使用 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 來搜尋字詞或片語，並指定加權值。 加權值是介於 0.0 到 1.0 之間的數字，用來指示每個字詞與片語在一組字詞與片語中的重要程度。 最小的加權值是 0.0，最大則為 1.0。  
  
下列範例顯示一項查詢，此查詢會搜尋所有客戶的地址，並使用加權值，找出以 "Bay" 字串開頭且連接 "Street" 或 "View" 的所有文字。 資料列中包含越多指定的字詞，結果就會為該資料列指定越高的等級。  
  
```sql  
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

##  <a name="Using_Boolean_Operators"></a> 使用布林運算子 (AND、OR 和 NOT)
 
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
  
##  <a name="Additional_Considerations"></a> 其他查詢選項

 當您撰寫全文檢索查詢時，也可以指定下列選項。
  
-   [語言]，含 **LANGUAGE** 選項。 許多查詢詞彙主要取決於斷詞工具行為。 若要確保您使用正確的斷詞工具 (和字幹分析器) 和同義字檔案，我們建議您指定 LANGUAGE 選項。 如需詳細資訊，請參閱 [選擇建立全文檢索索引時的語言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  

-   **區分大小寫**。 全文檢索搜尋查詢是不分大小寫的。 但在日文中，有多種發音拼字法，它的拼音正規化概念就類似不區分大小寫 (例如，kana = insensitivity)。 這類拼字法正規化並未支援。  

-   **停用字詞**。 定義全文檢索查詢時，全文檢索引擎會從搜尋準則中捨棄停用字詞 (也稱為非搜尋字)。 停用字詞是指 "a"、"and"、"is" 或 "the" 等字，這些字雖然經常出現，但通常對搜尋特定文字並無幫助。 停用字詞會列於停用字詞表中。 每個全文檢索索引都會與特定停用字詞表相關聯，以便判斷哪些停用字詞會在建立索引時，從查詢或索引中省略。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
-   **同義字**. FREETEXT 和 FREETEXTTABLE 查詢預設會使用同義字。 CONTAINS 和 CONTAINSTABLE 支援選擇性 THESAURUS 引數。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的同義字檔案](configure-and-manage-thesaurus-files-for-full-text-search.md)。
  
##  <a name="tokens"></a> 檢查 Token 化結果

將指定的斷詞工具、同義字和停用字詞表組合套用至查詢字串輸入之後，您就可以使用 **sys.dm_fts_parser** 動態管理檢視來檢視 Token 化結果。 如需詳細資訊，請參閱 [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [建立全文檢索搜尋查詢 &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [改善全文檢索查詢的效能](../../relational-databases/search/improve-the-performance-of-full-text-queries.md)
 
