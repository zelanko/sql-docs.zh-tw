---
title: "RTRIM (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/05/2017
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
- RTRIM_TSQL
- RTRIM
dev_langs:
- TSQL
helpviewer_keywords:
- RTRIM function
- character strings [SQL Server], trailing blanks
- blank characters [SQL Server]
- trailing blanks
ms.assetid: 52fd6e8d-650c-4f66-abcf-67765aa5aa83
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 838bad2a5d5434fdb3bb338ba32f75ebdfd1460c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="rtrim-transact-sql"></a>RTRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回截斷所有尾端空白之後的字元字串。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
RTRIM ( character_expression )  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)字元資料。 *character_expression*可以是常數、 變數或資料行的字元或二進位資料。  
  
 *character_expression*隱含地轉換成資料類型必須是**varchar**。 否則，請使用[轉換](../../t-sql/functions/cast-and-convert-transact-sql.md)來明確轉換*character_expression*。  
  
## <a name="return-types"></a>傳回類型  
 **varchar**或**nvarchar**  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example"></a>A. 簡單範例  
 下列範例會採用在句尾具有空格的字元字串，並且傳回句尾沒有空格的文字。  
  
```  
SELECT RTRIM('Removes trailing spaces.   ');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
  `Removes trailing spaces.`  
  
### <a name="b-simple-example"></a>B： 簡單的範例  
 下列範例示範如何使用`RTRIM`移除尾端的空格。 目前有是串連的第一個字串，以顯示其空格已消失，另一個字串。  
  
```  
SELECT RTRIM('Four spaces are after the period in this sentence.    ') + 'Next string.';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
`Four spaces are after the period in this sentence.Next string.`  

### <a name="c-using-rtrim-with-a-variable"></a>C. 使用 RTRIM 搭配變數  
 下列範例會示範如何利用 `RTRIM` 來移除字元變數中的尾端空白。  
  
```  
DECLARE @string_to_trim varchar(60);  
SET @string_to_trim = 'Four spaces are after the period in this sentence.    ';  
SELECT @string_to_trim + ' Next string.';  
SELECT RTRIM(@string_to_trim) + ' Next string.';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```sql   
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence.     Next string.  
 
 (1 row(s) affected)`  
 
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence. Next string.  
 
 (1 row(s) affected)
 ```  
  

  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [TRIM &#40;TRANSACT-SQL &#41;](../../t-sql/functions/trim-transact-sql.md)  
 [LTRIM &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ltrim-transact-sql.md)  
  
  



