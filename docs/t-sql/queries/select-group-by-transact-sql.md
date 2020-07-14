---
title: GROUP BY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUP
- CUBE
- ROLLUP
- GROUPING_SETS_TSQL
- GROUP BY
- GROUPING SETS
- GROUP_BY_TSQL
- GROUP_TSQL
- CUBE_TSQL
- ROLLUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, about GROUP BY clause
- dividing tables into groups
- GROUPING SETS
- GROUP BY clause
- table groups [SQL Server]
- groups [SQL Server], tables divided into groups
- summary values [SQL Server]
ms.assetid: 40075914-6385-4692-b4a5-62fe44ae6cb6
author: shkale-msft
ms.author: shkale
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 03c9b8dae913f7fb8dd770effcfd56a32e368c96
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999779"
---
# <a name="select---group-by--transact-sql"></a>SELECT - GROUP BY- Transact-SQL
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

如果 SELECT 陳述式子句將查詢結果分成幾個資料列群組，通常是為了對每個群組執行一或多個彙總。 SELECT 陳述式會為每個群組傳回一個資料列。  
  
## <a name="syntax"></a>語法  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database   
-- ISO-Compliant Syntax  
  
GROUP BY {
      column-expression  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
    | GROUPING SETS ( <grouping_set> [ ,...n ]  )  
    | () --calculates the grand total 
} [ ,...n ] 
 
<group_by_expression> ::=  
      column-expression  
    | ( column-expression [ ,...n ] )    
   
<grouping_set> ::=  
      () --calculates the grand total  
    | <grouping_set_item>  
    | ( <grouping_set_item> [ ,...n ] )  
  
<grouping_set_item> ::=  
      <group_by_expression>  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
  

-- For backward compatibility only.
-- Non-ISO-Compliant Syntax for SQL Server and Azure SQL Database 
  
GROUP BY 
      [ ALL ] column-expression [ ,...n ] 
    | column-expression [ ,...n ] [ WITH { CUBE | ROLLUP } ]   

```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse 
  
GROUP BY {
      column-name [ WITH (DISTRIBUTED_AGG) ]  
    | column-expression
    | ROLLUP ( <group_by_expression> [ ,...n ] ) 
} [ ,...n ]

```

```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
GROUP BY {
      column-name [ WITH (DISTRIBUTED_AGG) ]  
    | column-expression
} [ ,...n ]

```  
    
## <a name="arguments"></a>引數 
 
### <a name="column-expression"></a>*column-expression*  
指定資料行，或在資料行進行非彙總計算。 此資料行可以屬於資料表、衍生資料表或檢視。 資料行必須出現在 SELECT 陳述式的 FROM 子句中，但不需要出現在 SELECT 清單中。 

如需有效的運算式，請參閱[運算式](~/t-sql/language-elements/expressions-transact-sql.md)。    

資料行必須出現在 SELECT 陳述式的 FROM 子句中，但不需要出現在 SELECT 清單中。 不過 \<select> 清單中任何非彙總運算式中的每一個資料表或檢視資料行都必須包含在 GROUP BY 清單中：  
  
允許使用下列陳述式：  
  
```sql  
SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA, ColumnB;  
SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA, ColumnB;  
SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
SELECT ColumnA + ColumnB + constant FROM T GROUP BY ColumnA, ColumnB;  
```  
  
不允許使用下列陳述式：  
  
```sql  
SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA + ColumnB;  
SELECT ColumnA + constant + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
```  

資料行運算式不能包含：

- SELECT 清單中定義的資料行別名。 它可用於 FROM 子句中定義之衍生資料表的資料行別名。
- **text**、**ntext** 或 **image** 類型的資料行。 不過，您可以使用 text、ntext 或 image 的資料行做為函數的引數，傳回有效資料類型的值。 例如，運算式可以使用 SUBSTRING() 與 CAST()。 這也適用於 HAVING 子句中的運算式。
- xml 資料類型方法。 可以包含使用 xml 資料類型方法的使用者定義函數。 可以包含使用 xml 資料類型方法的計算資料行。 
- 子查詢。 傳回錯誤 144。 
- 索引檢視表的資料行。 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY *column-expression* [ ,...n ] 

根據一或多個資料行運算式的清單值，群組 SELECT 陳述式的結果。 

例如，此查詢會建立一個有 Country、Region 和 Sales 資料行的 Sales 資料表。 查詢插入四個資料列，其中兩個資料列在 Country 和 Region 的值相同。  

```sql
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
Sales 資料表包含以下資料列：

| Country | 區域 | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | British Columbia | 200 |
| Canada | British Columbia | 300 |
| 美國 | Montana | 100 |

下一個查詢群組 Country 和 Region，並傳回每個值組合的彙總總和。  
 
```sql 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
查詢結果有 3 個資料列，因為 Country 和 Region 有 3 個值組合。 Canada 和 British Columbia 的 TotalSales 是兩個資料列的總和。 

| Country | 區域 | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | British Columbia | 500 |
| 美國 | Montana | 100 |

### <a name="group-by-rollup"></a>GROUP BY ROLLUP

為每個資料行運算式的組合建立群組。 此外，也會將結果「積存」到小計和總計。 為了執行，它會從右向左移動，減少建立群組和彙總的資料行運算式數目。 

資料行順序會影響 ROLLUP 的輸出，也會影響結果集中的資料列數。  

例如，`GROUP BY ROLLUP (col1, col2, col3, col4)` 會為下列清單中的每個資料行運算式組合建立群組。  

- col1, col2, col3, col4 
- col1, col2, col3, NULL
- col1, col2, NULL, NULL
- col1, NULL, NULL, NULL
- NULL, NULL, NULL, NULL -- 這是總計

此程式碼會使用先前範例的資料表，執行 GROUP BY ROLLUP 而不是簡單的 GROUP BY 作業。

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

查詢結果的彙總與簡單的 GROUP BY (沒有 ROLLUP) 的彙總相同。 此外，會為每個 Country 的值建立小計。 最後，提供所有資料列的總計。 結果如下所示：

| Country | 區域 | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | British Columbia | 500 |
| Canada | NULL | 600 |
| 美國 | Montana | 100 |
| 美國 | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>GROUP BY CUBE ( )  

GROUP BY CUBE 為所有可能的資料行組合建立群組。 如果是 GROUP BY CUBE (a, b)，結果會有 (a, b)、(NULL, b)、(a, NULL) 和 (NULL, NULL) 這些唯一值的群組。

此程式碼使用先前範例的資料表，對 Country 和 Region 執行 GROUP BY CUBE 作業。 

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

查詢結果會有 (Country, Region)、(NULL, Region)、(Country, NULL) 和 (NULL, NULL) 這些唯一值的群組。 結果如下：

| Country | 區域 | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| NULL | Alberta | 100 |
| Canada | British Columbia | 500 |
| NULL | British Columbia | 500 |
| 美國 | Montana | 100 |
| NULL | Montana | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| 美國 | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>GROUP BY GROUPING SETS ( )  
 
GROUPING SETS 選項可讓您將多個 GROUP BY 子句結合成一個 GROUP BY 子句。 結果等於指定之群組的 UNION ALL。 

例如，`GROUP BY ROLLUP (Country, Region)` 和 `GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )` 傳回相同的結果。 

當 GROUPING SETS 有兩個或多個元素時，結果是元素的聯集。 此範例傳回 Country 和 Region 之 ROLLUP 和 CUBE 結果的聯集。

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

結果與此查詢 (傳回兩個 GROUP BY 陳述式的聯集) 相同。

```sql
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region)
UNION ALL
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

SQL 不會合併針對 GROUPING SETS 清單所產生的重複群組。 例如，在 `GROUP BY ( (), CUBE (Country, Region) )` 中，兩個元素都傳回總計的資料列，但兩個資料列都會列在結果中。 

 ### <a name="group-by-"></a>GROUP BY ()  
指定產生總計的空群組。 當其中一個元素是 GROUPING SET 時，這非常有用。 例如，此陳述式計算每個國家/地區的銷售總額，然後計算所有國家/地區的總計。

```sql
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [ ALL ] column-expression [ ,...n ] 

適用於：SQL Server 和 Azure SQL Database

注意：提供此語法，只是為了回溯相容性。 未來的版本將予以移除。 請避免在新的開發工作中使用這個語法，並規劃修改目前使用這個語法的應用程式。

指定在結果中包含所有群組，不論它們是否符合 WHERE 子句中的搜尋準則。 不符合搜尋準則的群組彙總會是 NULL。 

GROUP BY ALL：
- 在存取遠端資料表的查詢中，如果查詢中也有 WHERE 子句，就不支援。
- 在具有 FILESTREAM 屬性的資料行上將會失敗。
  
### <a name="with-distributed_agg"></a>WITH (DISTRIBUTED_AGG)
適用於：Azure SQL 資料倉儲與平行處理資料倉儲

DISTRIBUTED_AGG 查詢提示會強制使用大量平行處理 (MPP) 系統，在執行彙總之前轉散發特定資料行上的資料表。 GROUP BY 子句中只有一個資料行可以有 DISTRIBUTED_AGG 查詢提示。 查詢完成後，轉散發的資料表就會卸除。 不會變更原始資料表。  

注意：提供 DISTRIBUTED_AGG 查詢提示是為了舊版平行處理資料倉儲的回溯相容性，不會改善大部分查詢的效能。 根據預設，MPP 在需要時就已經轉散發資料，以增進彙總的效能。 
  
## <a name="general-remarks"></a>一般備註

### <a name="how-group-by-interacts-with-the-select-statement"></a>GROUP BY 如何與 SELECT 陳述式互動
SELECT 清單：
- 向量彙總。 如果 SELECT 清單包括彙總函式，GROUP BY 會計算每個群組的摘要值。 這些稱為向量彙總。 
- 相異彙總。 ROLLUP、CUBE 和 GROUPING SETS 支援彙總 AVG (DISTINCT *column_name*)、COUNT (DISTINCT *column_name*) 和 SUM (DISTINCT *column_name*)。
  
WHERE 子句：
- SQL 會在執行任何群組作業之前，移除不符合 WHERE 子句之條件的資料列。  
  
HAVING 子句：
- SQL 會使用 HAVING 子句以篩選結果集中的群組。 
  
ORDER BY 子句：
- 請使用 ORDER BY 子句來排序結果集。 GROUP BY 子句不會排序結果集， 
  
NULL 值：
- 如果群組資料行包含 NULL 值，系統會把所有 NULL 值都視為相等，並將它們收集成單一群組。   
  
## <a name="limitations-and-restrictions"></a>限制事項

適用於：SQL Server (自 2008 起) 和 Azure SQL 資料倉儲

### <a name="maximum-capacity"></a>最大容量

對於使用 ROLLUP、CUBE 或 GROUPING SETS 的 GROUP BY 子句，運算式的最大數目為 32。 群組的最大數目為 4096 (2<sup>12</sup>)。 下列範例因為 GROUP BY 子句超過 4096 個群組而失敗。  
 
-   下列範例產生 4097 (2<sup>12</sup> + 1) 個群組集合，因此將失敗。  
  
    ```sql
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   下列範例產生 4097 (2<sup>12</sup> + 1) 個群組，因此將失敗。 `CUBE ()` 和 `()` 群組集合都會產生總計資料列，而且不會刪除重複的群組集合。  
  
    ```sql
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   此範例使用回溯相容語法。 產生 8192 (2<sup>13</sup>) 個群組集合，因此將失敗。  
  
    ```sql
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    如果是不包含 CUBE 或 ROLLUP 的回溯相容 GROUP BY 子句，分組項目數會受到 GROUP BY 資料行大小、彙總資料行，以及查詢所涉及的彙總值所限制。 這項限制起源於保存中繼查詢結果時所需要的中繼工作資料表之 8,060 位元組限制。 當指定 CUBE 或 ROLLUP 時，最多只允許 12 個群組運算式。

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>ISO 和 ANSI SQL-2006 GROUP BY 功能的支援

GROUP BY 子句支援 SQL-2006 標準內包含的所有 GROUP BY 功能，但是以下語法例外：  
  
-   GROUP BY 子句中不允許使用群組集合，除非它們屬於明確 GROUPING SETS 清單的一部分。 例如，標準中允許 `GROUP BY Column1, (Column2, ...ColumnN`)，但是 Transact-SQL 中不允許。  Transact-SQL 支援 `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` 和 `GROUP BY Column1, Column2, ... ColumnN`，這兩者語意相等。 其語意相當於之前的 `GROUP BY` 範例。 這是為了避免 `GROUP BY Column1, (Column2, ...ColumnN`) 可能錯誤地解譯為 `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`，這兩者語意不相等。  
  
-   群組集合內不允許使用群組集合。 例如，SQL-2006 標準中允許 `GROUP BY GROUPING SETS (A1, A2,...An, GROUPING SETS (C1, C2, ...Cn))`，但是 Transact-SQL 中不允許。 Transact-SQL 允許 `GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )` 或 `GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`，這兩者在語意上與第一個 GROUP BY 範例相同，而且語法更清楚。  
  
-   GROUP BY [ALL/DISTINCT] 只能在包含資料行運算式的簡單 GROUP BY 子句中使用。 不允許搭配 GROUPING SETS、ROLLUP、CUBE、WITH CUBE 或 WITH ROLLUP 建構。 ALL 為預設值而且是隱含的。 也只能在回溯相容的語法中使用。
  
### <a name="comparison-of-supported-group-by-features"></a>比較支援的 GROUP BY 功能  
 下表描述根據 SQL 版本和資料庫相容性層級所支援的 GROUP BY 功能。  
  
|功能|SQL Server Integration Services|SQL Server 相容性層級 100 或更高層級|相容性層級 90 的 SQL Server 2008 或更新版本。|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|DISTINCT 彙總|不支援 WITH CUBE 或 WITH ROLLUP。|支援 WITH CUBE、WITH ROLLUP、GROUPING SETS、CUBE 或 ROLLUP。|與相容性層級 100 相同。|  
|GROUP BY 子句中具有 CUBE 或 ROLLUP 名稱的使用者定義函數|允許在 GROUP BY 子句中使用使用者定義函式 **dbo.cube(** _arg1_ **,** _...argN_ **)** or **dbo.rollup(** _arg1_ **,** ..._argN_ **)** 。<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|不允許在 GROUP BY 子句中使用使用者定義函式 **dbo.cube (** _arg1_ **,** ...argN **)** or **dbo.rollup(** arg1 **,** _...argN_ **)** 。<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> 系統會傳回下列錯誤訊息：「關鍵字 'cube'&#124;'rollup' 附近的語法不正確。」<br /><br /> 若要避免這個問題，請使用 `dbo.cube` 取代 `[dbo].[cube]`，或使用 `dbo.rollup` 取代 `[dbo].[rollup]`。<br /><br /> 允許使用下列範例：`SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|允許在 GROUP BY 子句中使用使用者定義函式 **dbo.cube (** _arg1_ **,** _...argN_) or **dbo.rollup(** _arg1_ **,** _...argN_ **)**<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
|GROUPING SETS|不支援|支援|支援|  
|CUBE|不支援|支援|不支援|  
|ROLLUP|不支援|支援|不支援|  
|總計，例如 GROUP BY ()|不支援|支援|支援|  
|GROUPING_ID 函數|不支援|支援|支援|  
|GROUPING 函數|支援|支援|支援|  
|WITH CUBE|支援|支援|支援|  
|WITH ROLLUP|支援|支援|支援|  
|移除 WITH CUBE 或 WITH ROLLUP 的重複群組|支援|支援|支援| 
 
  
## <a name="examples"></a>範例  
  
### <a name="a-use-a-simple-group-by-clause"></a>A. 使用簡單的 GROUP BY 子句  
 下列範例會從 `SalesOrderID` 資料表中，擷取每個 `SalesOrderDetail` 的總計。 這個範例會使用 AdventureWorks。  
  
```sql  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>B. 使用 GROUP BY 子句搭配多個資料表  
 下列範例會從聯結至 `City` 資料表的 `Address` 資料表中，擷取每個 `EmployeeAddress` 的員工人數。 這個範例會使用 AdventureWorks。 
  
```sql  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>C. 使用 GROUP BY 子句搭配運算式  
 下列範例會使用 `DATEPART` 函數，擷取每年的銷售總額。 `SELECT` 清單和 `GROUP BY` 子句中必須出現相同的運算式。  
  
```sql  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>D. 使用 GROUP BY 子句搭配 HAVING 子句  
 下列範例會使用 `HAVING` 子句，指定 `GROUP BY` 子句中產生的哪一個群組要包含在結果集中。  
  
```sql  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>範例：SQL 資料倉儲與平行處理資料倉儲  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>E. GROUP BY 子句的基本使用  
 下列範例會尋找每天的所有銷售總額。 每天只會傳回一個包含所有銷售總和的資料列。  
  
```sql  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributed_agg-hint"></a>F. DISTRIBUTED_AGG 提示的基本使用  
 此範例使用 DISTRIBUTED_AGG 查詢提示在執行彙總之前，強制應用裝置輪換 `CustomerKey` 資料行上的資料表。  
  
```sql  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>G. GROUP BY 的語法變化  
 當選取清單沒有彙總時，選取清單中的每個資料行都必須包含在 GROUP BY 清單內。 GROUP BY 清單中可以列出選取清單中的計算資料行，但是並非必要。 以下是句法有效的 SELECT 陳述式範例：  
  
```sql  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>H. 使用 GROUP BY 搭配多個 GROUP BY 運算式  
 下列範例使用多個 `GROUP BY` 準則群組結果。 如果在每個 `OrderDateKey` 群組內，有一些子群組可以由 `DueDateKey` 區分，將會針對結果集定義新的群組。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales
GROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>I. 使用 GROUP BY 子句搭配 HAVING 子句  
 下列範例使用 `HAVING` 子句，指定 `GROUP BY` 子句中產生，應包含在結果集中的群組。 只有訂單日期在 2004 年或之後的群組才會包含在結果中。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>另請參閱  
 [GROUPING_ID &#40;Transact-SQL&#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [GROUPING &#40;Transact-SQL&#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [SELECT 子句 &#40;Transact-SQL&#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  




