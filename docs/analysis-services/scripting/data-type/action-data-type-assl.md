---
title: "Action 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
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
apiname:
- Action Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6dc68139ddfbce5151cb3750aaca1ffd54d37041
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="action-data-type-assl"></a>Action 資料類型 (ASSL)
  定義表示中的動作的抽象基本資料類型[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)， [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)， [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/collections/actions-element-assl.md)|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[應用程式](../../../analysis-services/scripting/properties/application-element-assl.md)，[標題](../../../analysis-services/scripting/properties/caption-element-assl.md)， [CaptionIsMdx](../../../analysis-services/scripting/properties/captionismdx-element-assl.md)，[條件](../../../analysis-services/scripting/properties/condition-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)，[引動過程](../../../analysis-services/scripting/properties/invocation-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[目標](../../../analysis-services/scripting/properties/target-element-assl.md)， [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)，[類型](../../../analysis-services/scripting/properties/type-element-action-assl.md)|  
|衍生的元素|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)， [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)， [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需動作的詳細資訊，請參閱[動作 &#40;Analysis Services - 多維度資料&#41;](../../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Perspective 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)   
 [PerspectiveAction 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

