---
title: CubeDimension 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7fd3894b7b1d255a8760da4822eff0de1315b72
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="cubedimension-data-type-assl"></a>CubeDimension 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表維度與 Cube 之間關聯性的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimension>  
      <ID>...</ID>  
   <Name>...</Name>  
   <Translations>...</Translations>  
   <DimensionID>...</DimensionID>  
   <Visible>...</Visible>  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
      <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotation>  
</CubeDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AllMemberAggregationUsage](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[屬性](../../../analysis-services/scripting/collections/attributes-element-assl.md)， [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md)，[階層](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)， [HierarchyUniqueNameStyle](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)， [MemberUniqueNameStyle](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[可見](../../../analysis-services/scripting/properties/visible-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|衍生的元素|[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)([維度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)集合[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 有一個**CubeDimension**每個維度關聯性上**Cube**。 **CubeDimension**涵蓋所有**MeasureGroups**的 cube。  
  
 A **CubeDimension**必須包含[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)如果維度與階層的特定項目，包括停用階層 （因而，允許的選取範圍階層要套用至特定維度使用方式），或變成不可見的階層。  
  
 同樣地， **CubeDimension**必須包含[CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md)前提維度與屬性特定項目。 (沒有任何方法可選取要套用至特定維度使用方式的屬性，不過您可以讓屬性隱藏)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubeDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
