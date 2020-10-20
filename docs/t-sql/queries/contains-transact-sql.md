---
title: CONTAINS (Transact-SQL) | Microsoft Docs
description: CONTAINS 語言元素的 Transact-SQL 參考。 用於搜尋另一個運算式中的單字或片語。
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CONTAINS_TSQL
- CONTAINS
dev_langs:
- TSQL
helpviewer_keywords:
- precise or fuzzy (less precise) matches [full-text search]
- CONTAINS predicate (Transact-SQL)
- conditions [SQL Server], CONTAINS
- fuzzy (less precise) word or phrase search [full-text search]
- word weighting values [full-text search]
- word searches [full-text search]
- weighted values [full-text search]
- LANGUAGE option
- word inflectionally generated from another [full-text search]
- NEAR option [full-text search]
- phrase searches [full-text search]
- word near another word search [full-text search]
- full-text search [SQL Server], searching on a property
- proximity searches [full-text search]
- less precise (fuzzy) searches [full-text search]
- property searching [SQL Server], searching on a property
- inflectional forms [full-text search]
- prefix searches [full-text search]
ms.assetid: 996c72fc-b1ab-4c96-bd12-946be9c18f84
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7e1e56c9132fe59a91274ff90598ddce3a6fe21c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035871"
---
# <a name="contains-transact-sql"></a>CONTAINS (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中搜尋單字和片語的精確或模糊 (較不精確) 相符項目、彼此在一定距離之間的單字，或加權相符項目。 CONTAINS 為用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT 陳述式之 [WHERE 子句](../../t-sql/queries/where-transact-sql.md)中的述詞，可在包含以字元為基礎之資料類型的全文檢索索引資料行上執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 全文檢索搜尋。  
  
 CONTAINS 可以搜尋下列項目：  
  
-   單字或片語。  
  
-   單字或片語的前置詞。  
  
-   接近另一個單字的單字。  
  
-   從另一個單字變化產生的單字 (如 drive 這個字是 drives、drove、driving 和 driven 等字的變化詞幹)。  
  
-   使用同義字 (Thesaurus) 時，另一個單字的同義字 (Synonym) (例如，"aluminum" 和 "steel" 等字是 "metal" 的同義字)。  
  
 如需有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所支援全文檢索搜尋形式的資訊，請參閱[使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)。  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
CONTAINS (   
     {   
        column_name | ( column_list )   
      | *   
      | PROPERTY ( { column_name }, 'property_name' )    
     }   
     , '<contains_search_condition>'  
     [ , LANGUAGE language_term ]  
   )   
  
<contains_search_condition> ::=   
  {   
      <simple_term>   
    | <prefix_term>   
    | <generation_term>   
    | <generic_proximity_term>   
    | <custom_proximity_term>   
    | <weighted_term>   
    }   
  |   
    { ( <contains_search_condition> )   
        [ { <AND> | <AND NOT> | <OR> } ]   
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
   ( {   
        {   
          <simple_term>   
        | <prefix_term>   
        | <generation_term>   
        | <proximity_term>   
        }   
      [ WEIGHT ( weight_value ) ]   
      } [ ,...n ]   
   )   
  
<AND> ::=   
  { AND | & }  
  
<AND NOT> ::=   
  { AND NOT | &! }  
  
<OR> ::=   
  { OR | | }  
  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *column_name*  
 這是在 FROM 子句中指定之資料表全文檢索索引資料行的名稱。 資料行可為以下類型：**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary** 或 **varbinary(max)** 。  
  
 *column_list*  
 指定兩個或多個以逗號分隔的資料行。 *column_list* 必須括在括號中。 除非已指定 *language_term*，否則 *column_list* 之所有資料行的語言都必須相同。  
  
 \*  
 指定查詢將會在 FROM 子句所指定的資料表中，針對指定的搜尋條件搜尋所有的全文檢索索引資料行。 CONTAINS 子句中的資料行必須來自包含全文檢索索引的單一資料表。 除非已指定 *language_term*，否則資料表之所有資料行的語言都必須相同。  
  
 PROPERTY ( *column_name* , '*property_name*')  
**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。 
  
 指定要在其上搜尋指定之搜尋條件的文件屬性。  
  
> [!IMPORTANT]  
>  *property_name* 必須在全文檢索索引的搜尋屬性清單中指定，而且全文檢索索引必須包含 *property_name* 的屬性特定項目，才能讓查詢傳回任何資料列。 如需詳細資訊，請參閱 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
 LANGUAGE *language_term*  
 這是在查詢中用於斷詞、確立詞幹、同義字擴充與取代，以及移除非搜尋字 (或[停用字詞](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) 的語言。 這是選擇性參數。  
  
 如果不同語言的文件當做二進位大型物件 (BLOB) 一起儲存在單一資料行中，給定文件的地區設定識別碼 (LCID) 會判斷要建立其內容索引所使用的語言。 查詢此種資料行時，指定 LANGUAGE *language_term* 可以增加完全相符的機率。  
  
 *language_term*以指定為對應於語言之 LCID 的字串、整數或十六進位值。 如果指定 *language_term*，系統就會將它所代表的語言套用至搜尋條件的所有元素上。 如果未指定任何值，就會使用資料行全文檢索語言。  
  
 當指定為字串時，*language_term* 會對應到 [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 相容性檢視表中的 **alias** 資料行值。 字串必須以單引號括住，如 '*language_term*'。 當指定為整數時，*language_term* 是用於識別語言的實際 LCID。 當指定為十六進位值時，*language_term* 是 0x，後面接著 LCID 的十六進位值。 十六進位值不能超出 8 位數，開頭的零也包括在內。  
  
 如果這個值是雙位元組字集 (DBCS) 格式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將它轉換成 Unicode。  
  
 如果指定的語言無效，或尚未安裝對應於這個語言的資源，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會傳回錯誤。 若要使用中性語言資源，請將 0x0 指定為 *language_term*。  
  
 \<*contains_search_condition*>  
 指定要在 *column_name* 中搜尋的文字，以及要比對的條件。  
  
*\<contains_search_condition>* 為 **nvarchar**。 當使用另一個字元資料類型當做輸入時，會發生隱含轉換。 不能使用大型字串資料類型 nvarchar(max) 和 varchar(max)。 在下列範例中，定義為 `@SearchWord` 的 `varchar(30)` 變數會造成 `CONTAINS` 述詞中的隱含轉換。
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord VARCHAR(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 由於「參數探測」不適用於轉換，因此請使用 **nvarchar** 來獲得更好的效能。 在此範例中，請將 `@SearchWord` 宣告為 `nvarchar(30)`。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord NVARCHAR(30)  
SET @SearchWord = N'performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 當產生的並非最佳計畫時，也可以使用 OPTIMIZE FOR 查詢提示。  
  
 *word*  
 這是不含空格或標點符號的字元字串。  
  
 *phrase*  
 這是一個或多個單字，各個字之間有空格。  
  
> [!NOTE]  
>  部分語言 (如亞洲某些地區所撰寫的語言) 可能會有不用空格來分隔的一個或多個單字所組成的片語。  
  
\<simple_term>  
指定符合完整的單字或片語。 "blue berry"、blueberry 和 "Microsoft SQL Server" 都是有效的簡單詞彙範例。 片語應該用雙引號 ("") 括住。 片語中的單字必須依照 *\<contains_search_condition>* 所指定、符合其出現在資料庫資料行中的相同順序顯示。 在單字或片語中搜尋字元並不區分大小寫。 全文檢索索引資料行中的非搜尋字 (或[停用字詞](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)，如 a、and 或 the) 不會儲存在全文檢索索引中。 如果在單一字的搜尋中使用非搜尋字，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回一則錯誤訊息，指出查詢只包含非搜尋字。 在每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 \Mssql\Binn\FTERef 目錄中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都併入了一份標準非搜尋字清單。  
  
 系統會忽略標點符號。 因此，`CONTAINS(testing, "computer failure")` 將比對含有此值的資料列："Where is my computer? Failure to find it would be expensive"。 如需斷詞工具行為的詳細資訊，請參閱[設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
 \<prefix_term>  
 指定符合開頭是指定之文字的單字或片語。 請用雙引號 ("") 括住前置詞彙，在後引號的前面加上星號 (\*)，以便找出所有開頭是星號前面所指定之簡單詞彙的文字。 這個子句的指定方式應該如下：`CONTAINS (column, '"text*"')`。 星號符合 (屬於單字或片語中一個或多個根單字) 零個、一個或多個字元。 如果並未用雙引號來分隔文字和星號，述詞便是 `CONTAINS (column, 'text*')`，此時全文檢索搜尋會將星號視為字元，因此，它會搜尋完全相符的 `text*`。 全文檢索引擎並不會找到開頭是星號 (\*) 的文字，因為斷詞工具通常會忽略這些字元。  
  
 當 *\<prefix_term>* 是片語時，片語所包含的每個單字都會被視為個別的前置詞。 因此，指定前置詞彙 "local wine*" 的查詢可能會符合開頭是 "local winery"、"locally wined and dined" 等文字的任何資料列。  
  
 \<generation_term>  
 指定符合「其中所包括的簡單詞彙含有要搜尋的原始單字之各種變化形」的單字。  
  
 INFLECTIONAL  
 在指定的簡單詞彙上，指定所用之特定語言的字幹分析器。 字幹分析器的行為是以每種特定語言的詞幹分析規則來定義的。 中性語言並沒有相關聯的字幹分析器。 系統會利用查詢之資料行的資料行語言來參考所需的字幹分析器。 如果有指定 *language_term*，便會使用對應於這個語言的字幹分析器。  
  
 *\<generation_term>* 內指定的 *\<simple_term>* 不會同時符合名詞和動詞。  
  
 THESAURUS  
 指定使用對應於資料行全文檢索語言或查詢指定之語言的同義字。 系統會利用 *\<simple_term>* 中一或多個最長的模式來比對這些同義字，且會產生其他詞彙來擴充或取代原始模式。 如果找不到 *\<simple_term>* 的完全或部分相符項目，就會將不相符的部分當做 *simple_term* 來處理。 如需全文檢索搜尋同義字的詳細資訊，請參閱[設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)。  
  
 \<generic_proximity_term>  
 指定必須符合要搜尋之文件中的單字或片語。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 建議您使用 \<custom_proximity_term>。  
  
 NEAR | ~  
 指出 NEAR 或 ~ 運算子兩側的單字或片語必須出現在要傳回之相符項目的文件中。 您必須指定兩個搜尋詞彙。 指定的搜尋詞彙可以是由雙引號分隔的一個單字或片語 ("*片語*")。  
  
 您可以將數個相近詞彙鏈結起來，例如：`a NEAR b NEAR c` 或 `a ~ b ~ c`。 鏈結的相近詞彙必須全部都在要傳回之相符項目的文件中。  
  
 例如，`CONTAINS(*column_name*, 'fox NEAR chicken')` 和 `CONTAINSTABLE(*table_name*, *column_name*, 'fox ~ chicken')` 都會在指定的資料行中傳回同時包含 "fox" 和 "chicken" 的任何文件。 此外，CONTAINSTABLE 會根據 "fox" 和 "chicken" 的距離，傳回每個文件的等級。 例如，如果文件包含 "The fox ate the chicken" 這個句子，其排名將會比較高，因為比起其他文件，這些詞彙彼此更接近。  
  
 如需有關一般相近詞彙的詳細資訊，請參閱[使用 NEAR 搜尋接近另一個單字的字詞](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)。  
  
 \<custom_proximity_term>  
**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。
  
 指定單字或片語比對，並選擇性地指定搜尋詞彙之間所允許的最大距離。 您也可以指定搜尋字詞必須依您指定的確切順序 (\<match_order>) 尋找。  
  
 指定的搜尋詞彙可以是由雙引號分隔的一個單字或片語 ("*片語*")。 每個指定的詞彙必須在要傳回之相符項目的文件中。 您必須至少指定兩個搜尋詞彙。 最大搜尋詞彙數目為 64。  
  
 根據預設，不論中間距離，也不論其順序，自訂相近詞彙會傳回包含指定之詞彙的任何資料列。 例如，文件中的任何地方、依任何順序只需要包含 `term1` 和 "`term3 term4`"，就會符合下列查詢：  
  
```sql  
CONTAINS(column_name, 'NEAR(term1,"term3 term4")')  
```  
  
 選擇性參數如下所示：  
  
 \<maximum_distance>  
 指定字串開始及結尾處的搜尋詞彙之間所允許的最大距離，才能讓該字串成為合格的相符項目。  
  
 *integer*  
 指定從 0 到 4294967295 的正整數。 這個值會控制第一個和最後一個搜尋詞彙之間 (排除任何其他指定的搜尋詞彙) 可以出現多少個非搜尋詞彙。  
  
 例如，下列查詢會依任一順序，在五個詞彙的最大距離內搜尋 `AA` 和 `BB`。  
  
```sql  
CONTAINS(column_name, 'NEAR((AA,BB),5)')  
```  
  
 字串 `AA one two three four five BB` 會是相符項目。 在下列範例中，查詢指定在五個詞彙的最大距離內搜尋三個搜尋詞彙，`AA`、`BB` 和 `CC`：  
  
```sql  
CONTAINS(column_name, 'NEAR((AA,BB,CC),5)')  
```  
  
 這個查詢會符合下列字串，其總距離是五個詞彙：  
  
 `BB   one two   CC   three four five A  A`  
  
 請注意到系統不會計算內部搜尋詞彙 `CC`。  
  
 **MAX**  
 不論詞彙之間距離，傳回包含指定之詞彙的任何資料列。 這是預設值。  
  
 \<match_order>  
 指定詞彙是否必須依指定順序出現，才會由搜尋查詢傳回。 若要指定 \<match_order>，您也必須指定 \<maximum_distance>。  
  
 \<match_order> 會採用下列其中一個值：  
  
 **TRUE**  
 強制詞彙內的指定順序。 例如，`NEAR(A,B)` 只符合 `A ... B`。  
  
 **FALSE**  
 略過指定的順序。 例如，`NEAR(A,B)` 符合 `A ... B` 和 `B ... A`。  
  
 這是預設值。  
  
 例如，下列相近詞彙會按照指定順序但不論最大距離來搜尋單字 "`Monday`"、"`Tuesday`" 和 "`Wednesday`"：  
  
```sql  
CONTAINS(column_name, 'NEAR ((Monday, Tuesday, Wednesday), MAX, TRUE)')  
```  
  
 如需使用自訂相近詞彙的詳細資訊，請參閱[使用 NEAR 搜尋接近另一個單字的字詞](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)。  
  
 \<weighted_term>  
 指定相符的資料列 (查詢所傳回) 會符合一份單字和片語清單，每個單字和片語各有其加權值。  
  
 ISABOUT  
 指定 *\<weighted_term>* 關鍵字。  
  
 WEIGHT(*weight_value*)  
 指定加權值，它是 0.0 至 1.0 的數字。 *\<weighted_term>* 中的每個元件都可以包含 *weight_value*。 *weight_value* 是一種可變更查詢的各個部分，以影響已指派給符合該查詢各個資料列之等級值的方法。 WEIGHT 不會影響 CONTAINS 查詢的結果，但 WEIGHT 會影響 [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) 查詢中的等級。  
  
> [!NOTE]  
> 不論作業系統地區設定為何，小數分隔符號一定是句點。  
  
 { AND \| & } \| { AND NOT \| &! } \| { OR \| \| }  
 指定兩個包含搜尋條件之間的邏輯運算。  
  
 { AND \| & }  
 指出相符項目必須符合這兩個包含搜尋條件。 您可以使用 & 符號取代 AND 關鍵字來表示 AND 運算子。  
  
 { AND NOT \| &! }  
 指出相符項目不能有第二個搜尋條件。 您可以使用後面接著驚歎號的 & 符號 (&!) 取代 AND NOT 關鍵字來表示 AND NOT 運算子。  
  
 { OR \| \| }  
 指出相符項目必須符合兩個包含搜尋條件的其中之一。 您可以利用垂直線符號 (|) 取代 OR 關鍵字來表示 OR 運算子。  
  
 當 *\<contains_search_condition>* 包含小括號內的群組時，會先評估這些小括號內的群組。 在評估附加括號的群組之後，當在包含搜尋條件中使用這些邏輯運算子，便適用下列規則：  
  
-   NOT 在 AND 前面套用。  
  
-   NOT 只能在 AND 之後，如同 AND NOT。 不允許 OR NOT 運算子。 不能在第一個詞彙前面指定 NOT。 例如，`CONTAINS (mycolumn, 'NOT "phrase_to_search_for" ' )` 無效。  
  
-   AND 在 OR 前面套用。  
  
-   同類型的 Boolean 運算子 (AND、OR) 是聯合的，因此，套用順序沒有任何限制。  
  
 *n*  
 這是一個預留位置，表示可以指定多個 CONTAINS 搜尋條件及其中的詞彙。  
  
## <a name="general-remarks"></a>一般備註  
 全文檢索述詞與函數會在 FROM 述詞中隱含的單一資料表上處理。 若要在多個資料表上進行搜尋，請使用 FROM 子句中聯結的資料表，在兩個或多個資料表之產品的結果集上進行搜尋。  
  
 當資料庫相容性層級設定為 100 時，[OUTPUT 子句](../../t-sql/queries/output-clause-transact-sql.md) 中不允許使用全文檢索述詞。  
  
## <a name="querying-remote-servers"></a>查詢遠端伺服器  
 您可以在 CONTAINS 或 [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) 述詞中使用四部分名稱，以便在連結的伺服器上查詢目標資料表的全文檢索索引資料行。 若要準備遠端伺服器來接收全文檢索查詢，請針對遠端伺服器上的目標資料表與資料行建立全文檢索索引，然後加入遠端伺服器成為連結的伺服器。  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE 與全文檢索搜尋的比較  
 相較於全文檢索搜尋， [LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 述詞只能針對字元模式運作。 您也無法使用 LIKE 述詞來查詢格式化的二進位資料。 此外，針對大量非結構化文字資料執行 LIKE 查詢的速度會比針對相同資料執行對等全文檢索查詢的速度要慢很多。 對於數百萬列的資料，使用 LIKE 查詢時可能要好幾分鐘才能傳回搜尋結果，但是使用全文檢索查詢時可能只要幾秒鐘的時間 (視傳回的資料列數目及其大小而定)。 另一個考量是 LIKE 只對整個資料表執行簡單模式掃描。 相對地，全文檢索查詢是語言感知，會在索引和查詢時間套用特定轉換，例如篩選停用字詞以及進行同義字和詞形變化的擴充。 這些轉換有助於全文檢索查詢改善其重新叫用及其結果的最終次序。  
  
## <a name="querying-multiple-columns-full-text-search"></a>查詢多個資料行 (全文檢索搜尋)  
 您可以指定要搜尋的資料行清單，來查詢多個資料行。 這些資料行必須來自相同的資料表。  
  
 例如，下列 CONTAINS 查詢會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫 `Production.Product` 資料表的 `Name` 和 `Color` 資料行中搜尋 `Red` 詞彙。  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Name, Color   
FROM Production.Product  
WHERE CONTAINS((Name, Color), 'Red');  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-contains-with-simple_term"></a>A. 搭配 \<simple_term> 使用 CONTAINS  
 下列範例會尋找所有價格是 `$80.99` ，且含有 `Mountain`這個單字的產品。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain');  
GO  
```  
  
### <a name="b-using-contains-and-phrase-with-simple_term"></a>B. 搭配 \<simple_term> 使用 CONTAINS 和片語  
 下列範例會傳回含有 `Mountain` 或 `Road` 片語的所有產品。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' Mountain OR Road ')  
GO  
```  
  
### <a name="c-using-contains-with-prefix_term"></a>C. 搭配 \<prefix_term> 使用 CONTAINS  
 下列範例會傳回所有至少有一個字的開頭是 `Name` 資料行中之前置詞鏈結的產品名稱。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' "Chain*" ');  
GO  
```  
  
### <a name="d-using-contains-and-or-with-prefix_term"></a>D. 搭配 \<prefix_term> 使用 CONTAINS 和 OR  
 下列範例會傳回所有包含前置詞為 `chain` 或 `full` 的字串之類別目錄描述。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, '"chain*" OR "full*"');  
GO  
```  
  
### <a name="e-using-contains-with-proximity_term"></a>E. 搭配 \<proximity_term> 使用 CONTAINS  
  
**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。 
  
 下列範例會在 `Production.ProductReview` 資料表中，於 "`control`" 單字的 10 個詞彙內搜尋包含單字 `bike`，且依據指定順序 (也就是 "`bike`" 需位於 "`control`" 之前) 的所有註解。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments , 'NEAR((bike,control), 10, TRUE)');  
GO  
```  
  
### <a name="f-using-contains-with-generation_term"></a>F. 搭配 \<generation_term> 使用 CONTAINS  
 下列範例會搜尋所有含 `ride` 一字下列各種形式的產品：riding、ridden 等等。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, ' FORMSOF (INFLECTIONAL, ride) ');  
GO  
```  
  
### <a name="g-using-contains-with-weighted_term"></a>G. 搭配 \<weighted_term> 使用 CONTAINS  
 下列範例會搜尋所有包含 `performance`、`comfortable` 或 `smooth` 等字的產品名稱，且每個字都各有不同的加權。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, 'ISABOUT (performance weight (.8),   
comfortable weight (.4), smooth weight (.2) )' );  
GO  
```  
  
### <a name="h-using-contains-with-variables"></a>H. 搭配變數使用 CONTAINS  
 下列範例會利用變數來取代特定搜尋詞彙。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord NVARCHAR(30)  
SET @SearchWord = N'Performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
GO  
```  
  
### <a name="i-using-contains-with-a-logical-operator-and"></a>I. 搭配邏輯運算子 (AND) 使用 CONTAINS  
 下列範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的 ProductDescription 資料表。 此查詢會使用 CONTAINS 述詞來搜尋描述識別碼不等於 5，而且描述同時包含 `Aluminum` 與 `spindle` 這兩個單字的描述。 搜尋條件會使用 AND 布林運算子。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'Aluminum AND spindle');  
GO  
```  
  
### <a name="j-using-contains-to-verify-a-row-insertion"></a>J. 使用 CONTAINS 來確認資料列插入  
 下列範例會在 SELECT 子查詢中使用 CONTAINS。 使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫時，查詢會取得 ProductReview 資料表中特定週期之所有註解的註解值。 搜尋條件會使用 AND 布林運算子。  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Production.ProductReview   
  (ProductID, ReviewerName, EmailAddress, Rating, Comments)   
VALUES  
  (780, 'John Smith', 'john@fourthcoffee.com', 5,   
'The Mountain-200 Silver from AdventureWorks2008 Cycles meets and exceeds expectations. I enjoyed the smooth ride down the roads of Redmond');  
  
-- Given the full-text catalog for these tables is Adv_ft_ctlg,   
-- with change_tracking on so that the full-text indexes are updated automatically.  
WAITFOR DELAY '00:00:30';     
-- Wait 30 seconds to make sure that the full-text index gets updated.  
  
SELECT r.Comments, p.Name  
FROM Production.ProductReview AS r  
JOIN Production.Product AS p   
    ON r.ProductID = p.ProductID  
    AND r.ProductID = (SELECT ProductID  
FROM Production.ProductReview  
WHERE CONTAINS (Comments,   
    ' AdventureWorks2008 AND   
    Redmond AND   
    "Mountain-200 Silver" '));  
GO  
```  
  
### <a name="k-querying-on-a-document-property"></a>K. 在文件屬性上進行查詢  
  
**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。 
  
 下列查詢會在 `Title` 資料表之 `Document` 資料行的 `Production.Document` 索引屬性上進行搜尋。 此查詢只會傳回其 `Title` 屬性包含 `Maintenance` 或 `Repair` 字串的文件。  
  
> [!NOTE]  
>  若要讓屬性搜尋傳回資料列，索引期間剖析資料行的篩選必須擷取指定的屬性。 此外，指定之資料表的全文檢索索引必須已經設定為包含該屬性。 如需詳細資訊，請參閱 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Document 
FROM Production.Document  
WHERE CONTAINS(PROPERTY(Document,'Title'), 'Maintenance OR Repair');  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋使用者入門](../../relational-databases/search/get-started-with-full-text-search.md)   
 [建立及管理全文檢索目錄](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [建立全文檢索搜尋查詢 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-full-text-search-queries-visual-database-tools.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
