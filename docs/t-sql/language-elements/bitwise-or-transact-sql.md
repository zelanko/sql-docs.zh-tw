---
title: "|(位元 OR)(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '|'
- '|_TSQL'
- Bitwise OR
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator
- bitwise OR (|)
- '| (bitwise OR operator)'
ms.assetid: 86a3b87f-9688-4eaf-a552-29f1b01d880a
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 932b8cc8997a2faec55e56786a80e511fa9c273a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="-bitwise-or-transact-sql"></a>| (位元 OR) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  當在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式內轉換成二進位運算式時，執行兩個指定整數值之間的位元邏輯 OR 運算。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```   
expression | expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)整數資料類型類別目錄，或**元**，**二進位**，或**varbinary**資料型別。 *運算式*會被視為位元運算的二進位數字。  
  
> [!NOTE]  
>  只有一個*運算式*可以是**二進位**或**varbinary**位元運算中的資料類型。  
  
## <a name="result-types"></a>結果類型  
 傳回**int**如果輸入的值為**int**、 **smallint**如果輸入的值為**smallint**，或**tinyint**如果輸入的值為**tinyint**。  
  
## <a name="remarks"></a>備註  
 位元 | 運算子會在兩個運算式之間執行位元邏輯 OR 運算，兩個運算式各有一個對應的位元。 如果輸入運算式的兩個位元或其中一個位元 (針對目前所解析的位元) 的值是 1，結果中的位元都會設為 1；如果輸入運算式中的兩個位元都不是 1，結果中的位元便設為 0。  
  
 如果左邊和右邊的運算式具有相同的整數資料類型 (例如，左*運算式*是**smallint**和右邊*運算式*是**int**)，較小的資料類型的引數會轉換成較大的資料類型。 在此範例中， **smallint***運算式*轉換成**int**。  
  
## <a name="examples"></a>範例  
 下列範例會建立具有資料表**int**資料類型，以顯示原始值，並將資料表放入一個資料列。  
  
```tsql  
CREATE TABLE bitwise  
(   
 a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 下列查詢上執行位元 OR 運算**a_int_value**和**b_int_value**資料行。  
  
```  
SELECT a_int_value | b_int_value  
FROM bitwise;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
235           
  
(1 row(s) affected)  
```  
  
 170 的二進位表示法 (**a_int_value**或`A`底下) 是`0000 0000 1010 1010`。 75 的二進位表示法 (**b_int_value**或`B`底下) 是`0000 0000 0100 1011`。 對這兩個值執行位元 OR 運算，會產生二進位結果 `0000 0000 1110 1011`，也就是十進位的 235。  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [位元運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124; = &#40;位元 OR EQUALS &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



