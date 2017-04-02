---
title: "~ (位元 Not) (SSIS 運算式) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "位元運算 NOT (~)"
  - "~ (位元運算 NOT)"
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# ~ (位元 Not) (SSIS 運算式)
  執行整數的位元否定運算。 此運算子可套用至帶正負號及不帶正負號的整數資料類型。  
  
## 語法  
  
```  
  
~integer_expression  
  
```  
  
## 引數  
 *integer_expression*  
 是任何整數資料類型的有效運算式。 *integer*_*expression* 是整數，會轉換成二進位數字以進行位元運算。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## 結果類型  
 傳回 *integer_expression* 的資料類型。  
  
## 備註  
 無  
  
## 運算式範例  
 此範例會在數字 170 (0000 0000 1010 1010) 上執行位元 ~ (NOT) 運算。 此數字為帶正負號的整數。  
  
```  
  
~ 170  
```  
  
 運算式評估結果為 -170 (1111111101010101)。  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## 請參閱＜  
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  