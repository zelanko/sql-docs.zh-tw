---
title: "DatabaseToConnect 元素 (DTA) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "DatabaseToConnect 元素"
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# DatabaseToConnect 元素 (DTA)
  指定微調工作負載時，Database Engine Tuning Advisor 所連接的第一個資料庫。  
  
## 語法  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## 元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|**string**，沒有長度限制。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 每個 **TuningOptions** 元素可以使用這個元素一次。|  
  
## 元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[TuningOptions 元素 &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**子元素**|無|  
  
## 備註  
 請利用 **DatabaseToConnect** 來指定 Database Engine Tuning Advisor 開始微調工作階段時，所要連接的第一個資料庫的名稱。 您只能利用這個元素來指定一個資料庫。 如果指定了多個資料庫名稱，Database Engine Tuning Advisor 就會傳回錯誤。  
  
## 範例  
 如需使用範例，請參閱[含內嵌工作負載的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md)。  
  
## 另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  