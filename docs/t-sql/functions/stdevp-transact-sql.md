---
title: "STDEVP (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
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
- STDEVP
- STDEVP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STDEVP function [Transact-SQL]
- expressions [SQL Server], statistical standard deviation
- statistical standard deviation
ms.assetid: 29f2a906-d084-4464-abc3-4b275ed19442
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: af2c89686b804e263d0a7e576a3c91e926a65644
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="stdevp-transact-sql"></a>STDEVP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定運算式中之所有值的母體統計標準差。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
STDEVP ( [ ALL | DISTINCT ] expression )   
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregate Function Syntax   
STDEVP ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax   
STDEVP (expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>引數  
 **ALL**  
 將函數套用至所有值。 ALL 是預設值。  
  
 DISTINCT  
 指定要考量每個唯一值。  
  
 *expression*  
 這是一個數值[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 不允許彙總函式和子查詢。 *運算式*是精確數值或相近數值資料類型類別目錄運算式除外**元**資料型別。  
  
 透過**(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*將分割成資料分割要套用函式的 FROM 子句所產生的結果集。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。 *order_by_clause*決定執行作業的邏輯順序。 *order_by_clause*需要。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>傳回類型  
 **float**  
  
## <a name="remarks"></a>備註  
 如果在 SELECT 陳述式的所有項目上使用 STDEVP，結果集中的每個值都會包含在計算中。 STDEVP 只能搭配數值資料行來使用。 會忽略 Null 值。  
  
 STDEVP 未搭配 OVER 和 ORDER BY 子句使用時，是具決定性函數。 使用 OVER 和 ORDER BY 子句指定時，則不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stdevp"></a>答： 使用 STDEVP  
 下列範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之`SalesPerson` 資料表中所有獎金值的母體標準差。  
  
```  
SELECT STDEVP(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-stdevp"></a>B： 使用 STDEVP  
 下列範例會傳回`STDEVP`資料表中的銷售配額值`dbo.FactSalesQuota`。 第一個資料行包含的所有相異值的標準差，而第二個資料行包含包括任何重複的項目值的所有值的標準差。  
  
```  
-- Uses AdventureWorks  
  
SELECT STDEVP(DISTINCT SalesAmountQuota)AS Distinct_Values, STDEVP(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;SELECT STDEVP(DISTINCT Quantity)AS Distinct_Values, STDEVP(Quantity) AS All_Values  
FROM ProductInventory;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values  
----------------  ----------------  
397676.79         397226.44
```  
  
### <a name="c-using-stdevp-with-over"></a>C. STDEVP 使用容錯移轉  
 下列範例會傳回`STDEVP`日曆年度的每一季的銷售配額值。 請注意，`ORDER BY` 子句中的 `OVER` 會排列 `STDEVP` 的順序，而 `ORDER BY` 陳述式的 `SELECT` 會排列結果集的順序。  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       STDEVP(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS StdDeviation  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              StdDeviation  
----  -------  ----------------------  -------------------  
2002  1         91000.0000             0.00  
2002  2        140000.0000             24500.00  
2002  3         70000.0000             29329.55  
2002  4        154000.0000             34426.55
```  
  
## <a name="see-also"></a>請參閱＜  
 [彙總函式 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

