---
title: "Recommendation 元素 (DTA) | Microsoft Docs"
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
  - "Recommendation 元素"
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Recommendation 元素 (DTA)
  包含屬於使用者指定組態之一部份的假設性索引的相關資訊。  
  
## 語法  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## 元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|選擇性。 每個 **Table** 元素可以使用這個元素一次。|  
  
## 元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[結構描述的 Table 元素 &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)|  
|**子元素**|[Create 元素 &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> **Drop** 元素。 如需詳細資訊，請參閱＜ [Database Engine Tuning Advisor XML 結構描述](http://go.microsoft.com/fwlink/?linkid=43100)＞。|  
  
## 備註  
 在 Database Engine Tuning Advisor XML 結構描述中，這個元素的名稱為 **RecommendationTypecomplexType**。 它用來指定假設性組態的索引。 請勿混淆這個 **Recommendation** 元素與可用來指定資料分割 (**RecommendationPType**) 或檢視 (**RecommendationViewType**) 的其他類型。 如需其他 **Recommendation** 元素類型的相關資訊，請參閱 [Database Engine Tuning Advisor XML Schema](http://go.microsoft.com/fwlink/?linkid=43100) (Database Engine Tuning Advisor XML 結構描述)。  
  
## 範例  
 如需此元素的使用範例，請參閱[含使用者指定組態的 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## 另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  