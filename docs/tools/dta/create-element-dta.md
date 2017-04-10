---
title: "Create 元素 (DTA) | Microsoft Docs"
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
  - "Create 元素 (DTA)"
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Create 元素 (DTA)
  包含使用者指定組態中之索引、統計資料或堆積結構的相關資訊。  
  
## 語法  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## 元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個實體設計結構類型 (索引、統計資料或堆積結構) 都需要使用這個元素一次。|  
  
## 元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Recommendation 元素 &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)|  
|**子元素**|[Index 元素 &#40;DTA&#41;](../../tools/dta/index-element-dta.md)<br /><br /> **Statistics** 元素 (如需相關資訊，請參閱 [Database Engine Tuning Advisor XML schema](http://schemas.microsoft.com/sqlserver/) (Database Engine Tuning Advisor XML 結構描述))<br /><br /> **Heap** 元素 (如需相關資訊，請參閱 [Database Engine Tuning Advisor XML schema](http://schemas.microsoft.com/sqlserver/) (Database Engine Tuning Advisor XML 結構描述))|  
  
## 備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **CreateTypecomplexType**。 它用來建立使用者指定組態的索引、統計資料和堆積結構。 請勿混淆這個 **Create** 元素與可用來建立檢視 (**CreateViewType**) 或資料分割 (**CreatePType**) 的其他類型。 如需其他 **Create** 元素類型的資訊，請參閱 [Database Engine Tuning Advisor XML schema](http://schemas.microsoft.com/sqlserver/) (Database Engine Tuning Advisor XML 結構描述)。  
  
## 範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## 另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  