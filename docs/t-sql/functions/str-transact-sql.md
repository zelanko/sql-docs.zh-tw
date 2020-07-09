---
title: STR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STR
- STR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- converting numbers to characters
- characters [SQL Server], converting
- character data [SQL Server]
- STR function
ms.assetid: de03531b-d9e7-4c3c-9604-14e582ac20c6
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 58cfb510f3b7e0903a98a2c6cf44879326777167
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85995411"
---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回從數值資料轉換而來的字元資料。 字元資料為靠右對齊，且具有指定的長度和小數點有效位數。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *float_expression*  
 這是含小數點的近似數值 (**float**) 資料類型的運算式。  
  
 *length*  
 這是總長度。 其中包括小數點、正負號、數字和空格。 預設值為 10。  
  
 *decimal*  
 這是小數點右方的位數。 *decimal*必須小於或等於 16。 如果 *decimal* 大於 16，則結果就會截斷為小數點右方的十六位數。  
  
## <a name="return-types"></a>傳回型別  
 **varchar**  
  
## <a name="remarks"></a>備註  
 如果提供的話，STR 的 *length* 和 *decimal* 參數值應該是正數。 根據預設，如果 decimal 參數是 0，這個數字會捨入到整數。 指定的長度應該大於或等於小數點前面的數字部分，再加上數字的正負號 (如果有的話)。 在指定長度中，短的 *float_expression* 會靠右對齊，長的 *float_expression* 會在指定的小數位數截斷。 例如，STR(12, 10) 所產生的結果為 12。 這會在結果集中靠右對齊。 不過，STR(1223, 2) 會將結果集截斷為 \*\*。 字串函數可以是巢狀函數。  
  
> [!NOTE]  
>  若要轉換成 Unicode 資料，請在 CONVERT 或 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 轉換函數內使用 STR。  
  
## <a name="examples"></a>範例  
 下列範例會將五個位數和小數點組成的運算式轉換成六個位數的字元字串。 數字的小數點後部份會捨入到一個小數位數。  
  
```  
SELECT STR(123.45, 6, 1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------  
 123.5  
  
(1 row(s) affected)  
```  
  
 當運算式超出指定長度時，字串會針對指定字串傳回 `**`。  
  
```  
SELECT STR(123.45, 2, 2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--  
**  
  
(1 row(s) affected)  
```  
  
 即使數值資料巢狀放置在 `STR` 內，結果也是含指定格式的字元資料。  
  
```  
SELECT STR (FLOOR (123.45), 8, 3);
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [FORMAT &#40;Transact-SQL&#41;](../../t-sql/functions/format-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

