---
title: "GETUTCDATE (SSIS 運算式) | Microsoft Docs"
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
  - "日期 [Integration Services], GETUTCDATE"
  - "目前日期"
  - "UTC 時間"
  - "GETUTCDATE 函數"
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# GETUTCDATE (SSIS 運算式)
  使用 DT_DBTIMESTAMP 格式，傳回 UTC 時間格式 (世界標準時間或格林威治標準時間) 的系統目前日期。 GETUTCDATE 函數不接受引數。  
  
## 語法  
  
```  
  
GETUTCDATE()  
```  
  
## 引數  
 無  
  
## 結果類型  
 DT_DBTIMESTAMP  
  
## 運算式範例  
 此範例會傳回 UTC 時間格式的目前日期之年份。  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 此範例會傳回 **ModifiedDate** 資料行中的日期與目前 UTC 日期之間的天數。  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 此範例會將目前的 UTC 日期加上三個月。  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## 請參閱＜  
 [GETDATE &#40;SSIS 運算式&#41;](../../integration-services/expressions/getdate-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  