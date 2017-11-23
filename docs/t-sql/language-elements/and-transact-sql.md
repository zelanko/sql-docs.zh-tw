---
title: "和 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
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
- AND_TSQL
- AND
dev_langs: TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- TRUE
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 34014541d124b0226218012d907fd2f99e0b1610
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="and-transact-sql"></a>AND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  結合兩個布林運算式，並傳回**TRUE**這兩個運算式時**TRUE**。 陳述式中使用一個以上的邏輯運算子時**AND**運算子會先評估。 您可以使用括號來變更驗算的順序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>引數  
 *boolean_expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)傳回布林值： **TRUE**， **FALSE**，或**未知**。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
## <a name="result-value"></a>結果值  
 當兩個運算式都是 TRUE 時，便傳回 TRUE。  
  
## <a name="remarks"></a>備註  
 下圖顯示利用 AND 運算子比較 TRUE 和 FALSE 值的結果。  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**為 TRUE**|TRUE|FALSE|UNKNOWN|  
|**FALSE**|FALSE|FALSE|FALSE|  
|**未知**|UNKNOWN|FALSE|UNKNOWN|  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-and-operator"></a>A. 使用 AND 運算子  
 下列範例會選取職稱為 `Marketing Assistant` 而且可用休假時數超過 `41` 之員工的相關資訊。  
  
```  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>B. 在 IF 陳述式中使用 AND 運算子  
 下列範例將示範如何在 IF 陳述式中使用 AND。 在第一個陳述式中，`1 = 1` 和 `2 = 2` 都是 true。因此，結果為 true。 在第二個範例中，引數 `2 = 17` 是 false。因此，結果為 false。  
  
```  
IF 1 = 1 AND 2 = 2  
BEGIN  
   PRINT 'First Example is TRUE'  
END  
ELSE PRINT 'First Example is FALSE';  
GO  
  
IF 1 = 1 AND 2 = 17  
BEGIN  
   PRINT 'Second Example is TRUE'  
END  
ELSE PRINT 'Second Example is FALSE' ;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
