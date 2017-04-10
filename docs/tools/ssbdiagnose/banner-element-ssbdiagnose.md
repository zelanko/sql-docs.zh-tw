---
title: "Banner 元素 (ssbdiagnose) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "banner 元素"
  - "XML 輸出檔格式 [ssbdiagnose], 橫幅元素"
  - "ssbdiagnose"
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Banner 元素 (ssbdiagnose)
  識別產生 **ssbdiagnose** 輸出 XML 檔的公用程式。  
  
## 語法  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## 元素屬性  
  
|Attribute|描述|  
|---------------|-----------------|  
|**title**|識別產生 **ssbdiagnose** XML 輸出檔的公用程式。|  
|**product**|識別產生 **ssbdiagnose** XML 輸出檔的產品。|  
|**version**|識別產生 XML 輸出檔的公用程式版本。|  
  
## 元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 **ssbdiagnose** 輸出 XML 檔各出現一次。|  
  
## 元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DiagnosticInformation 元素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**子元素**|無。|  
  
## 範例  
 這是 banner 元素的範例。  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## 另請參閱  
 [ssbdiagnose 公用程式 &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  