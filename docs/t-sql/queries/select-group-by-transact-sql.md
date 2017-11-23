---
title: "GROUP BY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
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
dev_langs: TSQL
helpviewer_keywords:
- GROUP BY clause, about GROUP BY clause
- dividing tables into groups
- GROUPING SETS
- GROUP BY clause
- table groups [SQL Server]
- groups [SQL Server], tables divided into groups
- summary values [SQL Server]
ms.assetid: 40075914-6385-4692-b4a5-62fe44ae6cb6
caps.latest.revision: "80"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 49b572a8ce91287faa4c162efa8de8e7f0113235
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="select---group-by--transact-sql"></a>選取的群組 BY Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

SELECT 陳述式子句分成群組的資料列，通常是為了針對每個群組執行一或多個彙總的查詢結果。 SELECT 陳述式會傳回每個群組的一個資料列。  
  
## <a name="syntax"></a>語法  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
```  
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
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GROUP BY {
      column-name [ WITH (DISTRIBUTED_AGG) ]  
    | column-expression
} [ ,...n ]

```  
  
## <a name="arguments"></a>引數 
 
### <a name="column-expression"></a>*資料行運算式*  
指定資料行或非彙總計算的資料行上。 此資料行可以屬於資料表、 衍生的資料表或檢視。 資料行必須出現在 FROM 子句的 SELECT 陳述式，但不需要出現在選取清單中。 

如需有效運算式，請參閱[運算式](~/t-sql/language-elements/expressions-transact-sql.md)。    

資料行必須出現在 FROM 子句的 SELECT 陳述式，但不需要出現在選取清單中。 不過，每個資料表或檢視任何非彙總運算式中的資料行\<選取 > 清單必須包含在 GROUP BY 清單：  
  
允許使用下列陳述式：  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + ColumnB + constant FROM T GROUP BY ColumnA, ColumnB;  
    ```  
  
不允許使用下列陳述式：  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + constant + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    ```  
資料行運算式不能包含：

- 選取清單中定義資料行別名。 它可用於 FROM 子句中定義的衍生資料表的資料行別名。
- 類型的資料行**文字**， **ntext**，或**映像**。 不過，您可以使用 text、 ntext 或 image 的資料行做為引數函式的傳回值的有效資料型別。 例如，運算式可以使用 substring （） 與 cast （）。 這也適用於 HAVING 子句中的運算式。
- xml 資料類型方法。 它可以包含使用 xml 資料類型方法的使用者定義函式。 它可以包含使用 xml 資料類型方法的計算資料行。 
- 子查詢。 傳回錯誤 144。 
- 索引檢視表中的資料行。 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY*資料行運算式*[，.....n] 

根據清單中的值一或多個資料行運算式的 SELECT 陳述式結果的群組。 

例如，此查詢會建立 「 銷售 」 資料表具有資料行的國家/地區、 區域和銷售。 它將四個資料列插入兩個資料列具有相符的值的國家和地區。  

```
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
[Sales] 資料表會包含這些資料列：

| Country | Region | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | 不列顛哥倫比亞省 | 200 |
| Canada | 不列顛哥倫比亞省 | 300 |
| United States | Montana | 100 |

下一個查詢群組國家和地區，並傳回每一個值組合的彙總總和。  
 
``` 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
查詢結果會有 3 個資料列，因為有 3 的值國家和地區組合。 加拿大和不列顛哥倫比亞省的 TotalSales 是兩個資料列的總和。 

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | 不列顛哥倫比亞省 | 500 |
| United States | Montana | 100 |

### <a name="group-by-rollup"></a>GROUP BY 彙總套件

建立一個群組，每個資料行運算式的組合。 此外，它 「 彙總 」 結果到小計和總計。 若要這樣做，它會移動由右至左減少資料行運算式，它在其上建立群組和 aggregation(s) 數目。 

資料行順序會影響彙總輸出，而且可能會影響結果集中的資料列數目。  

例如，`GROUP BY ROLLUP (col1, col2, col3, col4)`會建立下列清單中的每個資料行運算式組合的群組。  

- col1，col2，col3，第 4 欄 
- col1，col2，col3，NULL
- col1，col2，NULL NULL
- col1，NULL，NULL NULL
- NULL，NULL，NULL，NULL-這是總計

使用從先前的範例資料表，此程式碼會執行而不是簡單的 GROUP BY GROUP BY ROLLUP 作業。

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

查詢結果必須為簡單的 GROUP BY 彙總不相同的彙總。 此外，它會建立每個值的國家/地區的小計。 最後，它提供所有資料列總計。 結果看起來像這樣：

| Country | Region | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | 不列顛哥倫比亞省 | 500 |
| Canada | NULL | 600 |
| United States | Montana | 100 |
| United States | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>GROUP BY CUBE （)  

GROUP BY CUBE 建立所有可能組合的資料行的群組。 GROUP BY CUBE (a、 b) 的結果具有唯一值的群組 (a、 b) 的 NULL (b），(a、 NULL)，以及 NULL (NULL）。

使用從先前的範例資料表，此程式碼會執行 GROUP BY CUBE 作業國家和地區。 

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

查詢結果有群組唯一值的 （國家地區），NULL (區域），國家 (NULL），以及 NULL (NULL）。 結果看起來像這樣：

| Country | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| NULL | Alberta | 100 |
| Canada | 不列顛哥倫比亞省 | 500 |
| NULL | 不列顛哥倫比亞省 | 500 |
| United States | Montana | 100 |
| NULL | Montana | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| United States | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>GROUP BY 群組集 （）  
 
GROUPING SETS 選項可讓您將多個 GROUP BY 子句結合成一個 GROUP BY 子句。 結果等於指定之群組的 UNION ALL。 

例如，`GROUP BY ROLLUP (Country, Region)`和`GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )`傳回相同的結果。 

當 GROUPING SETS 有兩個或多個項目時，則結果為的項目聯集。 這個範例會傳回國家及區域 ROLLUP 和 CUBE 結果的聯集。

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

結果是此查詢會傳回兩個的 GROUP BY 陳述式的 union 相同。

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region)
UNION ALL
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region)
;
```

SQL 不會不會將合併 GROUPING SETS 清單的產生重複的群組。 例如，在`GROUP BY ( (), CUBE (Country, Region) )`、 兩個項目傳回一個資料列的總計和兩個資料列將列在結果中。 

 ### <a name="group-by-"></a>GROUP BY ()  
指定空的群組會產生總計。 這非常有用，做為其中一個群組設定的項目。 例如，此陳述式提供每個國家/地區的銷售總額，，然後指定所有國家 （地區） 的 格蘭總計。

```
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [ALL] 資料行的運算式 [，.....n] 

適用於： SQL Server 和 Azure SQL Database

注意： 這種語法會提供回溯相容性。 它將在未來版本中移除。 避免在新的開發工作中使用此語法，並規劃修改目前使用此語法的應用程式。

指定將所有群組都包含在結果中，不論它們是否符合 WHERE 子句中的搜尋準則。 不符合搜尋準則的群組彙總有 null 值。 

所有的群組：
- 不支援的查詢中，如果也沒有 WHERE 子句在查詢中存取遠端資料表。
- 具有 FILESTREAM 屬性的資料行上，將會失敗。
  
### <a name="with-distributedagg"></a>使用 (DISTRIBUTED_AGG)
適用於： Azure SQL 資料倉儲和 Parallel Data Warehouse

DISTRIBUTED_AGG 查詢提示會強制轉散發針對特定資料行的資料表，然後再執行彙總的大量平行處理 (MPP) 系統。 GROUP BY 子句中的只能有一個資料行可以有 DISTRIBUTED_AGG 查詢提示。 查詢完成後，卸除轉散發的資料表。 不會變更原始資料表。  

請注意： DISTRIBUTED_AGG 查詢提示會提供回溯相容性與舊版的平行處理資料倉儲，並不會改善效能，對於大部分查詢。 根據預設，MPP 已經會轉散發資料視以增進效能彙總。 
  
## <a name="general-remarks"></a>一般備註

### <a name="how-group-by-interacts-with-the-select-statement"></a>GROUP BY 的互動方式在 SELECT 陳述式
選取的清單：
- 向量彙總。 如果選取清單中包含彙總函式，GROUP BY 會計算每個群組的摘要值。 這些稱為向量彙總。 
- 相異彙總。 彙總 AVG (DISTINCT *column_name*)，COUNT (DISTINCT *column_name*)，和 SUM (DISTINCT *column_name*) 搭配 ROLLUP、 CUBE 和 GROUPING SETS 支援。
  
WHERE 子句：
- SQL 會移除任何群組作業執行之前不符合 WHERE 子句中的條件的資料列。  
  
HAVING 子句：
- SQL 會使用 having 子句來篩選結果集內的群組。 
  
ORDER BY 子句：
- 請使用 ORDER BY 子句來排序結果集。 GROUP BY 子句不會排序結果集， 
  
NULL 值：
- 如果群組資料行包含 NULL 值，所有 NULL 值都視為相等，並被收集到單一群組。   
  
## <a name="limitations-and-restrictions"></a>限制事項

適用於： SQL Server （從 2008年起） 和 Azure SQL 資料倉儲

### <a name="maximum-capacity"></a>最大容量

GROUP BY 子句使用 ROLLUP、 CUBE 或 GROUPING SETS，運算式的最大數目為 32。 群組數目上限為 4096 (2<sup>12</sup>)。 下列範例失敗是因為 GROUP BY 子句已超過 4096 個群組。  
 
-   下列範例會產生 4097 (2<sup>12</sup> + 1) 群組集合，而且將會失敗。  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   下列範例會產生 4097 (2<sup>12</sup> + 1) 分組，並將會失敗。 `CUBE ()` 和 `()` 群組集合都會產生總計資料列，而且不會刪除重複的群組集合。  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   這個範例會使用回溯相容語法。 它會產生 8192 (2<sup>13</sup>) 群組集合，而且將會失敗。  
  
    ```  
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    回溯相容性的 GROUP BY 子句不包含 CUBE 或 ROLLUP，由項目群組的數目會受到 GROUP BY 資料行大小，彙總的資料行，以及查詢中涉及的彙總的值。 這項限制起源於保存中繼查詢結果時所需要的中繼工作資料表之 8,060 位元組限制。 當指定 CUBE 或 ROLLUP 時，最多只允許 12 個群組運算式。

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>ISO 和 ANSI SQL-2006 GROUP BY 功能的支援

GROUP BY 子句支援 GROUP BY 的所有功能具有以下語法例外 sql-2006 標準內包含：  
  
-   GROUP BY 子句中不允許使用群組集合，除非它們屬於明確 GROUPING SETS 清單的一部分。 例如， `GROUP BY Column1, (Column2, ...ColumnN`) 標準中，但在 TRANSACT-SQL 中不允許。  TRANSACT-SQL 支援`GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`和`GROUP BY Column1, Column2, ... ColumnN`，其語意相等。 其語意相當於之前的 `GROUP BY` 範例。 這是為了避免可能的`GROUP BY Column1, (Column2, ...ColumnN`) 可能會錯誤解譯為`GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`，並不是語意相等。  
  
-   群組集合內不允許使用群組集合。 例如， `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))` sql-2006 標準中，但在 TRANSACT-SQL 中不允許。 可讓 TRANSACT-SQL`GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )`或`GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`，其語意相當於第一個 GROUP BY 範例和具有更清楚的語法。  
  
-   GROUP BY [ALL/DISTINCT] 只能簡單 GROUP BY 子句中包含資料行運算式。 不允許使用 GROUPING SETS、 ROLLUP、 CUBE、 WITH CUBE 或 WITH ROLLUP 建構。 ALL 為預設值而且是隱含的。 它也只允許在回溯相容的語法。
  
### <a name="comparison-of-supported-group-by-features"></a>比較支援的 GROUP BY 功能  
 下表描述支援的 SQL 版本和資料庫相容性層級為基礎的 GROUP BY 功能。  
  
|功能|SQL Server Integration Services|SQL Server 相容性層級 100 或更高層級|相容性層級 90 的 SQL Server 2008 或更新版本。|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|DISTINCT 彙總|不支援 WITH CUBE 或 WITH ROLLUP。|支援 WITH CUBE、WITH ROLLUP、GROUPING SETS、CUBE 或 ROLLUP。|與相容性層級 100 相同。|  
|GROUP BY 子句中具有 CUBE 或 ROLLUP 名稱的使用者定義函數|使用者定義函數**dbo.cube (***arg1***，***.....argn***)**或**dbo.rollup (***arg1***，**...*argN***)**允許在 GROUP BY 子句。<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|使用者定義函數**dbo.cube (***arg1***，**.....argn**)**或**dbo.rollup (**arg1**，***.....argn***)**不允許在 GROUP BY 子句。<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> 會傳回下列錯誤訊息: 「 不正確的語法，接近關鍵字 'cube' &#124;'彙總套件 '。 」<br /><br /> 若要避免這個問題，請使用 `dbo.cube` 取代 `[dbo].[cube]`，或使用 `dbo.rollup` 取代 `[dbo].[rollup]`。<br /><br /> 下列範例被可行的：`SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|使用者定義函數**dbo.cube (***arg1***，***.....argn*) 或**dbo.rollup (** *arg1***，***.....argn***)**允許在 GROUP BY 子句<br /><br /> 例如： `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
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
  
```  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>B. 多個資料表使用 GROUP BY 子句  
 下列範例會從聯結至 `City` 資料表的 `Address` 資料表中，擷取每個 `EmployeeAddress` 的員工人數。 這個範例會使用 AdventureWorks。 
  
```  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>C. 使用 GROUP BY 子句的運算式  
 下列範例會使用 `DATEPART` 函數，擷取每年的銷售總額。 `SELECT` 清單和 `GROUP BY` 子句中必須出現相同的運算式。  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>D. 使用 GROUP BY 子句搭配 HAVING 子句  
 下列範例會使用 `HAVING` 子句，指定 `GROUP BY` 子句中產生的哪一個群組要包含在結果集中。  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>範例： SQL 資料倉儲和 Parallel Data Warehouse  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>E. 基本使用 GROUP BY 子句  
 下列範例會尋找每一天所有銷售的總金額。 每一天就會傳回一個資料列，其中包含所有銷售的總和。  
  
```  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>F. 基本使用 DISTRIBUTED_AGG 提示  
 此範例使用 DISTRIBUTED_AGG 查詢提示來強制執行的應用裝置，以隨機播放資料表`CustomerKey`才能執行彙總的資料行。  
  
```  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>G. 對於 分組方式的語法變化  
 當選取清單中有沒有彙總時，在選取清單中的每個資料行必須包含在 GROUP BY 清單中。 選取清單中的計算資料行可以列出，但是並非必要，GROUP BY 清單中。 這些是句法有效 SELECT 陳述式的範例：  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>H. 使用 GROUP BY 與多個 GROUP BY 運算式  
 下列範例使用多個的結果進行分組`GROUP BY`準則。 如果，在每個`OrderDateKey`群組，有可以由區分的子群組`DueDateKey`，將會針對結果集來定義新的群組。  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSalesGROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>I. 使用 GROUP BY 子句搭配 HAVING 子句  
 下列範例會使用`HAVING`子句來指定群組中產生`GROUP BY`應該包含在結果集中的子句。 訂單日期 2004年或更新版本為這些群組將會包含在結果中。  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [GROUPING_ID &#40;TRANSACT-SQL &#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [群組 &#40;TRANSACT-SQL &#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [SELECT 子句 &#40;TRANSACT-SQL &#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  




