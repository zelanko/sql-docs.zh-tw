---
title: "- （負）(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- negative
dev_langs:
- TSQL
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
- negative values
ms.assetid: d6c14d14-d379-403b-82db-c197ad58c896
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47a9eb729127e53dc3ee72fe5353ad536c56d922
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="unary-operators---negative"></a>一元運算子-負數
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回數值運算式 (一元運算子) 的負值。 一元運算子只能在屬於數值資料類型類別目錄之任何資料類型的單一運算式上執行運算。   
  
|運算子|意義|  
|--------------|-------------|  
|[+ (正)](../../t-sql/language-elements/unary-operators-positive.md)|數值是正的。|  
|[- (負)](../../t-sql/language-elements/unary-operators-negative.md)|數值是負的。|  
|[~ (位元 NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)|傳回數字的一補數。|  
  
 屬於數值資料類型類別目錄之任一資料類型的任何有效運算式，都可以使用 + (正) 和 - (負) 運算子。 ~ (位元 NOT) 運算子只能用在屬於整數資料類型類別目錄之任一資料類型的運算式上。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
- numeric_expression  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)其中任何一個資料類型的數值資料類型類別目錄以外的日期和時間類別目錄。  
  
## <a name="result-types"></a>結果類型  
 傳回的資料型別*numeric_expression*，不同之處在於不帶正負號**tinyint**運算式升級到帶正負號**smallint**結果。  
  
## <a name="examples"></a>範例  
  
### <a name="a-setting-a-variable-to-a-negative-value"></a>A. 將變數設為負值  
 下列範例會將變數設為負值。  
  
```  
USE tempdb;  
GO  
DECLARE @MyNumber decimal(10,2);  
SET @MyNumber = -123.45;  
SELECT @MyNumber AS NegativeValue;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
NegativeValue  
---------------------------------------  
-123.45  
  
(1 row(s) affected)  
  
```  
  
### <a name="b-changing-a-variable-to-a-negative-value"></a>B. 將變數變更為負值  
 下列範例會將變數改成負值。  
  
```  
USE tempdb;  
GO  
DECLARE @Num1 int;  
SET @Num1 = 5;  
SELECT @Num1 AS VariableValue, -@Num1 AS NegativeValue;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
VariableValue NegativeValue  
------------- -------------  
5             -5  
  
(1 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-the-negative-of-a-positive-constant"></a>C. 傳回的負數正數的常數  
 下列範例會傳回的負數正數的常數。  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) - 17 FROM DimEmployee;  
```  
  
 傳回值  
  
```  
-17  
```  
  
### <a name="d-returning-the-positive-of-a-negative-constant"></a>D. 傳回負常數的正數  
 下列範例會傳回負常數的正數。  
  
```  
USE ssawPDW;  
  
SELECT TOP (1) – ( - 17) FROM DimEmployee;  
```  
  
 傳回值  
  
```  
17  
```  
  
### <a name="e-returning-the-negative-of-a-column"></a>E. 傳回的負數，資料行  
 下列範例會傳回的負數`BaseRate`值中的每一位員工`dimEmployee`資料表。  
  
```  
USE ssawPDW;  
  
SELECT - BaseRate FROM DimEmployee;  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  


