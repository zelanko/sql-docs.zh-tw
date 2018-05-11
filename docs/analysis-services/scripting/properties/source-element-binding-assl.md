---
title: Source 元素 (Binding) (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 078f4d9f9e1b7ab1229b754a9d110e172d7c3133
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="source-element-binding-assl"></a>Source 元素 (Binding) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  識別父元素所繫結的資料來源。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationInstance> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Source>...</Source>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|請參閱下表。|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[AggregationInstanceMeasure](../../../analysis-services/scripting/data-type/aggregationinstancemeasure-data-type-assl.md)|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|從衍生的資料類型[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)，端視父代**DataItem**。 如需詳細資訊，請參閱＜備註＞。|  
|[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)， [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[量值群組](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|[MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|[CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|  
|[資料分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|從衍生的資料類型[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)，視使用的父代的處理和通知選項**ProactiveCaching**項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)， [AggregationInstanceMeasure](../../../analysis-services/scripting/data-type/aggregationinstancemeasure-data-type-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)， [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)，[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)， [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)。|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在**來源**元素中，衍生**繫結**中允許的資料型別**DataItem**項目而定的父代**DataItem**項目。  
  
|DataItem 父系|允許的資料類型|  
|---------------------|------------------------|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [TimeAttributeBinding](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md) (僅適用於[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md))。|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)。|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
  
 如需有關**繫結**型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表**繫結**型別和繼承階層架構的**繫結**類型，請參閱[繫結資料型別&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)。  
  
 如需有關 ASSL 中資料繫結的詳細資訊，請參閱[資料來源和繫結 & #40;SSAS 多維度 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
