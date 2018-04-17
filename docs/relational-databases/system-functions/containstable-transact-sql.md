---
title: CONTAINSTABLE (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 07/24/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONTAINSTABLE
- CONTAINSTABLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- fuzzy (less precise) word or phrase search [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- values [SQL Server], ranked
- LANGUAGE option
- NEAR option [full-text search]
- RANK column
- phrase searches [full-text search]
- conditions [SQL Server], CONTAINSTABLE
- relevance ranking values [full-text search]
- proximity searches [full-text search]
- CONTAINSTABLE function (Transact-SQL)
- ranked results [full-text search]
- rankings [full-text search]
- less precise (fuzzy) searches [full-text search]
ms.assetid: e580c210-cf57-419d-9544-7f650f2ab814
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a9f4ab666351984b62e47d664d17d9e2769337cd
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2018
---
# <a name="containstable-transact-sql"></a>CONTAINSTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對資料行傳回含有零個、一個或多個資料列的資料表，這些資料行包含與單一文字或詞組的精確或模糊 (較不精確) 相符、單字彼此在一定距離之間的接近度，或加權相符。 CONTAINSTABLE 會用於[FROM 子句](../../t-sql/queries/from-transact-sql.md)的[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT 陳述式，並如同正規資料表名稱參考。 它會在包含以字元為基礎之資料類型的全文檢索索引資料行上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文檢索搜尋。  
  
 CONTAINSTABLE 會用於相同類型的相符項目做為[CONTAINS 述詞](../../t-sql/queries/contains-transact-sql.md)，並為包含使用相同的搜尋條件。  
  
 和 CONTAINS 不同的是，使用 CONTAINSTABLE 的查詢會傳回每個資料列的相關次序值 (RANK) 和全文檢索索引鍵 (KEY)。  如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所支援全文檢索搜尋形式的資訊，請參閱[使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CONTAINSTABLE   
( table , { column_name | ( column_list ) | * } , ' <contains_search_condition> '   
     [ , LANGUAGE language_term]   
  [ , top_n_by_rank ]   
)   
  
<contains_search_condition> ::=   
    { <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    |  <weighted_term>   
    }   
    | { ( <contains_search_condition> )   
    { { AND | & } | { AND NOT | &! } | { OR | | } }   
     <contains_search_condition> [ ...n ]   
    }  
  
<simple_term> ::=   
     { word | "phrase" }  
<prefix term> ::=   
     { "word*" | "phrase*" }   
<generation_term> ::=   
     FORMSOF ( { INFLECTIONAL | THESAURUS } , <simple_term> [ ,...n ] )   
  
<generic_proximity_term> ::=   
     { <simple_term> | <prefix_term> } { { { NEAR | ~ }   
     { <simple_term> | <prefix_term> } } [ ...n ] }  
  
<custom_proximity_term> ::=   
  NEAR (   
     {  
        { <simple_term> | <prefix_term> } [ ,…n ]  
     |  
        ( { <simple_term> | <prefix_term> } [ ,…n ] )   
      [, <maximum_distance> [, <match_order> ] ]  
     }  
       )   
  
      <maximum_distance> ::= { integer | MAX }  
      <match_order> ::= { TRUE | FALSE }   
  
<weighted_term> ::=   
     ISABOUT  
    ( { {   
  <simple_term>   
  | <prefix_term>   
  | <generation_term>   
  | <proximity_term>   
  }   
   [ WEIGHT ( weight_value ) ]   
   } [ ,...n ]   
    )  
  
```  
  
## <a name="arguments"></a>引數  
 *table*  
 這是已經過全文檢索索引處理的資料表名稱。 *資料表*可以是一段、 兩段、 三段或四部分資料庫物件名稱。 當查詢檢視時，只能包含一個全文檢索索引基底資料表。  
  
 *資料表*無法同時指定伺服器名稱，並且不能用在連結伺服器查詢。  
  
 *column_name*  
 這是為了全文檢索搜尋而進行索引處理的一個或多個資料行名稱。 資料行可為以下類型：**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary** 或 **varbinary(max)**。  
  
 *column_list*  
 指出您可以指定多個資料行，各資料行用逗號分隔。 *column_list* 必須括在括號中。 除非已指定 *language_term*，否則 *column_list* 之所有資料行的語言都必須相同。  
  
 \*  
 指定的所有全文檢索都索引中的資料行*資料表*應該用來搜尋給定的搜尋條件。 除非已指定 *language_term*，否則資料表之所有資料行的語言都必須相同。  
  
 LANGUAGE *language_term*  
 是的語言其資源來斷詞、 詞幹分析和同義字和非搜尋字 (或[停用字詞](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) 移除，因為查詢的一部分。 這個參數是選擇性的，可以指定成對應於語言地區設定識別碼 (LCID) 的字串、整數或十六進位值。 如果指定 *language_term*，系統就會將它所代表的語言套用至搜尋條件的所有項。 如果未指定任何值，就會使用資料行全文檢索語言。  
  
 如果不同語言的文件當做二進位大型物件 (BLOB) 一起儲存在單一資料行中，給定文件的地區設定識別碼 (LCID) 會判斷要建立其內容索引所使用的語言。 查詢這類資料行時，指定 *LANGUAGE**language_term* 可以增加完全相符的機率。  
  
 當指定為字串， *language_term*對應至**別名**中的資料行值[sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)相容性檢視。  字串必須以單引號括住，如 '*language_term*'。 當指定為整數時，*language_term* 是用於識別語言的實際 LCID。 當指定為十六進位值時，*language_term* 是 0x，後面接著 LCID 的十六進位值。 十六進位值不能超出 8 位數，開頭的零也包括在內。  
  
 如果這個值是雙位元組字集 (DBCS) 格式，[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將它轉換成 Unicode。  
  
 如果指定的語言無效，或尚未安裝對應於這個語言的資源，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會傳回錯誤。 若要使用中性語言資源，請將 0x0 指定為 *language_term*。  
  
 *top_n_by_rank*  
 指定只有*n*最高等級的相符項目以遞減順序，會傳回。 整數值時才適用*n*，指定。 如果結合 *top_n_by_rank* 與其他參數，則查詢所傳回的資料列數目會少於實際符合所有述詞的資料列數目。 *top_n_by_rank*可讓您可以重新呼叫最相關叫用來提升查詢效能。  
  
 <contains_search_condition>  
 指定要在 *column_name* 中搜尋的文字，以及要比對的條件。 搜尋條件的相關資訊，請參閱[CONTAINS &#40;TRANSACT-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)。  
  
## <a name="remarks"></a>備註  
 全文檢索述詞與函數會在 FROM 述詞中隱含的單一資料表上處理。 若要在多個資料表上進行搜尋，請使用 FROM 子句中聯結的資料表，在兩個或多個資料表之產品的結果集上進行搜尋。  
  
 傳回的資料表有資料行名為**金鑰**且含有全文檢索索引鍵值。 每個全文檢索索引的資料表具有資料行的數值保證是唯一的並在傳回的值**金鑰**資料行是全文檢索索引鍵值的資料列符合選取準則中指定的包含搜尋條件。 **TableFulltextKeyColumn**從 OBJECTPROPERTYEX 函數中取得的屬性提供這個唯一索引鍵資料行的識別。 若要取得全文檢索索引的全文檢索索引鍵相關聯的資料行的識別碼，請使用**sys.fulltext_indexes**。 如需詳細資訊，請參閱[sys.fulltext_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)。  
  
 若要取得原始資料表中您想要的資料列，請指定含有 CONTAINSTABLE 資料列的聯結。 使用 CONTAINSTABLE 的 SELECT 陳述式之 FROM 子句的一般形式如下：  
  
```  
SELECT select_list  
FROM table AS FT_TBL INNER JOIN  
   CONTAINSTABLE(table, column, contains_search_condition) AS KEY_TBL  
   ON FT_TBL.unique_key_column = KEY_TBL.[KEY];  
```  
  
 Containstable 產生的資料表包括名為資料行**陣序規範**。 **陣序規範**資料行是每個資料列用於指示資料列符合選取準則的程度的值 （0 至 1000年)。 SELECT 陳述式通常利用下列其中一種方法來使用這個等級值：  
  
-   在 ORDER BY 子句中，傳回等級最高的資料列做為資料表中前面的資料列。  
  
-   在選取清單中，查看指派給每個資料列的等級值。  
  
## <a name="permissions"></a>Permissions  
 使用者必須有資料表或所參考之資料表資料行的適當 SELECT 權限，才能取得執行權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example"></a>A. 簡單範例  
 下列範例會建立並填入簡單資料表的兩個資料行，列出 3 郡和其旗標的色彩。 It 會建立並擴展全文檢索目錄和資料表上的索引。 然後在**CONTAINSTABLE**示範的語法。 此範例示範如何次序值成長到較高搜尋的值符合多次時。 在最後一個查詢中，其中包含綠色及黑色坦尚尼亞具有較高的等級比義大利包含其中一個查詢的色彩。  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM CONTAINSTABLE (Flags, FlagColors, 'Green') ORDER BY RANK DESC;  
SELECT * FROM CONTAINSTABLE (Flags, FlagColors, 'Green or Black') ORDER BY RANK DESC;  
```  
  
### <a name="b-returning-rank-values"></a>B. 傳回等級值  
 下列範例會搜尋所有包含 "frame"、"wheel" 或 "tire" 等字的產品名稱，且每個字都各有不同的加權。 每個符合這些搜尋準則的傳回資料列，都會顯示相符項目的相對相似程度 (等級值)。 另外，等級最高的資料列會最先傳回。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Name, KEY_TBL.RANK  
    FROM Production.Product AS FT_TBL   
        INNER JOIN CONTAINSTABLE(Production.Product, Name,   
        'ISABOUT (frame WEIGHT (.8),   
        wheel WEIGHT (.4), tire WEIGHT (.2) )' ) AS KEY_TBL  
            ON FT_TBL.ProductID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
### <a name="c-returning-rank-values-greater-than-a-specified-value"></a>C. 傳回大於指定值的等級值  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
 下列範例會使用 NEAR 搜尋在 `bracket` 資料表中彼此接近的 "`reflector`" 和 "`Production.Document`"。 只會傳回排名值大於或等於 50 的資料列。  
  
```  
USE AdventureWorks2012  
GO  
  
SELECT DocumentNode, Title, DocumentSummary  
FROM Production.Document AS DocTable   
INNER JOIN CONTAINSTABLE(Production.Document, Document,  
  'NEAR(bracket, reflector)' ) AS KEY_TBL  
  ON DocTable.DocumentNode = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 50  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
> [!NOTE]  
>  如果全文檢索查詢並沒有指定做為最大距離的整數，文件若僅包含間距大於 100 個邏輯詞彙的叫用數，就不會符合 NEAR 需求，而其等級將會是 0。  
  
### <a name="d-returning-top-5-ranked-results-using-topnbyrank"></a>D. 利用 top_n_by_rank 傳回前 5 個等級的結果  
 下列範例會傳回 `Description` 資料行在 "light" 或 "lightweight" 字附近包含 "aluminum" 一字之前 5 項產品的描述。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY];  
GO  
```  
  
 `GO`  
  
### <a name="e-specifying-the-language-argument"></a>E. 指定 LANGUAGE 引數  
 下列範例顯示如何使用 `LANGUAGE` 引數。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)',  
      LANGUAGE N'English',  
      5  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY];  
GO  
```  
  
> [!NOTE]  
>  語言*language_term* argumentis 不需要使用*top_n_by_rank。*  
  
## <a name="see-also"></a>另請參閱  
 [限制 RANK 的搜索結果](../../relational-databases/search/limit-search-results-with-rank.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [建立全文檢索搜尋查詢 &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  
