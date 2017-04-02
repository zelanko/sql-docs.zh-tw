---
title: "HEX (SSIS 運算式) | Microsoft Docs"
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
  - "十六進位資料"
  - "HEX 函數"
ms.assetid: f5d471ee-aeef-421c-b6e1-55b9676c3842
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# HEX (SSIS 運算式)
  傳回代表整數的十六進位值的字串。  
  
## 語法  
  
```  
  
HEX(integer_expression)  
```  
  
## 引數  
 *integer_expression*  
 是帶正負號或不帶正負號的整數。  
  
## 結果類型  
 DT_WSTR  
  
## 備註  
 如果 *integer_expression* 是 Null，則 HEX 會傳回 Null。  
  
 *integer_expression* 引數必須評估為整數。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
 傳回結果不包含限定詞，例如 0x 前置詞。 若要包含前置詞，請使用 + (串連) 運算子。 如需詳細資訊，請參閱 [+ &#40;串連&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/concatenate-ssis-expression.md)。  
  
 HEX 標記法中使用的字母 A – F 會以大寫字元顯示。  
  
 整數資料類型的結果字串長度如下：  
  
-   DT_I1 和 DT_UI1 傳回最大長度為 2 的字串。  
  
-   DT_I2 和 DT_UI2 傳回最大長度為 4 的字串。  
  
-   DT_I4 和 DT_UI4 傳回最大長度為 8 的字串。  
  
-   DT_I8 和 DT_UI8 傳回最大長度為 16 的字串。  
  
## 運算式範例  
 這個範例使用數值常值。 函數傳回值 190。  
  
```  
HEX(400)   
```  
  
 此範例使用 **ReorderPoint** 資料行。 資料行資料類型為 **smallint**。 如果 **ReorderPoint** 是 750，則函數會傳回 2EE。  
  
```  
HEX(ReorderPoint)   
```  
  
 此範例使用系統變數 **LocaleID**。 如果 **LocaleID** 是 1033，則函數會傳回 409。  
  
```  
HEX(@LocaleID)  
```  
  
## 請參閱＜  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  