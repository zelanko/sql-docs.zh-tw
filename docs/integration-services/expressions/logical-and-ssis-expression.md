---
title: "&amp;&amp; (邏輯 AND) (SSIS 運算式) | Microsoft Docs"
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
  - "&& (邏輯 AND)"
  - "AND, 邏輯 AND"
  - "邏輯 AND (&&)"
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# &amp;&amp; (邏輯 AND) (SSIS 運算式)
  執行邏輯 AND 運算。 如果所有條件均為 TRUE，則運算式的評估結果為 TRUE。  
  
## 語法  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## 引數  
 *boolean _expression1、boolean_expression2*  
 評估為 TRUE、FALSE 或 NULL 的任何有效運算式。  
  
## 結果類型  
 DT_BOOL  
  
## 備註  
 下表顯示 && 運算子的結果。  
  
|結果|運算式|運算式|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## 運算式範例  
 此範例使用 **StandardCost** 和 **ListPrice** 資料行。 如果 **StandardCost** 資料行的值小於 300，且 **ListPrice** 資料行的值大於 500，則範例的評估結果為 TRUE。  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 此範例使用 **SPrice** 和 **LPrice** 變數，而非常值。  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## 請參閱＜  
 [& &#40;位元 AND&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)   
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  