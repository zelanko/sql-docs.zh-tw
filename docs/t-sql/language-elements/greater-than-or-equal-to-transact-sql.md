---
title: "&gt;= (大於或等於) (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Greater
- '>='
- '>= (Greater Than or Equal To)'
- Equal To
- '>=_TSQL'
- Greater Than
- Equal
dev_langs: TSQL
helpviewer_keywords:
- greater than or equal to operator (>=)
- '>= (greater than or equal to operator)'
ms.assetid: 641ee28d-7536-46dd-a48a-6c63c2d59278
caps.latest.revision: "38"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: c3a6bb29426989cb19df574eab60e76b754c89a8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="gt-greater-than-or-equal-to-transact-sql"></a>&gt;= (大於或等於) (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  比較大於或等於 (比較運算子) 的兩個運算式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression >= expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 這兩個運算式的類型，都必須是可以隱含轉換的資料類型。 轉換的規則是根據[資料類型優先順序](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="result-types"></a>結果類型  
 布林  
  
## <a name="remarks"></a>備註  
 當您在比較非 Null 運算式時，如果左運算元的值大於或等於右運算元，則結果為 TRUE，否則結果就是 FALSE。  
  
 與 = (等於) 比較運算子不同的是，兩個 NULL 值的 >= 比較結果不受到 ANSI_NULLS 設定的影響。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using--in-a-simple-query"></a>A. 在簡單的查詢中使用 >=  
 下列範例會傳回 `HumanResources.Department` 資料表中，`DepartmentID` 的值大於或等於 13 的所有資料列。  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID >= 13  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
13           Quality Assurance  
14           Facilities and Maintenance  
15           Shipping and Receiving  
16           Executive  
  
(4 row(s) affected)  
  
```  
  
## <a name="see-also"></a>請參閱＜  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [= &#40;Equals &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/equals-transact-sql.md)   
 [&#62;&#40;大於 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
