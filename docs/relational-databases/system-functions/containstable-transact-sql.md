---
title: CONTAINSTABLE （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3107dbb5771731fd15bb1432b2a180af612c86fa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790446"
---
# <a name="containstable-transact-sql"></a>CONTAINSTABLE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  針對資料行傳回含有零個、一個或多個資料列的資料表，這些資料行包含與單一文字或詞組的精確或模糊 (較不精確) 相符、單字彼此在一定距離之間的接近度，或加權相符。 CONTAINSTABLE 用於 SELECT 語句的[from 子句](../../t-sql/queries/from-transact-sql.md)中 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，其參考方式就像是一般資料表名稱一樣。 它會在包含以字元為基礎之資料類型的全文檢索索引資料行上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文檢索搜尋。  
  
 CONTAINSTABLE 適用于與[contains](../../t-sql/queries/contains-transact-sql.md)述詞相同的相符專案類型，並使用與 contains 相同的搜尋條件。  
  
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
        { <simple_term> | <prefix_term> } [ ,...n ]  
     |  
        ( { <simple_term> | <prefix_term> } [ ,...n ] )   
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
 這是已經過全文檢索索引處理的資料表名稱。 *資料表*可以是一、兩個、三個或四個部分的資料庫物件名稱。 當查詢檢視時，只能包含一個全文檢索索引基底資料表。  
  
 *資料表*無法指定伺服器名稱，而且無法用於針對連結伺服器的查詢。  
  
 *column_name*  
 這是為了全文檢索搜尋而進行索引處理的一個或多個資料行名稱。 資料行可為以下類型：**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary** 或 **varbinary(max)** 。  
  
 *column_list*  
 指出您可以指定多個資料行，各資料行用逗號分隔。 *column_list* 必須括在括號中。 除非已指定 *language_term*，否則 *column_list* 之所有資料行的語言都必須相同。  
  
 \*  
 指定*資料表*中的所有全文檢索索引資料行都應該用來搜尋指定的搜尋條件。 除非已指定 *language_term*，否則資料表之所有資料行的語言都必須相同。  
  
 LANGUAGE *language_term*  
 這是在查詢過程中，其資源將用於斷詞、詞幹分析、同義字和非搜尋字（或[停用字詞](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)）移除的語言。 這個參數是選擇性的，可以指定成對應於語言地區設定識別碼 (LCID) 的字串、整數或十六進位值。 如果指定 *language_term*，系統就會將它所代表的語言套用至搜尋條件的所有項。 如果未指定任何值，就會使用資料行全文檢索語言。  
  
 如果不同語言的文件當做二進位大型物件 (BLOB) 一起儲存在單一資料行中，給定文件的地區設定識別碼 (LCID) 會判斷要建立其內容索引所使用的語言。 查詢這類資料行時，指定 *LANGUAGE**language_term* 可以增加完全相符的機率。  
  
 當指定為字串時， *language_term*對應到[sys.sys語言](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)相容性檢視中的**alias**資料行值。  字串必須以單引號括住，如 '*language_term*'。 當指定為整數時，*language_term* 是用於識別語言的實際 LCID。 當指定為十六進位值時，*language_term* 是 0x，後面接著 LCID 的十六進位值。 十六進位值不能超出 8 位數，開頭的零也包括在內。  
  
 如果這個值是雙位元組字集（DBCS）格式， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將它轉換成 Unicode。  
  
 如果指定的語言無效，或尚未安裝對應於這個語言的資源，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會傳回錯誤。 若要使用中性語言資源，請將 0x0 指定為 *language_term*。  
  
 *top_n_by_rank*  
 指定只傳回*n*個最高等級的相符專案（遞減順序）。 只有在指定整數值*n*時，才適用。 如果結合 *top_n_by_rank* 與其他參數，則查詢所傳回的資料列數目會少於實際符合所有述詞的資料列數目。 *top_n_by_rank*可讓您僅重新叫用最相關的叫用，以提高查詢效能。  
  
 <contains_search_condition>  
 指定要在 *column_name* 中搜尋的文字，以及要比對的條件。 如需搜尋條件的詳細資訊，請參閱[CONTAINS &#40;transact-sql&#41;](../../t-sql/queries/contains-transact-sql.md)。  
  
## <a name="remarks"></a>備註  
 全文檢索述詞與函數會在 FROM 述詞中隱含的單一資料表上處理。 若要在多個資料表上進行搜尋，請使用 FROM 子句中聯結的資料表，在兩個或多個資料表之產品的結果集上進行搜尋。  
  
 傳回的資料表有一個名稱為**KEY**的資料行，其中包含全文檢索索引鍵值。 每個全文檢索索引資料表都有一個資料行，其值保證是唯一的，而且在索引**鍵**資料行中傳回的值，是符合包含搜尋條件中所指定之選取條件之資料列的全文檢索索引鍵值。 從 OBJECTPROPERTYEX 函數取得的**TableFulltextKeyColumn**屬性會提供此唯一索引鍵資料行的識別。 若要取得與全文檢索索引之全文檢索索引鍵相關聯之資料行的識別碼，請使用**sys.databases fulltext_indexes**。 如需詳細資訊，請參閱[fulltext_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)。  
  
 若要取得原始資料表中您想要的資料列，請指定含有 CONTAINSTABLE 資料列的聯結。 使用 CONTAINSTABLE 的 SELECT 陳述式之 FROM 子句的一般形式如下：  
  
```  
SELECT select_list  
FROM table AS FT_TBL INNER JOIN  
   CONTAINSTABLE(table, column, contains_search_condition) AS KEY_TBL  
   ON FT_TBL.unique_key_column = KEY_TBL.[KEY];  
```  
  
 CONTAINSTABLE 所產生的資料表包含一個名為**RANK**的資料行。 **次序**資料行是每個資料列的值（從0到1000），表示資料列與選取準則相符的程度。 SELECT 陳述式通常利用下列其中一種方法來使用這個等級值：  
  
-   在 ORDER BY 子句中，傳回等級最高的資料列做為資料表中前面的資料列。  
  
-   在選取清單中，查看指派給每個資料列的等級值。  
  
## <a name="permissions"></a>權限  
 使用者必須有資料表或所參考之資料表資料行的適當 SELECT 權限，才能取得執行權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example"></a>A. 簡單範例  
 下列範例會建立並填入兩個數據行的簡單資料表，其中列出3個縣/市和其旗標中的色彩。 它會建立並填入資料表的全文檢索目錄和索引。 然後會示範**CONTAINSTABLE**語法。 這個範例會示範當搜尋值符合多次時，次序值如何增加高。 在最後一個查詢中，同時包含綠色和黑色的坦尚尼亞，其順位高於僅包含其中一個查詢色彩的。  
  
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
|**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。|  
  
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
  
### <a name="d-returning-top-5-ranked-results-using-top_n_by_rank"></a>D. 利用 top_n_by_rank 傳回前 5 個等級的結果  
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
>  使用 top_n_by_rank 不需要*language_term* argumentis 語言 *。*  
  
## <a name="see-also"></a>另請參閱  
 [使用 RANK 限制搜尋結果](../../relational-databases/search/limit-search-results-with-rank.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [建立全文檢索搜尋查詢 &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  
