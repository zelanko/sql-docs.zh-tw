---
title: "STUFF (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: df9a3d019f22ec8a0ba610f2dd694e45a8bd9da3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="stuff-transact-sql"></a>STUFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  STUFF 函數會將字串插入另一個字串。 它會在第一個字串的開始位置刪除指定長度的字元，然後將第二個字串插入第一個字串的開始位置。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STUFF ( character_expression , start , length , replaceWith_expression )  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)字元資料。 *character_expression*可以是常數、 變數或資料行的字元或二進位資料。  
  
 *啟動*  
 這是一個開始刪除和插入之位置的整數值。 如果*啟動*或*長度*是負數，會傳回 null 字串。 如果*啟動*超過第一個*character_expression*，會傳回空字串。 *啟動*可以屬於型別**bigint**。  
  
 *length*  
 這是一個整數，指定要刪除的字元數。 如果*長度*超過第一個*character_expression*，就會刪除到最後一個到最後一個字元*character_expression*。 *長度*可以屬於型別**bigint**。  
  
 *replaceWith_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)字元資料。 *character_expression*可以是常數、 變數或資料行的字元或二進位資料。 這個運算式會取代*長度*字元*character_expression*開始*啟動*。 提供`NULL`為*replaceWith_expression*，而不需要插入任何項目移除的字元。   
  
## <a name="return-types"></a>傳回類型  
 如果傳回的字元資料*character_expression*是其中一個支援的字元資料類型。 傳回二進位資料，如果*character_expression*是其中一個支援的二進位資料類型。  
  
## <a name="remarks"></a>備註  
 如果開始位置或長度是負的，或如果開始位置大於第一個字串的長度，則會傳回空的字串。 如果開始位置是 0，則會傳回 null 值。 如果刪除的長度大於第一個字串，則會刪除到剩下第一個字串中的第一個字元。  

如果產生的值大於傳回類型所支援的最大值，便會引發錯誤。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 當使用 SC 定序，同時*character_expression*和*replaceWith_expression*可以包含 surrogate 字組。 長度參數計算每個 surrogate *character_expression*做為單一字元。  
  
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
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  

