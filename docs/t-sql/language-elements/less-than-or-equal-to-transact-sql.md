---
title: "&lt;= （小於或等於） (TRANSACT-SQL) |Microsoft 文件"
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
- <=
- Less
- Equal To
- <=_TSQL
- Less Than
- Equal
dev_langs: TSQL
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 1f05474c-0377-48cb-b567-9d85d0c40479
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a330768916e0b57db1e11258cd124fb486174cf9
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="lt-less-than-or-equal-to-transact-sql"></a>&lt;= （小於或等於） (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  比較兩個運算式 (比較運算子)。 當您在比較非 Null 運算式時，如果左運算元的值小於或等於右運算元，則結果為 TRUE，否則結果就是 FALSE。  
  
 與 = (等於) 比較運算子不同的是，兩個 NULL 值的 >= 比較結果不受到 ANSI_NULLS 設定的影響。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression <= expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 這兩個運算式的類型，都必須是可以隱含轉換的資料類型。 轉換的規則是根據[資料類型優先順序](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
## <a name="examples"></a>範例  
  
### <a name="a-using--in-a-simple-query"></a>A. 使用 < = 簡單的查詢中  
 下列範例會傳回 `HumanResources.Department` 資料表中，`DepartmentID` 的值小於或等於 3 的所有資料列。  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID <= 3  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
1            Engineering  
2            Tool Design  
3            Sales  
  
(3 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
