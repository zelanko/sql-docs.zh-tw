---
title: "~ (位元 NOT) (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ~_TSQL
- bitwise
- NOT
- ~
- Bitwise NOT
dev_langs:
- TSQL
helpviewer_keywords:
- NOT keyword
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: 02da8016-f6c0-41ae-8d59-33eaa02bfc95
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3cfe0944a896548bfd0e0e0612b832ac91417016
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="-bitwise-not-transact-sql"></a>~ (位元 NOT) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在整數值上，執行位元邏輯 NOT 運算。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
~ expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)任一資料類型的整數資料類型類別目錄的**元**，或**二進位**或**varbinary**資料型別。 *運算式*會被視為位元運算的二進位數字。  
  
> [!NOTE]  
>  只有一個*運算式*可以是**二進位**或**varbinary**位元運算中的資料類型。  
  
## <a name="result-types"></a>結果類型  
 **int**如果輸入的值為**int**。  
  
 **smallint**如果輸入的值為**smallint**。  
  
 **tinyint**如果輸入的值為**tinyint**。  
  
 **位元**如果輸入的值為**元**。  
  
## <a name="remarks"></a>備註  
  **~** 位元運算子會執行位元邏輯 NOT for*運算式*，依次處理每個位元。 如果*運算式*的值為 0，結果集中的位元會設為 1; 否則結果中的位元會清除為 0 的值。 換句話說，1 會變更為零，零則會變更為 1。  
  
> [!IMPORTANT]  
>  當您執行任何種類的位元運算時，位元運算所用的運算式儲存長度非常重要。 我們建議您在儲存值時，使用這個相同的位元組數。 例如，儲存的十進位值 5 為**tinyint**， **smallint**，或**int**會產生不同位元組數目所儲存的值： **tinyint**使用 1 個位元組; 儲存資料**smallint**使用 2 個位元組，儲存資料和**int**使用 4 個位元組儲存資料。 因此，在上執行位元運算**int**十進位值可能會產生不同的結果，與使用直接二進位或十六進位轉換，尤其是當 **~**  (位元 NOT) 運算子使用。 位元 NOT 運算可能發生在長度較短的變數上。 在這個情況下，當較短的長度轉換成較長的資料類型變數時，上面 8 位元中的位元可能不會設為預期的值。 我們建議您將較小的資料類型變數轉換成較長的資料類型，之後，在結果上執行 NOT 運算。  
  
## <a name="examples"></a>範例  
 下列範例會建立資料表，使用**int**資料類型來儲存值，而且兩個值插入單一資料列。  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 下列查詢在 `a_int_value` 和 `b_int_value` 資料行上執行位元 NOT 運算。  
  
```  
SELECT ~ a_int_value, ~ b_int_value  
FROM bitwise;  
```  
  
 以下為結果集：  
  
```  
--- ---   
-171  -76   
  
(1 row(s) affected)  
```  
  
 170 的二進位表示法 (`a_int_value`或`A`) 是`0000 0000 1010 1010`。 對這個值執行位元 NOT 運算，會產生二進位結果 `1111 1111 0101 0101`，也就是十進位的 -171。 75 的二進位表示是 `0000 0000 0100 1011`。 執行位元 NOT 運算會產生 `1111 1111 1011 0100`，也就是十進位的 -76。  
  
```  
 (~A)     
         0000 0000 1010 1010  
         -------------------  
         1111 1111 0101 0101  
(~B)     
         0000 0000 0100 1011  
         -------------------  
         1111 1111 1011 0100  
```  
  
 
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [位元運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  



