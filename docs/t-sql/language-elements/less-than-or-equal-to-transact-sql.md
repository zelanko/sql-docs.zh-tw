---
title: '&lt;= (小於或等於) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- <=
- Less
- Equal To
- <=_TSQL
- Less Than
- Equal
dev_langs:
- TSQL
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 1f05474c-0377-48cb-b567-9d85d0c40479
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ad25557ac49be75e80872e124320ac4459315eee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lt-less-than-or-equal-to-transact-sql"></a>&lt;= (小於或等於) (Transact-SQL)
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
 這是任何有效的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 這兩個運算式的類型，都必須是可以隱含轉換的資料類型。 轉換會隨著[資料類型優先順序](../../t-sql/data-types/data-type-precedence-transact-sql.md)的規則而不同。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
## <a name="examples"></a>範例  
  
### <a name="a-using--in-a-simple-query"></a>A. 在簡單查詢中使用 <=  
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
 [運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
