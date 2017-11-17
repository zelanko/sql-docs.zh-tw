---
title: "LEFT (TRANSACT-SQL) |Microsoft 文件"
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
- LEFT
- LEFT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- character strings [SQL Server], LEFT
- characters [SQL Server], leftmost
- LEFT function
- leftmost character of expression
ms.assetid: 44a8c71b-63d8-458b-8b5d-99d570067c3c
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0b0ec58ed9e8bbaae6f4f4ae90834f415476b039
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="left-transact-sql"></a>LEFT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回字元字串含指定字元數的左側部分。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
LEFT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的字元或二進位資料。 *character_expression*可以是常數、 變數或資料行。 *character_expression*可以是任何資料類型，除了**文字**或**ntext**，，可以隱含地轉換成**varchar**或**nvarchar**。 否則，請使用[轉換](../../t-sql/functions/cast-and-convert-transact-sql.md)函式可明確轉換*character_expression*。  
  
 *integer_expression*  
 這是一個正整數，指定的字元數*character_expression*會傳回。 如果*clause><*是負數，則會傳回錯誤。 如果*clause><*是型別**bigint**和包含大數值， *character_expression*必須是大型的資料類型例如**varchar（max)**.  
  
 *Clause><*參數會計算成一個字元的 utf-16 surrogate 字元。  
  
## <a name="return-types"></a>傳回類型  
 傳回**varchar**時*character_expression*是非 Unicode 字元資料類型。  
  
 傳回**nvarchar**時*character_expression*是 Unicode 字元資料類型。  
  
## <a name="remarks"></a>備註  
 當使用 SC 定序， *clause><*參數也 utf-16 surrogate 字組視為一個字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-left-with-a-column"></a>A. 使用 LEFT 搭配資料行  
 下列範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的 `Product` 資料表中，每個產品名稱最左邊的五個字元。  
  
```  
SELECT LEFT(Name, 5)   
FROM Production.Product  
ORDER BY ProductID;  
GO  
```  
  
### <a name="b-using-left-with-a-character-string"></a>B. 使用 LEFT 搭配字元字串  
 下列範例會利用 `LEFT` 來傳回字元字串 `abcdefg` 最左側兩個字元。  
  
```  
SELECT LEFT('abcdefg',2);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab   
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-left-with-a-column"></a>C. 使用 LEFT 搭配資料行  
 下列範例會傳回每個產品名稱的最左側五個字元。  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT(EnglishProductName, 5)   
FROM dbo.DimProduct  
ORDER BY ProductKey;  
```  
  
### <a name="d-using-left-with-a-character-string"></a>D. 使用 LEFT 搭配字元字串  
 下列範例會利用 `LEFT` 來傳回字元字串 `abcdefg` 最左側兩個字元。  
  
```  
-- Uses AdventureWorks  
  
SELECT LEFT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--   
ab  
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


