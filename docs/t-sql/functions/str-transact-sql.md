---
title: "STR (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 7cddf1af7eba56824e41ad1ebaedb9aecdc37074
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="str-transact-sql"></a>STR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回從數值資料轉換而來的字元資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STR ( float_expression [ , length [ , decimal ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *float_expression*  
 近似數值運算式 (**float**) 資料類型，含小數點。  
  
 *length*  
 這是總長度。 其中包括小數點、正負號、數字和空格。 預設值是 10。  
  
 *decimal*  
 這是小數點右方的位數。 *十進位*必須小於或等於 16。 如果*十進位*超過 16，則結果會截斷為小數點右邊的十六位數。  
  
## <a name="return-types"></a>傳回類型  
 **varchar**  
  
## <a name="remarks"></a>備註  
 如果提供，如值*長度*和*十進位*str 參數應該是正數。 根據預設，如果 decimal 參數是 0，這個數字會捨入到整數。 指定的長度應該大於或等於小數點前面的數字部分，再加上數字的正負號 (如果有的話)。 一個簡短*float_expression*是靠右對齊，在指定的長度和一個長整數*float_expression*截斷為指定的小數位數。 例如，STR (12**，**10) 產生的結果是 12。 這會在結果集中靠右對齊。 不過，STR (1223年**，**2) 會截斷結果集 * *。 字串函數可以是巢狀函數。  
  
> [!NOTE]  
>  若要轉換的 Unicode 資料，內使用 STR 轉換或[轉換](../../t-sql/functions/cast-and-convert-transact-sql.md)轉換函式。  
  
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
SELECT STR (FLOOR (123.45), 8, 3;)  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------  
 123.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


