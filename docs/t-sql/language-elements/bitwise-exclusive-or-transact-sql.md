---
title: "^ (位元互斥 OR) (TRANSACT-SQL) |Microsoft 文件"
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
- ^_TSQL
- Bitwise Exclusive OR
- Exclusive
- ^
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- OR operator
- exclusive OR mathematical operations
- bitwise exclusive OR (^)
ms.assetid: f38f0ad4-46d0-40ea-9851-0f928fda5293
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 635cdf87939b15fad65ba4cc103166bff2ba04d2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="-bitwise-exclusive-or-transact-sql"></a>^ (位元互斥 OR) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在兩個整數值之間，執行位元互斥 OR 運算。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression ^ expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)其中任何一個資料類型的整數資料類型類別目錄，或**元**，或**二進位**或**varbinary**資料型別。 *運算式*會被視為位元運算的二進位數字。  
  
> [!NOTE]  
>  只有一個*運算式*可以是**二進位**或**varbinary**位元運算中的資料類型。  
  
## <a name="result-types"></a>結果類型  
 **int**如果輸入的值為**int**。  
  
 **smallint**如果輸入的值為**smallint**。  
  
 **tinyint**如果輸入的值為**tinyint**。  
  
## <a name="remarks"></a>備註  
  **^** 位元運算子會執行位元邏輯互斥 OR 兩個運算式，運算式各有一個對應的位元的兩個運算式之間。 如果輸入運算式的其中一個位元 (針對目前所解析的位元) 的值是 1 (兩個位元值不能同時是 1)，結果中的兩個位元都會設為 1。 如果兩個位元同時是 0 或同時是 1，便會清除結果中的位元而成為 0 值。  
  
 如果左邊和右邊的運算式具有相同的整數資料類型 (例如，左*運算式*是**smallint**和右邊*運算式*是**int**)，較小的資料類型的引數會轉換成較大的資料類型。 在此情況下， **smallint***運算式*轉換成**int**。  
  
## <a name="examples"></a>範例  
 下列範例會建立資料表，使用**int**資料類型來儲存原始值，而且兩個值插入單一資料列。  
  
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
  
 下列查詢在 `a_int_value` 和 `b_int_value` 資料行上執行位元互斥 OR 運算。  
  
```  
SELECT a_int_value ^ b_int_value  
FROM bitwise;  
GO  
```  
  
 以下為結果集：  
  
```  
-----------   
225           
  
(1 row(s) affected)  
```  
  
 170 的二進位表示法 (`a_int_value`或`A`) 是`0000 0000 1010 1010`。 75 (`b_int_value` 或 `B`) 的二進位表示法是 `0000 0000 0100 1011`。 對這兩個值執行位元互斥 OR 運算，會產生二進位結果 `0000 0000 1110 0001`，也就是十進位的 225。  
  
```  
(A ^ B)     
         0000 0000 1010 1010  
         0000 0000 0100 1011  
         -------------------  
         0000 0000 1110 0001  
```  
  

  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [位元運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [^ = &#40;位元互斥 OR EQUALS &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)   
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



