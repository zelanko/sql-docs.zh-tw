---
title: ROUND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97e6792bcd9ed9ea106e93e65c1c8bbdef70ec88
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947396"
---
# <a name="round-transact-sql"></a>ROUND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回數值，捨入到指定的長度或有效位數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ROUND ( numeric_expression , length [ ,function ] )  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 這是精確數值或近似數值資料類型類別的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，但 **bit** 資料類型除外。  
  
 *length*  
 這是 *numeric_expression* 捨入到的有效位數。 *length* 必須是 **tinyint**、**smallint** 或 **int** 類型的運算式。當 *length* 是正數時，*numeric_expression* 會捨入到 *length* 所指定的十進位數。 當 *length* 是負數時，*numeric_expression* 會依照 *length* 所指定的方式，在小數點左側捨入。  
  
 *函數*  
 這是要執行的作業類型。 *function* 必須是 **tinyint**、**smallint** 或 **int**。當 *function* 遭到省略或者值為 0 (預設值) 時，會捨入 *numeric_expression*。 當指定 0 以外的值時，會截斷 *numeric_expression*。  
  
## <a name="return-types"></a>傳回類型  
 傳回下列資料類型。  
  
|運算式結果|傳回類型|  
|-----------------------|-----------------|  
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**ssNoversion**|**int**|  
|**bigint**|**bigint**|  
|**decimal** 和 **numeric** 類別 (p, s)|**decimal(p, s)**|  
|**money** 和 **smallmoney** 類別|**money**|  
|**float** 和 **real** 類別|**float**|  
  
## <a name="remarks"></a>Remarks  
 ROUND 會一律傳回值。 如果 *length* 是負的，且大於小數點前面的位數，ROUND 會傳回 0。  
  
|範例|結果|  
|-------------|------------|  
|ROUND(748.58, -4)|0|  
  
 當 *length* 是負數時，不論資料類型為何，ROUND 都會傳回捨入的 *numeric_expression*。  
  
|範例|結果|  
|--------------|------------|  
|ROUND(748.58, -1)|750.00|  
|ROUND(748.58, -2)|700.00|  
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
  
## <a name="see-also"></a>另請參閱  
 [CEILING &#40;Transact-SQL&#41;](../../t-sql/functions/ceiling-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [FLOOR &#40;Transact-SQL&#41;](../../t-sql/functions/floor-transact-sql.md)   
 [數學函數 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
