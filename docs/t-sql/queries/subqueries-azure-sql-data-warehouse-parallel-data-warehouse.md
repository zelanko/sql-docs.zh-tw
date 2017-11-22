---
title: "子查詢 （Azure SQL 資料倉儲、 Parallel Data Warehouse） |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a2560bfb07ceac4c8b75c9501cf4ed45a3f6087e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>子查詢 （Azure SQL 資料倉儲、 Parallel Data Warehouse）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  本主題提供使用中的子查詢的範例[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
 SELECT 陳述式，請參閱[SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-transact-sql.md)  
  
## <a name="contents"></a>目錄  
  
-   [基本概念](#Basics)  
  
-   [範例： SQL 資料倉儲和 Parallel Data Warehouse](#Examples)  
  
##  <a name="Basics"></a>基本概念  
 子查詢  
 子查詢是指在 SELECT、INSERT、UPDATE 或 DELETE 陳述式中，或在另一個子查詢之中為巢狀的。 這也稱為內部查詢或內部的 select。  
  
 外部查詢  
 包含子查詢陳述式。 這也稱為外部 select。  
  
 相互關聯子查詢  
 外部查詢中的資料表是指子查詢。  
  
##  <a name="Examples"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 本章節提供支援的子查詢的範例[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>A. TOP 和 ORDER BY 的子查詢中  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>B. HAVING 子句中的使用相互關聯子查詢  
  
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
  
### <a name="c-correlated-subqueries-with-analytics"></a>C. 分析相互關聯子查詢  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>D. 相互關聯子查詢中的 union 陳述式  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>E. 子查詢中聯結述詞  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>F. 子查詢中的相互關聯的聯結述詞  
  
```  
SELECT * FROM RA   
    WHERE RA.a2 IN   
    (SELECT 1 FROM RB INNER JOIN RC ON RA.a1=RB.b1+RC.c1);  
```  
  
### <a name="g-correlated-subselects-as-data-sources"></a>G. 相互關聯子選擇做為資料來源  
  
```  
SELECT * FROM RA   
    WHERE 3 = (SELECT COUNT(*)   
        FROM (SELECT b1 FROM RB WHERE RB.b1 = RA.a1) X);  
```  
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>H. 相互關聯子查詢中搭配彙總的資料值  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>I. 使用以相互關聯子查詢  
 下列範例在相關或重複的子查詢中使用 `IN`。 這是一項相依於外部查詢來取得其值的查詢。 重複執行內部查詢時，每個資料列一次，可能會選取外部查詢。 此查詢會擷取的一個執行個體`EmployeeKey`加上的每位員工的姓氏和名字`OrderQuantity`中`FactResellerSales`資料表是`5`和員工識別碼相符的`DimEmployee`和`FactResellerSales`資料表。  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>J. 使用 EXISTS 與使用子查詢  
 下列範例顯示查詢的語意相當於說明使用之間的差異`EXISTS`關鍵字和`IN`關鍵字。 兩者都是會擷取產品子類別目錄的每個產品名稱的一個執行個體的子查詢`Road Bikes`。 `ProductSubcategoryKey`符合`DimProduct`和`DimProductSubcategory`資料表。  
  
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
  
### <a name="k-using-multiple-correlated-subqueries"></a>K. 使用多個相互關聯子查詢  
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
  
  
