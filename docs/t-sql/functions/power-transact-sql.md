---
title: POWER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- POWER_TSQL
- POWER
dev_langs:
- TSQL
helpviewer_keywords:
- POWER function
ms.assetid: 0fd34494-90b9-4559-8011-a8c1b9f40239
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c11afa07f04e01919b51daf92025ed5d82902ee7
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111898"
---
# <a name="power-transact-sql"></a>POWER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  將指定之運算式的值傳回給指定的乘冪。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
POWER ( float_expression , y )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *float_expression*  
 為 [float](../../t-sql/language-elements/expressions-transact-sql.md) 類型或能夠隱含轉換成 **float** 類型的**運算式**。  
  
 *y*  
 為 *float_expression* 相乘的乘冪。 *y*　可為精確數值或近似數值資料類型類別目錄的運算式，但 **bit** 資料類型除外。  
  
## <a name="return-types"></a>傳回型別  
 傳回型別取決於 *float_expression* 的輸入類型：
 
|輸入類型|傳回類型|  
|----------|-----------|  
|**float**、**real**|**float**|
|**decimal(*p*, *s*)**|**decimal(38, *s*)**|
|**int**、**smallint**、**tinyint**|**int**|
|**bigint**|**bigint**|
|**money**、 **smallmoney**|**money**|
|**bit**、**char**、**nchar**、**varchar**、**nvarchar**|**float**|
 
如果結果不符合傳回型別，就會發生算術溢位錯誤。
  
## <a name="examples"></a>範例  
  
### <a name="a-using-power-to-return-the-cube-of-a-number"></a>A. 使用 POWER 傳回數字的立方  
 下列範例示範將某個數字自乘 3 次 (數字的立方)。  
  
```  
DECLARE @input1 FLOAT;  
DECLARE @input2 FLOAT;  
SET @input1= 2;  
SET @input2 = 2.5;  
SELECT POWER(@input1, 3) AS Result1, POWER(@input2, 3) AS Result2;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result1                Result2  
---------------------- ----------------------  
8                      15.625  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-power-to-show-results-of-data-type-conversion"></a>B. 利用 POWER 來顯示資料類型轉換的結果  
 下列範例示範 *float_expression* 如何保留可能會傳回非預期結果的資料類型。  
  
```  
SELECT   
POWER(CAST(2.0 AS FLOAT), -100.0) AS FloatResult,  
POWER(2, -100.0) AS IntegerResult,  
POWER(CAST(2.0 AS INT), -100.0) AS IntegerResult,  
POWER(2.0, -100.0) AS Decimal1Result,  
POWER(2.00, -100.0) AS Decimal2Result,  
POWER(CAST(2.0 AS DECIMAL(5,2)), -100.0) AS Decimal2Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FloatResult            IntegerResult IntegerResult Decimal1Result Decimal2Result Decimal2Result  
---------------------- ------------- ------------- -------------- -------------- --------------  
7.88860905221012E-31   0             0             0.0            0.00           0.00  
```  
  
### <a name="c-using-power"></a>C. 使用 POWER  
 下列範例會傳回 `POWER` 的 `2` 結果。  
  
```  
DECLARE @value INT, @counter INT;  
SET @value = 2;  
SET @counter = 1;  
  
WHILE @counter < 5  
   BEGIN  
      SELECT POWER(@value, @counter)  
      SET NOCOUNT ON  
      SET @counter = @counter + 1  
      SET NOCOUNT OFF  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
2             
  
(1 row(s) affected)  
  
-----------   
4             
  
(1 row(s) affected)  
  
-----------   
8             
  
(1 row(s) affected)  
  
-----------   
16            
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-power-to-return-the-cube-of-a-number"></a>D：使用 POWER 傳回數字的立方  
 下列範例示範傳回 `POWER` 的 3 次方 `2.0` 結果。  
  
```  
SELECT POWER(2.0, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
------------ 
8.0
```  
  
## <a name="see-also"></a>另請參閱  
 [decimal 和 numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)   
 [float 和 real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)   
 [int、bigint、smallint 和 tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)   
 [數學函數 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [money 和 smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
  
  

