---
title: "SIGN (SSIS 運算式) | Microsoft Docs"
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
  - "正值 [Integration Services]"
  - "SIGN 函數"
  - "負值"
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# SIGN (SSIS 運算式)
  傳回數值運算式的正 (+1)、負 (-1) 或零 (0) 符號。  
  
## 語法  
  
```  
  
SIGN(numeric_expression)  
```  
  
## 引數  
 *numeric_expression*  
 是帶正負號的有效數值運算式。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## 結果類型  
 DT_I4  
  
## 備註  
 如果引數為 Null，則 SIGN 會傳回 Null 結果。  
  
## 運算式範例  
 此範例會傳回數值常值的正負號。 傳回結果為 -1。  
  
```  
SIGN(-123.45)  
```  
  
 此範例會傳回從 **DealerPrice** 資料行減去 **StandardCost** 資料行之結果的正負號。  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## 請參閱＜  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  