---
title: "比較運算子 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 45c0e85b89d542dce815104eb8e831169599227b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="comparison-operators-transact-sql"></a>比較運算子 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  比較運算子用來測試兩個運算式是否相同。 比較運算子可以用於運算式除外的所有運算式**文字**， **ntext**，或**映像**資料型別。 下表會列出 [!INCLUDE[tsql](../../includes/tsql-md.md)] 比較運算子。  
  
|運算子|意義|  
|--------------|-------------|  
|[= (等於)](../../t-sql/language-elements/equals-transact-sql.md)|等於|  
|[> (大於)](../../t-sql/language-elements/greater-than-transact-sql.md)|大於|  
|[< (小於)](../../t-sql/language-elements/less-than-transact-sql.md)|小於|  
|[>= (大於或等於)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|大於或等於|  
|[<= (小於或等於)](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|小於或等於|  
|[<> (不等於)](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|不等於|  
|[!= (不等於)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|不等於 (不是 ISO 標準)|  
|[!< (不小於)](../../t-sql/language-elements/not-less-than-transact-sql.md)|不小於 (不是 ISO 標準)|  
|[!> (不大於)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|不大於 (不是 ISO 標準)|  
  
## <a name="boolean-data-type"></a>布林資料類型  
 比較運算子的結果具有**布林**資料型別。 它有三個值：TRUE、FALSE 和 UNKNOWN。 傳回運算式**布林**資料型別稱為布林運算式。  
  
 不同於其他[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別，**布林**資料型別不能指定為資料表資料行或變數的資料類型，並且不可傳回結果集內。  
  
 當 SET ANSI_NULLS 是 ON 時，有一或兩個 NULL 運算式的運算子會傳回 UNKNOWN。 當 SET ANSI_NULLS 是 OFF 時，如果兩個運算式都是 NULL，除了等於 (=) 運算子會傳回 TRUE，也適用相同的規則。 例如，當 SET ANSI_NULLS 是 OFF 時，NULL = NULL 會傳回 TRUE。  
  
 使用運算式**布林**資料類型都會用於 WHERE 子句來篩選符合的資料列流程控制語言陳述式中的搜尋條件，如 IF 和 WHILE，例如：  
  
```  
-- Uses AdventureWorks  
  
DECLARE @MyProduct int;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
