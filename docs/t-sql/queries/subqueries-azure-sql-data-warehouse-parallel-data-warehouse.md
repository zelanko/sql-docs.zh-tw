---
title: 子查詢 (Azure SQL 資料倉儲、平行處理資料倉儲) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ab20f771fae4aa1ea5a31a11bc8c3e3f1e7c4ead
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>子查詢 (Azure SQL 資料倉儲、平行處理資料倉儲)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  本主題提供在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中使用子查詢的範例。  
  
 如需了解 SELECT 陳述式，請參閱 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
## <a name="contents"></a>目錄  
  
-   [基本概念](#Basics)  
  
-   [範例：SQL 資料倉儲和平行處理資料倉儲](#Examples)  
  
##  <a name="Basics"></a> 基本概念  
 子查詢  
 子查詢是指在 SELECT、INSERT、UPDATE 或 DELETE 陳述式中，或在另一個子查詢之中為巢狀的。 這也稱為內部查詢或內部選取。  
  
 外部查詢  
 包含子查詢的陳述式。 這也稱為外部選取。  
  
 相互關聯的子查詢  
 參考外部查詢中資料表的子查詢。  
  
##  <a name="Examples"></a> 範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 本節提供 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中所支援子查詢的範例。  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>A. 子查詢中的 TOP 和 ORDER BY  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>B. 含有相互關聯子查詢的 HAVING 子句  
  
```  
SELECT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
GROUP BY dm.EmployeeKey, dm.FirstName, dm.LastName  
HAVING 5000 <=   
(SELECT sum(OrderQuantity)  
FROM FactResellerSales AS frs  
WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
  
```  
  
### <a name="c-correlated-subqueries-with-analytics"></a>C. 含有分析的相互關聯子查詢  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>D. 子查詢中相互關聯的聯集陳述式  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>E. 子查詢中的聯結述詞  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>F. 子查詢中相互關聯的聯結述詞  
  
```  
SELECT * FROM RA   
    WHERE RA.a2 IN   
    (SELECT 1 FROM RB INNER JOIN RC ON RA.a1=RB.b1+RC.c1);  
```  
  
### <a name="g-correlated-subselects-as-data-sources"></a>G. 作為資料來源的相互關聯子選擇  
  
```  
SELECT * FROM RA   
    WHERE 3 = (SELECT COUNT(*)   
        FROM (SELECT b1 FROM RB WHERE RB.b1 = RA.a1) X);  
```  
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>H. 與彙總搭配使用的資料值中相互關聯子查詢  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>I. 搭配相互關聯子查詢使用 IN  
 下列範例在相關或重複的子查詢中使用 `IN`。 這是一項相依於外部查詢來取得其值的查詢。 內部查詢會重複執行，針對外部查詢可能選取的每個資料列各執行一次。 這個查詢會擷取一個 `EmployeeKey` 執行個體，再加上 `FactResellerSales` 資料表中 `OrderQuantity` 為 `5` 且員工識別碼在 `DimEmployee` 和 `FactResellerSales` 資料表中相符之每位員工的名字和姓氏。  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>J. 搭配子查詢使用 EXISTS 和 IN 之比較  
 下列範例示範語意相等的查詢，以說明使用 `EXISTS` 關鍵字和 `IN` 關鍵字之間的差異。 兩者都是子查詢的範例，會針對產品子類別為 `Road Bikes` 的每個產品名稱各擷取一個執行個體。 `ProductSubcategoryKey` 會在 `DimProduct` 與 `DimProductSubcategory`資料表之間進行比對。  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE EXISTS  
    (SELECT *  
     FROM DimProductSubcategory AS dps   
     WHERE dp.ProductSubcategoryKey = dps.ProductSubcategoryKey  
           AND dps.EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
 或  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE dp.ProductSubcategoryKey IN  
    (SELECT ProductSubcategoryKey  
     FROM DimProductSubcategory   
     WHERE EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
### <a name="k-using-multiple-correlated-subqueries"></a>K. 使用多個相互關聯的子查詢  
 這個範例利用相關的子查詢來尋找銷售了特定產品的員工名稱。  
  
```  
SELECT DISTINCT LastName, FirstName, e.EmployeeKey  
FROM DimEmployee e JOIN FactResellerSales s ON e.EmployeeKey = s.EmployeeKey  
WHERE ProductKey IN  
(SELECT ProductKey FROM DimProduct WHERE ProductSubcategoryKey IN  
(SELECT ProductSubcategoryKey FROM DimProductSubcategory   
 WHERE EnglishProductSubcategoryName LIKE '%Bikes'))  
ORDER BY LastName  
;  
  
```  
  
  
