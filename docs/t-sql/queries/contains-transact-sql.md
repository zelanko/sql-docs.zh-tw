---
title: "包含 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONTAINS_TSQL
- CONTAINS
dev_langs: TSQL
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
caps.latest.revision: "117"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6c2f2f2f6bca2048ead7dc9565b5338bc2505c8e
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="contains-transact-sql"></a>CONTAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中搜尋單字和片語的精確或模糊 (較不精確) 相符項目、彼此在一定距離之間的單字，或加權相符項目。 CONTAINS 是用於述詞[WHERE 子句](../../t-sql/queries/where-transact-sql.md)的[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT 陳述式來執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]全文檢索搜尋的全文檢索索引資料行包含以字元為基礎的資料類型。  
  
 CONTAINS 可以搜尋下列項目：  
  
-   單字或片語。  
  
-   單字或片語的前置詞。  
  
-   接近另一個單字的單字。  
  
-   從另一個單字變化產生的單字 (如 drive 這個字是 drives、drove、driving 和 driven 等字的變化詞幹)。  
  
-   使用同義字 (Thesaurus) 時，另一個單字的同義字 (Synonym) (例如，"aluminum" 和 "steel" 等字是 "metal" 的同義字)。  
  
 如需所支援的全文檢索搜尋形式的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱[使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)。  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
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
  
## <a name="arguments"></a>引數  
 *column_name*  
 這是在 FROM 子句中指定之資料表全文檢索索引資料行的名稱。 資料行可以是類型**char**， **varchar**， **nchar**， **nvarchar**，**文字**， **ntext**，**映像**， **xml**， **varbinary**，或**varbinary （max)**。  
  
 *column_list*  
 指定兩個或多個以逗號分隔的資料行。 *column_list*必須括在括號。 除非*language_term*指定，則所有資料行的語言*column_list*必須相同。  
  
 \*  
 指定查詢給定的搜尋條件的 FROM 子句中指定的資料表中，搜尋所有全文檢索索引資料行。 CONTAINS 子句中的資料行必須來自包含全文檢索索引的單一資料表。 除非*language_term*指定，則資料表的所有資料行的語言必須相同。  
  
 屬性 ( *column_name* ，'*property_name*')  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 指定要在其上搜尋指定之搜尋條件的文件屬性。  
  
> [!IMPORTANT]  
>  針對查詢傳回任何資料列， *property_name*必須指定搜尋屬性清單的全文檢索索引和全文檢索索引必須包含特定屬性的項目*property_name*。 如需詳細資訊，請參閱 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
 語言*language_term*  
 是用於斷詞、 詞幹分析、 同義字擴充與取代和非搜尋字的語言 (或[停用字詞](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) 移除，因為查詢的一部分。 這個參數是選擇性的。  
  
 如果不同語言的文件當做二進位大型物件 (BLOB) 一起儲存在單一資料行中，給定文件的地區設定識別碼 (LCID) 會判斷要建立其內容索引所使用的語言。 當查詢這類資料行指定語言*language_term*可以增加完全相符的機率。  
  
 *language_term*可以指定為字串、 整數或對應於語言 LCID 的十六進位值。 如果*language_term*指定時，它代表的語言會套用至搜尋條件的所有項目。 如果未指定任何值，就會使用資料行全文檢索語言。  
  
 當指定為字串， *language_term*對應至**別名**中的資料行值[sys.syslanguages &#40;TRANSACT-SQL &#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)相容性檢視。 字串必須括在單引號括住，如 '*language_term*'。 當指定為整數， *language_term*是識別之語言的實際 LCID。 當指定為十六進位值， *language_term* 0x 後面接著 LCID 的十六進位值。 十六進位值不能超出 8 位數，開頭的零也包括在內。  
  
 如果值是雙位元組字集 (DBCS) 格式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將它轉換成 Unicode。  
  
 如果指定的語言無效，或尚未安裝對應於這個語言的資源，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會傳回錯誤。 若要使用的中性語言資源，指定 0x0 *language_term*。  
  
 \<*contains_search_condition*>  
 指定要搜尋的文字*column_name*和比對條件。  
  
*\<contains_search_condition >*是**nvarchar**。 當使用另一個字元資料類型當做輸入時，會發生隱含轉換。 不能使用大型的字串資料類型 nvarchar （max） 和 varchar （max）。 在下列範例中，定義為 `@SearchWord` 的 `varchar(30)` 變數會造成 `CONTAINS` 述詞中的隱含轉換。
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord varchar(30)  
SET @SearchWord ='performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
```  
  
 「 參數探測 」 不適用於跨越轉換，因為使用**nvarchar**以提升效能。 在範例中，宣告`@SearchWord`為`nvarchar(30)`。  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @SearchWord nvarchar(30)  
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
指定符合完整的單字或片語。 "blue berry"、blueberry 和 "Microsoft SQL Server" 都是有效的簡單詞彙範例。 片語應該用雙引號 ("") 括住。 單字在片語必須出現在相同的順序中所指定 *\<contains_search_condition >*濆婞剢謅資料庫資料行。 在單字或片語中搜尋字元並不區分大小寫。 非搜尋字 (或[停用字詞](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)) (例如，，或) 中全文檢索索引資料行不會儲存在全文檢索索引。 如果在單一字的搜尋中使用非搜尋字，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回一則錯誤訊息，指出查詢只包含非搜尋字。 在每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 \Mssql\Binn\FTERef 目錄中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 都併入了一份標準非搜尋字清單。  
  
 系統會忽略標點符號。 因此，`CONTAINS(testing, "computer failure")` 將比對含有此值的資料列："Where is my computer? Failure to find it would be expensive"。 如需有關斷詞工具行為的詳細資訊，請參閱[設定和管理的斷詞工具與字幹分析器搜尋](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
 \<prefix_term>  
 指定符合開頭是指定之文字的單字或片語。 以雙引號括住前置詞彙 ("") 和加上星號 (\*) 結尾的引號前，以便以簡單詞彙為開頭的所有文字之前都指定星號時要比對。 這個子句的指定方式應該如下：`CONTAINS (column, '"text*"')`。 星號符合 (屬於單字或片語中一個或多個根單字) 零個、一個或多個字元。 如果並未用雙引號來分隔文字和星號，述詞便是 `CONTAINS (column, 'text*')`，此時全文檢索搜尋會將星號視為字元，因此，它會搜尋完全相符的 `text*`。 全文檢索引擎不會尋找開頭是星號 (\*) 因為斷詞工具通常會忽略這類字元的字元。  
  
 當 *\<contains >*是片語而言，片語中所包含的每個單字都會被視為個別的前置詞。 因此，指定前置詞彙 "local wine*" 的查詢可能會符合開頭是 "local winery"、"locally wined and dined" 等文字的任何資料列。  
  
 \<generation_term>  
 指定符合「其中所包括的簡單詞彙含有要搜尋的原始單字之各種變化形」的單字。  
  
 INFLECTIONAL  
 在指定的簡單詞彙上，指定所用之特定語言的字幹分析器。 字幹分析器的行為是以每種特定語言的詞幹分析規則來定義的。 中性語言並沒有相關聯的字幹分析器。 系統會利用查詢之資料行的資料行語言來參考所需的字幹分析器。 如果*language_term*指定，則對應到會使用語言的字幹分析器。  
  
 給定 *\<contains >*內 *\<contains >*不會符合名詞和動詞。  
  
 THESAURUS  
 指定使用對應於資料行全文檢索語言或查詢指定之語言的同義字。 最長的模式或模式從 *\<contains >*比對這些同義字並會產生其他詞彙來擴充或取代原始模式。 如果所有或部分找不到相符項目 *\<contains >*，不相符的部分會被視為*contains*。 如需有關全文檢索搜尋同義字的詳細資訊，請參閱[設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)。  
  
 \<generic_proximity_term>  
 指定必須符合要搜尋之文件中的單字或片語。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]我們建議您改用\<c >。  
  
 NEAR | ~  
 指出 NEAR 或 ~ 運算子兩側的單字或片語必須出現在要傳回之相符項目的文件中。 您必須指定兩個搜尋詞彙。 指定的搜尋詞彙可以是一個單字或片語以雙引號分隔 ("*片語*")。  
  
 您可以將數個相近詞彙鏈結起來，例如：`a NEAR b NEAR c` 或 `a ~ b ~ c`。 鏈結的相近詞彙必須全部都在要傳回之相符項目的文件中。  
  
 例如，`CONTAINS(*column_name*, 'fox NEAR chicken')`和`CONTAINSTABLE(*table_name*, *column_name*, 'fox ~ chicken')`會傳回任何文件中包含"fox"和"chicken"的指定資料行。 此外，CONTAINSTABLE 會根據 "fox" 和 "chicken" 的距離，傳回每個文件的等級。 例如，如果文件包含 "The fox ate the chicken" 這個句子，其排名將會比較高，因為比起其他文件，這些詞彙彼此更接近。  
  
 如需有關泛型相近詞彙的詳細資訊，請參閱[搜尋靠近另一個單字使用 NEAR 字](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)。  
  
 \<custom_proximity_term>  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
 指定單字或片語比對，並選擇性地指定搜尋詞彙之間所允許的最大距離。 您也可以指定搜尋詞彙必須位於您指定的正確順序 (\<match_order >)。  
  
 指定的搜尋詞彙可以是一個單字或片語以雙引號分隔 ("*片語*")。 每個指定的詞彙必須在要傳回之相符項目的文件中。 您必須至少指定兩個搜尋詞彙。 最大搜尋詞彙數目為 64。  
  
 根據預設，不論中間距離，也不論其順序，自訂相近詞彙會傳回包含指定之詞彙的任何資料列。 例如，文件中的任何地方、依任何順序只需要包含 `term1` 和 "`term3 term4`"，就會符合下列查詢：  
  
```  
CONTAINS(column_name, 'NEAR(term1,"term3 term4")')  
```  
  
 選擇性參數如下所示：  
  
 \<maximum_distance>  
 指定字串開始及結尾處的搜尋詞彙之間所允許的最大距離，才能讓該字串成為合格的相符項目。  
  
 *integer*  
 指定從 0 到 4294967295 的正整數。 這個值會控制第一個和最後一個搜尋詞彙之間 (排除任何其他指定的搜尋詞彙) 可以出現多少個非搜尋詞彙。  
  
 例如，下列查詢會搜尋搜尋`AA`和`BB`，按照任何順序，在五個最大距離內。  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB),5)')  
```  
  
 字串`AA one two three four five BB`是相符項目。 在下列範例中，查詢會指定三個搜尋詞彙， `AA`， `BB`，和`CC`五個最大距離內：  
  
```  
CONTAINS(column_name, 'NEAR((AA,BB,CC),5)')  
```  
  
 這個查詢會符合下列字串，其總距離是五個詞彙：  
  
 `BB   one two   CC   three four five A  A`  
  
 請注意內部搜尋詞彙， `CC`，就不會計算。  
  
 **MAX**  
 不論詞彙之間距離，傳回包含指定之詞彙的任何資料列。 這是預設值。  
  
 \<match_order>  
 指定詞彙是否必須依指定順序出現，才會由搜尋查詢傳回。 若要指定\<match_order >，您也必須指定\<maximum_distance >。  
  
 \<match_order > 採用下列值之一：  
  
 **TRUE**  
 強制詞彙內的指定順序。 例如，`NEAR(A,B)` 只符合 `A … B`。  
  
 **FALSE**  
 略過指定的順序。 例如，`NEAR(A,B)` 符合 `A … B` 和 `B … A`。  
  
 這是預設值。  
  
 例如，下列相近詞彙會按照指定順序但不論最大距離來搜尋單字 "`Monday`"、"`Tuesday`" 和 "`Wednesday`"：  
  
```  
CONTAINS(column_name, 'NEAR ((Monday, Tuesday, Wednesday), MAX, TRUE)')  
```  
  
 如需有關如何使用自訂相近詞彙的詳細資訊，請參閱[搜尋靠近另一個單字使用 NEAR 字](../../relational-databases/search/search-for-words-close-to-another-word-with-near.md)。  
  
 \<weighted_term>  
 指定相符的資料列 (查詢所傳回) 會符合一份單字和片語清單，每個單字和片語各有其加權值。  
  
 ISABOUT  
 指定 *\<contains >*關鍵字。  
  
 WEIGHT(*weight_value*)  
 指定加權值，它是 0.0 至 1.0 的數字。 在每個元件 *\<contains >*可能包括*weight_value*。 *weight_value*是變更查詢的各個部分如何影響指派給符合查詢的每個資料列的等級值的方式。 權數不會影響 CONTAINS 查詢中，但加權影響陣序規範中的結果[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)查詢。  
  
> [!NOTE]  
>  不論作業系統地區設定為何，小數分隔符號一定是句點。  
  
 { AND | & } | { AND NOT | &! } | { OR | | }   
 指定兩個包含搜尋條件之間的邏輯運算。  
  
 {和 | （& S)}  
 指出相符項目必須符合這兩個包含搜尋條件。 您可以利用 & 符號取代 AND 關鍵字來表示 AND 運算子。  
  
 {而非 | & ！ }  
 指出相符項目不能有第二個搜尋條件。 您可以利用後面接著驚歎號的連字號 (&!) 取代 AND NOT 關鍵字來表示 AND NOT 運算子。  
  
 {或 | |}  
 指出相符項目必須符合兩個包含搜尋條件的其中之一。 您可以利用垂直線符號 (|) 取代 OR 關鍵字來表示 OR 運算子。  
  
 當 *\<contains_search_condition >*包含括號括住的群組，群組會先評估這些附加括號。 在評估附加括號的群組之後，當在包含搜尋條件中使用這些邏輯運算子，便適用下列規則：  
  
-   NOT 在 AND 前面套用。  
  
-   NOT 只能在 AND 之後，如同 AND NOT。 不允許 OR NOT 運算子。 不能在第一個詞彙前面指定 NOT。 例如，`CONTAINS (mycolumn, 'NOT "phrase_to_search_for" ' )` 無效。  
  
-   AND 在 OR 前面套用。  
  
-   同類型的 Boolean 運算子 (AND、OR) 是聯合的，因此，套用順序沒有任何限制。  
  
 *n*  
 這是一個預留位置，表示可以指定多個 CONTAINS 搜尋條件及其中的詞彙。  
  
## <a name="general-remarks"></a>一般備註  
 全文檢索述詞與函數會在 FROM 述詞中隱含的單一資料表上處理。 若要在多個資料表上進行搜尋，請使用 FROM 子句中聯結的資料表，在兩個或多個資料表之產品的結果集上進行搜尋。  
  
 全文檢索述詞中不允許[OUTPUT 子句](../../t-sql/queries/output-clause-transact-sql.md)當資料庫相容性層級設定為 100。  
  
## <a name="querying-remote-servers"></a>查詢遠端伺服器  
 您可以使用四部分名稱中包含或[FREETEXT](../../t-sql/queries/freetext-transact-sql.md)述詞來查詢全文檢索索引連結的伺服器上的目標資料表的資料行。 若要準備遠端伺服器來接收全文檢索查詢，請針對遠端伺服器上的目標資料表與資料行建立全文檢索索引，然後加入遠端伺服器成為連結的伺服器。  
  
## <a name="comparison-of-like-to-full-text-search"></a>LIKE 與全文檢索搜尋的比較  
 相較於全文檢索搜尋，[LIKE](../../t-sql/language-elements/like-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 述詞只能針對字元模式運作。 您也無法使用 LIKE 述詞來查詢格式化的二進位資料。 此外，針對大量非結構化文字資料執行 LIKE 查詢的速度會比針對相同資料執行對等全文檢索查詢的速度要慢很多。 對於數百萬列的資料，使用 LIKE 查詢時可能要好幾分鐘才能傳回搜尋結果，但是使用全文檢索查詢時可能只要幾秒鐘的時間 (視傳回的資料列數目及其大小而定)。 另一個考量是 LIKE 只對整個資料表執行簡單模式掃描。 相對地，全文檢索查詢是語言感知，會在索引和查詢時間套用特定轉換，例如篩選停用字詞以及進行同義字和詞形變化的擴充。 這些轉換有助於全文檢索查詢改善其重新叫用及其結果的最終次序。  
  
## <a name="querying-multiple-columns-full-text-search"></a>查詢多個資料行 (全文檢索搜尋)  
 您可以指定要搜尋的資料行清單，來查詢多個資料行。 這些資料行必須來自相同的資料表。  
  
 例如，下列 CONTAINS 查詢搜尋詞彙`Red`中`Name`和`Color`的資料行`Production.Product`資料表[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]範例資料庫。  
  
```sql  
Use AdventureWorks2012;  
GO  
SELECT Name, Color   
FROM Production.Product  
WHERE CONTAINS((Name, Color), 'Red');  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-contains-with-simpleterm"></a>A. 使用與 CONTAINS \<contains >  
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
  
### <a name="b-using-contains-and-phrase-with-simpleterm"></a>B. 使用 CONTAINS 和具有片語\<contains >  
 下列範例會傳回含有 `Mountain` 或 `Road` 片語的所有產品。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' Mountain OR Road ')  
GO  
```  
  
### <a name="c-using-contains-with-prefixterm"></a>C. 使用與 CONTAINS \<contains >  
 下列範例會傳回所有至少有一個字的開頭是 `Name` 資料行中之前置詞鏈結的產品名稱。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, ' "Chain*" ');  
GO  
```  
  
### <a name="d-using-contains-and-or-with-prefixterm"></a>D. 使用 CONTAINS 和 or 與\<contains >  
 下列範例會傳回所有包含前置詞為 `chain` 或 `full` 的字串之類別目錄描述。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE CONTAINS(Name, '"chain*" OR "full*"');  
GO  
```  
  
### <a name="e-using-contains-with-proximityterm"></a>E. 使用與 CONTAINS \<contains >  
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
 下列範例會搜尋`Production.ProductReview`資料表的所有註解包含單字`bike`單字的 10 個詞彙內"`control`」 和指定的順序 (亦即，其中"`bike`「 之前 」`control`")。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments , 'NEAR((bike,control), 10, TRUE)');  
GO  
```  
  
### <a name="f-using-contains-with-generationterm"></a>F. 使用與 CONTAINS \<contains >  
 下列範例會搜尋所有含 `ride` 一字下列各種形式的產品：riding、ridden 等等。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT Description  
FROM Production.ProductDescription  
WHERE CONTAINS(Description, ' FORMSOF (INFLECTIONAL, ride) ');  
GO  
```  
  
### <a name="g-using-contains-with-weightedterm"></a>G. 使用與 CONTAINS \<contains >  
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
DECLARE @SearchWord nvarchar(30)  
SET @SearchWord = N'Performance'  
SELECT Description   
FROM Production.ProductDescription   
WHERE CONTAINS(Description, @SearchWord);  
GO  
```  
  
### <a name="i-using-contains-with-a-logical-operator-and"></a>I. 搭配邏輯運算子 (AND) 使用 CONTAINS  
 下列範例會使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的 ProductDescription 資料表。 此查詢會使用 CONTAINS 述詞來搜尋所在描述識別碼不等於 5，而且描述同時包含兩個單字`Aluminum`和 word `spindle`。 搜尋條件會使用 AND 布林運算子。  
  
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
  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 
  
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
 [建立全文檢索目錄 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [建立全文檢索搜尋查詢 &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
