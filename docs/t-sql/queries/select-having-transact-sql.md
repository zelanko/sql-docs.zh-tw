---
title: HAVING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HAVING
- HAVING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restricting conditions for result set
- search conditions [SQL Server], HAVING clause
- HAVING clause
- HAVING clause, about HAVING clause
ms.assetid: 55650709-001e-42f4-902f-ead09a3c34af
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d0a0e10f4cef3eaffc55a691758f50e6f48d1efe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33059215"
---
# <a name="select---having-transact-sql"></a>SELECT - HAVING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定群組或彙總的搜尋條件。 HAVING 只能搭配 SELECT 陳述式使用。 HAVING 通常會與 GROUP BY 子句搭配使用。 未使用 GROUP BY 時，會有隱含的單一彙總群組。   
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>引數  
\<search_condition> 指定一或多個要讓群組和/或彙總相符的述詞。 如需有關搜尋條件和述詞的詳細資訊，請參閱[搜尋條件 &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)。  
  
 在 HAVING 子句中，不能使用 **text**、**image** 及 **ntext** 資料類型。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會使用 `HAVING` 子句從 `FactInternetSales` 資料表中，擷取 `OrderDateKey` 在 2004 年或之後的每個 `SalesAmount` 的總計。  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>另請參閱  
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

