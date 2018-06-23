---
title: RelationshipEndTranslation 元素 (ASSL) |Microsoft 文件
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
ms.assetid: 04e09370-fdfe-4051-9998-4a6859ce8c54
caps.latest.revision: 4
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bb93b3cdaf3eda1b8be15679b0736e626a802cf3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031120"
---
# <a name="relationshipendtranslation-element-assl"></a>RelationshipEndTranslation 元素 (ASSL)
  定義代表當地語系化的翻譯的基本資料類型[RelationshipEnd](relationshipend-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationshipEndTranslation>  
   <Language>...</Language>  
   <Caption>...</Caption>  
   <CollectionCaption>...</Caption>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Annotations>...</Annotations>  
</RelationshipEndTranslation>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[AttributeTranslation](translation-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[翻譯](../collections/translations-element-assl.md)|  
|子元素|[註解](../collections/annotations-element-assl.md)，[標題](../properties/caption-element-assl.md)， [CollectionCaption](../properties/caption-element-assl.md)，[描述](../properties/description-element-assl.md)， [DisplayFolder](../properties/displayfolder-element-assl.md)， [語言](../properties/language-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  