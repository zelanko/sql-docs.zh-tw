---
title: SUM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SUM
- SUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], sum of all
- SUM function [Transact-SQL]
- values [SQL Server]
- summation [SQL Server]
- expressions [SQL Server], sum of all values
- DISTINCT keyword
- totals [SQL Server], SUM
- summary values [SQL Server]
ms.assetid: 9af94d0f-55d4-428f-a840-ec530160f379
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ee00afa6e27d91df473091df64a30f49b427c19d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sum-transact-sql"></a>SUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回運算式中所有值的總和，或只傳回 DISTINCT 值的總和。 SUM 只能搭配數值資料行來使用。 會忽略 Null 值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SUM ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SUM ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>引數  
 ALL  
 將彙總函式套用至所有值。 ALL 是預設值。  
  
 DISTINCT  
 指定 SUM 傳回唯一值的總和。  
  
 *expression*  
 常數、資料行或函數，或任何算術、位元和字串運算子的組合。 *expression* 為精確數值或近似數值資料類型類別的運算式，但是 **bit** 資料類型除外。 不允許彙總函式和子查詢。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 OVER **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* 會將 FROM 子句產生的結果集分割成函數所要套用的分割區。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。 *order_by_clause* 可決定執行作業的邏輯順序。 *order_by_clause* 為必要項目。 如需詳細資訊，請參閱 [OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)。  
  
## <a name="return-types"></a>傳回類型  
 以最精確的 *expression* 資料類型傳回所有 *expression* 值的總和。  
  
|運算式結果|傳回類型|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**decimal** 類別 (p, s)|**decimal(38, s)**|  
|**money** 和 **smallmoney** 類別|**money**|  
|**float** 和 **real** 類別|**float**|  
  
## <a name="remarks"></a>Remarks  
 SUM 未搭配 OVER 和 ORDER BY 子句使用時，是具決定性函數。 使用 OVER 和 ORDER BY 子句指定時，則不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-sum-to-return-summary-data"></a>A. 使用 SUM 傳回摘要資料  
 下列範例示範如何使用 SUM 函數傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的摘要資料。  
  
```  
SELECT Color, SUM(ListPrice), SUM(StandardCost)  
FROM Production.Product  
WHERE Color IS NOT NULL   
    AND ListPrice != 0.00   
    AND Name LIKE 'Mountain%'  
GROUP BY Color  
ORDER BY Color;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Color
--------------- --------------------- ---------------------
Black           27404.84              5214.9616
Silver          26462.84              14665.6792
White           19.00                 6.7926

(3 row(s) affected)
 ```  
  
### <a name="b-using-the-over-clause"></a>B. 使用 OVER 子句  
 下列範例搭配 OVER 子句使用 SUM 函數，為 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之 `Sales.SalesPerson` 資料表中各領域的年度銷售提供累計總和。 `TerritoryID` 負責分割資料，而 `SalesYTD` 會進行邏輯性地排序。 這表示，將會根據銷售年度來針對每一個領域計算 SUM 函數。 請注意，在 `TerritoryID` 1 中，2005 銷售年度有兩個資料列，分別表示在該年度有銷售業績的兩個銷售人員。 計算這兩個資料列的累計銷售額，然後將表示 2006 年度銷售額的第三個資料列納入計算。  
  
```  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
 在這個範例中，OVER 子句未包含 PARTITION BY。 這表示，該函數將套用到查詢所傳回的所有資料列。 OVER 子句中指定的 ORDER BY 子句會決定套用 SUM 函數的邏輯順序。 此查詢會依照 WHERE 子句中指定的所有銷售領域傳回依年度的銷售量累計總和。 SELECT 陳述式中指定的 ORDER BY 子句會決定查詢的資料列顯示的順序。  
  
```  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-a-simple-sum-example"></a>C. 簡單的 SUM 範例  
 下列範例會傳回 2003 年每個產品銷售的總數。  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductKey, SUM(SalesAmount) AS TotalPerProduct  
FROM dbo.FactInternetSales  
WHERE OrderDateKey >= '20030101'   
      AND OrderDateKey < '20040101'  
GROUP BY ProductKey  
ORDER BY ProductKey;  
  
```  
  
 以下為部分結果集。  
  
 ```
ProductKey  TotalPerProduct
----------  ---------------
214         31421.0200
217         31176.0900
222         29986.4300
225          7956.1500
 ```
  
### <a name="d-calculating-group-totals-with-more-than-one-column"></a>D. 計算多個資料行的群組總計  
 下列範例會針對 `ListPrice` 資料表中所列出的每個顏色，來計算 `StandardCost` 和 `Product` 的總和。  
  
```  
-- Uses AdventureWorks  
  
SELECT Color, SUM(ListPrice)AS TotalList,   
       SUM(StandardCost) AS TotalCost  
FROM dbo.DimProduct  
GROUP BY Color  
ORDER BY Color;  
```  
  
 結果集的第一個部分如下所示：  
  
 ```
Color       TotalList      TotalCost
----------  -------------  --------------
Black       101295.7191    57490.5378
Blue         24082.9484    14772.0524
Grey           125.0000       51.5625
Multi          880.7468      526.4095
NA            3162.3564     1360.6185
 ```  
  
## <a name="see-also"></a>另請參閱  
 [彙總函數 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

