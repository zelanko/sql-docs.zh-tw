---
title: "建立使用者定義函式 (Database Engine) | Microsoft Docs"
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d4ea2a247e4d8a55cd3467510f19115cc3163bc2
ms.lasthandoff: 04/11/2017

---
# <a name="create-user-defined-functions-database-engine"></a>建立使用者定義函數 (Database Engine)
  本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立使用者定義函數 (UDF)。  

  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   使用者定義函數不能用來執行修改資料庫狀態的動作。  
  
-   使用者定義函數不得包含具有資料表當做其目標的 OUTPUT INTO 子句。  
  
-   使用者定義函數無法傳回多個結果集。 如果您需要傳回多個結果集，請使用預存程序。  
  
-   使用者定義函數中限制錯誤處理。 UDF 不支援 TRY…CATCH、@ERROR 或 RAISERROR。  
  
-   使用者定義函數無法呼叫預存程序，但是可以呼叫擴充預存程序。  
  
-   使用者定義函數無法利用動態 SQL 或暫存資料表。 允許使用資料表變數。  
  
-   使用者定義函數中不允許使用 SET 陳述式。  
  
-   不允許使用 FOR XML 子句  
  
-   使用者定義函數可以具有巢狀結構；也就是說，某個使用者定義函數可以呼叫另一個使用者定義函數。 被呼叫的函數開始執行時，巢狀層級會遞增；被呼叫的函數完成執行時，巢狀層級會遞減。 使用者定義函數所建立的巢狀結構最多可以有 32 個層級。 超過巢狀層級上限會導致整個呼叫函數鏈結失敗。 依照 32 個層級巢狀限制，Transact-SQL 使用者定義函數之 Managed 程式碼的任何參考都算是一個層級。 從 Managed 程式碼內叫用的方法，不列入這項限制。  
  
-   下列 Service Broker 陳述式 **無法包含在** Transact-SQL 使用者定義函數的定義中：  
  
    -   BEGIN DIALOG CONVERSATION  
  
    -   END CONVERSATION  
  
    -   GET CONVERSATION GROUP  
  
    -   MOVE CONVERSATION  
  
    -   RECEIVE  
  
    -   SEND  
  
###  <a name="Security"></a> Permissions 

需要資料庫中的 CREATE FUNCTION 權限，以及此函數建立所在之結構描述上的 ALTER 權限。 如果此函數指定使用者定義型別，則需要該型別的 EXECUTE 權限。  
  
##  <a name="Scalar"></a> 純量函數  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中建立多重陳述式純量函數。 這個函數使用了一個輸入值 `ProductID`，並傳回單一資料值，也就是指定產品的彙總存貨量。  
  
```  
IF OBJECT_ID (N'dbo.ufnGetInventoryStock', N'FN') IS NOT NULL  
    DROP FUNCTION ufnGetInventoryStock;  
GO  
CREATE FUNCTION dbo.ufnGetInventoryStock(@ProductID int)  
RETURNS int   
AS   
-- Returns the stock level for the product.  
BEGIN  
    DECLARE @ret int;  
    SELECT @ret = SUM(p.Quantity)   
    FROM Production.ProductInventory p   
    WHERE p.ProductID = @ProductID   
        AND p.LocationID = '6';  
     IF (@ret IS NULL)   
        SET @ret = 0;  
    RETURN @ret;  
END;  
GO  
  
```  
  
 以下範例會使用 `ufnGetInventoryStock` 函數來傳回 `ProductModelID` 介於 75 和 80 之間的產品目前的存貨量。  
  
```  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
  
```  
  
##  <a name="TVF"></a> 資料表值函式  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中建立內嵌資料表值函式。 這個函數使用了一個輸入參數，也就是客戶 (商店) 識別碼，並傳回 `ProductID`和 `Name`資料行，以及從年初至今將每項產品銷售給商店的彙總銷售額 `YTD Total` 。  
  
```  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
  
```  
  
 下例會叫用這個函數並指定客戶識別碼 602。  
  
```  
SELECT * FROM Sales.ufn_SalesByStore (602);  
  
```  
  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中建立資料表值函式。 這個函數使用單一輸入參數 `EmployeeID` ，並傳回一份清單，列出這位指定員工的所有直接或間接下屬。 然後叫用此函數並指定員工識別碼 109。  
  
```  
IF OBJECT_ID (N'dbo.ufn_FindReports', N'TF') IS NOT NULL  
    DROP FUNCTION dbo.ufn_FindReports;  
GO  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0 -- Get the initial list of Employees for Manager n  
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1 -- Join recursive member to anchor  
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
  
```  
  
## <a name="more-examples"></a>更多範例  
 - [使用者定義的函式](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 - [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md) 
  - [Alter Function (Transact SQL)](https://msdn.microsoft.com/library/ms173799.aspx) 
 - [Drop Function (Transact SQL)](https://msdn.microsoft.com/library/ms173799.aspx)
 - [Drop Partition Function (Transact SQL)](https://msdn.microsoft.com/library/ms187759(SQL.130).aspx)
 - [社群](https://www.bing.com/search?q=user%20defined%20function%20%22sql%20server%202016%22%20examples&qs=n&form=QBRE&pq=user%20defined%20function%20%22sql%20server%202016%22%20examples&sc=0-48&sp=-1&sk=&cvid=C3AD337125A840AD9EEFA3AAC36A3712)中有更多範例
  

