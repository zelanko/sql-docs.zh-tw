---
title: NamingTemplateTranslation 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dc6c6689f4028c0983267a38435c76e7258768a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132962"
---
# <a name="namingtemplatetranslation-element-assl"></a>NamingTemplateTranslation 元素 (ASSL)
  提供當地語系化的翻譯的[NamingTemplate](../properties/namingtemplate-element-assl.md)父項目[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)資料型別。  
  
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
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[NamingTemplateTranslations](../collections/translations-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值`NamingTemplateTranslation`項目僅供父屬性 (換言之，值的[使用量](../properties/usage-element-dimensionattribute-assl.md)的項目`DimensionAttribute`父代設定為*父*) 來儲存當地語系化轉譯`NamingTemplate`給定語言的值。  
  
 對應目的父代的項目`NamingTemplateTranslations`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [NamingTemplate 元素&#40;ASSL&#41;](../properties/namingtemplate-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  