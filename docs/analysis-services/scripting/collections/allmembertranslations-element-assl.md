---
title: "AllMemberTranslations 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AllMemberTranslations Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AllMemberTranslations
helpviewer_keywords: AllMemberTranslations element
ms.assetid: 982ee2bf-c88d-4da5-a679-7a6b08a48a0d
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 63eb22e9012da8043a57956bada680f0c30dfbf7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="allmembertranslations-element-assl"></a>AllMemberTranslations 元素 (ASSL)
  包含集合[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)元素之 All 成員標題[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Hierarchy>  
   ...  
   <AllMemberTranslations>  
      <AllMemberTranslation xsi:type="Translation">...  
            </AllMemberTranslation>  
   </AllMemberTranslations>  
      ...  
</Hierarchy>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無 (集合)|  
|預設值|無 (集合)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
|子元素|[AllMemberTranslation](../../../analysis-services/scripting/objects/allmembertranslation-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**AllMemberTranslations**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Hierarchy>。  
  
## <a name="see-also"></a>請參閱＜  
 [Translation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)   
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
