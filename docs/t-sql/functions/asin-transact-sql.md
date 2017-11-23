---
title: "ASIN (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASIN_TSQL
- ASIN
dev_langs: TSQL
helpviewer_keywords:
- ASIN function
- sine
- arcsine
ms.assetid: 6256dd7d-83d5-486e-a933-1d59afc7e417
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 687c8bfde3b2f78d0136044ebe75c7206cb31d90
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="asin-transact-sql"></a>ASIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回角度，以弧度為單位，其正弦就是指定**float**運算式。 這也稱為反正弦函數 (Arcsine)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
ASIN ( float_expression )  
```  
  
## <a name="arguments"></a>引數  
*float_expression*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)型別的**float**或可以隱含地轉換成浮點數，其值介於-1 到 1 的型別。 超出這個範圍的值會傳回 NULL 並且回報網域錯誤。
  
## <a name="return-types"></a>傳回型別
**float**
  
## <a name="examples"></a>範例  
下列範例會**float**運算式並傳回指定角度的 ASIN。
  
```sql
/* The first value will be -1.01. This fails because the value is   
outside the range.*/  
DECLARE @angle float  
SET @angle = -1.01  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
  
-- The next value is -1.00.  
DECLARE @angle float  
SET @angle = -1.00  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
  
-- The next value is 0.1472738.  
DECLARE @angle float  
SET @angle = 0.1472738  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-------------------------  
.Net SqlClient Data Provider: Msg 3622, Level 16, State 1, Line 3  
A domain error occurred.  
  
---------------------------------   
The ASIN of the angle is: -1.5708                          
  
(1 row(s) affected)  
  
----------------------------------   
The ASIN of the angle is: 0.147811                         
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
下列範例會傳回 1.00 的反正弦值。
  
```sql
SELECT ASIN(1.00) AS asinCalc;  
```  
  
下列範例會傳回錯誤，因為它要求的值超出允許範圍的反正弦值。
  
```sql
SELECT ASIN(1.1472738) AS asinCalc;  
```  
  
## <a name="see-also"></a>另請參閱
[CEILING &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)  
[數學函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[SET ARITHIGNORE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-arithignore-transact-sql.md)  
[SET ARITHABORT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-arithabort-transact-sql.md)
  
  

