---
title: "陣序 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/25/2016
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
- RANK
- RANK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row ranking [SQL Server]
- tied rows [SQL Server]
- ranking rows
- RANK function [Transact-SQL]
ms.assetid: 2d96f6d2-5db7-4b3c-a63e-213c58e4af55
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 657f152f295fd93d3749ed6ff4865cd753dc3e95
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="rank-transact-sql"></a>RANK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回結果集分割區內，每個資料列的次序。 資料列的次序等於一加上前述資料列之前的次序數目。  

  ROW_NUMBER 和陣序規範很類似。 ROW_NUMBER 數字所有資料列依序 （例如 1、 2、 3、 4、 5）。 陣序規範會提供相同的數值 （例如 1、 2、 2、 4、 5） 的繫結。   
  
> [!NOTE]
> 陣序規範為執行查詢時計算暫存值。 若要保存在資料表中的數字，請參閱[IDENTITY 屬性](../../t-sql/statements/create-table-transact-sql-identity-property.md)和[順序](../../t-sql/statements/create-sequence-transact-sql.md)。 
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
RANK ( ) OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>引數  
 透過**(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*將分割成資料分割要套用函式的 FROM 子句所產生的結果集。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。 *order_by_clause*套用函數之前，決定資料的順序。 *Order_by_clause*需要。 \<資料列或範圍子句 > 的 OVER 子句不能指定為 RANK 函數。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>傳回類型  
 **bigint**  
  
## <a name="remarks"></a>備註  
 如果兩個或多個資料列有相同的次序，每個繫結的資料列就會收到相同的次序。 例如，如果兩位超級業務員有相同的 SalesYTD 值，他們的次序便都是第一。 SalesYTD 次高的業務員之次序便是第三，因為有兩個資料列次序比它高。 因此，RANK 函數不一定會傳回連續整數。  
  
 整個查詢所用的排序順序，決定了資料列在結果集中的出現順序。  
  
 RANK 不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-ranking-rows-within-a-partition"></a>A. 排序分割區中的資料列  
 下列範例會根據庫存產品數量來排列指定庫存位置的庫存產品次序。 `LocationID` 分割結果集，而 `Quantity` 邏輯地排序結果集。 請注意產品 494 和 495 具相同的數量。 因為它們綁在一起，且它們同時排名為一。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT i.ProductID, p.Name, i.LocationID, i.Quantity  
    ,RANK() OVER   
    (PARTITION BY i.LocationID ORDER BY i.Quantity DESC) AS Rank  
FROM Production.ProductInventory AS i   
INNER JOIN Production.Product AS p   
    ON i.ProductID = p.ProductID  
WHERE i.LocationID BETWEEN 3 AND 4  
ORDER BY i.LocationID;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
ProductID   Name                   LocationID   Quantity Rank  
----------- ---------------------- ------------ -------- ----  
494         Paint - Silver         3            49       1  
495         Paint - Blue           3            49       1  
493         Paint - Red            3            41       3  
496         Paint - Yellow         3            30       4  
492         Paint - Black          3            17       5  
495         Paint - Blue           4            35       1  
496         Paint - Yellow         4            25       2  
493         Paint - Red            4            24       3  
492         Paint - Black          4            14       4  
494         Paint - Silver         4            12       5  
 (10 row(s) affected)  
```  
  
### <a name="b-ranking-all-rows-in-a-result-set"></a>B. 排序結果集中的所有資料列  
 下列範例會依員工薪水的排序傳回前 10 位員工。 因為沒有指定 PARTITION BY 子句，RANK 函數應用到在結果集的所有資料列。  
  
```  
USE AdventureWorks2012  
SELECT TOP(10) BusinessEntityID, Rate,   
       RANK() OVER (ORDER BY Rate DESC) AS RankBySalary  
FROM HumanResources.EmployeePayHistory AS eph1  
WHERE RateChangeDate = (SELECT MAX(RateChangeDate)   
                        FROM HumanResources.EmployeePayHistory AS eph2  
                        WHERE eph1.BusinessEntityID = eph2.BusinessEntityID)  
ORDER BY BusinessEntityID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Rate                  RankBySalary  
---------------- --------------------- --------------------  
1                125.50                1  
2                63.4615               4  
3                43.2692               8  
4                29.8462               19  
5                32.6923               16  
6                32.6923               16  
7                50.4808               6  
8                40.8654               10  
9                40.8654               10  
10               42.4808               9  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-ranking-rows-within-a-partition"></a>C： 排序資料分割內的資料列  
 下列範例會根據銷售代表在每個銷售地區根據他們的銷售總額。 資料列集由 `SalesTerritoryGroup` 來進行資料分割，依照 `SalesAmountQuota` 來排序。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
LastName          TotalSales     SalesTerritoryGroup  RankResult
----------------  -------------  -------------------  --------
Tsoflias          1687000.0000   Australia            1
Saraiva           7098000.0000   Canada               1
Vargas            4365000.0000   Canada               2
Carson            12198000.0000  Central              1
Varkey Chudukatil 5557000.0000   France               1
Valdez            2287000.0000   Germany              1
Blythe            11162000.0000  Northeast            1
Campbell          4025000.0000   Northwest            1
Ansman-Wolfe      3551000.0000   Northwest            2
Mensa-Annan       2753000.0000   Northwest            3
Reiter            8541000.0000   Southeast            1
Mitchell          11786000.0000  Southwest            1
Ito               7804000.0000   Southwest            2
Pak               10514000.0000  United Kingdom       1
```  
  
## <a name="see-also"></a>請參閱＜  
 [DENSE_RANK &#40;TRANSACT-SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [ROW_NUMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [NTILE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)   
 [排名函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



