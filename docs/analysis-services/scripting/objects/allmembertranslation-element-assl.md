---
title: "AllMemberTranslation 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AllMemberTranslation Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AllMemberTranslation
helpviewer_keywords: AllMemberTranslation element
ms.assetid: 31ec0c44-8f1d-457c-9e8b-61dd5bc468f7
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a4b77445df79e358a635365f40bf0497673fd935
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="allmembertranslation-element-assl"></a>AllMemberTranslation 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含之 All 成員標題的翻譯[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AllMemberTranslations>  
   <AllMemberTranslation xsi:type="Translation">...  
   </AllMemberTranslation>  
</AllMemberTranslations>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AllMemberTranslations](../../../analysis-services/scripting/collections/allmembertranslations-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**AllMemberTranslations**分析管理物件 (AMO) 物件模型中的集合是<xref:Microsoft.AnalysisServices.Hierarchy>。  
  
## <a name="see-also"></a>請參閱  
 [Translation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/translation-element-assl.md)   
 [Hierarchy 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
