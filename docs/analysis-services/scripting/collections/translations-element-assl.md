---
title: "Translations 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Translations Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Translations
helpviewer_keywords:
- Translations element
ms.assetid: 7f6b8ff2-e834-44d3-a176-216203158a8d
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 459308948a39c4a35069b1e2a5a4df40c5fb7bf8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="translations-element-assl"></a>Translations 元素 (ASSL)
  包含集合[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)元素與父元素相關聯。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action><!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Translations>  
      <Translation>...</Translation>  
      <!-- or -->  
      <Translation xsi:type="AttributeTranslation">...</Translation><!-- parent: DimensionAttribute or ScalarMiningStructureColumn -->  
      <!-- or -->  
      <Translation xsi:type="RelationshipEndTranslation">...</Translation><!-- parent: RelationshipEnd -->  
   </Translations>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)， [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)， [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)，[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)，[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[層級](../../../analysis-services/scripting/objects/level-element-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)，[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)， [RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)， [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)， [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|  
|子元素|請參閱下表。|  
  
|上階或父系|子元素|  
|------------------------|-------------------|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)或[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)型別的[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|  
|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|[轉譯](../../../analysis-services/scripting/data-type/relationshipendtranslation-element-assl.md)型別的[RelationshipEndTranslation](../../../analysis-services/scripting/data-type/relationshipendtranslation-element-assl.md)|  
|All others|[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.TranslationCollection> 和 <xref:Microsoft.AnalysisServices.AttributeTranslationCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

