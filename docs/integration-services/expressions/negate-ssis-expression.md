---
title: "- (負) (SSIS 運算式) | Microsoft Docs"
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
  - "- (負)"
  - "負運算子 (-)"
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# - (負) (SSIS 運算式)
  執行數值運算式的否定運算。  
  
## 語法  
  
```  
  
-numeric_expression  
  
```  
  
## 引數  
 *numeric_expression*  
 是任何數值資料類型的任何有效運算式。 只支援帶正負號的數值資料類型。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## 結果類型  
 傳回 *numeric_expression* 的資料類型。  
  
## 運算式範例  
 此範例會執行 **Counter** 變數值的否定運算並與數值常值 50 相加。  
  
```  
-@Counter + 50  
```  
  
## 請參閱＜  
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  