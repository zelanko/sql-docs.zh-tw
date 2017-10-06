---
title: "LAG (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LAG_TSQL
- LAG
dev_langs:
- TSQL
helpviewer_keywords:
- LAG function
- analytic functions, LAG
ms.assetid: a9a90bdb-3f80-4c97-baca-b7407bcdc7f0
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 77598feb87f6766f6c24c454dace2c138315e69b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lag-transact-sql"></a>LAG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  不使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的自我聯結，而從相同結果集的前一個資料列存取資料。 LAG 會提供對於目前資料列之前給定實體位移之資料列的存取。 在 SELECT 陳述式中使用這個分析函數，比較目前資料列中的值與前一個資料列中的值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
LAG (scalar_expression [,offset] [,default])  
    OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
## <a name="arguments"></a>引數  
 *scalar_expression*  
 根據指定的位移傳回數值。 它是傳回單一 (純量) 值的任一類型運算式。 *scalar_expression*不能是分析函數。  
  
 *位移*  
 從取得數值的目前資料列傳回資料列的數目。 若未加以指定，預設為 1。 *位移*可以是資料行、 子查詢或另一個運算式評估為正整數或可以隱含地轉換為**bigint**。 *位移*不能是負值或分析函數。  
  
 *預設值*  
 當傳回值*scalar_expression*在*位移*是 NULL。 如果未指定預設值，會傳回 NULL。 *預設*可以是資料行、 子查詢或其他運算式，但不是能是分析函數。 *預設*必須是相容的型別與*scalar_expression*。  
  
 透過**(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause*將分割成資料分割要套用函式的 FROM 子句所產生的結果集。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。 *order_by_clause*套用函數之前，決定資料的順序。 如果*partition_by_clause*指定時，它會判斷資料分割中資料的順序。 *Order_by_clause*需要。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>傳回類型  
 指定的資料型別*scalar_expression*。 如果傳回 NULL *scalar_expression*可為 null 或*預設*設為 NULL。  
  
## <a name="general-remarks"></a>一般備註  
 LAG 不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-compare-values-between-years"></a>A. 比較不同年份的值  
 下列範例使用 LAG 函數傳回特定員工於前幾年之間的銷售配額差異。 請注意，由於第一列沒有可用的 lag 值，所以會傳回預設值零 (0)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, YEAR(QuotaDate) AS SalesYear, SalesQuota AS CurrentQuota,   
       LAG(SalesQuota, 1,0) OVER (ORDER BY YEAR(QuotaDate)) AS PreviousQuota  
FROM Sales.SalesPersonQuotaHistory  
WHERE BusinessEntityID = 275 and YEAR(QuotaDate) IN ('2005','2006');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
BusinessEntityID SalesYear   CurrentQuota          PreviousQuota  
---------------- ----------- --------------------- ---------------------  
275              2005        367000.00             0.00  
275              2005        556000.00             367000.00  
275              2006        502000.00             556000.00  
275              2006        550000.00             502000.00  
275              2006        1429000.00            550000.00  
275              2006        1324000.00            1429000.00  
  
```  
  
### <a name="b-compare-values-within-partitions"></a>B. 比較分割區中的值  
 下列範例使用 LAG 函數比較年初至今各員工的銷售額。 指定 PARTITION BY 子句可依照銷售領域分割結果集中的資料列。 LAG 函數會分別套用至每個分割區，並會針對每個分割區重新開始計算。 OVER 子句中的 ORDER BY 子句會將每個分割區中的資料列排序。 SELECT 陳述式中的 ORDER BY 子句會排序整個結果集的資料列。 請注意，由於每個分割區的第一列沒有可用的 lag 值，所以會傳回預設值零 (0)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TerritoryName, BusinessEntityID, SalesYTD,   
       LAG (SalesYTD, 1, 0) OVER (PARTITION BY TerritoryName ORDER BY SalesYTD DESC) AS PrevRepSales  
FROM Sales.vSalesPerson  
WHERE TerritoryName IN (N'Northwest', N'Canada')   
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
TerritoryName            BusinessEntityID SalesYTD              PrevRepSales  
-----------------------  ---------------- --------------------- ---------------------  
Canada                   282              2604540.7172          0.00  
Canada                   278              1453719.4653          2604540.7172  
Northwest                284              1576562.1966          0.00  
Northwest                283              1573012.9383          1576562.1966  
Northwest                280              1352577.1325          1573012.9383  
  
```  
  
### <a name="c-specifying-arbitrary-expressions"></a>C. 指定任意的運算式  
 下列範例將示範如何在 LAG 函數語法中指定多種任意的運算式。  
  
```  
CREATE TABLE T (a int, b int, c int);   
GO  
INSERT INTO T VALUES (1, 1, -3), (2, 2, 4), (3, 1, NULL), (4, 3, 1), (5, 2, NULL), (6, 1, 5);   
  
SELECT b, c,   
    LAG(2*c, b*(SELECT MIN(b) FROM T), -c/2.0) OVER (ORDER BY a) AS i  
FROM T;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
b           c           i  
----------- ----------- -----------  
1           -3          1  
2           4           -2  
1           NULL        8  
3           1           -6  
2           NULL        NULL  
1           5           NULL  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-compare-values-between-quarters"></a>D： 比較季之間的值  
 下列範例會示範 LAG 函式。 查詢會使用 LAG 函數傳回特定員工於前一個日曆季的銷售配額差異。 請注意，由於第一列沒有可用的 lag 值，所以會傳回預設值零 (0)。  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear, CalendarQuarter, SalesAmountQuota AS SalesQuota,  
       LAG(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS PrevQuota,  
       SalesAmountQuota - LAG(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Diff  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear IN (2001, 2002)  
ORDER BY CalendarYear, CalendarQuarter;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year Quarter  SalesQuota  PrevQuota  Diff  
---- -------  ----------  ---------  -------------  
2001 3        28000.0000      0.0000   28000.0000  
2001 4         7000.0000  28000.0000  -21000.0000  
2001 1        91000.0000   7000.0000   84000.0000  
2002 2       140000.0000  91000.0000   49000.0000  
2002 3         7000.0000 140000.0000  -70000.0000  
2002 4       154000.0000   7000.0000   84000.0000
```  
  
## <a name="see-also"></a>另請參閱  
 [負責人 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/lead-transact-sql.md)  
  
  



