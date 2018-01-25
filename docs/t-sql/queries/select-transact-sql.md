---
title: "選取 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT_TSQL
- SELECT
dev_langs: TSQL
helpviewer_keywords:
- retrieving rows
- SELECT statement [SQL Server]
- SELECT statement [SQL Server], about SELECT statement
- row retrieval [SQL Server], SELECT statement
- DML [SQL Server], SELECT statement
- data manipulation language [SQL Server], SELECT statement
- row retrieval [SQL Server]
- queries [SQL Server], results
ms.assetid: dc85caea-54d1-49af-b166-f3aa2f3a93d0
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b8cca7419cce15dcbb83b4aa72dc551e5eb89eb1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="select-transact-sql"></a>SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  從資料庫擷取資料列，並可讓您選取一個或多個資料列或從一個或多個資料表中的資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 SELECT 陳述式的完整語法很複雜，但主要子句可摘要如下：  
  
[ WITH { [ XMLNAMESPACES ,] [ \<common_table_expression> ] } ]
  
 SELECT *select_list* [ INTO *new_table* ]  
  
 [ FROM *table_source* ] [ WHERE *search_condition* ]  
  
 [ GROUP BY *group_by_expression* ]  
  
 [ HAVING *search_condition* ]  
  
 [ ORDER BY *order_expression* [ ASC | DESC ] ]  
  
 UNION、 EXCEPT 和 INTERSECT 運算子可用來結合或比較其結果成為一個結果集的查詢之間。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<SELECT statement> ::=    
    [ WITH { [ XMLNAMESPACES ,] [ <common_table_expression> [,...n] ] } ]  
    <query_expression>   
    [ ORDER BY { order_by_expression | column_position [ ASC | DESC ] }   
  [ ,...n ] ]   
    [ <FOR Clause>]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]   
<query_expression> ::=   
    { <query_specification> | ( <query_expression> ) }   
    [  { UNION [ ALL ] | EXCEPT | INTERSECT }  
        <query_specification> | ( <query_expression> ) [...n ] ]   
<query_specification> ::=   
SELECT [ ALL | DISTINCT ]   
    [TOP ( expression ) [PERCENT] [ WITH TIES ] ]   
    < select_list >   
    [ INTO new_table ]   
    [ FROM { <table_source> } [ ,...n ] ]   
    [ WHERE <search_condition> ]   
    [ <GROUP BY> ]   
    [ HAVING < search_condition > ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ WITH <common_table_expression> [ ,...n ] ]  
SELECT <select_criteria>  
[;]  
  
<select_criteria> ::=  
    [ TOP ( top_expression ) ]   
    [ ALL | DISTINCT ]   
    { * | column_name | expression } [ ,...n ]   
    [ FROM { table_source } [ ,...n ] ]  
    [ WHERE <search_condition> ]   
    [ GROUP BY <group_by_clause> ]   
    [ HAVING <search_condition> ]   
    [ ORDER BY <order_by_expression> ]  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
  
```  
  
## <a name="remarks"></a>備註  
 由於 SELECT 陳述式十分複雜，因此將會依子句顯示詳細的語法元素及引數：  
  
|||  
|-|-|  
|[WITH XMLNAMESPACES](../../t-sql/xml/with-xmlnamespaces.md)<br /><br /> [WITH common_table_expression](../../t-sql/queries/with-common-table-expression-transact-sql.md)|[HAVING](../../t-sql/queries/select-having-transact-sql.md)|  
|[SELECT 子句](../../t-sql/queries/select-clause-transact-sql.md)|[等位](../../t-sql/language-elements/set-operators-union-transact-sql.md)|  
|[INTO 子句](../../t-sql/queries/select-into-clause-transact-sql.md)|[EXCEPT 和 INTERSECT](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)|  
|[FROM](../../t-sql/queries/from-transact-sql.md)|[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md)|  
|[WHERE](../../t-sql/queries/where-transact-sql.md)|[FOR 子句](../../t-sql/queries/select-for-clause-transact-sql.md)|  
|[GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md)|[OPTION 子句](../../t-sql/queries/option-clause-transact-sql.md)|  
  
 子句順序對 SELECT 陳述式而言十分重要。 您可以省略任何選擇性的子句，但當使用選擇性的子句時，它們必須以適當的順序顯示。  
  
 只有在這些 SELECT 陳述式的選取清單包含指派使用者自訂函數之本機變數值的運算式時，才能在使用者自訂函數中，允許 SELECT 陳述式。  
  
 利用 OPENDATASOURCE 函數來建構成伺服器名稱部分的四部分名稱，每當 SELECT 陳述式中出現資料表名稱時，都可用來做為資料表來源。 無法為指定四部分名稱[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 部分語法限制只適用於牽涉到遠端資料表的 SELECT 陳述式。  
  
## <a name="logical-processing-order-of-the-select-statement"></a>SELECT 陳述式的邏輯處理順序  
 下列步驟顯示 SELECT 陳述式的邏輯處理順序或繫結順序。 此順序會決定在某個步驟中定義的物件提供給後續步驟之子句使用的時間。 例如，如果查詢處理器可繫結至 (存取) FROM 子句中定義的資料表或檢視表，這些物件及其資料行就會提供給所有後續步驟使用。 反之，因為 SELECT 子句是步驟 8，所以前面的子句無法參考該子句中定義的任何資料行別名或衍生資料行。 不過，ORDER BY 子句等後續子句都可以參考它們。 陳述式的實際執行由查詢處理器和順序可能與此清單不同。  
  
1.  FROM  
2.  ON  
3.  JOIN  
4.  WHERE  
5.  GROUP BY  
6.  WITH CUBE 或 WITH ROLLUP  
7.  HAVING  
8.  SELECT  
9. DISTINCT  
10. ORDER BY  
11. 頂端  

> [!WARNING]
> 以上順序，通常會情況。 不過，有一些不常見的情況下的順序可能不同之處。
>
> 例如，假設您有叢集的索引的檢視，並檢視排除某些資料表資料列和檢視的選取資料行清單使用變更的資料類型的轉換*varchar*至*整數*。 在此情況下，可能會轉換執行之前執行的 WHERE 子句。 常見確實。 通常是可以修改您的檢視，以避免不同的序列，如果它在您的案例中很重要。 

## <a name="permissions"></a>Permissions  
 選取資料需要資料表或檢視的 **SELECT** 權限；此權限可從較高的範圍繼承而來，例如結構描述的 **SELECT** 權限或資料表的 **CONTROL** 權限。 需要的成員資格或**db_datareader**或**db_owner**固定資料庫角色或**sysadmin**固定的伺服器角色。 建立新的資料表使用**SELECTINTO**也需要**CREATETABLE**權限，而**ALTERSCHEMA**擁有新資料表的結構描述權限。  
  
## <a name="examples"></a>範例:   
下列範例使用 [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] 資料庫。
  
### <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. 使用 SELECT 擷取資料列和資料行  
 此區段會顯示三個程式碼範例。 第一個程式碼範例會傳回所有資料列 （沒有 WHERE 子句指定） 和所有資料行 (使用`*`) 從`DimEmployee`資料表。  
  
```sql  
SELECT *  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
 下一個範例使用資料表別名，以達成相同結果。  
  
```sql  
SELECT e.*  
FROM DimEmployee AS e  
ORDER BY LastName;  
```  
  
 這個範例會傳回所有資料列 （沒有 WHERE 子句指定） 和資料行的子集 (`FirstName`， `LastName`， `StartDate`) 從`DimEmployee`資料表中`AdventureWorksPDW2012`資料庫。 第三個資料行標題已重新命名為`FirstDay`。  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
ORDER BY LastName;  
```  
  
 這個範例會傳回的資料列`DimEmployee`具有`EndDate`不是 NULL 和`MaritalStatus`的是 ' （已婚）。  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
WHERE EndDate IS NOT NULL   
AND MaritalStatus = 'M'  
ORDER BY LastName;  
```  
  
### <a name="b-using-select-with-column-headings-and-calculations"></a>B. 使用 SELECT 與資料行標題及計算  
 下列範例會傳回所有資料列從`DimEmployee`資料表，並根據每位員工計算 gross 支付其`BaseRate`和 40 小時的工作日。  
  
```sql  
SELECT FirstName, LastName, BaseRate, BaseRate * 40 AS GrossPay  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
### <a name="c-using-distinct-with-select"></a>C. 使用 DISTINCT 與 SELECT  
 下列範例會使用`DISTINCT`產生之所有中的唯一項目的清單`DimEmployee`資料表。  
  
```sql  
SELECT DISTINCT Title  
FROM DimEmployee  
ORDER BY Title;  
```  
  
### <a name="d-using-group-by"></a>D. 使用 GROUP BY  
 下列範例會尋找每一天所有銷售的總金額。  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
 因為`GROUP BY`子句中，只有一個資料列，其中包含所有銷售的總和會傳回每一天。  
  
### <a name="e-using-group-by-with-multiple-groups"></a>E. 使用 GROUP BY 與多個群組  
 下列範例會尋找平均價格和網際網路銷售總和的每一天，依訂單日期和升級索引鍵分組。  
  
```sql  

SELECT OrderDateKey, PromotionKey, AVG(SalesAmount) AS AvgSales, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey, PromotionKey  
ORDER BY OrderDateKey;   
```  
  
### <a name="f-using-group-by-and-where"></a>F. 使用 GROUP BY 與 WHERE  
 下列範例會將結果分組之後擷取的訂單日期晚於 2002 年 8 月 1 日的資料列。  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
WHERE OrderDateKey > '20020801'  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="g-using-group-by-with-an-expression"></a>G. 使用 GROUP BY 與運算式  
 下列範例會依運算式來分組。 如果運算式不包括彙總函式，您可以依運算式來進行分組。  
  
```sql  
SELECT SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY (OrderDateKey * 10);  
```  
  
### <a name="h-using-group-by-with-order-by"></a>H. 使用 GROUP BY 與 ORDER BY  
 下列範例會尋找每個日期和訂單的銷售總和的每日。  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-the-having-clause"></a>I. 使用 HAVING 子句  
 此查詢會使用`HAVING`子句來限制結果。  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
HAVING OrderDateKey > 20010000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>另請參閱  
 [精選的範例 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
 [提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql.md)
  

