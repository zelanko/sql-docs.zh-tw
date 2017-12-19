---
title: "有 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAVING
- HAVING_TSQL
dev_langs: TSQL
helpviewer_keywords:
- restricting conditions for result set
- search conditions [SQL Server], HAVING clause
- HAVING clause
- HAVING clause, about HAVING clause
ms.assetid: 55650709-001e-42f4-902f-ead09a3c34af
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: cf99ee7aece979c973d2d162062ac2bae7aac296
ms.sourcegitcommit: 721ad1cbc10e8147c087ae36b36296d72cbb0de8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/07/2017
---
# <a name="select---having-transact-sql"></a>選取-具有 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定群組或彙總的搜尋條件。 HAVING 只能搭配 SELECT 陳述式使用。 HAVING 通常搭配 GROUP BY 子句。 當未使用 GROUP BY 時，沒有隱含的單一的彙總群組。   
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>引數  
\<s > 指定的群組和/或彙總符合一或多個述詞。 如需有關搜尋條件和述詞的詳細資訊，請參閱[搜尋條件 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 **文字**，**映像**，和**ntext**資料型別不能在 HAVING 子句。  
  
## <a name="examples"></a>範例  
 使用簡單 `HAVING` 子句的下列範例會從 `SalesOrderID` 資料表中，擷取超出 `SalesOrderDetail` 的每個 `$100000.00` 的總計。  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID  
HAVING SUM(LineTotal) > 100000.00  
ORDER BY SalesOrderID ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會使用`HAVING`擷取總計每個子句`SalesAmount`從`FactInternetSales`資料表`OrderDateKey`處於 2004年以後的年份。  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>請參閱  
 [GROUP BY &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

