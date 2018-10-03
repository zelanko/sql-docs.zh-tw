---
title: Translations 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Translations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Translations
helpviewer_keywords:
- Translations element
ms.assetid: 7f6b8ff2-e834-44d3-a176-216203158a8d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7ea3c98e2263b78f947d75c5b225d2a3a63ef40
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061228"
---
# <a name="translations-element-assl"></a>Translations 元素 (ASSL)
  包含的集合[翻譯](../objects/translation-element-assl.md)元素與父元素相關聯。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)， [AttributeRelationship](../objects/attributerelationship-element-assl.md)， [CalculationProperty](../objects/calculationproperty-element-assl.md)， [Cube](../objects/cube-element-assl.md)， [CubeDimension](../data-type/dimension-data-type-assl.md)， [資料庫](../objects/database-element-assl.md)，[維度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)，[階層](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)， [層級](../objects/level-element-assl.md)，[量值](../objects/measure-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [觀點來看](../objects/perspective-element-assl.md)， [RelationshipEnd](../data-type/relationshipend-data-type-assl.md)， [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)， [TableMiningStructureColumn](../data-type/tableminingstructurecolumn-data-type-assl.md)|  
  
 **項目子系**  
  
|上階或父系|子元素|  
|------------------------|-------------------|  
|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)或[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[翻譯](../objects/translation-element-assl.md)型別的[AttributeTranslation](../data-type/translation-data-type-assl.md)|  
|[RelationshipEnd](../data-type/relationshipendtranslation-element-assl.md)型別的[RelationshipEndTranslation](../data-type/relationshipendtranslation-element-assl.md)|  
|All others|[轉譯](../objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.TranslationCollection> 和 <xref:Microsoft.AnalysisServices.AttributeTranslationCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
