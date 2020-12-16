---
description: VARP (Transact-SQL)
title: VARP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VARP_TSQL
- VARP
dev_langs:
- TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VARP function [Transact-SQL]
ms.assetid: ce5d2e32-01da-4e18-b8ed-a08b61d84456
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d950b90d42def78b927b03a6d13ffcc3d4dcfb3b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461139"
---
# <a name="varp-transact-sql"></a>VARP (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回指定運算式中之所有值的母體擴展的統計變異數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Aggregate Function Syntax   
VARP ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VARP ([ ALL ] expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 **ALL**  
 將函數套用至所有值。 ALL 是預設值。  
  
 DISTINCT  
 指定要考量每個唯一值。  
  
 *expression*  
 這是精確數值或近似數值資料類型類別的 [運算式](../../t-sql/language-elements/expressions-transact-sql.md)，但 **bit** 資料類型除外。 不允許彙總函式和子查詢。  
  
 OVER **(** [ _partition\_by\_clause_ ] _order\_by\_clause_ **)**  
 _partition\_by\_clause_ 會將 FROM 子句所產生結果集分割成函式所要套用的分割區。 如未指定，此函數會將查詢結果集的所有資料列視為單一群組。 _order\_by\_clause_ 可決定執行作業的邏輯順序。 需要 _order\_by\_clause_。 如需詳細資訊，請參閱 [OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)。  
  
## <a name="return-types"></a>傳回型別  
 **float**  
  
## <a name="remarks"></a>備註  
 如果在 SELECT 陳述式的所有項目上使用 VARP，結果集中的每個值都會包含在計算中。 VARP 只能搭配數值資料行來使用。 會忽略 Null 值。  
  
 VARP 未搭配 OVER 和 ORDER BY 子句使用時，是具決定性函數。 使用 OVER 和 ORDER BY 子句指定時，則不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-varp"></a>A：使用 VARP  
 下列範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之`SalesPerson` 資料表中所有獎金值母體的變異數。  
  
```sql  
SELECT VARP(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-varp"></a>B：使用 VARP  
 下列範例會傳回 `dbo.FactSalesQuota` 資料表中所有銷售配額值的 `VARP`。 第一個資料行包含所有相異值的變異數，而第二個資料行則包含所有值的變異數 (包含任何重複的值)。  
  
```sql  
-- Uses AdventureWorks  
  
SELECT VARP(DISTINCT SalesAmountQuota)AS Distinct_Values, VARP(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
158146830494.18   157788848582.94
```  
  
### <a name="c-using-varp-with-over"></a>C. 搭配使用 OVER 和 VARP  
 下列範例會傳回日曆年度內每一季銷售配額值的 `VARP`。 請注意，OVER 子句中的 ORDER BY 會排序統計變異數，而 SELECT 陳述式的 ORDER BY 會排序結果集。  
  
```sql 
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VARP(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              Variance
----  -------  ----------------------  -------------------
2002  1         91000.0000             0.00
2002  2        140000.0000             600250000.00
2002  3         70000.0000             860222222.22
2002  4        154000.0000             1185187500.00
```  
  
## <a name="see-also"></a>另請參閱  
 [彙總函數 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

