---
title: "所有 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- ALL_TSQL
- ALL
dev_langs: TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
caps.latest.revision: "40"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2e65fc9cacbcfe868c072713f282c42c95839e48
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="all-transact-sql"></a>ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  比較純量值與單一資料行集的值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>引數  
 *scalar_expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 這是一個比較運算子。  
  
 *subquery*  
 這是傳回單一資料行結果集的子查詢。 傳回的資料行的資料類型必須是相同的資料類型的資料類型為*scalar_expression*。  
  
 這是一個受限制的 SELECT 陳述式，其中不允許使用 ORDER BY 子句和 INTO 關鍵字。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
## <a name="result-value"></a>結果值  
 當指定的比較為 TRUE，則傳回 TRUE 的所有配對 (*scalar_expression***，***x)*，當*x*是單一資料行集中的值; 否則傳回 FALSE。  
  
## <a name="remarks"></a>備註  
 ALL 需要*scalar_expression*正面比較到子查詢會傳回每個值。 例如，如果子查詢傳回 2 和 3 個值*scalar_expression* < = ALL （子查詢） 會評估為 TRUE 的*scalar_expression*為 2。 如果子查詢傳回 2 和 3 個值*scalar_expression* = ALL （子查詢） 會評估為 FALSE，因為部分子查詢 （即值 3） 的值不符合準則的運算式。  
  
 需要的陳述式*scalar_expression*正面比較只有一個子查詢所傳回的值，請參閱[部分 &#124;任何 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 此主題中所使用的子查詢都是指 ALL。 都可用來與[UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md)和[選取](../../t-sql/queries/select-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會建立預存程序會決定是否將指定的所有元件`SalesOrderID`中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫可以在指定的天數內製造出來。 這個範例會使用子查詢，針對特定 `DaysToManufacture` 的所有組件建立一份 `SalesOrderID` 值數目的清單，然後確認所有 `DaysToManufacture` 都在指定的天數範圍內。  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE DaysToBuild @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays >= ALL  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'All items for this order can be manufactured in specified number of days or less.'  
ELSE   
PRINT 'Some items for this order cannot be manufactured in specified number of days or less.' ;  
  
```  
  
 若要測試這個程序，請使用 `SalesOrderID 49080` 來執行程序，其具有一個需要 `2` 天時間來製造的組件，以及兩個需要 0 天來製造的組件。 下列的第一個陳述式符合此準則， 第二個查詢則不符合。  
  
```  
EXECUTE DaysToBuild 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in specified number of days or less.`  
  
```  
EXECUTE DaysToBuild 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Some items for this order cannot be manufactured in specified number of days or less.`  
  
## <a name="see-also"></a>另請參閱  
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  
