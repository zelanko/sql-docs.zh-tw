---
title: STUFF (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STUFF
- STUFF_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting characters
- STUFF function
- length characters
- removing characters
- replacing characters
- characters [SQL Server], replacing
- inserting data
ms.assetid: abb0afa9-44f6-42a2-a871-5f471dfb222b
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0bb5b030b138fa49f90c77c13e12bf2f64968da3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71341998"
---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  STUFF 函數會將字串插入另一個字串。 它會在第一個字串的開始位置刪除指定長度的字元，然後將第二個字串插入第一個字串的開始位置。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 這是字元資料的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 *character_expression* 可以是字元或二進位資料的常數、變數或資料行。  
  
 *start*  
 這是一個開始刪除和插入之位置的整數值。 如果 *start* 是負數或零，則會傳回 Null 字串。 如果 *start* 長度超出第一個 *character_expression*，則會傳回 Null 字串。 *start* 可以是 **bigint** 類型。  
  
 *length*  
 這是一個整數，指定要刪除的字元數。 如果 *length* 是負數，則會傳回 Null 字串。 如果 *length* 長度超出第一個 *character_expression*，則刪除動作就會進行到最後一個 *character_expression*的最後一個字元。  如果 *length* 為零，則會在 *start* 位置進行插入，且不會刪除任何字元。 *length* 可以是 **bigint** 類型。

 *replaceWith_expression*  
 這是字元資料的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 *character_expression* 可以是字元或二進位資料的常數、變數或資料行。 這個運算式會從 *start* 開始取代 *character_expression* 的 *length* 字元。 提供 `NULL` 當做 *replaceWith_expression*，移除字元且不插入任何內容。   
  
## <a name="return-types"></a>傳回型別  
 如果 *character_expression* 是其中一個支援的字元資料類型，就會傳回字元資料。 如果 *character_expression* 是其中一個支援的二進位資料類型，就會傳回二進位資料。  
  
## <a name="remarks"></a>備註  
 如果開始位置或長度是負的，或如果開始位置大於第一個字串的長度，則會傳回空的字串。 如果開始位置是 0，則會傳回 null 值。 如果刪除的長度大於第一個字串，則會刪除到剩下第一個字串中的第一個字元。  

如果產生的值大於傳回類型所支援的最大值，便會引發錯誤。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 當使用 SC 定序時，*character_expression* 和 *replaceWith_expression* 都可以包含代理字組。 長度參數會將 *character_expression* 中的每個 Surrogate 計算為單一字元。  
  
## <a name="examples"></a>範例  
 下列範例會傳回從第一個字串 (`abcdef`) 中，從位置 `2` (`b`) 開始，刪除三個字元所建立的字元字串，且會在刪除點插入第二個字串。  
  
```  
SELECT STUFF('abcdef', 2, 3, 'ijklmn');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
aijklmnef   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
