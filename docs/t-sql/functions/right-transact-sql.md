---
title: "權限 (TRANSACT-SQL) |Microsoft 文件"
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
- RIGHT_TSQL
- RIGHT
dev_langs:
- TSQL
helpviewer_keywords:
- rightmost character of expression
- RIGHT function
- character strings [SQL Server], RIGHT
ms.assetid: 43f1fe1f-aa18-47e3-ba20-e03e32254a6d
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 19dcdea078648b6ff41e08fcf82c9a4c705abe4c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="right-transact-sql"></a>RIGHT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定字元數之字元字串的右側部分。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
RIGHT ( character_expression , integer_expression )  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的字元或二進位資料。 *character_expression*可以是常數、 變數或資料行。 *character_expression*可以是任何資料類型，除了**文字**或**ntext**，，可以隱含地轉換成**varchar**或**nvarchar**。 否則，請使用[轉換](../../t-sql/functions/cast-and-convert-transact-sql.md)函式可明確轉換*character_expression*。  
  
 *integer_expression*  
 這是一個正整數，指定的字元數*character_expression*會傳回。 如果*clause><*是負數，則會傳回錯誤。 如果*clause><*是型別**bigint**和包含大數值， *character_expression*必須是大型的資料類型例如**varchar（max)**.  
  
## <a name="return-types"></a>傳回類型  
 傳回**varchar**時*character_expression*是非 Unicode 字元資料類型。  
  
 傳回**nvarchar**時*character_expression*是 Unicode 字元資料類型。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 當使用 SC 定序時，RIGHT 參數也將 UTF-16 Surrogate 字組視為單一字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-right-with-a-column"></a>答： 使用具有資料行的權限  
 下列範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中每個人名字最右邊的五個字元。  
  
```  
SELECT RIGHT(FirstName, 5) AS 'First Name'  
FROM Person.Person  
WHERE BusinessEntityID < 5  
ORDER BY FirstName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
First Name  
----------  
Ken  
Terri  
berto  
Rob  
  
(4 row(s) affected)  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>B. 使用具有資料行的權限  
 下列範例會傳回每個姓氏的五個最右邊字元`DimEmployee`資料表。  
  
```  
-- Uses AdventureWorks  
  
SELECT RIGHT(LastName, 5) AS Name  
FROM dbo.DimEmployee  
ORDER BY EmployeeKey;  
```  
  
 以下為部分結果集。  
  
 ```
Name
-----
lbert
Brown
rello
lters
 ```  
  
### <a name="c-using-right-with-a-character-string"></a>C. 直接使用搭配字元字串  
 下列範例會使用`RIGHT`傳回字元字串的兩個最右邊字元`abcdefg`。  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP(1) RIGHT('abcdefg',2) FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


