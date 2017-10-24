---
title: "聯集 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UNION
- UNION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UNION queries
- combining query results
- UNION operator [SQL Server]
ms.assetid: 607c296f-8a6a-49bc-975a-b8d0c0914df7
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 29f86913fd2fb6bf04c4c00d95427d34128c8fee
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-operators---union-transact-sql"></a>設定運算子為等位 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將兩個或更多查詢的結果結合成單一結果集，其中包括屬於聯集中之所有查詢的所有資料列。 UNION 作業不同於利用聯結來結合兩份資料表的資料行。  
  
 以下是利用 UNION 來組合兩項查詢的結果集之基本規則：  
  
-   在所有查詢中，資料行的數目和順序都必須相同。  
  
-   資料類型必須相容。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
    { <query_specification> | ( <query_expression> ) }   
  UNION [ ALL ]   
  <query_specification | ( <query_expression> )   
 [ UNION [ ALL ] <query_specification> | ( <query_expression> )   
    [ ...n ] ]   
```  
  
## <a name="arguments"></a>引數  
\<query_specification > |( \<query_expression >) 是一個查詢規格或查詢運算式會傳回要與另一個查詢規格或查詢運算式中的資料結合的資料。 UNION 作業中的資料行定義不必相同，但必須能夠透過隱含的轉換而相容。 當資料類型不同時，產生的資料類型取決於規則[資料類型優先順序](../../t-sql/data-types/data-type-precedence-transact-sql.md)。 當類型相同，但有效位數、小數位數或長度不同時，結果取決於相同的運算式組合規則。 如需詳細資訊，請參閱[有效位數、小數位數和長度 &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
 資料行的**xml**資料類型必須相等。 所有資料行都必須是 XML 結構描述類型，或不具類型。 如果具備類型，它們的類型必須是相同的 XML 結構描述集合。  
  
 UNION  
 指定組合多個結果集，以及當做單一結果集傳回。  
  
 ALL  
 將所有資料列納入結果中。 其中包括複本。 若未指定，就會移除資料列複本。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-a-simple-union"></a>A. 使用簡單 UNION  
 在下列範例中，結果集包括 `ProductModelID` 和 `Name` 資料表之 `ProductModel` 和 `Gloves` 資料行的內容。  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Here is the simple union.  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
```  
  
### <a name="b-using-select-into-with-union"></a>B. 搭配 UNION 使用 SELECT INTO  
 在下列範例中，第二個 `INTO` 陳述式中的 `SELECT` 子句指定利用名稱為 `ProductResults` 的資料表，保留 `ProductModel` 和 `Gloves` 資料表的指定資料行之聯集的最終結果集。 請注意，`Gloves` 資料表建立在第一個 `SELECT` 陳述式中。  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.ProductResults', 'U') IS NOT NULL  
DROP TABLE dbo.ProductResults;  
GO  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
INTO dbo.ProductResults  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
SELECT ProductModelID, Name   
FROM dbo.ProductResults;  
  
```  
  
### <a name="c-using-union-of-two-select-statements-with-order-by"></a>C. 搭配 ORDER BY 使用兩個 SELECT 陳述式的 UNION  
 搭配 UNION 子句使用之特定參數的順序非常重要。 下列範例會顯示在兩個 `UNION` 陳述式中的輸出重新命名一個資料行時，`SELECT` 的正確和不正確用法。  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
/* INCORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
ORDER BY Name  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
/* CORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
  
```  
  
### <a name="d-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>D. 利用三個 SELECT 陳述式的 UNION 來顯示 ALL 和括號的作用  
 下列範例會利用 `UNION` 來結合有 5 個相同資料列的三份資料表的結果。 第一個範例利用 `UNION ALL` 來顯示重複的記錄，以及傳回所有的 15 個資料列。 第二個範例利用不含 `UNION` 的 `ALL` 來刪除三個 `SELECT` 陳述式之組合結果中重複的資料列，並傳回 5 個資料列。  
  
 第三個範例搭配第一個 `ALL` 來使用 `UNION`，用括號括住未使用 `UNION` 的第二個 `ALL`。 第二個 `UNION` 會先處理，因為它在括號中，且會傳回 5 個資料列，因為並未使用 `ALL` 選項，複本會移除。 這 5 個資料列利用 `SELECT` 關鍵字，與第一個 `UNION ALL` 的結果結合起來。 這並不會在兩組 5 個資料列之間移除複本。 最終結果有 10 個資料列。  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.EmployeeOne', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeOne;  
GO  
IF OBJECT_ID ('dbo.EmployeeTwo', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeTwo;  
GO  
IF OBJECT_ID ('dbo.EmployeeThree', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeThree;  
GO  
  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeOne  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeTwo  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeThree  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
-- Union ALL  
SELECT LastName, FirstName, JobTitle  
FROM dbo.EmployeeOne  
UNION ALL  
SELECT LastName, FirstName ,JobTitle  
FROM dbo.EmployeeTwo  
UNION ALL  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle  
FROM dbo.EmployeeOne  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeOne  
UNION ALL  
(  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree  
);  
GO  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-simple-union"></a>E. 使用簡單 UNION  
 在下列範例中，結果集會包含的內容`CustomerKey`兩者的資料行`FactInternetSales`和`DimCustomer`資料表。 因為未使用 ALL 關鍵字，從結果中排除重複項目。  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="f-using-union-of-two-select-statements-with-order-by"></a>F. 搭配 ORDER BY 使用兩個 SELECT 陳述式的 UNION  
 UNION 陳述式中的任何 SELECT 陳述式包含 ORDER BY 子句，該子句應該有之後所有 SELECT 陳述式中。 下列範例顯示正確和不正確使用`UNION`兩個`SELECT`陳述式中搭配 ORDER BY 排序資料行。  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT  
SELECT CustomerKey   
FROM FactInternetSales    
ORDER BY CustomerKey  
UNION   
SELECT CustomerKey   
FROM DimCustomer  
ORDER BY CustomerKey;  
  
-- CORRECT   
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="g-using-union-of-two-select-statements-with-where-and-order-by"></a>G. 使用聯集的兩個 SELECT 陳述式使用 WHERE 和 ORDER BY  
 下列範例顯示正確和不正確使用`UNION`兩個`SELECT`陳述式的位置，且不需要 ORDER BY。  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT   
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
ORDER BY CustomerKey   
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
  
-- CORRECT  
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="h-using-union-of-three-select-statements-to-show-effects-of-all-and-parentheses"></a>H. 利用三個 SELECT 陳述式的 UNION 來顯示所有的效果和括號  
 下列範例會使用`UNION`合併的結果**相同資料表**為了示範括號和所有作用時使用`UNION`。  
  
 第一個範例會使用`UNION ALL`顯示重複的記錄，並傳回每個資料列的來源資料表中三次。 第二個範例會使用`UNION`沒有`ALL`以消除重複的資料列從合併的結果，這三個`SELECT`陳述式並傳回不重複資料列從來源資料表。  
  
 第三個範例會使用`ALL`的第一個`UNION`和括號封入第二個`UNION`未使用`ALL`。 第二個`UNION`會先處理，因為它位於括號內。 它只有不重複的資料列從資料表傳回因為`ALL`未使用選項，並移除重複項目。 這些資料列可結合的第一個結果`SELECT`使用`UNION ALL`關鍵字。 這不會移除兩個集合間的重複項目。  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL  
(  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
);  
```  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [精選的範例 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
  
  


