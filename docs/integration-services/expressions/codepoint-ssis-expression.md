---
title: "CODEPOINT (SSIS 運算式) | Microsoft Docs"
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
  - "CODEPOINT 函數"
  - "運算式的最左邊字元"
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# CODEPOINT (SSIS 運算式)
  傳回字元運算式最左邊字元的 Unicode 字碼指標。  
  
## 語法  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## 引數  
 *character_expression*  
 是將要評估最左邊字元的字元運算式。  
  
## 結果類型  
 DT_UI2  
  
## 備註  
 *character_expression* 引數必須是 DT_WSTR 資料類型。  
  
 如果 *character_expression* 為 Null 或空字串，則 CODEPOINT 會傳回 Null 結果。  
  
## 運算式範例  
 這個範例使用字串常值。 傳回結果為 77，即 M 的 Unicode 字碼指標。  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 這個範例使用變數。 如果 **Name** 是 Touring Front Wheel，則傳回結果為 84，即 T 的 Unicode 字碼指標。  
  
```  
CODEPOINT(@Name)  
```  
  
## 請參閱＜  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  