---
title: "+ （一元加號）(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- + (positive)
- +
- positive
dev_langs:
- TSQL
helpviewer_keywords:
- + (positive operator)
- positive operator (+)
- positive values [SQL Server]
ms.assetid: 0f31c5cc-3078-4f6a-9870-7eb1a98053fb
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a0e451cc1e4341d7e516733ab8d82efe09b1be7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="unary-operators---positive"></a>一元運算子-正數
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回數值運算式 (一元運算子) 的值。 一元運算子只能在屬於數值資料類型類別目錄之任何資料類型的單一運算式上執行運算。   
  
|運算子|意義|  
|--------------|-------------|  
|[+ (正)](../../t-sql/language-elements/unary-operators-positive.md)|數值是正的。|  
|[- (負)](../../t-sql/language-elements/unary-operators-negative.md)|數值是負的。|  
|[~ (位元 NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|傳回數字的一補數。|  
  
 屬於數值資料類型類別目錄之任一資料類型的任何有效運算式，都可以使用 + (正) 和 - (負) 運算子。 ~ (位元 NOT) 運算子只能用在屬於整數資料類型類別目錄之任一資料類型的運算式上。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
+ numeric_expression  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)之任何資料類型的數值資料類型類別目錄中，除了**datetime**和**smalldatetime**資料型別。  
  
## <a name="result-types"></a>結果類型  
 傳回 *numeric_expression*的資料類型。  
  
## <a name="remarks"></a>備註  
 雖然一元加號可以出現在任何數值運算式之前，但從運算式傳回的值，它並不會做任何處理。 明確地說，如果運算式是負的，它便不會傳回正值。 若要傳回正值運算式是負的請使用[ABS](../../t-sql/functions/abs-transact-sql.md)函式。  
  
## <a name="examples"></a>範例  
  
### <a name="a-setting-a-variable-to-a-positive-value"></a>A. 將變數設為正值  
 下列範例會將變數設為正值。  
  
```  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = +123.45;  
SELECT @MyNumber;  
GO  
```  
  
 以下為結果集：  
  
```  
-----------   
123.45            
  
(1 row(s) affected)  
```  
  
### <a name="b-using-the-unary-plus-operator-with-a-negative-value"></a>B. 在負值上使用一元加號運算子  
 下列範例會顯示在相同的負運算式上使用一元加號和 ABS() 函數。 一元加號不會影響運算式，ABS 函數會傳回運算式的正值。  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = -5;  
SELECT +@Num1, ABS(@Num1);  
GO  
```  
  
 以下為結果集：  
  
```  
----------- -----------  
-5          5  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [ABS &#40;TRANSACT-SQL &#41;](../../t-sql/functions/abs-transact-sql.md)  
  
  
