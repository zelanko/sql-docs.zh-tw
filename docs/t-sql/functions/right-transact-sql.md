---
description: RIGHT (Transact-SQL)
title: RIGHT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 219d071b6cb85dad1014a1cdf5b40926aaba634a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422622"
---
# <a name="right-transact-sql"></a>RIGHT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回指定字元數之字元字串的右側部分。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
RIGHT ( character_expression , integer_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *character_expression*  
 這是字元或二進位資料的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 *character_expression* 可以是常數、變數或資料行。 *character_expression* 可以是除了 **text** 或 **ntext** 之外的任何資料類型，可隱含地轉換為 **varchar** 或 **nvarchar**。 否則，請使用 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) 函數來明確轉換 *character_expression*。  
   
> [!NOTE]  
> 若 *string_expression* 是 **二進位** 或 **varbinary** 的類型，RIGHT 就會執行隱含轉換成 **varchar**，所以不會保留二進位輸入。  
  
 *integer_expression*  
 這是一個指定將傳回的 *character_expression* 字元數的正整數。 如果 *integer_expression* 是負數，則會傳回錯誤。 如果 *integer_expression* 是 **bigint** 類型且包含大數值，則 *character_expression* 必須屬於大型資料類型，例如 **varchar(max)** 。  
  
## <a name="return-types"></a>傳回型別  
 當 *character_expression* 是非 Unicode 字元資料類型時，則傳回 **varchar**。  
  
 當 *character_expression* 是 Unicode 字元資料類型時，則傳回 **nvarchar**。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 當使用 SC 定序時，RIGHT 參數也將 UTF-16 Surrogate 字組視為單一字元。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-right-with-a-column"></a>A：搭配資料行使用 RIGHT  
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-right-with-a-column"></a>B. 搭配資料行使用 RIGHT  
 下列範例會傳回 `DimEmployee` 資料表中，每個姓氏的最右側五個字元。  
  
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
  
### <a name="c-using-right-with-a-character-string"></a>C. 搭配字元字串使用 RIGHT  
 下列範例會利用 `RIGHT` 來傳回字元字串 `abcdefg` 最右側兩個字元。  
  
```  
SELECT RIGHT('abcdefg', 2); 
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
-------  
fg
```  
  
## <a name="see-also"></a>另請參閱  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

