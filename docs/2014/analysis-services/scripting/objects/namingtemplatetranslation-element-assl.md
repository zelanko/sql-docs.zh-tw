---
title: NamingTemplateTranslation 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NamingTemplateTranslation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplateTranslation
helpviewer_keywords:
- NamingTemplateTranslation element
ms.assetid: 4a97a31d-23bc-4afd-a4dc-bc0ad7121f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7689c1b2d83abb7673253550e133cd0fa0ea5e20
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086251"
---
# <a name="namingtemplatetranslation-element-assl"></a>NamingTemplateTranslation 元素 (ASSL)
  提供的當地語系化的翻譯[NamingTemplate](../properties/namingtemplate-element-assl.md)父元素[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)資料型別。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<NamingTemplateTranslations>  
   <NamingTemplateTranslation xsi:type="Translation">...</NamingTemplateTranslation>  
</NamingTemplateTranslations>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[轉譯](translation-element-assl.md)|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[NamingTemplateTranslations](../collections/translations-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 值`NamingTemplateTranslation`項目僅供父屬性 (亦即的值[使用量](../properties/usage-element-dimensionattribute-assl.md)項目`DimensionAttribute`父代設定為*父*) 來儲存當地語系化轉譯`NamingTemplate`給定語言的值。  
  
 對應至父系的元素`NamingTemplateTranslations`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [NamingTemplate 元素&#40;ASSL&#41;](../properties/namingtemplate-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
