---
title: REPLACE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 330a3d79893bd24e3253eced054fa029b7f8d1d9
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將指定字串值的所有相符項目取代成另一個字串值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>引數  
 *string_expression*  
 這是要搜尋的字串[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 *string_expression* 可以是字元或二進位資料類型。  
  
 *string_*pattern  
 這是要尋找的子字串。 *string_pattern* 可以是字元或二進位資料類型。 *string_pattern*不可以是空字串 ('')，並且不得超過分頁所能容納的最大位元組數目。  
  
 *string_*replacement  
 這是取代字串。 *string_replacement* 可以是字元或二進位資料類型。  
  
## <a name="return-types"></a>傳回類型  
 如果其中一個輸入引數是 **nvarchar** 資料類型，便傳回 **nvarchar**；否則，REPLACE 會傳回 **varchar**。  
  
 如果任何一個引數是 NULL，便會傳回 NULL。  
  
 如果 *string_expression* 的類型不是 **varchar(max)** 或 **nvarchar(max)，則 REPLACE** 會將傳回值截斷為 8,000 位元組。 若要傳回大於 8,000 位元組的值，*string_expression* 必須明確轉換成大數值資料類型。  
  
## <a name="remarks"></a>Remarks  
 REPLACE 會以輸入的定序為基礎來執行比較。 若要執行指定定序的比較，您可以利用 [COLLATE](~/t-sql/statements/collations.md)，將明確定序套用至輸入。  
  
 0x0000 (**char(0)**) 是 Windows 定序中未定義的字元，而且不得包含在 REPLACE 中。  
  
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
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
