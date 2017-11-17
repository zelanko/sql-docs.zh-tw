---
title: "ROUND (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
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
- ROUND_TSQL
- ROUND
dev_langs:
- TSQL
helpviewer_keywords:
- rounding expressions
- ROUND function [Transact-SQL]
ms.assetid: 23921ed6-dd6a-4c9e-8c32-91c0d44fe4b7
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: cba8b5a9b62a21fc810ff9bb5fcd3d0c6429f9f5
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回數值，捨入到指定的長度或有效位數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ROUND (numeric_expression , length )  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)精確數值或相近數值資料類型類別目錄，除了**元**資料型別。  
  
 *length*  
 有效位數的*numeric_expression*會捨入。 *長度*必須是類型的運算式**tinyint**， **smallint**，或**int**。當*長度*是正數， *numeric_expression*所指定的十進位數字會捨入*長度*。 當*長度*為負數， *numeric_expression*所指定小數點左側捨入*長度*。  
  
 *函數*  
 這是要執行的作業類型。 *函式*必須**tinyint**， **smallint**，或**int**。當*函式*省略或者值為 0 （預設）、 *numeric_expression*會捨入。 指定 0 以外的值時， *numeric_expression*會被截斷。  
  
## <a name="return-types"></a>傳回類型  
 傳回下列資料類型。  
  
|運算式結果|傳回類型|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**十進位**和**數值**類別目錄 （p，s）|**decimal （p，s）**|  
|**money**和**smallmoney**類別|**money**|  
|**float**和**真實**類別|**float**|  
  
## <a name="remarks"></a>備註  
 ROUND 會一律傳回值。 如果*長度*是負數且大於小數點前面的位數，ROUND 會傳回 0。  
  
|範例|結果|  
|-------------|------------|  
|ROUND （748.58、-4）|0|  
  
 ROUND 會傳回捨入*numeric_expression*，不論資料類型時*長度*為負數。  
  
|範例|結果|  
|--------------|------------|  
|ROUND （748.58，-1）|750.00|  
|ROUND （748.58，-2）|700.00|  
|ROUND(748.58, -3)|導致算術溢位，因為 748.58 預設為 decimal(5,2)，而它不可能傳回 1000.00。|  
|若要無條件進位至 4 位數，請變更輸入的資料類型。 例如：<br /><br /> `SELECT ROUND(CAST (748.58 AS decimal (6,2)),-3);`|1000.00|  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-round-and-estimates"></a>A. 使用 ROUND 與估計  
 下列範例顯示利用 `ROUND` 來示範的兩個運算式，最後一位數永遠是一項估計。  
  
```  
SELECT ROUND(123.9994, 3), ROUND(123.9995, 3);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -----------  
123.9990    124.0000      
```  
  
### <a name="b-using-round-and-rounding-approximations"></a>B. 使用 ROUND 與捨入近似值  
 下列範例顯示捨入和近似值。  
  
```  
SELECT ROUND(123.4545, 2), ROUND(123.45, -2);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ----------
123.45    100.00
```
  
### <a name="c-using-round-to-truncate"></a>C. 利用 ROUND 截斷  
 下列範例利用兩個 `SELECT` 陳述式，來示範捨入和截斷之間的差異。 第一個陳述式會捨入結果。 第二個陳述式會截斷結果。  
  
```  
SELECT ROUND(150.75, 0);  
GO  
SELECT ROUND(150.75, 0, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
151.00  
  
(1 row(s) affected)  
  
--------  
150.00  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-round-and-estimates"></a>D. 使用 ROUND 與估計  
 下列範例顯示利用 `ROUND` 來示範的兩個運算式，最後一位數永遠是一項估計。  
  
```  
SELECT ROUND(123.994999, 3), ROUND(123.995444, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

 ```
--------  ---------
123.995000    123.995444
```
  
## <a name="see-also"></a>另請參閱  
 [CEILING &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40;TRANSACT-SQL &#41;](../../t-sql/functions/floor-transact-sql.md)   
 [數學函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  


