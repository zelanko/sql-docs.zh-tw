---
title: "TOP (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
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
- TOP_TSQL
- TOP
dev_langs: TSQL
helpviewer_keywords:
- TOP clause
- first set of query result rows [SQL Server]
- TOP clause, about TOP clause
- queries [SQL Server], results
ms.assetid: da983c0a-06c5-4cf8-a6a4-7f9d66f34f2c
caps.latest.revision: "60"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 9e00921e1b97ffb6cf732445569a913533d8f4f9
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="top-transact-sql"></a>TOP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，將查詢結果集中所傳回的資料列數限制為指定數目的資料列或是資料列的百分比。 當 TOP 與 ORDER BY 子句一起使用時，結果集是限制為前*N*個已排序資料列，否則會傳回前*N*未定義順序中的資料列數字。 使用這個子句以指定 SELECT 陳述式所傳回的資料列數目或受到 INSERT、UPDATE、MERGE 或 DELETE 陳述式所影響的資料列數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[   
    TOP (expression) [PERCENT]  
    [ WITH TIES ]  
]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[   
    TOP ( expression )   
    [ WITH TIES ]  
]  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 這是指定要傳回的資料列數目之數值運算式。 *運算式*隱含地轉換成**float**值如果百分比已指定，否則，它會轉換成**bigint**。  
  
 PERCENT  
 表示查詢傳回的第一個*運算式*從結果集中的資料列的百分比。 含小數的值會無條件進位到下一個整數值。  
  
 WITH TIES  
 當您想要針對限制結果集中的最後一個位數傳回兩個或多個繫結的資料列時使用。 必須搭配**ORDER BY**子句。 **WITH TIES**可能會導致傳回比中指定的值的多個資料列*運算式*。 例如，如果*運算式*設為 5，但 2 的值的其他資料列符合**ORDER BY**列 5，結果集資料行中的會包含 7 個資料列。  
  
 只有在 SELECT 陳述式中，且只在指定了 ORDER BY 子句時，才能指定 TOP...WITH TIES。 有同值記錄的傳回順序是任意的。 ORDER BY 不會影響此規則。  
  
## <a name="best-practices"></a>最佳作法  
 在 SELECT 陳述式中，永遠搭配 TOP 子句使用 ORDER BY 子句。 這是以預測的方式指示哪些資料列受到 TOP 影響的唯一方法。  
  
 在 ORDER BY 子句中使用 OFFSET 和 FETCH 子句 (而不要使用 TOP 子句)，來實作查詢分頁方案。 使用 OFFSET 和 FETCH 子句，比較容易實作分頁方案 (也就是將資料區塊或「頁面」傳送到用戶端)。 如需詳細資訊，請參閱 [ORDER BY 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)。  
  
 使用 TOP 或 OFFSET 和 FETCH (而不要使用 SET ROWCOUNT) 來限制傳回的資料列數目。 這些方法優於 SET ROWCOUNT 用法，原因如下：  
  
-   SELECT 陳述式，查詢最佳化工具可以考量的值*運算式*在查詢最佳化期間 TOP 或 FETCH 子句中。 因為 SET ROWCOUNT 是在執行查詢的陳述式之外使用，所以它的值不能在查詢計劃中列入考量。  
  
## <a name="compatibility-support"></a>相容性支援  
 基於回溯相容性，括號在 SELECT 陳述式中是選擇性。 我們建議您永遠在 SELECT 陳述式中的 TOP 使用括號，以便與 INSERT、UPDATE、MERGE 和 DELETE 陳述式中的必要括號保持一致性。  
  
## <a name="interoperability"></a>互通性  
 TOP 運算式不會影響因觸發程序而執行的陳述式。 **插入**和**刪除**觸發程序中的資料表會傳回真正受 INSERT、 UPDATE、 MERGE 或 DELETE 陳述式的資料列。 例如，如果因使用 TOP 子句的 INSERT 陳述式而引發 INSERT TRIGGER，  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許透過檢視表更新資料列。 由於 TOP 子句可包含在檢視表定義中，因此，如果資料列不再符合 TOP 運算式的需求，部分資料列可能會因更新而在檢視表中消失。  
  
 MERGE 陳述式中指定時，會套用 TOP 子句*之後*整個來源資料表和整個目標資料表聯結在一起，並移除不符合插入、 更新或刪除動作的聯結資料列。 TOP 子句會進一步將聯結的資料列數減少為指定的值，而且插入、更新或刪除動作會依照未排序的方式套用到剩餘的聯結資料列。 也就是說，將資料列散發到 WHEN 子句中定義的動作時，沒有任何特定順序。 例如，如果指定 TOP (10) 會影響 10 個資料列，在這些資料列中，可能會更新 7 個及插入 3 個，或者可能會刪除 1 個、更新 5 個及插入 4 個，依此類推。 因為 MERGE 陳述式會針對來源和目標資料表執行完整資料表掃描，所以當使用 TOP 子句，藉由建立多個批次來修改大型資料表時，I/O 效能可能會受到影響。 在此狀況中，請務必確保所有後續批次都是以新的資料列為目標。  
  
 在查詢中指定包含了 UNION、UNION ALL、EXCEPT 或 INTERSECT 運算子的 TOP 子句時，請特別小心。 您可能撰寫一個傳回非預期結果的查詢，因為當這些運算子用於選取作業時，TOP 和 ORDER BY 子句的邏輯處理順序不一定是直覺式。 例如，提供下列資料表和資料時，假設您想要傳回最便宜的紅色汽車和最便宜的藍色汽車。 也就是紅色轎車和藍色小貨車。  
  
```  
CREATE TABLE dbo.Cars(Model varchar(15), Price money, Color varchar(10));  
INSERT dbo.Cars VALUES  
    ('sedan', 10000, 'red'), ('convertible', 15000, 'blue'),   
    ('coupe', 20000, 'red'), ('van', 8000, 'blue');  
```  
  
 若要達成這些結果，您可能撰寫下列查詢。  
  
```  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'red'  
UNION ALL  
SELECT TOP(1) Model, Color, Price  
FROM dbo.Cars  
WHERE Color = 'blue'  
ORDER BY Price ASC;  
```  
  
 以下為結果集：  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 convertible   blue       15000.00
 ```  
  
 傳回未預期的結果，因為 TOP 子句邏輯上在 ORDER BY 子句之前執行，這樣會排序運算子的結果 (在此例中為 UNION ALL)。 因此，上一個查詢會傳回任何一輛紅色汽車和任何一輛藍色汽車，然後依價格來排序該聯集的結果。 下列範例會顯示為了達到所要的結果，正確撰寫查詢的方法。  
  
```  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'red'  
      ORDER BY Price ASC) AS a  
UNION ALL  
SELECT Model, Color, Price  
FROM (SELECT TOP(1) Model, Color, Price  
      FROM dbo.Cars  
      WHERE Color = 'blue'  
      ORDER BY Price ASC) AS b;  
```  
  
 藉由在子選擇作業中使用 TOP 和 ORDER BY，可以確保在套用至 TOP 子句時會使用 ORDER BY 子句的結果，而不會排序 UNION 作業的結果。  
  
 以下為結果集：  
  
 ```
 Model         Color      Price  
 ------------- ---------- -------  
 sedan         red        10000.00  
 van           blue        8000.00
 ```  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 搭配 INSERT、UPDATE、MERGE 或 DELETE 使用 TOP 時，不會以任何順序排列參考的資料列，也不可以直接在這些陳述式中指定 ORDER BY 子句。 如果您需要使用 TOP 依有意義的時序來插入、刪除或修改資料列，TOP 必須與子選擇陳述式中指定的 ORDER BY 子句一起使用。 請參閱本主題稍後的＜範例＞一節。  
  
 TOP 不能用於分割區檢視上的 UPDATE 和 DELETE 陳述式。  
  
 TOP 無法與相同查詢運算式 (相同查詢範圍) 中的 OFFSET 和 FETCH 結合。 如需詳細資訊，請參閱 [ORDER BY 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
|類別目錄|代表性語法元素|  
|--------------|------------------------------|  
|[基本語法](#BasicSyntax)|TOP • PERCENT|  
|[包括相同值](#tie)|WITH TIES|  
|[限制受 DELETE、 INSERT 或 UPDATE 的資料列](#DML)|DELETE • INSERT • UPDATE|  
  
###  <a name="BasicSyntax"></a>基本語法  
 本節的範例會使用所需的最少語法來示範 ORDER BY 子句的基本功能。  
  
#### <a name="a-using-top-with-a-constant-value"></a>A. 搭配常數值使用 TOP  
 下列範例使用常數值，來指定查詢結果集內傳回的員工人數。 在第一個範例中，因為未使用 ORDER BY 子句，所以會傳回前 10 個未定義的資料列。 在第二個範例中，ORDER BY 子句用來傳回前 10 名最近雇用的員工。  
  
```  
USE AdventureWorks2012;  
GO  
-- Select the first 10 random employees.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee;  
GO  
-- Select the first 10 employees hired most recently.  
SELECT TOP(10)JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
  
```  
  
#### <a name="b-using-top-with-a-variable"></a>B. 搭配變數使用 TOP  
 下列範例使用變數，來指定查詢結果集內傳回的員工人數。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @p AS int = 10;  
SELECT TOP(@p)JobTitle, HireDate, VacationHours  
FROM HumanResources.Employee  
ORDER BY VacationHours DESC  
GO  
  
```  
  
#### <a name="c-specifying-a-percentage"></a>C. 指定百分比  
 下列範例使用 PERCENT，來指定查詢結果集內傳回的員工人數。 `HumanResources.Employee` 資料表有 290 名員工。 因為 290 的 5% 是含小數的值，所以此值會無條件進位到下一個整數。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TOP(5)PERCENT JobTitle, HireDate  
FROM HumanResources.Employee  
ORDER BY HireDate DESC;  
  
```  
  
###  <a name="tie"></a>包括相同值  
  
#### <a name="a-using-with-ties-to-include-rows-that-match-the-values-in-the-last-row"></a>A. 使用 WITH TIES 包含符合最後一個資料列中之值的資料列  
 下列範例會取得所有員工中薪資最高的 `10`%，且會依照薪資的遞減順序傳回。 指定 `WITH TIES` 可確定任何薪資是所傳回之最低薪資 (最後一個資料列) 的員工也會包含在結果集中，即使這麼做會超出員工的 `10`%，也是如此。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TOP(10)WITH TIES  
pp.FirstName, pp.LastName, e.JobTitle, e.Gender, r.Rate  
FROM Person.Person AS pp   
    INNER JOIN HumanResources.Employee AS e  
        ON pp.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeePayHistory AS r  
        ON r.BusinessEntityID = e.BusinessEntityID  
ORDER BY Rate DESC;  
  
```  
  
###  <a name="DML"></a>限制受 DELETE、 INSERT 或 UPDATE 的資料列  
  
#### <a name="a-using-top-to-limit-the-number-of-rows-deleted"></a>A. 使用 TOP 限制刪除的資料列數目  
 當 TOP (*n*) 子句與 DELETE 一起，則未定義的系列上執行刪除作業 *n* 個資料列。 也就是說，DELETE 陳述式會選擇任何 (*n*) 數目符合 WHERE 子句中定義之準則的資料列。 下列範例會從 `20` 資料表刪除到期日早於 2002 年 7 月 1 日的 `PurchaseOrderDetail` 個資料列。  
  
```  
USE AdventureWorks2012;  
GO  
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
  
```  
  
 如果您必須使用 TOP 依有意義的時序來刪除資料列，就必須在 subselect 陳述式中同時使用 TOP 和 ORDER BY。 下列查詢會刪除 `PurchaseOrderDetail` 資料表中具有最早到期日的 10 個資料列。 為確保只刪除 10 個資料列，subselect 陳述式 (`PurchaseOrderID`) 中指定的資料行是資料表的主索引鍵。 如果指定的資料行包含重複值，則在 subselect 陳述式中使用非索引鍵資料行會造成刪除 10 個以上的資料列。  
  
```  
USE AdventureWorks2012;  
GO  
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
#### <a name="b-using-top-to-limit-the-number-of-rows-inserted"></a>B. 使用 TOP 限制插入的資料列數目  
 下列範例會建立 `EmployeeSales` 資料表，而且會將 `HumanResources.Employee` 資料表的前 5 名員工的姓名和今年到目前的銷售資料插入其中。 INSERT 陳述式會選擇 `SELECT` 所傳回符合 WHERE 子句中所定義準則的任 5 個資料列。  OUTPUT 子句會顯示插入到 `EmployeeSales` 資料表的資料列。 請注意，SELECT 陳述式中的 ORDER BY 子句不會用來判斷前 5 名員工。  
  
```  
USE AdventureWorks2012 ;  
GO  
IF OBJECT_ID ('dbo.EmployeeSales', 'U') IS NOT NULL  
    DROP TABLE dbo.EmployeeSales;  
GO  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   nvarchar(11) NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  YearlySales  money NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
  
```  
  
 如果您必須使用 TOP 依有意義的時序來插入資料列，就必須搭配子選擇陳述式中指定的 ORDER BY 子句來使用 TOP，如下列範例所示。 OUTPUT 子句會顯示插入到 `EmployeeSales` 資料表的資料列。 請注意，現在插入的前 5 名員工是依據 ORDER BY 子句的結果，而不是未定義的資料列。  
  
```  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
  
```  
  
#### <a name="c-using-top-to-limit-the-number-of-rows-updated"></a>C. 使用 TOP 限制更新的資料列數目  
 下列範例會利用 TOP 子句來更新資料表中的資料列。 當 TOP (*n*) 子句與 UPDATE，則未定義的資料列數目上執行更新作業。 也就是說，UPDATE 陳述式會選擇任何 (*n*) 數目符合 WHERE 子句中定義之準則的資料列。 下列範例會從某位銷售人員指派 10 位客戶給另一位銷售人員。  
  
```  
USE AdventureWorks2012;  
UPDATE TOP (10) Sales.Store  
SET SalesPersonID = 276  
WHERE SalesPersonID = 275;  
GO  
```  
  
 如果您必須使用 TOP 依有意義的時間順序套用更新，就要在子選擇陳述式中同時使用 TOP 與 ORDER BY。 下例會更新最早雇用的前 10 名員工的休假時數。  
  
```  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回符合查詢準則的最上層 31 資料列。 **ORDER BY**子句用來確保 31 傳回資料列會先 31 取決於的字母順序排序的資料列`LastName`資料行。  
  
 使用**頂端**但未指定繫結。  
  
```  
SELECT TOP (31) FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
 結果： 會傳回 31 資料列。  
  
 使用 TOP，指定 WITH TIES。  
  
```  
SELECT TOP (31) WITH TIES FirstName, LastName   
FROM DimEmployee ORDER BY LastName;  
```  
  
 結果： 33 會傳回資料列，因為名為 Brown 3 員工有相同的第 31 資料列。  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [ORDER BY 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)   
 [SET ROWCOUNT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-rowcount-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  
  
  

