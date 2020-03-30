---
title: GROUPING_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GROUPING_ID_TSQL
- GROUPING_ID
dev_langs:
- TSQL
helpviewer_keywords:
- GROUP BY clause, GROUPING_ID
- GROUPING_ID function
ms.assetid: c1050658-b19f-42ee-9a05-ecd6a73b896c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 13680aea1d34b83d76647d39d0f40b84609b2e8c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "67910649"
---
# <a name="grouping_id-transact-sql"></a>GROUPING_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  這是計算群組層級的函數。 當指定 GROUP BY 時，GROUPING_ID 只能在 SELECT \<select> 清單、HAVING 或 ORDER BY 子句中使用。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
GROUPING_ID ( <column_expression>[ ,...n ] )  
```  
  
## <a name="arguments"></a>引數  
 \<column_expression>  
 為 *GROUP BY* 子句中的 [column_expression](../../t-sql/queries/select-group-by-transact-sql.md)。  
  
## <a name="return-type"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 GROUPING_ID \<column_expression> 必須完全符合 GROUP BY 清單中的運算式。 例如，若您要根據 DATEPART (yyyy, \<*column name*>) 分組，請使用 GROUPING_ID (DATEPART (yyyy, \<資料行名稱  >))。若您要根據 \<資料行名稱  > 分組，請使用 GROUPING_ID (\<資料行名稱  >)。  
  
## <a name="comparing-grouping_id--to-grouping-"></a>比較 GROUPING_ID () 與 GROUPING ()  
 GROUPING_ID (\<column_expression> [ **,** ...*n* ]) 針對每一個輸出資料列中資料行清單中的每一個資料行輸入等於 GROUPING (\<column_expression>) 傳回的項目 (當作一和零的字串)。 GROUPING_ID 會將此字串解譯為以 2 為基底的數字，並傳回對等的整數。 例如，假設有以下的陳述式：`SELECT a, b, c, SUM(d),``GROUPING_ID(a,b,c)``FROM T GROUP BY <group by list>`。 下表顯示 GROUPING_ID () 輸入和輸出值。  
  
|彙總資料行|GROUPING_ID (a, b, c) 輸入 = GROUPING(a) + GROUPING(b) + GROUPING(c)|GROUPING_ID () 輸出|  
|------------------------|---------------------------------------------------------------------------------------|------------------------------|  
|`a`|`100`|`4`|  
|`b`|`010`|`2`|  
|`c`|`001`|`1`|  
|`ab`|`110`|`6`|  
|`ac`|`101`|`5`|  
|`bc`|`011`|`3`|  
|`abc`|`111`|`7`|  
  
## <a name="technical-definition-of-grouping_id-"></a>GROUPING_ID () 的技術定義  
 每一個 GROUPING_ID 引數都必須是 GROUP BY 清單中的元素。 GROUPING_ID () 會傳回**整數**點陣圖，可能會引發其最低的 N 位元。 引發的**位元**表示對應的引數不是指定輸出資料列的群組資料行。 最低順位的**位元**會對應到引數 N；而第 N-1 個<sup></sup>最低順位的**位元**會對應到引數 1。  
  
## <a name="grouping_id--equivalents"></a>GROUPING_ID () 對等項目  
 如果是單一群組查詢，GROUPING (\<column_expression>) 會等於 GROUPING_ID (\<column_expression>) 並傳回 0。  
  
 例如，下列陳述式是相等的：  
  
 陳述式 A：  
  
```  
SELECT GROUPING_ID(A,B)  
FROM T   
GROUP BY CUBE(A,B)   
```  
  
 陳述式 B：  
  
```  
SELECT 3 FROM T GROUP BY ()  
UNION ALL  
SELECT 1 FROM T GROUP BY A  
UNION ALL  
SELECT 2 FROM T GROUP BY B  
UNION ALL  
SELECT 0 FROM T GROUP BY A,B  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-grouping_id-to-identify-grouping-levels"></a>A. 使用 GROUPING_ID 識別群組層級  
 下列範例會依據 `Name` 和 `Title`、`Name,` 和公司總數傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的員工計數。 `GROUPING_ID()` 會用來針對 `Title` 資料行中識別彙總層級的每一個資料列各建立一個值。  
  
```  
SELECT D.Name  
    ,CASE   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 0 THEN E.JobTitle  
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 1 THEN N'Total: ' + D.Name   
    WHEN GROUPING_ID(D.Name, E.JobTitle) = 3 THEN N'Company Total:'  
        ELSE N'Unknown'  
    END AS N'Job Title'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle);  
```  
  
### <a name="b-using-grouping_id-to-filter-a-result-set"></a>B. 使用 GROUPING_ID 篩選結果集  
  
#### <a name="simple-example"></a>簡單範例  
 在下列程式碼中，若只要依據職稱傳回具有員工計數的資料列，請從 `HAVING GROUPING_ID(D.Name, E.JobTitle); = 0` 資料庫的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 中移除註解字元。 若只要依據部門傳回具有員工計數的資料列，請從 `HAVING GROUPING_ID(D.Name, E.JobTitle) = 1;` 中移除註解字元。  
  
```  
SELECT D.Name  
    ,E.JobTitle  
    ,GROUPING_ID(D.Name, E.JobTitle) AS 'Grouping Level'  
    ,COUNT(E.BusinessEntityID) AS N'Employee Count'  
FROM HumanResources.Employee AS E  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS DH  
        ON E.BusinessEntityID = DH.BusinessEntityID  
    INNER JOIN HumanResources.Department AS D  
        ON D.DepartmentID = DH.DepartmentID       
WHERE DH.EndDate IS NULL  
    AND D.DepartmentID IN (12,14)  
GROUP BY ROLLUP(D.Name, E.JobTitle)  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 0; --All titles  
--HAVING GROUPING_ID(D.Name, E.JobTitle) = 1; --Group by Name;  
```  
  
 以下是未篩選的結果集。  
  
|名稱|Title|Grouping Level|Employee Count|名稱|  
|----------|-----------|--------------------|--------------------|----------|  
|Document Control|Control Specialist|0|2|Document Control|  
|Document Control|Document Control Assistant|0|2|Document Control|  
|Document Control|Document Control Manager|0|1|Document Control|  
|Document Control|NULL|1|5|Document Control|  
|Facilities and Maintenance|Facilities Administrative Assistant|0|1|Facilities and Maintenance|  
|Facilities and Maintenance|Facilities Manager|0|1|Facilities and Maintenance|  
|Facilities and Maintenance|Janitor|0|4|Facilities and Maintenance|  
|Facilities and Maintenance|Maintenance Supervisor|0|1|Facilities and Maintenance|  
|Facilities and Maintenance|NULL|1|7|Facilities and Maintenance|  
|NULL|NULL|3|12|NULL|  
  
#### <a name="complex-example"></a>複雜範例  
 下列範例使用 `GROUPING_ID()` 篩選包含多個群組層級的結果集 (藉由群組層級)。 類似的程式碼可用來建立有數個群組層級的檢視以及可呼叫此檢視的預存程序，其方式是傳遞藉由分組層級篩選檢視的參數。 此範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```  
DECLARE @Grouping nvarchar(50);  
DECLARE @GroupingLevel smallint;  
SET @Grouping = N'CountryRegionCode Total';  
  
SELECT @GroupingLevel = (  
    CASE @Grouping  
        WHEN N'Grand Total'             THEN 15  
        WHEN N'SalesPerson Total'       THEN 14  
        WHEN N'Store Total'             THEN 13  
        WHEN N'Store SalesPerson Total' THEN 12  
        WHEN N'CountryRegionCode Total' THEN 11  
        WHEN N'Group Total'             THEN 7  
        ELSE N'Unknown'  
    END);  
  
SELECT   
    T.[Group]  
    ,T.CountryRegionCode  
    ,S.Name AS N'Store'  
    ,(SELECT P.FirstName + ' ' + P.LastName   
        FROM Person.Person AS P   
        WHERE P.BusinessEntityID = H.SalesPersonID)  
        AS N'Sales Person'  
    ,SUM(TotalDue)AS N'TotalSold'  
    ,CAST(GROUPING(T.[Group])AS char(1)) +   
        CAST(GROUPING(T.CountryRegionCode)AS char(1)) +   
        CAST(GROUPING(S.Name)AS char(1)) +   
        CAST(GROUPING(H.SalesPersonID)AS char(1))   
        AS N'GROUPING base-2'  
    ,GROUPING_ID((T.[Group])  
        ,(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
        ) AS N'GROUPING_ID'  
    ,CASE   
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 15 THEN N'Grand Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 14 THEN N'SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 13 THEN N'Store Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 12 THEN N'Store SalesPerson Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) = 11 THEN N'CountryRegionCode Total'  
        WHEN GROUPING_ID(  
            (T.[Group]),(T.CountryRegionCode)  
            ,(S.Name),(H.SalesPersonID)  
            ) =  7 THEN N'Group Total'  
        ELSE N'Error'  
        END AS N'Level'  
FROM Sales.Customer AS C  
    INNER JOIN Sales.Store AS S  
        ON C.StoreID  = S.BusinessEntityID   
    INNER JOIN Sales.SalesTerritory AS T  
        ON C.TerritoryID  = T.TerritoryID   
    INNER JOIN Sales.SalesOrderHeader AS H  
        ON C.CustomerID = H.CustomerID  
GROUP BY GROUPING SETS ((S.Name,H.SalesPersonID)  
    ,(H.SalesPersonID),(S.Name)  
    ,(T.[Group]),(T.CountryRegionCode),()  
    )  
HAVING GROUPING_ID(  
    (T.[Group]),(T.CountryRegionCode),(S.Name),(H.SalesPersonID)  
    ) = @GroupingLevel  
ORDER BY   
    GROUPING_ID(S.Name,H.SalesPersonID),GROUPING_ID((T.[Group])  
    ,(T.CountryRegionCode)  
    ,(S.Name)  
    ,(H.SalesPersonID))ASC;  
```  
  
### <a name="c-using-grouping_id--with-rollup-and-cube-to-identify-grouping-levels"></a>C. 搭配 ROLLUP 和 CUBE 使用 GROUPING_ID () 來識別群組層級  
 下列範例的程式碼會示範如何使用 `GROUPING()` 來計算 `Bit Vector(base-2)` 資料行。 `GROUPING_ID()` 是用來計算對應的 `Integer Equivalent` 資料行。 `GROUPING_ID()` 函數中的資料行順序與 `GROUPING()` 函數串連之資料行的資料行順序相反。  
  
 在這些範例中，`GROUPING_ID()` 是用來針對 `Grouping Level` 資料行中的每一個資料列各建立一個值，以識別群組的層級。 群組層級不一定是以 1 (0、1、2...*n*) 開頭之整數的連續清單。  
  
> [!NOTE]  
>  GROUPING 和 GROUPING_ID 可用於 HAVING 子句來篩選結果集。  
  
#### <a name="rollup-example"></a>ROLLUP 範例  
 在此範例中，所有的群組層級不會與下列 CUBE 範例一樣出現。 如果 `ROLLUP` 清單中的資料行順序改變，`Grouping Level` 資料行中的層級值也必須改變。 此範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
     AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'not used'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY ROLLUP(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(mm,OrderDate)  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 以下為部分結果集。  
  
|Year|Month|Day|Total Due|Bit Vector (base-2)|Integer Equivalent|Grouping Level|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|Year Month Day|  
|2007|1|2|21772.3494|000|0|Year Month Day|  
|2007|2|1|2705653.5913|000|0|Year Month Day|  
|2007|2|2|21684.4068|000|0|Year Month Day|  
|2008|1|1|1908122.0967|000|0|Year Month Day|  
|2008|1|2|46458.0691|000|0|Year Month Day|  
|2008|2|1|3108771.9729|000|0|Year Month Day|  
|2008|2|2|54598.5488|000|0|Year Month Day|  
|2007|1|NULL|1519224.956|100|1|Year Month|  
|2007|2|NULL|2727337.9981|100|1|Year Month|  
|2008|1|NULL|1954580.1658|100|1|Year Month|  
|2008|2|NULL|3163370.5217|100|1|Year Month|  
|2007|NULL|NULL|4246562.9541|110|3|Year|  
|2008|NULL|NULL|5117950.6875|110|3|Year|  
|NULL|NULL|NULL|9364513.6416|111|7|總計|  
  
#### <a name="cube-example"></a>CUBE 範例  
 在此範例中，`GROUPING_ID()` 函數是用來針對 `Grouping Level` 資料行中的每一個資料列各建立一個值，以識別群組的層級。  
  
 與之前範例中的 `ROLLUP` 不同，`CUBE` 會輸出所有群組層級。 如果 `CUBE` 清單中的資料行順序改變，`Grouping Level` 資料行中的層級值也必須改變。 此範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,DATEPART(mm,OrderDate) AS N'Month'  
    ,DATEPART(dd,OrderDate) AS N'Day'  
    ,SUM(TotalDue) AS N'Total Due'  
    ,CAST(GROUPING(DATEPART(dd,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(mm,OrderDate))AS char(1)) +   
        CAST(GROUPING(DATEPART(yyyy,OrderDate))AS char(1))   
        AS N'Bit Vector(base-2)'  
    ,GROUPING_ID(DATEPART(yyyy,OrderDate)  
        ,DATEPART(mm,OrderDate)  
        ,DATEPART(dd,OrderDate))   
        AS N'Integer Equivalent'  
    ,CASE  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)  
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 0 THEN N'Year Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 1 THEN N'Year Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 2 THEN N'Year Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 3 THEN N'Year'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 4 THEN N'Month Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 5 THEN N'Month'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 6 THEN N'Day'  
        WHEN GROUPING_ID(DATEPART(yyyy,OrderDate)   
            ,DATEPART(mm,OrderDate),DATEPART(dd,OrderDate)  
            ) = 7 THEN N'Grand Total'  
    ELSE N'Error'  
    END AS N'Grouping Level'  
FROM Sales.SalesOrderHeader  
WHERE DATEPART(yyyy,OrderDate) IN(N'2007',N'2008')  
    AND DATEPART(mm,OrderDate) IN(1,2)  
    AND DATEPART(dd,OrderDate) IN(1,2)  
GROUP BY CUBE(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate))  
ORDER BY GROUPING_ID(DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate)  
    )  
    ,DATEPART(yyyy,OrderDate)  
    ,DATEPART(mm,OrderDate)  
    ,DATEPART(dd,OrderDate);  
```  
  
 以下為部分結果集。  
  
|Year|Month|Day|Total Due|Bit Vector (base-2)|Integer Equivalent|Grouping Level|  
|----------|-----------|---------|---------------|----------------------------|------------------------|--------------------|  
|2007|1|1|1497452.6066|000|0|Year Month Day|  
|2007|1|2|21772.3494|000|0|Year Month Day|  
|2007|2|1|2705653.5913|000|0|Year Month Day|  
|2007|2|2|21684.4068|000|0|Year Month Day|  
|2008|1|1|1908122.0967|000|0|Year Month Day|  
|2008|1|2|46458.0691|000|0|Year Month Day|  
|2008|2|1|3108771.9729|000|0|Year Month Day|  
|2008|2|2|54598.5488|000|0|Year Month Day|  
|2007|1|NULL|1519224.956|100|1|Year Month|  
|2007|2|NULL|2727337.9981|100|1|Year Month|  
|2008|1|NULL|1954580.1658|100|1|Year Month|  
|2008|2|NULL|3163370.5217|100|1|Year Month|  
|2007|NULL|1|4203106.1979|010|2|Year Day|  
|2007|NULL|2|43456.7562|010|2|Year Day|  
|2008|NULL|1|5016894.0696|010|2|Year Day|  
|2008|NULL|2|101056.6179|010|2|Year Day|  
|2007|NULL|NULL|4246562.9541|110|3|Year|  
|2008|NULL|NULL|5117950.6875|110|3|Year|  
|NULL|1|1|3405574.7033|001|4|Month Day|  
|NULL|1|2|68230.4185|001|4|Month Day|  
|NULL|2|1|5814425.5642|001|4|Month Day|  
|NULL|2|2|76282.9556|001|4|Month Day|  
|NULL|1|NULL|3473805.1218|101|5|Month|  
|NULL|2|NULL|5890708.5198|101|5|Month|  
|NULL|NULL|1|9220000.2675|011|6|Day|  
|NULL|NULL|2|144513.3741|011|6|Day|  
|NULL|NULL|NULL|9364513.6416|111|7|總計|  
  
## <a name="see-also"></a>另請參閱  
 [GROUPING &#40;Transact-SQL&#41;](../../t-sql/functions/grouping-transact-sql.md)   
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)  
  
  
