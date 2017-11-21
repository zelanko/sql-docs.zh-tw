---
title: "LOG10 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOG10
- LOG10_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- LOG10 function
- base-10 logarithms
- logarithm of expression
ms.assetid: 1eb7fb34-1937-4a39-a936-f5c0c7c7e06f
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d8cc5b0ef6af319e55744a3ca373f0e6b11e230b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="log10-transact-sql"></a>LOG10 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定的基底 10 對數**float**運算式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
LOG10 ( float_expression )  
```  
  
## <a name="arguments"></a>引數  
 *float_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)型別的**float**或可以隱含地轉換成的型別**float**。  
  
## <a name="return-types"></a>傳回類型  
 **float**  
  
## <a name="remarks"></a>備註  
 LOG10 和 POWER 函數是彼此反向關聯。 例如，10 ^ LOG10 (*n*) =  *n* 。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calculating-the-base-10-logarithm-for-a-variable"></a>A. 針對某個變數，計算以 10 為基底的對數。  
 下列範例會計算指定變數的 `LOG10`。  
  
```  
DECLARE @var float;  
SET @var = 145.175643;  
SELECT 'The LOG10 of the variable is: ' + CONVERT(varchar,LOG10(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The LOG10 of the variable is: 2.16189      
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-result-of-raising-a-base-10-logarithm-to-a-specified-power"></a>B. 將以 10 為基底的對數提升到指定的乘冪，再計算其結果。  
 下列範例會傳回將以 10 為基底的對數提升到指定乘冪之後所得出的結果。  
  
```  
SELECT POWER (10, LOG10(5));   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------  
5  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-base-10-logarithm-for-a-value"></a>C： 計算值的基底 10 對數。  
 下列範例會計算`LOG10`指定的值。  
  
```  
SELECT LOG10(145.175642);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-------------------  
2.16
```  
  
## <a name="see-also"></a>另請參閱  
 [數學函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [電源 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/power-transact-sql.md)   
 [記錄檔 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/log-transact-sql.md)  
  
  


