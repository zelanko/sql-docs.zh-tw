---
title: "&amp;(位元 AND)(TRANSACT-SQL) |Microsoft 文件"
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
- bitwise
- '&'
- '&_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 20275755-4fa7-47b1-a9be-ac85606d63b0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 094c127434f2339a4a3e977c4455ca6ce904ab01
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="amp-bitwise-and-transact-sql"></a>&amp;(位元 AND)(TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在兩個整數值之間，執行位元邏輯 AND 運算。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression & expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的任何資料類型的整數資料類型類別目錄，或**元**，或**二進位**或**varbinary**資料型別。 *運算式*會被視為位元運算的二進位數字。  
  
> [!NOTE]  
>  在位元作業中，只有一個*運算式*可以是**二進位**或**varbinary**資料型別。  
  
## <a name="result-types"></a>結果類型  
 **int**如果輸入的值為**int**。  
  
 **smallint**如果輸入的值為**smallint**。  
  
 **tinyint**如果輸入的值為**tinyint**或**元**。  
  
## <a name="remarks"></a>備註  
 **&** 位元運算子會執行兩個運算式，運算式各有一個對應的位元的兩個運算式之間的位元邏輯 AND 運算。 只有在輸入運算式的兩個位元 (針對目前所解析的位元) 的值都是 1 時，結果中的兩個位元才會都設為 1；否則，結果中的位元便設為 0。  
  
 如果左邊和右邊的運算式具有相同的整數資料類型 (例如，左*運算式*是**smallint**和右邊*運算式*是**int**)，較小的資料類型的引數會轉換成較大的資料類型。 在此情況下，**smallint * * * 運算式*轉換成**int**。  
  
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
  
 這個查詢在 `a_int_value` 和 `b_int_value` 資料行之間執行位元 AND 運算。  
  
```  
SELECT a_int_value & b_int_value  
FROM bitwise;  
GO  
```  
  
 以下為結果集：  
  
```  
-----------   
10            
  
(1 row(s) affected)  
```  
  
 170 的二進位表示法 (`a_int_value`或`A`) 是`0000 0000 1010 1010`。 75 (`b_int_value` 或 `B`) 的二進位表示法是 `0000 0000 0100 1011`。 對這兩個值執行位元 AND 運算，會產生二進位結果 `0000 0000 0000 1010`，也就是十進位的 10。  
  
```  
(A & B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 0000 1010  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [位元運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [& = &#40;位元 AND 指派 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


