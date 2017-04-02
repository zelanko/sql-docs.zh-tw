---
title: "FLOOR (SSIS 運算式) | Microsoft Docs"
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
  - "小於或等於運算式的最大整數"
  - "FLOOR 函數 [SSIS]"
ms.assetid: 168084db-badd-40f2-87b4-1f5bc45c3e24
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# FLOOR (SSIS 運算式)
  傳回小於或等於數值運算式的最大整數。  
  
## 語法  
  
```  
  
FLOOR(numeric_expression)  
```  
  
## 引數  
 *numeric_expression*  
 有效的數值運算式。  
  
## 結果類型  
 引數運算式的數值資料類型。 結果是計算值的整數部分，與 *numeric_expression* 具有相同的資料類型。  
  
## 備註  
 如果引數為 Null，則 FLOOR 會傳回 Null 結果。  
  
## 運算式範例  
 這些範例會將 FLOOR 函數套用至正值、負值和零值。  
  
```  
FLOOR(123.45)  
```  
  
 傳回 123.00  
  
```  
FLOOR(-123.45)  
```  
  
 傳回 -124.00  
  
```  
FLOOR(0.00)  
```  
  
 傳回 0.00  
  
## 請參閱＜  
 [CEILING &#40;SSIS 運算式&#41;](../../integration-services/expressions/ceiling-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  