---
title: "Configuration 元素 (DTA) | Microsoft Docs"
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
  - "Configuration 元素"
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# Configuration 元素 (DTA)
  指定由現有的實體設計結構和假設的實體設計結構所組成，供 Database Engine Tuning Advisor 在微調工作負載時進行分析的使用者指定組態。  
  
## 語法  
  
```  
  
<DTAInput>  
    <Server>...</Server>  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions  
    <Configuration [SpecificationMode="Relative" | "Absolute"]>  
    ...code removed here...  
    </Configuration>  
</DTAInput>  
```  
  
## 元素屬性  
  
|組態屬性|描述|  
|-----------------------------|-----------------|  
|**SpecificationMode**|選擇性。 指定 Database Engine Tuning Advisor 應該關聯於目前現有的組態來分析指定的組態，或將它當作全新的獨立組態來進行分析。 請利用 **string** 資料類型和下列其中一個允許的值，來指定這個屬性：<br /><br /> **Relative**：<br />                  關聯於正在微調的資料庫其中之實體設計結構 (索引、索引檢視、資料分割) 目前現有的組態來評估指定的組態。 例如：<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**：<br />                  將指定的組態當作獨立組態來評估。 當指定 Absolute 時，Database Engine Tuning Advisor 不會考慮現有的組態。 例如：<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## 元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 每個 **DTAInput** 元素可以使用這個元素一次。|  
  
## 元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**子元素**|[組態的 Server 元素 &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## 範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## 另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  