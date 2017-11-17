---
title: "LAST_VALUE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LAST_VALUE
- LAST_VALUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- analytic functions, LAST_VALUE
- LAST_VALUE function
ms.assetid: fd833e34-8092-42b7-80fc-95ca6b0eab6b
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 680f3e88f31c413c7ceaa40fbec63bd3acf81e14
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lastvalue-transact-sql"></a>LAST_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  傳回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中一組經過排序之值的最後一個值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
LAST_VALUE ( [scalar_expression )   
    OVER ( [ partition_by_clause ] order_by_clause rows_range_clause )   
```  
  
## <a name="arguments"></a>引數  
 *scalar_expression*  
 要傳回的值。 *scalar_expression*可以是資料行、 子查詢或其他會產生單一值的運算式。 不允許其他分析函數。  
  
 透過**(** [ *partition_by_clause* ] *order_by_clause* [ *rows_range_clause* ] **)**  
 *partition_by_clause*將分割成資料分割要套用函式的 FROM 子句所產生的結果集。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。  
  
 *order_by_clause*套用函數之前，決定資料的順序。 *Order_by_clause*需要。 *rows_range_clause*藉由指定開始和結束點，以進一步限制資料分割內的資料列。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>傳回類型  
 是相同的型別*scalar_expression*。  
  
## <a name="general-remarks"></a>一般備註  
 LAST_VALUE 不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-lastvalue-over-partitions"></a>A. 對分割區使用 LAST_VALUE  
 下列範例會就給定的薪資 (費用)，傳回每個部門中最後一名員工的雇用日期。 PARTITION BY 子句會依部門分割員工，而 LAST_VALUE 函數則會個別套用到每個分割區。 OVER 子句中指定的 ORDER BY 子句，可決定 LAST_VALUE 函數套用至每個分割區中之資料列的邏輯順序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate, HireDate,   
    LAST_VALUE(HireDate) OVER (PARTITION BY Department ORDER BY Rate) AS LastValue  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
INNER JOIN HumanResources.EmployeePayHistory AS eph    
    ON eph.BusinessEntityID = edh.BusinessEntityID  
INNER JOIN HumanResources.Employee AS e  
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department                  LastName                Rate         HireDate     LastValue  
--------------------------- ----------------------- ------------ ----------   ----------  
Document Control            Chai                    10.25        2003-02-23   2003-03-13  
Document Control            Berge                   10.25        2003-03-13   2003-03-13  
Document Control            Norred                  16.8269      2003-04-07   2003-01-17  
Document Control            Kharatishvili           16.8269      2003-01-17   2003-01-17  
Document Control            Arifin                  17.7885      2003-02-05   2003-02-05  
Information Services        Berg                    27.4038      2003-03-20   2003-01-24  
Information Services        Meyyappan               27.4038      2003-03-07   2003-01-24  
Information Services        Bacon                   27.4038      2003-02-12   2003-01-24  
Information Services        Bueno                   27.4038      2003-01-24   2003-01-24  
Information Services        Sharma                  32.4519      2003-01-05   2003-03-27  
Information Services        Connelly                32.4519      2003-03-27   2003-03-27  
Information Services        Ajenstat                38.4615      2003-02-18   2003-02-23  
Information Services        Wilson                  38.4615      2003-02-23   2003-02-23  
Information Services        Conroy                  39.6635      2003-03-08   2003-03-08  
Information Services        Trenary                 50.4808      2003-01-12   2003-01-12  
  
```  
  
### <a name="b-using-firstvalue-and-lastvalue-in-a-computed-expression"></a>B. 在計算運算式中使用 FIRST_VALUE 及 LAST_VALUE  
 下列範例會使用計算運算式中的 FIRST_VALUE 及 LAST_VALUE 函數，分別顯示給定員工人數當季與年度第一季和最後一季銷售量配額值之間的差異。 FIRST_VALUE 函數會當年度第一季的銷售配額值，並將該值從當季的銷售配額值中減去。 其會隨附在衍生資料行 DifferenceFromFirstQuarter 中傳回。 年度第一季的 DifferenceFromFirstQuarter 資料行值為 0。 LAST_VALUE 函數會傳回年度最後一季的銷售額值，並會從本季的銷售額值減去該值。 其會隨附在衍生資料行 DifferenceFromLastQuarter 中傳回。 對於當年度的最後一季，DifferenceFromLastQuarter 資料行的值為 0。  
  
 在此範例中，若要在 DifferenceFromLastQuarter 資料行中傳回非零的值，必須要有 “RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING” 子句，如下所示。 預設範圍為 “RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW”。 在此範例中，使用該預設範圍 (或不包含範圍而使用預設值) 會導致 DifferenceFromLastQuarter 資料行中傳回零。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
SELECT BusinessEntityID, DATEPART(QUARTER,QuotaDate)AS Quarter, YEAR(QuotaDate) AS SalesYear,   
    SalesQuota AS QuotaThisQuarter,   
    SalesQuota - FIRST_VALUE(SalesQuota)   
        OVER (PARTITION BY BusinessEntityID, YEAR(QuotaDate)   
              ORDER BY DATEPART(QUARTER,QuotaDate) ) AS DifferenceFromFirstQuarter,   
    SalesQuota - LAST_VALUE(SalesQuota)   
        OVER (PARTITION BY BusinessEntityID, YEAR(QuotaDate)   
              ORDER BY DATEPART(QUARTER,QuotaDate)   
              RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING ) AS DifferenceFromLastQuarter   
FROM Sales.SalesPersonQuotaHistory   
WHERE YEAR(QuotaDate) > 2005   
AND BusinessEntityID BETWEEN 274 AND 275   
ORDER BY BusinessEntityID, SalesYear, Quarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID Quarter     SalesYear   QuotaThisQuarter      DifferenceFromFirstQuarter DifferenceFromLastQuarter  
---------------- ----------- ----------- --------------------- --------------------------- -----------------------  
274              1           2006        91000.00              0.00                        -63000.00  
274              2           2006        140000.00             49000.00                    -14000.00  
274              3           2006        70000.00              -21000.00                   -84000.00  
274              4           2006        154000.00             63000.00                    0.00  
274              1           2007        107000.00             0.00                        -9000.00  
274              2           2007        58000.00              -49000.00                   -58000.00  
274              3           2007        263000.00             156000.00                   147000.00  
274              4           2007        116000.00             9000.00                     0.00  
274              1           2008        84000.00              0.00                        -103000.00  
274              2           2008        187000.00             103000.00                   0.00  
275              1           2006        502000.00             0.00                        -822000.00  
275              2           2006        550000.00             48000.00                    -774000.00  
275              3           2006        1429000.00            927000.00                   105000.00  
275              4           2006        1324000.00            822000.00                   0.00  
275              1           2007        729000.00             0.00                        -489000.00  
275              2           2007        1194000.00            465000.00                   -24000.00  
275              3           2007        1575000.00            846000.00                   357000.00  
275              4           2007        1218000.00            489000.00                   0.00  
275              1           2008        849000.00             0.00                        -20000.00  
275              2           2008        869000.00             20000.00                    0.00  
  
(20 row(s) affected)  
  
```  
  
  

