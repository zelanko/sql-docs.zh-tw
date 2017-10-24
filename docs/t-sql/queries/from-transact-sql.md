---
title: "從 (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JOIN
- FROM_TSQL
- FROM
- JOIN_TSQL
- CROSS_TSQL
- CROSS_APPLY_TSQL
- APPLY_TSQL
- CROSS_JOIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- OUTER APPLY operator
- hints [SQL Server], FROM clause
- SELECT statement [SQL Server], FROM clause
- ISO syntax
- DELETE statement [SQL Server], FROM clause
- CROSS APPLY operator
- FROM clause
- APPLY operator
- joins [SQL Server], FROM clause
- UPDATE statement [SQL Server], FROM clause
- derived tables
ms.assetid: 36b19e68-94f6-4539-aeb1-79f5312e4263
caps.latest.revision: 97
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 6ae83ccf18cac45339d63e4ce1326c72a58c0339
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="from-transact-sql"></a>FROM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中指定 DELETE、SELECT 和 UPDATE 陳述式中使用的資料表、檢視表、衍生資料表及聯結資料表。 在 SELECT 陳述式中，除非選取清單只包含常數、變數及算術運算式 (無資料行名稱)，否則都需要 FROM 子句。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ FROM { <table_source> } [ ,...n ] ]   
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ]   
        [ <tablesample_clause> ]   
        [ WITH ( < table_hint > [ [ , ]...n ] ) ]   
    | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
    | user_defined_function [ [ AS ] table_alias ]  
    | OPENXML <openxml_clause>   
    | derived_table [ [ AS ] table_alias ] [ ( column_alias [ ,...n ] ) ]   
    | <joined_table>   
    | <pivoted_table>   
    | <unpivoted_table>  
    | @variable [ [ AS ] table_alias ]  
    | @variable.function_call ( expression [ ,...n ] )   
        [ [ AS ] table_alias ] [ (column_alias [ ,...n ] ) ]  
    | FOR SYSTEM_TIME <system_time>   
}  
<tablesample_clause> ::=  
    TABLESAMPLE [SYSTEM] ( sample_number [ PERCENT | ROWS ] )   
        [ REPEATABLE ( repeat_seed ) ]   
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON <search_condition>   
    | <table_source> CROSS JOIN <table_source>   
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
<join_type> ::=   
    [ { INNER | { { LEFT | RIGHT | FULL } [ OUTER ] } } [ <join_hint> ] ]  
    JOIN  
  
<pivoted_table> ::=  
    table_source PIVOT <pivot_clause> [ [ AS ] table_alias ]  
  
<pivot_clause> ::=  
        ( aggregate_function ( value_column [ [ , ]...n ])   
        FOR pivot_column   
        IN ( <column_list> )   
    )   
  
<unpivoted_table> ::=  
    table_source UNPIVOT <unpivot_clause> [ [ AS ] table_alias ]  
  
<unpivot_clause> ::=  
    ( value_column FOR pivot_column IN ( <column_list> ) )   
  
<column_list> ::=  
    column_name [ ,...n ]   
  
<system_time> ::=  
{  
       AS OF <date_time>  
    |  FROM <start_date_time> TO <end_date_time>  
    |  BETWEEN <start_date_time> AND <end_date_time>  
    |  CONTAINED IN (<start_date_time> , <end_date_time>)   
    |  ALL  
}  
  
    <date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <start_date_time>::=  
        <date_time_literal> | @date_time_variable  
  
    <end_date_time>::=  
        <date_time_literal> | @date_time_variable  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
FROM { <table_source> [ ,...n ] }  
  
<table_source> ::=   
{  
    [ database_name . [ schema_name ] . | schema_name . ] table_or_view_name [ AS ] table_or_view_alias  
    | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]  
    | <joined_table>  
}  
  
<joined_table> ::=   
{  
    <table_source> <join_type> <table_source> ON search_condition   
    | <table_source> CROSS JOIN <table_source> 
    | left_table_source { CROSS | OUTER } APPLY right_table_source   
    | [ ( ] <joined_table> [ ) ]   
}  
  
<join_type> ::=   
    [ INNER ] [ <join hint> ] JOIN  
    | LEFT  [ OUTER ] JOIN  
    | RIGHT [ OUTER ] JOIN  
    | FULL  [ OUTER ] JOIN  
  
<join_hint> ::=   
    REDUCE  
    | REPLICATE  
    | REDISTRIBUTE  
```  
  
## <a name="arguments"></a>引數  
\<t >  
 指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中使用的資料表、檢視表、資料表變數或衍生資料表來源 (含有別名或不含別名)。 陳述式中最多只能使用 256 個資料表來源 (雖然這項限制會隨著可用記憶體和查詢中之其他運算式的複雜度而改變)。 個別查詢可能無法支援多達 256 個資料表來源。  
  
> [!NOTE]  
>  如果查詢中參考大量資料表，則可能會降低查詢效能。 編譯和最佳化時間也會受其他因素影響。 這些包括出現的索引和索引檢視表上每個\<t > 的大小和\<select_list > SELECT 陳述式中。  
  
 FROM 關鍵字後面的資料表來源順序不會影響傳回的結果集。 當 FROM 子句中出現重複的名稱時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤。  
  
 *table_or_view_name*  
 這是資料表或檢視表的名稱。  
  
 如果資料表或檢視表存在於相同的執行個體上的另一個資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，表單中使用完整限定的名稱*資料庫*。*結構描述*。*object_name*。  
  
 如果資料表或檢視表存在於執行個體的外部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l，表單中使用四部分名稱*linked_server*。*目錄*。*結構描述*。*物件*。 如需詳細資訊，請參閱 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)的資料。 建構使用四部分名稱[OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md)做為伺服器名稱的一部分也可用來指定遠端資料表來源。 指定 OPENDATASOURCE 時， *database_name*和*schema_name*可能不適用於所有資料來源而且受限於存取遠端物件的 OLE DB 提供者的功能。  
  
 [AS]*table_alias*  
 是的別名*t*為了方便起見，或為區分資料表或檢視中的自我聯結或子查詢可使用。 別名通常是一個縮短的資料表名稱，可用來參考聯結中之資料表的特定資料行。 如果相同的資料行名稱存在於聯結中的多個資料表中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會要求資料行名稱必須被資料表名稱、檢視表名稱或別名所限定。 如果已定義別名，就不能使用資料表名稱。  
  
 使用衍生的資料表、 資料列集或資料表值函式或運算子子句 （如 PIVOT 或 UNPIVOT） 時，所需*table_alias*子句結尾是所有資料行，包括群組作業資料行相關聯的資料表名稱傳回。  
  
 使用 (\<table_hint >)  
 指定查詢最佳化工具必須搭配這份資料表，並針對這個陳述式來使用最佳化或鎖定策略。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 *rowset_function*  

**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 指定資料列集函數之一 (如 OPENROWSET)，利用該函數來傳回可使用的物件，而不是傳回資料表參考。 資料列集函數的清單的相關資訊，請參閱[資料列集函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md).  
  
 使用 OPENROWSET 和 OPENQUERY 函數來指定遠端物件時，主要取決於存取此物件之 OLE DB 提供者的功能。  
  
 *bulk_column_alias*  

**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 這是一個用以取代結果集中之資料行名稱的選擇性別名。 資料行別名只能用在搭配 BULK 選項使用 OPENROWSET 函數的 SELECT 陳述式中。 當您使用*bulk_column_alias*，指定檔案中的資料行的相同順序的每個資料表資料行的別名。  
  
> [!NOTE]  
>  這個別名會覆寫 XML 格式檔之 COLUMN 元素中的 NAME 屬性。  
  
 *user_defined_function*  
 指定資料表值函式。  
  
 OPENXML \<openxml_clause >  

**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 透過 XML 文件提供資料列集的檢視。 如需詳細資訊，請參閱[OPENXML &#40;TRANSACT-SQL &#41;](../../t-sql/functions/openxml-transact-sql.md).  
  
 *derived_table*  
 這是從資料庫中擷取資料列的子查詢。 *derived_table*用做為外部查詢的輸入。  
  
 *衍生* *_table*可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]資料表值建構函式功能，來指定多個資料列。 例如， `SELECT * FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);`。 如需詳細資訊，請參閱[資料表值建構函式 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 *column_alias*  
 這是一個用以取代衍生資料表結果集中之資料行名稱的選擇性別名。 選取清單中的每個資料行都包含一個資料行別名，且會利用括號包住資料行別名的完整清單。  
  
 *table_or_view_name* FOR SYSTEM_TIME \<system_time >  

**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 指定特定版本的資料會傳回從指定的時態表和其連結的系統建立版本歷程記錄資料表  
  
\<tablesample_clause >  
 指定必須從資料表傳回資料範例。 該範例可能只是近似資料。 這個子句可用於 SELECT、UPDATE 或 DELETE 陳述式中的任何主要或聯結資料表。 TABLESAMPLE 不能利用檢視表來指定。  
  
> [!NOTE]  
>  當您針對升級到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料庫使用 TABLESAMPLE 時，而且資料庫的相容性層級設定為 110 或更高層級，則遞迴通用資料表運算式 (CTE) 查詢中不允許 PIVOT。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
 SYSTEM  
 這是 ISO 標準所指定之依實作方式而定的取樣方法。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這是唯一的可用取樣方法，而且預設會採用這種方法。 SYSTEM 採用頁面型取樣方法，這種方法會從資料表中為範例選擇一組隨機頁面，然後將這些頁面上的所有資料列當做範例子集傳回。  
  
 *sample_number*  
 這是用以代表資料列之百分比或數目的精確或近似常數數值運算式。 當利用 PERCENT，指定*sample_number*隱含地轉換成**float**值; 否則它會轉換為**bigint**。 PERCENT 是預設值。  
  
 PERCENT  
 指定*sample_number*應該從資料表中擷取資料表資料列的百分比。 當指定 PERCENT 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回所指定之百分比的近似值。 當指定 PERCENT 時*sample_number*運算式必須評估為值從 0 到 100。  
  
 ROWS  
 指定近似之*sample_number*將擷取的資料列。 當指定 ROWS 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回所指定之資料列數的近似值。 當指定 ROWS 時， *sample_number*運算式必須評估為整數值小於或等於零。  
  
 REPEATABLE  
 指出所選範例可以重新傳回。 當指定的相同*repeat_seed*值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，只要資料表中的所有資料列尚未進行任何變更將會傳回相同的資料列子集。 當指定使用不同*repeat_seed*值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有可能會傳回資料表中的資料列的不同取樣。 對資料表執行的下列動作均視為變更：插入、更新、刪除、索引重建或重新組織，以及資料庫還原或附加。  
  
 *repeat_seed*  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為了產生隨機數字所使用的常數整數運算式。 *repeat_seed*是**bigint**。 如果*repeat_seed*未指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會隨機指派一個值。 針對特定*repeat_seed*值，取樣結果一律會相同如果資料表已不套用任何變更。 *Repeat_seed*運算式必須評估為大於零的整數。  
  
 \<joined_table >  
 這是兩個或兩個以上的資料表所產生的結果集。 如果是多個聯結，請利用括號來變更聯結的自然順序。  
  
\<join_type >  
 指定聯結動作的類型。  
  
 **內部**  
 指定必須傳回所有相符的資料列配對。 捨棄兩份資料表中不相符的資料列。 如果未指定聯點類型，這就是預設值。  
  
 FULL [ OUTER ]  
 指定左資料表或右資料表中不符合聯結條件的資料列必須併入結果集中，且對應於其他資料表的輸出資料行必須設為 NULL。 這是通常由 INNER JOIN 傳回之所有資料列以外的項目。  
  
 LEFT [ OUTER ]  
 指定左資料表中不符合聯結條件的所有資料列必須併入結果集中，而且，除了內部聯結所傳回的所有資料列以外，還必須將其他資料表中的輸出資料行設為 NULL。  
  
 RIGHT [OUTER]  
 指定右資料表中不符合聯結條件的所有資料列必須併入結果集中，而且，除了內部聯結所傳回的所有資料列以外，還必須將對應於其他資料表的輸出資料行設為 NULL。  
  
\<join_hint >  
 如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查詢最佳化工具使用一個聯結提示或執行演算法，每個查詢的 FROM 子句中指定的聯結。 如需詳細資訊，請參閱[聯結提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql-join.md).  
  
 如[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，這些聯結提示套用至兩個與通訊群組不相容的資料行上的 INNER 聯結。 它們可以改善查詢效能，藉由限制的查詢處理期間發生的資料移動量。 允許的聯結提示的[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]如下：  
  
 減少  
 會減少資料表聯結的右邊移動才能讓兩個散發相容資料表相容的資料列數目。 REDUCE 提示也稱為半聯結提示。  
  
 REPLICATE  
 會使的聯結資料行中要複寫到所有節點之聯結左側資料表中的值。 在右側資料表已加入至複寫版本的這些資料行。  
  
 轉散發  
 強制兩個資料來源，以聯結子句中指定的資料行散發。 分散式資料表[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會隨機移動。 針對複寫的資料表，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會修剪移動。 若要了解這些移動型別，請參閱 < DMS 查詢計劃作業 > 主題中的區段 > 的 < 了解查詢計畫中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。 查詢計劃使用廣播的移動解決發佈不相容的聯結時，這個提示可改善效能。  
  
 JOIN  
 指出所指定的聯結作業必須發生在所指定的資料表來源或檢視表之間。  
  
 ON \<s >  
 指定聯結所根據的條件。 條件可以指定任何述詞 (雖然通常都是使用資料行和比較運算子)，例如：  
  
```tsql
SELECT p.ProductID, v.BusinessEntityID  
FROM Production.Product AS p   
JOIN Purchasing.ProductVendor AS v  
ON (p.ProductID = v.ProductID);  
  
```  
  
 當條件指定資料行時，這些資料行不必有相同的名稱或相同的資料類型；不過，如果資料類型不同，它們必須相容的類型或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以利用隱含方式轉換的類型。 如果資料類型無法利用隱含方式轉換，條件必須藉由 CONVERT 函數，利用明確方式轉換資料類型。  
  
 ON 子句中可以有僅涉及其中一個聯結資料表的述詞。 這類述詞也可以在查詢的 WHERE 子句中。 雖然這類述詞的放置不會影響 INNER 聯結，不過，如果涉及 OUTER 聯結，就可能會造成不同的結果。 這是因為 ON 子句中的述詞會套用至聯結之前的資料表，但在語意上，WHERE 子句則套用至聯結的結果。  
  
 如需有關搜尋條件和述詞的詳細資訊，請參閱[搜尋條件 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CROSS JOIN  
 指定兩個資料表的交叉乘積。 所傳回的資料列與舊式非 SQL-92 樣式聯結中不指定任何 WHERE 子句時所傳回的資料列相同。  
  
 *left_table_source* {跨 |外部} 套用*right_table_source*  
 指定*right_table_source*是 APPLY 運算子會針對每個資料列的評估*left_table_source*。 此功能會很有用時*right_table_source*包含接受資料行值的資料表值函式*left_table_source*做為其中一個引數。  
  
 必須利用 APPLY 指定 CROSS 或 OUTER。 當指定 CROSS 時，會產生任何資料列時*right_table_source*就會根據指定的資料列的評估*left_table_source*並傳回空的結果集。  
  
 當指定 OUTER 時，每個資料列產生一個資料列*left_table_source*即使*right_table_source*評估針對該資料列，並傳回空的結果集。  
  
 如需詳細資訊，請參閱＜備註＞一節。  
  
 *left_table_source*  
 這是資料表來源，如前一個引數所定義的一樣。 如需詳細資訊，請參閱＜備註＞一節。  
  
 *right_table_source*  
 這是資料表來源，如前一個引數所定義的一樣。 如需詳細資訊，請參閱＜備註＞一節。  
  
 *t* PIVOT \<pivot_clause >  
 指定*t*樞紐根據*pivot_column*。 *t*是資料表或資料表運算式。 輸出是包含的所有資料行的資料表*t*除了*pivot_column*和*value_column*。 資料行*t*，除了*pivot_column*和*value_column*，稱為樞紐運算子的群組資料行。 如需 PIVOT 和 UNPIVOT 的詳細資訊，請參閱[使用 PIVOT 和 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)。  
  
 PIVOT 會對與群組作業資料行相關的輸入資料表執行群組作業，並為每個群組傳回一個資料列。 此外，輸出會包含每個值中指定的一個資料行*column_list* ，會出現在*pivot_column*的*input_table*。  
  
 如需詳細資訊，請參閱稍後的＜備註＞一節。  
  
 *aggregate_function*  
 為接受一個或多個輸入的系統或使用者定義的彙總函式。 該彙總函式對 Null 值必須是不變的。 對 Null 值不變的彙總函式在評估彙總值時，不會考量群組中的 Null 值。  
  
 不允許使用 COUNT(*) 系統彙總函式。  
  
 *value_column*  
 這是 PIVOT 運算子的值資料行。 當搭配 UNPIVOT 使用時， *value_column*不能在輸入中的現有資料行名稱*t*。  
  
 如*pivot_column*  
 這是 PIVOT 運算子的樞紐資料行。 *pivot_column*必須是隱含或明確地轉換為型別**nvarchar()**。 此資料行不能**映像**或**rowversion**。  
  
 當使用 UNPIVOT 時， *pivot_column*是指從輸出資料行名稱*t*。 不能有現有的資料行中*t*具有該名稱。  
  
 IN (*column_list* )  
 在 PIVOT 子句中，清單中的值*pivot_column*中會成為輸出資料表的資料行名稱。 清單不能指定在輸入中的任何資料行名稱已經存在於*t* ，要進行樞紐作業。  
  
 在 UNPIVOT 子句中，清單中的資料行*t*會縮短為單一*pivot_column*。  
  
 *table_alias*  
 這是輸出資料表的別名名稱。 *pivot_table_alias*必須指定。  
  
 UNPIVOT \< unpivot_clause >  
 指定輸入的資料表會從多個資料行中縮小*column_list*插入單一資料行稱為*pivot_column*。 如需 PIVOT 和 UNPIVOT 的詳細資訊，請參閱[使用 PIVOT 和 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)。  
  
 從\<日期 _ 時間 >  

**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 傳回含有每個資料列單一記錄的資料表，內含的值在過去的指定時間點為實際 (目前)。 就內部而言，時態表和其歷程記錄資料表之間執行等位，並將結果篩選為傳回的值所指定的時間點上有效的資料列中*\<日期 _ 時間 >*參數。 資料列的值會被視為有效如果*system_start_time_column_name*值小於或等於*\<日期 _ 時間 >*參數值和*system_end_time_column_name*值大於*\<日期 _ 時間 >*參數值。   
  
 從\<開始日期時間 > TO\<結束日期時間 >

**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。

  
 傳回資料表，其中指定的時間範圍內，不論其是否正在使用中之前的作用中的所有記錄版本值*\<開始日期時間 >* FROM 的參數值引數，或不在作用中後*\<結束日期時間 >* TO 引數的參數值。 就內部而言，時態表和其歷程記錄資料表之間會執行等位，且會將結果篩選為傳回所有資料列版本的值，該值在指定的時間範圍任何時間點內皆為作用中。 會併入變得較低的恰好在 FROM 端點所定義在使用中的資料列而變成右上恰好在 TO 端點所定義在使用中狀態的資料列不包含。  
  
 之間\<開始日期時間 > AND\<結束日期時間 >  

**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 如同上方**FROM\<開始日期時間 > TO\<結束日期時間 >**描述，但它包含資料列變為作用中所定義的上限\<結束日期時間 >端點。  
  
 在 CONTAINED IN (\<開始日期時間 >，\<結束日期時間 >)  

**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  

  
 傳回資料表，其中內含所有記錄版本的值，該值在 CONTAINED IN 引數兩個日期時間值所定義的指定時間範圍內為開啟及關閉。 包含恰好在範圍下限變為作用中的資料列，或是恰好在範圍上限就不在作用中的資料列。  
  
 ALL  
 從目前的資料表和記錄資料表的所有資料列會傳回資料表，其中的值。  
  
## <a name="remarks"></a>備註  
 FROM 子句支援聯結資料表和衍生資料表的 SQL-92-SQL 語法。 SQL-92 語法提供 INNER、LEFT OUTER、RIGHT OUTER、FULL OUTER 及 CROSS 聯結運算子。  
  
 在檢視表內的衍生資料表和子查詢中，都支援 FROM 子句內的 UNION 和 JOIN。  
  
 自我聯結是指一份聯結至本身的資料表。 以自我聯結為基礎的插入或更新作業會遵照 FROM 子句中的順序。  
  
 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會考量提供資料行散發統計資料之連結伺服器的散發和基數統計資料，所以並不需要利用 REMOTE 聯結提示，從遠端強制評估聯結。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢處理器會考量遠端統計資料，然後判斷遠端聯結策略是否適當。 對於不提供資料行散發統計資料的提供者而言，REMOTE 聯結提示是很有用處的。  
  
## <a name="using-apply"></a>使用 APPLY  
 APPLY 運算子的左運算元和右運算元都是資料表運算式。 這些運算元之間的主要差異在於*right_table_source*可以使用會採用資料行從資料表值函式*left_table_source*做為其中一個函式的引數。 *Left_table_source*可以包含資料表值函式，但它不能包含的資料行的引數*right_table_source*。  
  
 APPLY 運算子利用下列方式來產生 FROM 子句的資料表來源：  
  
1.  評估*right_table_source*針對每個資料列的*left_table_source*來產生資料列集。  
  
     中的值*right_table_source*相依於*left_table_source*。 *right_table_source*可以表示近似以下的方式： `TVF(left_table_source.row)`，其中`TVF`是資料表值函式。  
  
2.  每個資料列評估之產生的結果集的結合*right_table_source*與*left_table_source*執行 UNION ALL 運算的方式。  
  
     APPLY 運算子的結果所產生的資料行的清單是從資料行集中*left_table_source*結合資料行清單*right_table_source*。  
  
## <a name="using-pivot-and-unpivot"></a>使用 PIVOT 和 UNPIVOT  
 *Pivot_column*和*value_column*是 PIVOT 運算子所使用的群組資料行。 PIVOT 會遵照下列處理序來取得輸出結果集：  
  
1.  GROUP BY 對其*input_table*對群組資料行，並且產生一個輸出資料列的每個群組。  
  
     群組中的資料行資料列的輸出取得該群組中的對應資料行值*input_table*。  
  
2.  執行下列作業，在每個輸出資料列的資料行清單中產生資料行的值：  
  
    1.  此外分組在 GROUP BY 對前一個步驟中產生的資料列*pivot_column*。  
  
         每個輸出資料行中*column_list*，選取符合條件的子群組：  
  
         `pivot_column = CONVERT(<data type of pivot_column>, 'output_column')`  
  
    2.  *aggregate_function*評估*value_column*這個子群組，且其結果會做為對應的值傳回*output_column*。 如果子群組是空的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生 null 值的*output_column*。 如果彙總函式是 COUNT，且子群組是空的，就會傳回零 (0)。  

> [!NOTE]
> 中的資料行識別碼`UNPIVOT`子句依照目錄定序。 如[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，定序一律為`SQL_Latin1_General_CP1_CI_AS`。 如[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]部分自主的資料庫，定序一律為`Latin1_General_100_CI_AS_KS_WS_SC`。 如果資料行就會結合其他資料行，然後 collate 子句 (`COLLATE DATABASE_DEFAULT`) 才能避免衝突。   
  
 如需 PIVOT 和 UNPIVOT 包括範例的詳細資訊，請參閱[使用 PIVOT 和 UNPIVOT](../../t-sql/queries/from-using-pivot-and-unpivot.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 DELETE、SELECT 或 UPDATE 陳述式的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-a-simple-from-clause"></a>A. 使用簡單的 FROM 子句  
 下列範例從 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫的 `TerritoryID` 資料表中擷取 `Name` 和 `SalesTerritory` 資料行。  
  
```tsql    
SELECT TerritoryID, Name  
FROM Sales.SalesTerritory  
ORDER BY TerritoryID ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
TerritoryID Name                            
----------- ------------------------------  
1           Northwest                       
2           Northeast                       
3           Central                         
4           Southwest                       
5           Southeast                       
6           Canada                          
7           France                          
8           Germany                         
9           Australia                       
10          United Kingdom                  
(10 row(s) affected)  
```  
  
### <a name="b-using-the-tablock-and-holdlock-optimizer-hints"></a>B. 使用 TABLOCK 和 HOLDLOCK 最佳化工具提示  
 下列部分交易顯示如何將明確共用資料表鎖定放在 `Employee` 上，以及如何讀取索引。 整個交易從頭到尾都會保留鎖定。  
  
```tsql    
BEGIN TRAN  
SELECT COUNT(*)   
FROM HumanResources.Employee WITH (TABLOCK, HOLDLOCK) ;  
```  
  
### <a name="c-using-the-sql-92-cross-join-syntax"></a>C. 使用 SQL-92 CROSS JOIN 語法  
 下列範例傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中 `Employee` 和 `Department` 這兩個資料表的交叉乘積。 所有可能組合的清單`BusinessEntityID`資料列與所有`Department`會傳回名稱的資料列。  
  
```wql    
SELECT e.BusinessEntityID, d.Name AS Department  
FROM HumanResources.Employee AS e  
CROSS JOIN HumanResources.Department AS d  
ORDER BY e.BusinessEntityID, d.Name ;  
```  
  
### <a name="d-using-the-sql-92-full-outer-join-syntax"></a>D. 使用 SQL-92 FULL OUTER JOIN 語法  
 下列範例傳回產品名稱和 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的 `SalesOrderDetail` 資料表中所有相對應的銷售訂單。 它也傳回未在 `Product` 資料表中列出產品的所有銷售訂單，並傳回含有不同於 `Product` 資料表所列銷售訂單之銷售訂單的所有產品。  
  
```tsql  
-- The OUTER keyword following the FULL keyword is optional.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
FULL OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="e-using-the-sql-92-left-outer-join-syntax"></a>E. 使用 SQL-92 LEFT OUTER JOIN 語法  
 下列範例聯結 `ProductID` 上的兩份資料表，並保留左資料表中不相符的資料列。 在每一份資料表中，`Product` 資料表與 `SalesOrderDetail` 資料行上的 `ProductID` 資料表相符。 所有產品 (已訂購或未訂購) 都會出現在結果集中。  
  
```tsql    
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
LEFT OUTER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="f-using-the-sql-92-inner-join-syntax"></a>F. 使用 SQL-92 INNER JOIN 語法  
 下列範例傳回所有產品名稱和銷售訂單識別碼。  
  
```tsql    
-- By default, SQL Server performs an INNER JOIN if only the JOIN   
-- keyword is specified.  
SELECT p.Name, sod.SalesOrderID  
FROM Production.Product AS p  
INNER JOIN Sales.SalesOrderDetail AS sod  
ON p.ProductID = sod.ProductID  
ORDER BY p.Name ;  
```  
  
### <a name="g-using-the-sql-92-right-outer-join-syntax"></a>G. 使用 SQL-92 RIGHT OUTER JOIN 語法  
 下列範例聯結 `TerritoryID` 上的兩份資料表，並保留與右資料表中不相符的資料列。 在每一份資料表中，`SalesTerritory` 資料表與 `SalesPerson` 資料行上的 `TerritoryID` 資料表相符。 所有的銷售員都會出現在結果集中 (不論是否已指派地區給這些銷售員)。  
  
```tsql    
SELECT st.Name AS Territory, sp.BusinessEntityID  
FROM Sales.SalesTerritory AS st   
RIGHT OUTER JOIN Sales.SalesPerson AS sp  
ON st.TerritoryID = sp.TerritoryID ;  
```  
  
### <a name="h-using-hash-and-merge-join-hints"></a>H. 使用 HASH 和 MERGE 聯結提示  
 下列範例從 `Product`、`ProductVendor` 及 `Vendor` 資料表中執行三資料表聯結，來產生產品及其供應商的清單。 查詢最佳化工具利用 MERGE 聯結來聯結 `Product` 和 `ProductVendor` ( `p` 和 `pv` )。 接著，再利用 HASH 聯結將 `Product` 和 `ProductVendor` MERGE 聯結 (`p` 和 `pv`) 的結果聯結至所要產生的 `Vendor` 資料表 (`p` 和 `pv`) 及 `v`。  
  
> [!IMPORTANT]  
>  指定聯結提示之後，INNER 關鍵字就不再是選擇性質，而是必須針對要執行的 INNER JOIN 加以明確陳述。  
  
```tsql    
SELECT p.Name AS ProductName, v.Name AS VendorName  
FROM Production.Product AS p   
INNER MERGE JOIN Purchasing.ProductVendor AS pv   
ON p.ProductID = pv.ProductID  
INNER HASH JOIN Purchasing.Vendor AS v  
ON pv.BusinessEntityID = v.BusinessEntityID  
ORDER BY p.Name, v.Name ;  
```  
  
### <a name="i-using-a-derived-table"></a>I. 使用衍生資料表  
 下列範例會利用衍生資料表 ( `SELECT` 子句後面的 `FROM` 陳述式) 來傳回所有員工的名字和姓氏，以及員工所居住的城市。  
  
```tsql    
SELECT RTRIM(p.FirstName) + ' ' + LTRIM(p.LastName) AS Name, d.City  
FROM Person.Person AS p  
INNER JOIN HumanResources.Employee e ON p.BusinessEntityID = e.BusinessEntityID   
INNER JOIN  
   (SELECT bea.BusinessEntityID, a.City   
    FROM Person.Address AS a  
    INNER JOIN Person.BusinessEntityAddress AS bea  
    ON a.AddressID = bea.AddressID) AS d  
ON p.BusinessEntityID = d.BusinessEntityID  
ORDER BY p.LastName, p.FirstName;  
```  
  
### <a name="j-using-tablesample-to-read-data-from-a-sample-of-rows-in-a-table"></a>J. 利用 TABLESAMPLE，從資料表的資料列樣本中讀取資料  
 下列範例會利用 `TABLESAMPLE` 子句中的 `FROM` 來傳回 `10` 資料表中大約百分之 `Customer` 的所有資料列。  
  
```tsql    
SELECT *  
FROM Sales.Customer TABLESAMPLE SYSTEM (10 PERCENT) ;  
```  
  
### <a name="k-using-apply"></a>K. 使用 APPLY  
 下列範例假設資料庫中存在含有下列結構描述的下列資料表：  
  
-   `Departments`: `DeptID`, `DivisionID`, `DeptName`, `DeptMgrID`  
  
-   `EmpMgr`: `MgrID`, `EmpID`  
  
-   `Employees`: `EmpID`, `EmpLastName`, `EmpFirstName`, `EmpSalary`  
  
 另外還有一個資料表值函式 `GetReports(MgrID)`，它會傳回所有員工的清單 ( `EmpID`、`EmpLastName`、`EmpSalary` - 這些項目會直接或間接向指定的 `MgrID` 報告)。  
  
 這個範例利用 `APPLY` 來傳回所有部門和各部門中的所有員工。 如果某特定部門沒有員工，就不會針對該部門傳回任何資料列。  
  
```tsql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d CROSS APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
 如果您想讓查詢產生沒有員工的部門資料列 (這些資料列會針對 `EmpID`、`EmpLastName` 及 `EmpSalary` 資料行產生 Null 值)，請改用 `OUTER APPLY`。  
  
```tsql
SELECT DeptID, DeptName, DeptMgrID, EmpID, EmpLastName, EmpSalary  
FROM Departments d OUTER APPLY dbo.GetReports(d.DeptMgrID) ;  
```  
  
### <a name="l-using-cross-apply"></a>L. 使用 CROSS APPLY  
 下列範例會查詢 `sys.dm_exec_cached_plans` 動態管理檢視來擷取快取中所有查詢計畫的計畫控制代碼，藉以擷取位於計畫快取中所有查詢計畫的快照集。 然後，指定 `CROSS APPLY` 運算子，以便將計畫控制代碼傳遞給 `sys.dm_exec_query_plan`。 目前在計畫快取中的每項計畫之 XML 顯示計畫輸出，都是在傳回的資料表之 `query_plan` 資料行中。  
  
```tsql
USE master;  
GO  
SELECT dbid, object_id, query_plan   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);   
GO  
```  
  
### <a name="m-using-for-systemtime"></a>M. 使用 FOR SYSTEM_TIME  
  
**適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 下列範例會傳回資料表的資料列已從 2014 年 1 月 1 日開始的實際 （目前） 使用 FOR SYSTEM_TIME AS OF date_time_literal_or_variable 引數。  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME AS OF '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 下列範例會使用 date_time_literal_or_variable 引數以 FOR SYSTEM_TIME FROM date_time_literal_or_variable 傳回皆為作用中期間定義為 2013 年 1 月 1 日開始，並以 2014 年 1 月 1 日結束的所有資料列不包括上限。  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM '2013-01-01' TO '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 下列範例會使用 FOR SYSTEM_TIME 之間 date_time_literal_or_variable 和 date_time_literal_or_variable 引數，以傳回所有資料列，皆為作用中定義為 2013 年 1 月 1 日開始，並以 2014 年 1 月 1 日結束的期間內含的上限。  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME BETWEEN '2013-01-01' AND '2014-01-01'  
WHERE ManagerID = 5;
```  
  
 下列範例會使用 FOR SYSTEM_TIME CONTAINED IN （date_time_literal_or_variable、 date_time_literal_or_variable） 引數傳回為開啟及關閉定義為 2013 年 1 月 1 日開始，並以結束期間的所有資料列2014 年 1 月 1日日。  
  
```tsql
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME CONTAINED IN ( '2013-01-01', '2014-01-01' )  
WHERE ManagerID = 5;
```  
  
 下列範例會使用變數，而不是常值來提供日期界限值的查詢。  
  
```tsql
DECLARE @AsOfFrom datetime2 = dateadd(month,-12, sysutcdatetime());
DECLARE @AsOfTo datetime2 = dateadd(month,-6, sysutcdatetime());
  
SELECT DepartmentNumber,   
    DepartmentName,   
    ManagerID,   
    ParentDepartmentNumber   
FROM DEPARTMENT  
FOR SYSTEM_TIME FROM @AsOfFrom TO @AsOfTo  
WHERE ManagerID = 5;
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="n-using-the-inner-join-syntax"></a>N. 使用 INNER JOIN 語法  
 下列範例會傳回`SalesOrderNumber`， `ProductKey`，和`EnglishProductName`中的資料行`FactInternetSales`和`DimProduct`資料表 where 聯結索引鍵， `ProductKey`，比對兩個資料表中。 `SalesOrderNumber`和`EnglishProductName`個資料行中存在其中一個資料表，所以不需要使用這些資料行中，指定資料表別名，所顯示，則這些別名會包含為提高可讀性。 Word **AS**之前別名名稱不需要但建議為了可讀性，以及符合 ANSI 標準。  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
INNER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 因為`INNER`關鍵字不內部聯結的必要的這個相同的查詢可以寫成：  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
ON dp.ProductKey = fis.ProductKey;  
```  
  
 A`WHERE`子句也可用於與此查詢限制傳回的結果。 此範例中將結果限制為`SalesOrderNumber`高於 'SO5000' 的值：  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey  
WHERE fis.SalesOrderNumber > 'SO50000'  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="o-using-the-left-outer-join-and-right-outer-join-syntax"></a>O. 使用 LEFT OUTER JOIN 和 RIGHT OUTER JOIN 語法  
 下列範例聯結`FactInternetSales`和`DimProduct`資料表上`ProductKey`資料行。 左方外部聯結語法保留不相符的資料列，從左邊 (`FactInternetSales`) 資料表。 因為`FactInternetSales`資料表不包含任何`ProductKey`值不符合`DimProduct`資料表，此查詢會傳回第一個內部聯結上述範例中為相同的資料列。  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM FactInternetSales AS fis 
LEFT OUTER JOIN DimProduct AS dp  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 此查詢也可以寫入不含`OUTER`關鍵字。  
  
 在右方外部聯結中，從右側資料表不符的資料列都會保留下來。 下列範例會傳回左方外部聯結上述範例中為相同的資料列。  
  
```tsql
-- Uses AdventureWorks  
  
SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
FROM DimProduct AS dp 
RIGHT OUTER JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
 下列查詢會使用`DimSalesTerritory`與左側資料表中左外部聯結的資料表。 它會擷取`SalesOrderNumber`值從`FactInternetSales`資料表。 如果沒有針對特定訂單`SalesTerritoryKey`，查詢會傳回 NULL`SalesOrderNumber`該資料列。 此查詢依據排序`SalesOrderNumber`資料行，以便將任何此資料行中的 Null 將會出現在結果的頂端。  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
LEFT OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 此查詢可以改寫右方外部聯結來擷取相同的結果：  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM FactInternetSales AS fis 
RIGHT OUTER JOIN DimSalesTerritory AS dst  
    ON fis.SalesTerritoryKey = dst.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="p-using-the-full-outer-join-syntax"></a>P. 使用 FULL OUTER JOIN 語法  
 下列範例會示範完整外部聯結中，這兩個聯結的資料表傳回所有資料列，但從另一個資料表不相符的值會傳回 NULL。  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL OUTER JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
 此查詢也可以寫入不含`OUTER`關鍵字。  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, dst.SalesTerritoryRegion, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
FULL JOIN FactInternetSales AS fis  
    ON dst.SalesTerritoryKey = fis.SalesTerritoryKey  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="q-using-the-cross-join-syntax"></a>Q. 使用 CROSS JOIN 語法  
 下列範例會傳回的交叉乘積`FactInternetSales`和`DimSalesTerritory`資料表。 所有可能組合的清單`SalesOrderNumber`和`SalesTerritoryKey`會傳回。 請注意如果沒有`ON`交叉聯結查詢中的子句。  
  
```tsql
-- Uses AdventureWorks  
  
SELECT dst.SalesTerritoryKey, fis.SalesOrderNumber  
FROM DimSalesTerritory AS dst 
CROSS JOIN FactInternetSales AS fis  
ORDER BY fis.SalesOrderNumber;  
```  
  
### <a name="r-using-a-derived-table"></a>R. 使用衍生資料表  
 下列範例會使用衍生的資料表 (`SELECT`之後的陳述式`FROM`子句) 來傳回`CustomerKey`和`LastName`中所有客戶的資料行`DimCustomer`資料表具有`BirthDate`值晚於年 1 月 1 日從 1970年和姓氏 'smith ' 距離。  
  
```tsql
-- Uses AdventureWorks  
  
SELECT CustomerKey, LastName  
FROM  
   (SELECT * FROM DimCustomer  
    WHERE BirthDate > '01/01/1970') AS DimCustomerDerivedTable  
WHERE LastName = 'Smith'  
ORDER BY LastName;  
```  
  
### <a name="s-reduce-join-hint-example"></a>S. 減少聯結提示範例  
 下列範例會使用`REDUCE`改變查詢中的衍生資料表的處理聯結提示。 當使用`REDUCE`聯結提示，在此查詢中，`fis.ProductKey`投影、 複寫和進行不同，，然後加入至`DimProduct`期間的隨機`DimProduct`上`ProductKey`。 衍生的資料表的結果分佈在`fis.ProductKey`。  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REDUCE JOIN FactInternetSales AS fis   
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="t-replicate-join-hint-example"></a>T. 複寫的聯結提示範例  
 下一個範例顯示相同的查詢，上述範例中，不同處在於`REPLICATE`而不是使用聯結提示`REDUCE`聯結提示。 使用`REPLICATE`提示會造成中的值`ProductKey`（聯結） 的資料行從`FactInternetSales`資料表複寫到所有節點。 `DimProduct`資料表已加入至複寫版本的這些值。  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN SELECT SalesOrderNumber  
FROM  
   (SELECT fis.SalesOrderNumber, dp.ProductKey, dp.EnglishProductName  
    FROM DimProduct AS dp   
      INNER REPLICATE JOIN FactInternetSales AS fis  
          ON dp.ProductKey = fis.ProductKey  
   ) AS dTable  
ORDER BY SalesOrderNumber;  
```  
  
### <a name="u-using-the-redistribute-hint-to-guarantee-a-shuffle-move-for-a-distribution-incompatible-join"></a>U. 若要保證發佈不相容的聯結的隨機移動使用 REDISTRIBUTE 提示  
 下列查詢會使用轉散發查詢提示上發佈不相容的聯結。 這可確保查詢最佳化工具會在查詢計畫中使用隨機移動。 這也會保證查詢計畫將不會使用廣播移動將分散式的資料表移到複寫資料表。  
  
 在下列範例中，REDISTRIBUTE 提示會強制 FactInternetSales 資料表上的隨機移動，因為 ProductKey 是 DimProduct 的散發資料行，而且不是 FactInternetSales 的散發資料行。  
  
```tsql
-- Uses AdventureWorks  
  
EXPLAIN  
SELECT dp.ProductKey, fis.SalesOrderNumber, fis.TotalProductCost  
FROM DimProduct AS dp 
INNER REDISTRIBUTE JOIN FactInternetSales AS fis  
    ON dp.ProductKey = fis.ProductKey;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENQUERY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/openquery-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  

