---
title: "計數 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT_TSQL
- COUNT
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT function
- totals [SQL Server]
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT function [Transact-SQL]
ms.assetid: 28d39da6-bc2e-46c7-858c-b1721c938830
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0342e593b0bf13b5e5a9b53600aae5f3c39ae59d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="count-transact-sql"></a>COUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回群組中的項目數。 COUNT 的運作方式類似[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)函式。 這兩個函數的唯一差異是它們的傳回值。 COUNT 一律會傳回**int**資料類型值。 COUNT_BIG 一律會傳回**bigint**資料類型值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )   
    [ OVER (   
        [ partition_by_clause ]   
        [ order_by_clause ]   
        [ ROW_or_RANGE_clause ]  
    ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregation Function Syntax  
COUNT ( { [ [ ALL | DISTINCT ] expression ] | * } )  

-- Analytic Function Syntax  
COUNT ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>引數  
**ALL**  
將彙總函式套用至所有值。 ALL 是預設值。
  
DISTINCT  
指定 COUNT 傳回唯一非 Null 值的數目。
  
*expression*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)以外的任何類型的**文字**，**映像**，或**ntext**。 不允許彙總函式和子查詢。
  
\*  
指定應該計算所有資料列，以傳回資料表中的資料列總數。 計數 (\*) 沒有參數，無法搭配 DISTINCT 來使用。 計數 (\*) 不需要*運算式*參數，因為根據定義，它不使用任何特定資料行的相關資訊。 COUNT(*) 會傳回指定資料表中不迴避複製的資料列數。 它會個別計算每個資料列。 其中包括含有 Null 值的資料列。
  
透過**(** [ *partition_by_clause* ] [ *order_by_clause* ] [ *ROW_or_RANGE_clause* ] **)**  
*partition_by_clause*將分割成資料分割要套用函式的 FROM 子句所產生的結果集。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。 *order_by_clause*決定執行作業的邏輯順序。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>傳回型別
 **int**  
  
## <a name="remarks"></a>備註  
COUNT(*) 會傳回群組中的項目數。 其中包括 NULL 值和複本。
  
計數 (所有*運算式*) 評估*運算式*每個資料列群組中，並傳回非 null 值的數目。
  
COUNT (DISTINCT*運算式*) 評估*運算式*每個資料列群組中，並傳回唯一且非 null 值的數目。
  
如果傳回值大於 2^31-1，COUNT 會產生錯誤。 請改用 COUNT_BIG。
  
COUNT 未搭配 OVER 和 ORDER BY 子句使用時，是具決定性函數。 使用 OVER 和 ORDER BY 子句指定時，則不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
## <a name="examples"></a>範例  
  
### <a name="a-using-count-and-distinct"></a>A. 使用 COUNT 與 DISTINCT  
下列範例會列出在 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 工作的員工所能擁有的不同職稱數目。
  
```sql
SELECT COUNT(DISTINCT Title)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67  
  
(1 row(s) affected)
```
  
### <a name="b-using-count"></a>B. 使用 COUNT(*)  
下列範例會尋找在 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 工作的員工總數。
  
```sql
SELECT COUNT(*)  
FROM HumanResources.Employee;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
290  
  
(1 row(s) affected)
```
  
### <a name="c-using-count-with-other-aggregates"></a>C. 搭配其他彙總使用 COUNT(*)  
下列範例會顯示 `COUNT(*)` 可以結合選取清單中的其他彙總函式。 此範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。
  
```sql
SELECT COUNT(*), AVG(Bonus)  
FROM Sales.SalesPerson  
WHERE SalesQuota > 25000;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
----------- ---------------------
14            3472.1428
  
(1 row(s) affected)
```
  
### <a name="d-using-the-over-clause"></a>D. 使用 OVER 子句  
下列範例會將 MIN、MAX、AVG 和 COUNT 函數搭配 OVER 子句一起使用，為 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之 `HumanResources.Department` 資料表中的各部門提供彙總值。
  
```sql
SELECT DISTINCT Name  
       , MIN(Rate) OVER (PARTITION BY edh.DepartmentID) AS MinSalary  
       , MAX(Rate) OVER (PARTITION BY edh.DepartmentID) AS MaxSalary  
       , AVG(Rate) OVER (PARTITION BY edh.DepartmentID) AS AvgSalary  
       ,COUNT(edh.BusinessEntityID) OVER (PARTITION BY edh.DepartmentID) AS EmployeesPerDept  
FROM HumanResources.EmployeePayHistory AS eph  
JOIN HumanResources.EmployeeDepartmentHistory AS edh  
     ON eph.BusinessEntityID = edh.BusinessEntityID  
JOIN HumanResources.Department AS d  
ON d.DepartmentID = edh.DepartmentID
WHERE edh.EndDate IS NULL  
ORDER BY Name;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Name                          MinSalary             MaxSalary             AvgSalary             EmployeesPerDept  
----------------------------- --------------------- --------------------- --------------------- ----------------  
Document Control              10.25                 17.7885               14.3884               5  
Engineering                   32.6923               63.4615               40.1442               6  
Executive                     39.06                 125.50                68.3034               4  
Facilities and Maintenance    9.25                  24.0385               13.0316               7  
Finance                       13.4615               43.2692               23.935                10  
Human Resources               13.9423               27.1394               18.0248               6  
Information Services          27.4038               50.4808               34.1586               10  
Marketing                     13.4615               37.50                 18.4318               11  
Production                    6.50                  84.1346               13.5537               195  
Production Control            8.62                  24.5192               16.7746               8  
Purchasing                    9.86                  30.00                 18.0202               14  
Quality Assurance             10.5769               28.8462               15.4647               6  
Research and Development      40.8654               50.4808               43.6731               4  
Sales                         23.0769               72.1154               29.9719               18  
Shipping and Receiving        9.00                  19.2308               10.8718               6  
Tool Design                   8.62                  29.8462               23.5054               6  
  
(16 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-count-and-distinct"></a>E. 使用 COUNT 與 DISTINCT  
下列範例會列出特定公司的員工可以保存的不同項目數目。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(DISTINCT Title)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-----------
67
```  
  
### <a name="f-using-count"></a>F. 使用 COUNT(*)  
下列範例會傳回中的資料列總數`dbo.DimEmployee`資料表。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(*)  
FROM dbo.DimEmployee;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
-------------
296
```  
  
### <a name="g-using-count-with-other-aggregates"></a>G. 搭配其他彙總使用 COUNT(*)  
下列範例會結合`COUNT(*)`與選取清單中的其他彙總函式。 查詢會傳回與年度的銷售配額的銷售代表的數量大於 $500000，平均銷售配額。
  
```sql
USE ssawPDW;  
  
SELECT COUNT(EmployeeKey) AS TotalCount, AVG(SalesAmountQuota) AS [Average Sales Quota]  
FROM dbo.FactSalesQuota  
WHERE SalesAmountQuota > 500000 AND CalendarYear = 2001;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
TotalCount  Average Sales Quota
----------  -------------------
10          683800.0000
```
  
### <a name="h-using-count-with-having"></a>H. 使用 HAVING COUNT  
下列範例會傳回部門中有超過 15 個員工的公司使用與 HAVING 子句的計數。
  
```sql
USE ssawPDW;  
  
SELECT DepartmentName,   
       COUNT(EmployeeKey)AS EmployeesInDept  
FROM dbo.DimEmployee  
GROUP BY DepartmentName  
HAVING COUNT(EmployeeKey) > 15;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
DepartmentName  EmployeesInDept
--------------  ---------------
Sales           18
Production      179
```
  
### <a name="i-using-count-with-over"></a>I. 使用容錯移轉的計數  
下列範例搭配 OVER 子句使用計數，來傳回每個指定的銷售訂單中所包含的產品數目。
  
```sql
USE ssawPDW;  
  
SELECT DISTINCT COUNT(ProductKey) OVER(PARTITION BY SalesOrderNumber) AS ProductCount  
    ,SalesOrderNumber  
FROM dbo.FactInternetSales  
WHERE SalesOrderNumber IN (N'SO53115',N'SO55981');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
ProductCount   SalesOrderID`
------------   -----------------
3              SO53115
1              SO55981
```
  
## <a name="see-also"></a>另請參閱
[彙總函式 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT_BIG &#40;TRANSACT-SQL &#41;](../../t-sql/functions/count-big-transact-sql.md)  
[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  


