---
title: "較低 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOWER
- LOWER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- characters [SQL Server], lowercase
- LOWER function
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
- converting uppercase to lowercase characters
ms.assetid: 1783352b-6852-4658-9d94-51963c59b9bf
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 545d3b5a0635c80f55aeb5b0a7a4e1804098e19c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lower-transact-sql"></a>LOWER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將大寫字元資料轉換成小寫之後，傳回字元運算式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LOWER ( character_expression )  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的字元或二進位資料。 *character_expression*可以是常數、 變數或資料行。 *character_expression*隱含地轉換成資料類型必須是**varchar**。 否則，請使用[轉換](../../t-sql/functions/cast-and-convert-transact-sql.md)來明確轉換*character_expression*。  
  
## <a name="return-types"></a>傳回類型  
 **varchar**或**nvarchar**  
  
## <a name="examples"></a>範例  
 下列範例會利用 `LOWER` 函數、`UPPER` 函數，且將 `UPPER` 函數巢狀放置於 `LOWER` 函數內，以選取價格在 $11 和 $20 之間的產品名稱。 這個範例會使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫。  
  
```  
SELECT LOWER(SUBSTRING(Name, 1, 20)) AS Lower,   
   UPPER(SUBSTRING(Name, 1, 20)) AS Upper,   
   LOWER(UPPER(SUBSTRING(Name, 1, 20))) As LowerUpper  
FROM Production.Product  
WHERE ListPrice between 11.00 and 20.00;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Lower                    Upper                    LowerUpper`  
  
 `---------------------    ---------------------    --------------------`  
  
 `minipump                 MINIPUMP                 minipump`  
  
 `taillights - battery     TAILLIGHTS - BATTERY     taillights - battery`  
  
 `(2 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會利用 `LOWER` 函數、`UPPER` 函數，且將 `UPPER` 函數巢狀放置於 `LOWER` 函數內，以選取價格在 $11 和 $20 之間的產品名稱。  
  
```  
-- Uses AdventureWorks  
  
SELECT LOWER(SUBSTRING(EnglishProductName, 1, 20)) AS Lower,   
       UPPER(SUBSTRING(EnglishProductName, 1, 20)) AS Upper,   
       LOWER(UPPER(SUBSTRING(EnglishProductName, 1, 20))) As LowerUpper  
FROM dbo.DimProduct  
WHERE ListPrice between 11.00 and 20.00;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Lower                 Upper                  LowerUpper`  
  
 `--------------------  ---------------------  --------------------`  
  
 `minipump              MINIPUMP               minipump`  
  
 `taillights – battery  TAILLIGHTS – BATTERY   taillights - battery`  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


