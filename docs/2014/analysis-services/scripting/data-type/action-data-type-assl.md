---
title: Action 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Action Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 21c13562fa53c0ba396a4c3826889e8d275f7d9a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197488"
---
# <a name="action-data-type-assl"></a>Action 資料類型 (ASSL)
  定義表示中的動作的抽象基本資料類型[Cube](../objects/cube-element-assl.md)項目或有[觀點來看](../objects/perspective-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Caption>...</Caption>  
      <CaptionIsMdx>...</CaptionIsMdx>  
      <Translations>...</Translations>  
   <TargetType>...</TargetType>  
   <Target>...</Target>  
   <Condition>...</Condition>  
   <Type>...</Type>  
   <Invocation>...</Invocation>  
   <Application>...</Application>  
      <Description>...</Description>  
      <Annotations>...</Annotations>  
</Action>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|None|  
|衍生資料類型|[DrillThroughAction](action-data-type-assl.md)， [ReportAction](reportaction-data-type-assl.md)， [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../collections/actions-element-assl.md)|  
|子元素|[註釋](../collections/annotations-element-assl.md)，[應用程式](../properties/application-element-assl.md)，[標題](../properties/caption-element-assl.md)， [CaptionIsMdx](../properties/captionismdx-element-assl.md)，[條件](../properties/condition-element-assl.md)，[描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)，[引動過程](../properties/invocation-element-assl.md)，[名稱](../properties/name-element-assl.md)，[目標](../properties/target-element-assl.md)， [TargetType](../properties/targettype-element-assl.md)，[翻譯](../collections/translations-element-assl.md)，[類型](../properties/type-element-action-assl.md)|  
|衍生的元素|[DrillThroughAction](action-data-type-assl.md)， [ReportAction](reportaction-data-type-assl.md)， [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需動作的詳細資訊，請參閱[動作 &#40;Analysis Services - 多維度資料&#41;](../../multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素&#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Perspective 元素&#40;ASSL&#41;](../objects/perspective-element-assl.md)   
 [PerspectiveAction 資料類型&#40;ASSL&#41;](perspectiveaction-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
