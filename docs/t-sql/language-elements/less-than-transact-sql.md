---
title: "&lt;（小於）(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- < (Less Than)
- <_TSQL
- Than
- Less
- <
- Less Than
dev_langs:
- TSQL
helpviewer_keywords:
- less than (<)
- < (less than operator)
ms.assetid: 54f50bdd-bb62-4593-9af9-4c49edecab75
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b7123b55623f6b8aa5e61fb7c200de1ea39c706
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lt-less-than-transact-sql"></a>&lt;（小於）(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  比較兩個運算式 (比較運算子)。 當您在比較非 Null 運算式時，如果左運算元的值小於右運算元，則結果為 TRUE，否則結果就是 FALSE。 如果任一個或兩個運算元都是 NULL，請參閱主題[SET ANSI_NULLS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression < expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 這兩個運算式的類型，都必須是可以隱含轉換的資料類型。 轉換的規則是根據[資料類型優先順序](../../t-sql/data-types/data-type-precedence-transact-sql.md)。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
## <a name="examples"></a>範例  
  
### <a name="a-using--in-a-simple-query"></a>A. 使用 < 簡單的查詢中  
 下列範例會傳回 `HumanResources.Department` 資料表中，`DepartmentID` 的值小於數值 3 的所有資料列。  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID < 3  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
1            Engineering  
2            Tool Design  
  
(2 row(s) affected)  
  
```  
  
### <a name="b-using--to-compare-two-variables"></a>B. 使用 < 比較兩個變數  
  
```  
DECLARE @a int = 45, @b int = 40;  
SELECT IIF ( @a < @b, 'TRUE', 'FALSE' ) AS Result;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------  
FALSE  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [IIF &#40;TRANSACT-SQL &#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  

