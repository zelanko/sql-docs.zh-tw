---
title: "取代 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs:
- TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8340c1b3af3ad843a0e3080cbfdc771d7353c7b7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將指定字串值的所有相符項目取代成另一個字串值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>引數  
 *string_expression*  
 是字串[運算式](../../t-sql/language-elements/expressions-transact-sql.md)搜尋。 *string_expression*可以是字元或二進位資料類型。  
  
 *string_*模式  
 這是要尋找的子字串。 *string_pattern*可以是字元或二進位資料類型。 *string_pattern*不可為空字串 （"），而且不得超過頁面所容納的位元組數目上限。  
  
 *string_*取代  
 這是取代字串。 *string_replacement*可以是字元或二進位資料類型。  
  
## <a name="return-types"></a>傳回類型  
 傳回**nvarchar**如果其中一個輸入引數的**nvarchar**資料類型; 否則 REPLACE 會傳回**varchar**。  
  
 如果任何一個引數是 NULL，便會傳回 NULL。  
  
 如果*string_expression*的類型不是**varchar （max)**或**nvarchar （max)，取代**會截斷為 8,000 個位元組的傳回值。 若要傳回值大於 8,000 個位元組， *string_expression*必須明確轉換成大數值資料類型。  
  
## <a name="remarks"></a>備註  
 REPLACE 會以輸入的定序為基礎來執行比較。 若要執行指定的定序的比較，您可以使用[COLLATE](~/t-sql/statements/collations.md)明確定序套用至輸入。  
  
 0x0000 (**char(0)**) 是 Windows 定序中未定義的字元，不包含在 REPLACE。  
  
## <a name="examples"></a>範例  
 下列範例利用 `cde` 來取代 `abcdefghi` 中的 `xxx` 字串。  
  
```sql  
SELECT REPLACE('abcdefghicde','cde','xxx');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
abxxxfghixxx  
(1 row(s) affected)  
```  
  
 下列範例使用 `COLLATE` 函數。  
  
```sql  
SELECT REPLACE('This is a Test'  COLLATE Latin1_General_BIN,  
'Test', 'desk' );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
This is a desk  
(1 row(s) affected)  
```  

  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  

