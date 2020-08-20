---
description: 搜尋條件 (Transact-SQL)
title: 搜尋條件 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- search
- Search Condition
- condition
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator [Transact-SQL]
- CONTAINS predicate (Transact-SQL)
- ESCAPE keyword
- operators [Transact-SQL], search condition
- search conditions [SQL Server]
- WHERE clause, search conditions
- ALL keyword
- FREETEXT predicate (Transact-SQL)
- EXISTS keyword
- search conditions [SQL Server], about search conditions
- NOT operator [Transact-SQL]
- BETWEEN operator
- SOME | ANY keyword
- predicates [full-text search]
- AND, about search conditions
- logical operators [SQL Server], about search conditions
- precedence [SQL Server], logical operators
- logical operators [SQL Server], precedence
- LIKE comparisons
ms.assetid: 09974469-c5d2-4be8-bc5a-78e404660b2c
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d42e04e6701d086784290e6c2ba7d6d9540961e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467580"
---
# <a name="search-condition-transact-sql"></a>搜尋條件 (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  這是使用 AND、OR 和 NOT 邏輯運算子的一個或多個述詞的組合。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
<search_condition> ::=  
    MATCH(<graph_search_pattern>) | <search_condition_without_match> | <search_condition> AND <search_condition>

<search_condition_without_match> ::= 
    { [ NOT ] <predicate> | ( <search_condition_without_match> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition_without_match> ) } ]   
[ ...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '<contains_search_condition>' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery )     }   
    
<graph_search_pattern> ::=
    { <node_alias> { 
                      { <-( <edge_alias> )- } 
                    | { -( <edge_alias> )-> }
                    <node_alias> 
                   } 
    }
  
<node_alias> ::=
    node_table_name | node_table_alias 

<edge_alias> ::=
    edge_table_name | edge_table_alias
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
< search_condition > ::=   
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | < | < = } expression   
    | string_expression [ NOT ] LIKE string_expression   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | expression [ NOT ] IN (subquery | expression [ ,...n ] )   
    | expression [ NOT ] EXISTS (subquery)     }   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 \<search_condition>  
 指定 SELECT 陳述式、查詢運算式或子查詢結果集中所傳回之資料列的條件。 如果是 UPDATE 陳述式，便指定要更新的資料列。 如果是 DELETE 陳述式，便指定要刪除的資料列。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式搜尋條件中所能包括的述詞數目沒有限制。  
  
 \<graph_search_pattern>  
 指定圖形搜尋模式。 如需此子句的引數詳細資訊，請參閱 [MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)
 
 NOT  
 執行述詞所指定之布林運算式的否定運算。 如需詳細資訊，請參閱 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)。  
  
 AND  
 組合兩個條件，當兩個條件都是 TRUE 時，便得出 TRUE。 如需詳細資訊，請參閱 [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)。  
  
 OR  
 組合兩個條件，當任何一個條件是 TRUE 時，便得出 TRUE。 如需詳細資訊，請參閱 [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)。  
  
 \< predicate >  
 這是傳回 TRUE、FALSE 或 UNKNOWN 的運算式。  
  
 *expression*  
 這是一個資料行名稱、常數、函數、變數、純量子查詢，或任何由一個或多個運算子來連接的資料行名稱、常數和函數之組合，或子查詢。 另外，運算式也可以包含 CASE 運算式。  
  
> [!NOTE]  
>  非 Unicode 字串常數和變數會使用與資料庫預設定序對應的字碼頁。 僅使用非 Unicode 字元資料及參考非 Unicode 字元資料類型 **char**、**varchar** 及 **text** 時，就會進行字碼頁轉換。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將非 Unicode 字串常數和變數，轉換成與所參考資料行之定序或使用 COLLATE 指定之定序對應的字碼頁，但前提是該字碼頁與和資料庫預設定序對應的字碼頁不同。 任何在新字碼頁中找不到的字元只要可以找到[最相符對應](https://www.unicode.org/Public/MAPPINGS/VENDORS/MICSFT/WindowsBestFit/)，就會轉譯成類似的字元，否則會轉換成預設的取代字元 "?"。  
>  
> 使用多個字碼頁時，可以在字元常數前面加上大寫字母 'N'，以及使用 Unicode 變數，來避免進行字碼頁轉換。  
  
 =  
 這是用來測試兩個運算式是否相等的運算子。  
  
 <>  
 這是用來測試兩個運算式不相等之狀況的運算子。  
  
 !=  
 這是用來測試兩個運算式不相等之狀況的運算子。  
  
 \>  
 這是用來測試一個運算式大於另一個運算式之狀況的運算子。  
  
 \>=  
 這是用來測試一個運算式大於或等於另一個運算式之狀況的運算子。  
  
 !>  
 這是用來測試一個運算式不大於另一個運算式之狀況的運算子。  
  
 <  
 這是用來測試一個運算式小於另一個運算式之狀況的運算子。  
  
 <=  
 這是用來測試一個運算式小於或等於另一個運算式之狀況的運算子。  
  
 !<  
 這是用來測試一個運算式不小於另一個運算式之狀況的運算子。  
  
 *string_expression*  
 這是字元和萬用字元所組成的字串。  
  
 [ NOT ] LIKE  
 指出要搭配模式比對使用的後續字元字串。 如需詳細資訊，請參閱 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)。  
  
 ESCAPE **'***escape_ character***'**  
 允許在字元字串中搜索萬用字元，而不是當做萬用字元使用。 *escape_character* 是放在萬用字元前方的字元，用來指出這個特殊用法。  
  
 [ NOT ] BETWEEN  
 指定值的範圍，頭尾包括在內。 請利用 AND 來分開起始值和結尾值。 如需詳細資訊，請參閱 [BETWEEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/between-transact-sql.md)。  
  
 IS [ NOT ] NULL  
 指定搜尋 NULL 值或非 NULL 值，這會隨著所用的關鍵字而不同。 如果有任何運算元是 NULL，含位元或算術運算子的運算式便會得出 NULL。  
  
 CONTAINS  
 搜尋包含字元型資料的資料行，以進行下列各種比對：單字和片語的精確或較不精確 (模糊) 比對、單字彼此在一定距離之間的接近度，或加權比對。 這個選項只能搭配 SELECT 陳述式使用。 如需詳細資訊，請參閱 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)。  
  
 FREETEXT  
 提供簡單的自然語言查詢形式，它會搜尋包含以字元為基礎的資料之資料行，以找出符合述詞中之意義 (而不是確實文字) 的值。 這個選項只能搭配 SELECT 陳述式使用。 如需詳細資訊，請參閱 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)。  
  
 [ NOT ] IN  
 指定根據運算式是否在清單中來搜尋運算式。 搜尋運算式可以是常數或資料行名稱，清單可能是一組常數，也可能是一個子查詢，通常是一個子查詢。 將值的清單括在括號內。 如需詳細資訊，請參閱 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)。  
  
 *subquery*  
 這可視為受限制的 SELECT 陳述式，且類似於 SELECT 陳述式中的 \<query_expression>。 不允許使用 ORDER BY 子句和 INTO 關鍵字。 如需詳細資訊，請參閱 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)。  
  
 ALL  
 用來搭配比較運算子和子查詢使用。 當為子查詢擷取的所有值都滿足比較運算時，會針對 \<predicate> 傳回 TRUE；當並非所有值都滿足比較時，或當子查詢未傳回任何資料列給外部陳述式時，則傳回 FALSE。 如需詳細資訊，請參閱 [ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)。  
  
 { SOME | ANY }  
 用來搭配比較運算子和子查詢使用。 當為子查詢擷取的任何值滿足比較運算時，會針對 \<predicate> 傳回 TRUE；當子查詢中沒有任何值滿足比較時，或當子查詢未傳回任何資料列給外部陳述式時，則傳回 FALSE。 否則，運算式便是 UNKNOWN。 如需詳細資訊，請參閱 [SOME &#124; ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)。  
  
 EXISTS  
 搭配子查詢來測試子查詢傳回的資料列是否存在。 如需詳細資訊，請參閱 [EXISTS &#40;Transact-SQL&#41;](../../t-sql/language-elements/exists-transact-sql.md)。  
  
## <a name="remarks"></a>備註  
 邏輯運算子的優先順序是 NOT (最高)，後面依序接著 AND 和 OR。 您可以利用括號來置換搜尋條件中的這個優先順序。 評估邏輯運算子的順序可能會隨著查詢最佳化工具所進行的選擇而不同。 如需有關邏輯運算子如何處理邏輯值的詳細資訊，請參閱 [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)、[OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md) 及 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-where-with-like-and-escape-syntax"></a>A. 搭配 LIKE 和 ESCAPE 語法使用 WHERE  
 下列範例會搜尋 `LargePhotoFileName` 資料行有 `green_` 字元的資料列，且會使用 `ESCAPE` 選項，因為 _ 是萬用字元。 在未指定 `ESCAPE` 選項的情況下，查詢會搜尋任何包含 `green` 一字後面再接著 _ 字元以外之任何單一字元的描述值。  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT *   
FROM Production.ProductPhoto  
WHERE LargePhotoFileName LIKE '%greena_%' ESCAPE 'a' ;  
```  
  
### <a name="b-using-where-and-like-syntax-with-unicode-data"></a>B. 搭配 Unicode 資料使用 WHERE 和 LIKE 語法  
 下列範例會利用 `WHERE` 子句來擷取在美國 (`US`) 以外，名稱開頭是 `Pa` 的城巿中，任何公司的郵寄地址。  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT AddressLine1, AddressLine2, City, PostalCode, CountryRegionCode    
FROM Person.Address AS a  
JOIN Person.StateProvince AS s ON a.StateProvinceID = s.StateProvinceID  
WHERE CountryRegionCode NOT IN ('US')  
AND City LIKE N'Pa%' ;  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-where-with-like"></a>C. 搭配 LIKE 使用 WHERE  
 下列範例會搜尋 `LastName` 資料行有 `and` 字元的資料列。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE '%and%';  
```  
  
### <a name="d-using-where-and-like-syntax-with-unicode-data"></a>D. 搭配 Unicode 資料使用 WHERE 和 LIKE 語法  
 下列範例會使用 `WHERE` 子句，以在 `LastName` 資料行上執行 Unicode 搜尋。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE N'%and%';  
```  
  
## <a name="see-also"></a>另請參閱  
 [彙總函數 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [資料指標 &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  

