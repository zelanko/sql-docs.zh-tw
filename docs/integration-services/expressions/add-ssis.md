---
title: "+ (加) (SSIS) | Microsoft Docs"
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
  - "+ (加)"
  - "加運算子 (+)"
  - "加入運算式"
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# + (加) (SSIS)
  加入兩個數值運算式。  
  
## 語法  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## 引數  
 *numeric_expression1、numeric_ expression2*  
 任何有效的數值資料類型運算式。  
  
## 結果類型  
 由兩個引數的資料類型決定。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## 備註  
 如果任一個運算元為 Null，則結果為 Null。  
  
## 運算式範例  
 此範例會加上數值常值。  
  
```  
5 + 6.09 + 7.0  
```  
  
 此範例會將 **VacationHours** 和 **SickLeaveHours** 資料行中的值相加。  
  
```  
VacationHours + SickLeaveHours  
```  
  
 此範例會將計算出的值加入至 **StandardCost** 資料行。 **Profit%** 變數必須加上方括號，因為名稱包含 % 字元。 如需詳細資訊，請參閱[識別碼 &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)。  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## 請參閱＜  
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  