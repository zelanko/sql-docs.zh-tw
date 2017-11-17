---
title: "某些 |任何 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- SOME
- SOME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a67801d62cb05cdb0b589548e8bd3f9676d5840a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="some--any-transact-sql"></a>SOME | ANY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  比較純量值與單一資料行集的值。 SOME 和 ANY 是相等的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
scalar_expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
     { SOME | ANY } ( subquery )   
```  
  
## <a name="arguments"></a>引數  
 *scalar_expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 這是任何有效的比較運算子。  
  
 SOME | ANY  
 指定應該進行比較。  
  
 *子查詢*  
 這是有單一資料行結果集的子查詢。 傳回的資料行的資料類型必須是相同的資料類型*scalar_expression*。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
## <a name="result-value"></a>結果值  
 SOME 或 ANY 傳回**TRUE**時指定的比較為 TRUE 的任何一對 (*scalar_expression***，***x*) 其中*x*是單一資料行集中的值; 否則傳回**FALSE**。  
  
## <a name="remarks"></a>備註  
 SOME 需要*scalar_expression*正面比較至少一個子查詢所傳回的值。 需要的陳述式*scalar_expression*正面比較到子查詢會傳回每個值，請參閱[所有 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/all-transact-sql.md). 例如，如果子查詢傳回 2 和 3 個值*scalar_expression* = SOME （子查詢） 會評估為 TRUE 的*scalar_express*為 2。 如果子查詢傳回 2 和 3 個值*scalar_expression* = ALL （子查詢） 會評估為 FALSE，因為部分子查詢 （即值 3） 的值不符合準則的運算式。  
  
## <a name="examples"></a>範例  
  
### <a name="a-running-a-simple-example"></a>A. 執行簡單範例  
 下列陳述式會建立一份簡單資料表，並將 `1`、`2`、`3` 和 `4` 的值加入至 `ID` 資料行。  
  
```  
CREATE TABLE T1  
(ID int) ;  
GO  
INSERT T1 VALUES (1) ;  
INSERT T1 VALUES (2) ;  
INSERT T1 VALUES (3) ;  
INSERT T1 VALUES (4) ;  
```  
  
 下列查詢會傳回 `TRUE`，因為 `3` 小於資料表中的某些值。  
  
```  
IF 3 < SOME (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
 下列查詢會傳回 `FALSE`，因為 `3` 不小於資料表中的所有值。  
  
```  
IF 3 < ALL (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
### <a name="b-running-a-practical-example"></a>B. 執行實際範例  
 下列範例會建立預存程序會決定是否將指定的所有元件`SalesOrderID`中`AdventureWorks2012`資料庫可以在指定的天數內製造出來。 這個範例會使用子查詢，針對特定 `DaysToManufacture` 的所有元件建立一份 `SalesOrderID` 值數目的清單，然後測試是否有任何一個子查詢傳回值大於所指定的天數。 如果傳回的每個 `DaysToManufacture` 值都小於提供的數目，則條件為 TRUE，並且會列印出第一個訊息。  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE ManyDaysToComplete @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays < SOME  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'At least one item for this order cannot be manufactured in specified number of days.'  
ELSE   
PRINT 'All items for this order can be manufactured in the specified number of days or less.' ;  
  
```  
  
 若要測試的程序，來執行程序使用`SalesOrderID``49080`，其具有一個需要的元件`2`天和兩個需要 0 天的元件。 第一個陳述式符合此準則， 第二個查詢則不符合。  
  
```  
EXECUTE ManyDaysToComplete 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in the specified number of days or less.`  
  
```  
EXECUTE ManyDaysToComplete 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `At least one item for this order cannot be manufactured in specified number of days.`  
  
## <a name="see-also"></a>另請參閱  
 [所有 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [案例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [在 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  

