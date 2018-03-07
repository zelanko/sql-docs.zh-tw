---
title: "ORDER BY 子句 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORDER_TSQL
- BY
- ORDER_BY_TSQL
- BY_TSQL
- ORDER
- ORDER BY
dev_langs:
- TSQL
helpviewer_keywords:
- ad-hoc query paging
- OFFSET clause
- SELECT statement [SQL Server], FETCH clause
- clauses [SQL Server], ORDER BY
- SELECT statement [SQL Server], limiting the rows returned
- data [SQL Server], limiting the rows returned
- data [SQL Server], ad-hoc query paging
- sort orders [SQL Server]
- SELECT statement [SQL Server], OFFSET clause
- ORDER BY clause [Transact-SQL]
- LIMIT
- limiting result sets
- SELECT statement [SQL Server], ORDER BY clause
- query paging
- data [SQL Server], sorting
- limiting data returned in a query
- sort orders [SQL Server], ORDER BY clause
- FETCH clause
ms.assetid: bb394abe-cae6-4905-b5c6-8daaded77742
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 08805ce7f01b11d9b87c587e543f5dae91734e68
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="select---order-by-clause-transact-sql"></a>選取-ORDER BY 子句 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  排序 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢所傳回的資料。 此子句可用於：  
  
-   依據指定的資料行清單排序查詢的結果集，並選擇性地將傳回的資料列限制在指定範圍內。 除非指定 ORDER BY 子句，否則不保證結果集中傳回資料列的順序。  
  
-   決定的順序[排名函數](../../t-sql/functions/ranking-functions-transact-sql.md)值套用至結果集。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  ORDER BY 不支援在選取 / 到或建立資料表 AS 選取 (CTAS) 中的陳述式[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。

## <a name="syntax"></a>語法  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  
  
ORDER BY order_by_expression  
    [ COLLATE collation_name ]   
    [ ASC | DESC ]   
    [ ,...n ]   
[ <offset_fetch> ]  
  
<offset_fetch> ::=  
{   
    OFFSET { integer_constant | offset_row_count_expression } { ROW | ROWS }  
    [  
      FETCH { FIRST | NEXT } {integer_constant | fetch_row_count_expression } { ROW | ROWS } ONLY  
    ]  
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ ORDER BY   
    {  
    order_by_expression   
    [ ASC | DESC ]   
    } [ ,...n ]   
]   
```  
  
## <a name="arguments"></a>引數  
 *order_by_expression*  
 指定要排序查詢結果集的資料行或運算式。 排序資料行可以指定為名稱或資料行別名，或代表選取清單中資料行位置的非負整數。  
  
 您可以指定多個排序資料行。 資料行名稱必須是唯一名稱。 ORDER BY 子句中的排序資料行順序用來定義排序結果集的組織。 也就是說，結果集依據第一個資料行來排序，然後該排序的清單依據第二個資料行來排序，依此類推。  
  
 ORDER BY 子句中參考的資料行名稱必須對應到選取清單中的資料行，或語意明確之 FROM 子句中指定之資料表的已定義資料行。  
  
 COLLATE *sys.databases*  
 指定應該根據中指定的定序執行 ORDER BY 作業*sys.databases*，而不是根據資料表或檢視表中定義之資料行的定序。 *sys.databases*可以是 Windows 定序名稱或 SQL 定序名稱。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。 COLLATE 會只適用於類型的資料行**char**， **varchar**， **nchar**，和**nvarchar**。  
  
 **ASC** | DESC  
 指定指定之資料行的值應該以遞增或遞減順序排序。 ASC 從最低值到最高值進行排序。 DESC 從最高值到最低值進行排序。 ASC 是預設排序次序。 Null 值會當做最低的可能值來處理。  
  
 OFFSET { *integer_constant* | *offset_row_count_expression* } { ROW | ROWS }  
 指定要略過的資料列數目，然後才開始從查詢運算式傳回資料列。 值可以是大於或等於零的整數常數或運算式。  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].s  
  
 *offset_row_count_expression*可以是變數、 參數或常數純量子查詢。 在使用子查詢時，它無法參考定義在外部查詢範圍中的任何資料行。 也就是，它不能與外部查詢相互關聯。  
  
 ROW 和 ROWS 是同義字，基於 ANSI 相容性提供它們。  
  
 在查詢執行計畫，位移資料列計數值會顯示在**位移**TOP 查詢運算子的屬性。  
  
 FETCH { FIRST | NEXT } { *integer_constant* | *fetch_row_count_expression* } { ROW | ROWS } ONLY  
 指定要在已處理 OFFSET 子句之後傳回的資料列數目。 值可以是大於或等於一的整數常數或運算式。  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 *fetch_row_count_expression*可以是變數、 參數或常數純量子查詢。 在使用子查詢時，它無法參考定義在外部查詢範圍中的任何資料行。 也就是，它不能與外部查詢相互關聯。  
  
 FIRST 和 NEXT 是同義字，基於 ANSI 相容性提供它們。  
  
 ROW 和 ROWS 是同義字，基於 ANSI 相容性提供它們。  
  
 在查詢執行計畫，位移資料列計數值會顯示在**列**或**頂端**TOP 查詢運算子的屬性。  
  
## <a name="best-practices"></a>最佳作法  
 避免將 ORDER BY 子句中的整數指定為選取清單中資料行的位置表示。 例如，雖然如 `SELECT ProductID, Name FROM Production.Production ORDER BY 2` 的陳述式有效，但相較於指定實際資料行名稱，此陳述式比較不容易為其他人了解。 此外，變更為選取清單中，例如變更資料行順序，或加入新資料行，需要修改 ORDER BY 子句，以避免非預期的結果。  
  
 在 SELECT TOP (*N*) 陳述式中，永遠使用 ORDER BY 子句。 這是以預測的方式指示哪些資料列受到 TOP 影響的唯一方法。 如需詳細資訊，請參閱[TOP &#40;TRANSACT-SQL &#41;](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="interoperability"></a>互通性  
 當搭配 SELECT...INTO 陳述式一起使用，以插入其他來源的資料列時，ORDER BY 子句無法保證資料列會依照指定順序插入。  
  
 檢視表中使用 OFFSET 和 FETCH，並不會變更檢視表的可更新性屬性。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 ORDER BY 子句中的資料行數目沒有限制；不過，ORDER BY 子句中所指定之資料行的大小總計不能超過 8,060 位元組。  
  
 類型的資料行**ntext**，**文字**，**映像**， **geography**，**幾何**，和**xml**不能在 ORDER BY 子句。  
  
 整數或常數不能指定何時*order_by_expression*排名函數中出現。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 如果資料表名稱在 FROM 子句中使用的是別名，則只能使用別名來限定其在 ORDER BY 子句中的資料行。  
  
 如果 SELECT 陳述式包含下列其中一個子句或運算子，ORDER BY 子句中指定的資料行名稱和別名必須定義在選取清單中：  
  
-   UNION 運算子  
  
-   EXCEPT 運算子  
  
-   INTERSECT 運算子  
  
-   SELECT DISTINCT  
  
 此外，當此陳述式包括 UNION、 EXCEPT 或 INTERSECT 運算子、 資料行名稱或資料行別名必須指定第一個 （左邊） 查詢的選取清單中。  
  
 在使用 UNION、EXCEPT 或 INTERSECT 運算子的查詢中，只在陳述式結尾處允許 ORDER BY。 這項限制只適用於當您指定 UNION、 EXCEPT 和 INTERSECT 最上層查詢中，而不是在子查詢。 請參閱稍後的＜範例＞一節。  
  
 除非同時也指定 TOP 或 OFFSET 和 FETCH 子句，否則 ORDER BY 子句在檢視表、內嵌函數、衍生資料表和子查詢中為無效。 在這些物件中使用 ORDER BY 子句時，這個子句只能用來判斷 TOP 子句或 OFFSET 和 FETCH 子句傳回的資料列。 除非同時在查詢本身指定 ORDER BY 子句，否則 ORDER BY 子句並不保證在查詢上述建構時會傳回排序的結果。  
  
 索引檢視表中或透過 CHECK OPTION 子句定義的檢視表中，不支援 OFFSET 和 FETCH。  
  
 在允許 TOP 和 ORDER BY 的任何查詢中，都可以使用 OFFSET 和 FETCH，但有下列限制：  
  
-   OVER 子句不支援 OFFSET 和 FETCH。  
  
-   OFFSET 和 FETCH 不能直接在 INSERT、UPDATE、MERGE 和 DELETE 陳述式中指定，但是可以在這些陳述式中所定義的子查詢中指定。 例如，在 INSERT INTO SELECT 陳述式中，OFFSET 和 FETCH 可以在 SELECT 陳述式中指定。  
  
-   在使用 UNION、EXCEPT 或 INTERSECT 運算子的查詢中，只能在指定查詢結果順序的最後查詢中指定 OFFSET 和 FETCH。  
  
-   TOP 無法與相同查詢運算式 (相同查詢範圍) 中的 OFFSET 和 FETCH 結合。  
  
## <a name="using-offset-and-fetch-to-limit-the-rows-returned"></a>使用 OFFSET 和 FETCH 限制傳回的資料列  
 我們建議您使用 OFFSET 和 FETCH 子句 (而不要使用 TOP 子句)，來實作查詢分頁方案，並限制傳送給用戶端應用程式的資料列數目。  
  
 如果使用 OFFSET 和 FETCH 做為分頁方案，需要針對傳回給用戶端應用程式的每一「頁」資料執行查詢一次。 例如，若要以 10 個資料列的增量傳回查詢結果，您必須執行一次查詢傳回 1 到 10 的資料列，然後再執行一次查詢傳回 11 到 20 的資料列，依此類推。 每個查詢各自獨立，無論如何都不相關。 這表示，不同於使用資料指標執行查詢一次，並在伺服器上維護狀態，用戶端應用程式會負責追蹤狀態。 若要使用 OFFSET 和 FETCH，在查詢要求之間達到穩定結果，必須符合下列條件：  
  
1.  查詢所使用的基礎資料不可以變更。 也就是說，查詢接觸的資料列不會更新，或者對網頁的所有查詢要求都是在使用快照集或可序列化交易隔離的單一交易中執行。 如需有關這些交易隔離等級的詳細資訊，請參閱[SET TRANSACTION ISOLATION LEVEL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
2.  ORDER BY 子句包含的資料行或資料行組合保證是唯一。  
  
 請參閱本主題稍後的＜範例＞一節中的範例＜在單一交易中執行多個查詢＞。  
  
 如果一致的執行計畫是分頁方案的要素，請考慮為 OFFSET 和 FETCH 參數使用 OPTIMIZE FOR 查詢提示。 請參閱本主題稍後的＜範例＞一節中的＜為 OFFSET 和 FETCH 值指定運算式＞。 如需有關 OPTIMZE FOR 的詳細資訊，請參閱[查詢提示 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="examples"></a>範例  
  
|類別目錄|代表性語法元素|  
|--------------|------------------------------|  
|[基本語法](#BasicSyntax)|ORDER BY|  
|[指定遞增和遞減順序](#SortOrder)|DESC • ASC|  
|[指定的定序](#Collation)|COLLATE|  
|[指定條件順序](#Case)|CASE 運算式|  
|[次序函數中使用 ORDER BY](#Rank)|排名函數|  
|[限制資料列數目傳回](#Offset)|OFFSET • FETCH|  
|[使用 ORDER BY 使用 UNION、 EXCEPT 和 INTERSECT](#Union)|UNION|  
  
###  <a name="BasicSyntax"></a>基本語法  
 本節的範例會使用所需的最少語法來示範 ORDER BY 子句的基本功能。  
  
#### <a name="a-specifying-a-single-column-defined-in-the-select-list"></a>A. 指定選取清單中所定義的單一資料行  
 下列範例會依據數值 `ProductID` 資料行來排序結果集。 因為未指定特定的排序次序，所以會使用預設值 (遞增順序)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY ProductID;  
```  
  
#### <a name="b-specifying-a-column-that-is-not-defined-in-the-select-list"></a>B. 指定選取清單中未定義的資料行  
 在下列範例中，結果集排序依據的資料行並不包含在選取清單中，而是定義在 FROM 子句中所指定的資料表中。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
ORDER BY ListPrice;  
  
```  
  
#### <a name="c-specifying-an-alias-as-the-sort-column"></a>C. 指定別名做為排序資料行  
 下列範例會指定資料行別名 `SchemaName` 做為排序次序資料行。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name, SCHEMA_NAME(schema_id) AS SchemaName  
FROM sys.objects  
WHERE type = 'U'  
ORDER BY SchemaName;  
  
```  
  
#### <a name="d-specifying-an-expression-as-the-sort-column"></a>D. 指定運算式做為排序資料行  
 下列範例會使用運算式做為排序資料行。 運算式是透過使用 DATEPART 函數來定義，以依據員工雇用年度來排序結果集。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY DATEPART(year, HireDate);  
  
```  
  
###  <a name="SortOrder"></a>指定遞增和遞減排序次序  
  
#### <a name="a-specifying-a-descending-order"></a>A. 指定遞減順序  
 下列範例會依據數值資料行 `ProductID` 以遞減順序來排序結果集。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY ProductID DESC;  
  
```  
  
#### <a name="b-specifying-an-ascending-order"></a>B. 指定以遞增的順序  
 下列範例會依據資料行 `Name` 以遞增順序來排序結果集。 依字母順序、 不是以數值排序的字元。 也就是說，10 會排序在 2 之前。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name FROM Production.Product  
WHERE Name LIKE 'Lock Washer%'  
ORDER BY Name ASC ;  
  
```  
  
#### <a name="c-specifying-both-ascending-and-descending-order"></a>C. 指定遞增和遞減順序  
 下列範例會依據兩個資料行來排序結果集。 查詢的結果集會先依據 `FirstName` 資料行以遞增順序排序，然後再依據 `LastName` 資料行以遞減順序排序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT LastName, FirstName FROM Person.Person  
WHERE LastName LIKE 'R%'  
ORDER BY FirstName ASC, LastName DESC ;  
  
```  
  
###  <a name="Collation"></a>指定的定序  
 下列範例示範 ORDER BY 子句中指定定序會如何變更傳回查詢結果的順序。 建立的資料表中包含一個資料行，這個資料行是透過使用不區分大小寫、不區分腔調字的定序來定義。 插入的值有各種不同的大小寫和腔調字。 因為 ORDER BY 子句中未指定定序，所以第一個查詢會在排序值時使用資料行的定序。 在第二個查詢中，ORDER BY 子句中指定區分大小寫、區分腔調字的定序，這變更傳回資料列的順序。  
  
```  
USE tempdb;  
GO  
CREATE TABLE #t1 (name nvarchar(15) COLLATE Latin1_General_CI_AI)  
GO  
INSERT INTO #t1 VALUES(N'Sánchez'),(N'Sanchez'),(N'sánchez'),(N'sanchez');  
  
-- This query uses the collation specified for the column 'name' for sorting.  
SELECT name  
FROM #t1  
ORDER BY name;  
-- This query uses the collation specified in the ORDER BY clause for sorting.  
SELECT name  
FROM #t1  
ORDER BY name COLLATE Latin1_General_CS_AS;  
  
```  
  
###  <a name="Case"></a>指定條件順序  
 下列範例在 ORDER BY 子句中使用 CASE 運算式，以條件方式判斷根據給定的資料行值的資料列的排序次序。 在第一則範例中，系統會評估 `SalariedFlag` 資料表之 `HumanResources.Employee` 資料行的值。 將 `SalariedFlag` 設定為 1 的員工會以 `BusinessEntityID` 的遞減順序傳回。 將 `SalariedFlag` 設定為 0 的員工會以 `BusinessEntityID` 的遞增順序傳回。 在第二則範例中，結果集會依照資料行 `TerritoryName` 排序 (當資料行 `CountryRegionName` 等於 'United States' 時) 以及依照 `CountryRegionName` 排序 (針對所有其他資料列)。  
  
```  
SELECT BusinessEntityID, SalariedFlag  
FROM HumanResources.Employee  
ORDER BY CASE SalariedFlag WHEN 1 THEN BusinessEntityID END DESC  
        ,CASE WHEN SalariedFlag = 0 THEN BusinessEntityID END;  
GO  
  
```  
  
```  
SELECT BusinessEntityID, LastName, TerritoryName, CountryRegionName  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL  
ORDER BY CASE CountryRegionName WHEN 'United States' THEN TerritoryName  
         ELSE CountryRegionName END;  
  
```  
  
###  <a name="Rank"></a>次序函數中使用 ORDER BY  
 下列範例在 ROW_NUMBER、RANK、DENSE_RANK 和 NTILE 次序函數中使用 ORDER BY 子句。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,ROW_NUMBER() OVER (ORDER BY a.PostalCode) AS "Row Number"  
    ,RANK() OVER (ORDER BY a.PostalCode) AS "Rank"  
    ,DENSE_RANK() OVER (ORDER BY a.PostalCode) AS "Dense Rank"  
    ,NTILE(4) OVER (ORDER BY a.PostalCode) AS "Quartile"  
    ,s.SalesYTD, a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL AND SalesYTD <> 0;  
  
```  
  
###  <a name="Offset"></a>限制資料列數目傳回  
 下列範例使用 OFFSET 和 FETCH 來限制查詢所傳回的資料列數目。  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
#### <a name="a-specifying-integer-constants-for-offset-and-fetch-values"></a>A. 為 OFFSET 和 FETCH 值指定整數常數  
 下列範例會指定整數常數做為 OFFSET 和 FETCH 子句的值。 第一個查詢傳回依資料行 `DepartmentID` 排序的所有資料列。 比較這個查詢所傳回的結果與後面兩個查詢的結果。 下一個查詢使用子句 `OFFSET 5 ROWS` 略過前 5 個資料列，並傳回所有其餘的資料列。 最後查詢使用子句 `OFFSET 0 ROWS` 從第一個資料列開始，然後再使用 `FETCH NEXT 10 ROWS ONLY`，將傳回的資料列限制在已排序結果集內的 10 個資料列。  
  
```  
USE AdventureWorks2012;  
GO  
-- Return all rows sorted by the column DepartmentID.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID;  
  
-- Skip the first 5 rows from the sorted result set and return all remaining rows.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID OFFSET 5 ROWS;  
  
-- Skip 0 rows and return only the first 10 rows from the sorted result set.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID   
    OFFSET 0 ROWS  
    FETCH NEXT 10 ROWS ONLY;  
  
```  
  
#### <a name="b-specifying-variables-for-offset-and-fetch-values"></a>B. 為 OFFSET 和 FETCH 值指定變數  
 下列範例會宣告變數 `@StartingRowNumber` 和 `@FetchRows`，並在 OFFSET 和 FETCH 子句中指定這些變數。  
  
```  
USE AdventureWorks2012;  
GO  
-- Specifying variables for OFFSET and FETCH values    
DECLARE @StartingRowNumber tinyint = 1  
      , @FetchRows tinyint = 8;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber ROWS   
    FETCH NEXT @FetchRows ROWS ONLY;  
  
```  
  
#### <a name="c-specifying-expressions-for-offset-and-fetch-values"></a>C. 為 OFFSET 和 FETCH 值指定運算式  
 下列範例使用 `@StartingRowNumber - 1` 運算式來指定 OFFSET 值，並使用 `@EndingRowNumber - @StartingRowNumber + 1` 運算式來指定 FETCH 值。 此外，也指定 OPTIMIZE FOR 查詢提示。 在查詢進行編譯和最佳化時，此提示可用來提供區域變數的特定值。 只有在查詢最佳化期間，才使用這個值，在查詢執行期間，不使用這個值。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Specifying expressions for OFFSET and FETCH values      
DECLARE @StartingRowNumber tinyint = 1  
      , @EndingRowNumber tinyint = 8;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber - 1 ROWS   
    FETCH NEXT @EndingRowNumber - @StartingRowNumber + 1 ROWS ONLY  
OPTION ( OPTIMIZE FOR (@StartingRowNumber = 1, @EndingRowNumber = 20) );  
  
```  
  
#### <a name="d-specifying-a-constant-scalar-subquery-for-offset-and-fetch-values"></a>D. 為 OFFSET 和 FETCH 值指定常數純量子查詢  
 下列範例使用常數純量子查詢來定義 FETCH 子句的值。 子查詢會從 `PageSize` 資料表中的 `dbo.AppSettings` 資料行傳回單一值。  
  
```  
-- Specifying a constant scalar subquery  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.AppSettings (AppSettingID int NOT NULL, PageSize int NOT NULL);  
GO  
INSERT INTO dbo.AppSettings VALUES(1, 10);  
GO  
DECLARE @StartingRowNumber tinyint = 1;  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber ROWS   
    FETCH NEXT (SELECT PageSize FROM dbo.AppSettings WHERE AppSettingID = 1) ROWS ONLY;  
  
```  
  
#### <a name="e-running-multiple-queries-in-a-single-transaction"></a>E. 在單一交易中執行多個查詢  
 下列範例示範實作分頁方案的其中一種方法，可確保所有查詢要求中傳回穩定的結果。 在使用快照集隔離等級的單一交易中執行查詢，而且 ORDER BY 子句中指定的資料行可確保資料行唯一性。  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Ensure the database can support the snapshot isolation level set for the query.  
IF (SELECT snapshot_isolation_state FROM sys.databases WHERE name = N'AdventureWorks2012') = 0  
    ALTER DATABASE AdventureWorks2012 SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
  
-- Set the transaction isolation level  to SNAPSHOT for this query.  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
  
-- Beging the transaction  
BEGIN TRANSACTION;  
GO  
-- Declare and set the variables for the OFFSET and FETCH values.  
DECLARE @StartingRowNumber int = 1  
      , @RowCountPerPage int = 3;  
  
-- Create the condition to stop the transaction after all rows have been returned.  
WHILE (SELECT COUNT(*) FROM HumanResources.Department) >= @StartingRowNumber  
BEGIN  
  
-- Run the query until the stop condition is met.  
SELECT DepartmentID, Name, GroupName  
FROM HumanResources.Department  
ORDER BY DepartmentID ASC   
    OFFSET @StartingRowNumber - 1 ROWS   
    FETCH NEXT @RowCountPerPage ROWS ONLY;  
  
-- Increment @StartingRowNumber value.  
SET @StartingRowNumber = @StartingRowNumber + @RowCountPerPage;  
CONTINUE  
END;  
GO  
COMMIT TRANSACTION;  
GO  
  
```  
  
###  <a name="Union"></a>使用 ORDER BY 使用 UNION、 EXCEPT 和 INTERSECT  
 當查詢使用 UNION、EXCEPT 或 INTERSECT 運算子時，ORDER BY 子句必須在陳述式結尾處指定，合併的查詢結果才會排序。 下列範例會傳回紅色或黃色的所有產品，並依據資料行 `ListPrice` 排序此組合清單。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Color, ListPrice  
FROM Production.Product  
WHERE Color = 'Red'  
-- ORDER BY cannot be specified here.  
UNION ALL  
SELECT Name, Color, ListPrice  
FROM Production.Product  
WHERE Color = 'Yellow'  
ORDER BY ListPrice ASC;  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例示範的結果集的數值排序`EmployeeKey`以遞增順序的資料行。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY EmployeeKey;  
```  
  
 下列範例訂單的結果集的數值`EmployeeKey`資料行以遞減的順序。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY EmployeeKey DESC;  
```  
  
 下列範例訂單的結果集所`LastName`資料行。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY LastName;  
```  
  
 下列範例訂單的兩個資料行。 此查詢第一次會以遞增順序排序`FirstName`資料行，然後再排序常見`FirstName`值以遞減的順序`LastName`資料行。  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, FirstName, LastName FROM DimEmployee  
WHERE LastName LIKE 'A%'  
ORDER BY LastName, FirstName;  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [排名函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [TOP &#40;TRANSACT-SQL &#41;](../../t-sql/queries/top-transact-sql.md)   
 [查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)   
 [除了及 INTERSECT &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)   
 [聯集 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/set-operators-union-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  

