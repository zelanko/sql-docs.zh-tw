---
title: Binding 資料類型 (ASSL) |Microsoft 文件
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
- Binding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- BINDING
helpviewer_keywords:
- Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 24847c70a0baf6ee12c1de6364cdd1e8d4327f91
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135490"
---
# <a name="binding-data-type-assl"></a>Binding 資料類型 (ASSL)
  定義代表兩個物件之間相依關聯性的抽象基本資料類型，其中某個物件的資料或中繼資料相依於繫結物件的資料或中繼資料。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[AttributeBinding](binding-data-type-assl.md), [ColumnBinding](columnbinding-data-type-assl.md), [CubeAttributeBinding](cubeattributebinding-data-type-assl.md), [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), [DimensionBinding](dimensionbinding-data-type-assl.md), [InheritedBinding](inheritedbinding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), [MeasureGroupBinding](measuregroupbinding-data-type-assl.md), [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md), [RowBinding](rowbinding-data-type-assl.md), [TabularBinding](tabularbinding-data-type-assl.md), [TimeAttributeBinding](timeattributebinding-data-type-assl.md), [TimeBinding](timebinding-data-type-assl.md), [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|無|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Binding>。  
  
 如需資料繫結的詳細資訊，請參閱[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="elements-of-type-binding"></a>Binding 類型的元素  
 下表列出 `Binding` 類型的元素。  
  
|父元素|`Binding` 類型的元素|註解|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../properties/source-element-binding-assl.md)的[CaptionColumn](../objects/column-element-assl.md) (型別[DataItem](dataitem-data-type-assl.md))|輸入的`Binding`必須[AttributeBinding](binding-data-type-assl.md)或[ColumnBinding](columnbinding-data-type-assl.md)|  
|[Cube](../objects/cube-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding （行的外）](../objects/group-element-assl.md)|輸入的`Binding`必須[MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[DataItem](dataitem-data-type-assl.md)|[Source](../properties/source-element-binding-assl.md)|`Binding` 可能屬於任何類型|  
|[Dimension](../objects/dimension-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[CubeDimensionBinding](dimensionbinding-data-type-assl.md)， [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)， [DimensionBinding](dimensionbinding-data-type-assl.md)，或[TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](dimensionattribute-data-type-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[AttributeBinding](binding-data-type-assl.md)或[UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](action-data-type-assl.md)|[資料行](../objects/column-element-assl.md)|輸入的`Binding`必須[CubeAttributeBinding](cubeattributebinding-data-type-assl.md)或[MeasureBinding](measurebinding-data-type-assl.md)|  
|[量值](../objects/measure-element-assl.md)|[來源](../properties/source-element-binding-assl.md)(型別[DataItem](dataitem-data-type-assl.md))|輸入的`Binding`必須[ColumnBinding](columnbinding-data-type-assl.md)， [CubeDimensionBinding](dimensionbinding-data-type-assl.md)， [MeasureBinding](measurebinding-data-type-assl.md)，或[RowBinding](rowbinding-data-type-assl.md)|  
|[量值群組](../objects/measuregroup-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[來源](../properties/source-element-binding-assl.md)的[KeyColumn](../objects/keycolumn-element-assl.md) (型別[DataItem](dataitem-data-type-assl.md))|輸入的`Binding`必須[AttributeBinding](binding-data-type-assl.md)或[ColumnBinding](columnbinding-data-type-assl.md)，或[InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding （行的外）](measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../objects/dimension-element-assl.md)|輸入的`Binding`必須[MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding （行的外）](measuregroupbinding-data-type-out-of-line-assl.md)|[量值](../objects/measure-element-assl.md)|輸入的`Binding`必須[MeasureBinding](measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding （行的外）](../objects/partition-element-assl.md)|輸入的`Binding`必須[PartitionBinding](partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding （行的外）](measuregroupbinding-data-type-out-of-line-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[TableBinding](tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](dimension-data-type-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[CubeDimensionBinding](dimensionbinding-data-type-assl.md)， [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)，或[DimensionBinding](dimensionbinding-data-type-assl.md)|  
|[資料分割](../objects/partition-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[TabularBinding](tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[Source](../properties/source-element-binding-assl.md)|輸入的`Binding`必須[AttributeBinding](binding-data-type-assl.md)， [CubeAttributeBinding 資料類型&#40;ASSL&#41;](cubeattributebinding-data-type-assl.md)，或[MeasureBinding 資料類型&#40;ASSL&#41;](measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/sourcemeasuregroup-element-assl.md)|輸入的`Binding`必須[MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  