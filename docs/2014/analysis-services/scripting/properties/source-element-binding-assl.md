---
title: Source 元素 (Binding) (ASSL) |Microsoft 文件
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
- Source Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 1032558c-7546-4ca7-888d-8139df23cb62
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 58bacab7c84d1432a57d16c709b08c8c79ac143d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135694"
---
# <a name="source-element-binding-assl"></a>Source 元素 (Binding) (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|請參閱資料類型表|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
 **資料類型和長度**  
  
|||  
|-|-|  
|上階或父系|資料類型|  
|[AggregationInstance](../data-type/binding-data-type-assl.md)|  
|[AggregationInstanceMeasure](../data-type/columnbinding-data-type-assl.md)|  
|[Cube](../data-type/datasourceviewbinding-data-type-assl.md)|  
|[DataItem](../data-type/dataitem-data-type-assl.md)|從衍生的資料類型[繫結](../data-type/binding-data-type-assl.md)，端視父代`DataItem`。 如需詳細資訊，請參閱＜備註＞。|  
|[維度](../data-type/dimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)， [TimeBinding](../data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../data-type/attributebinding-data-type-assl.md)， [UserDefinedGroupBinding](../data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[量值群組](../data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupDimension](../data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[CubeDimensionBinding](../data-type/cubedimensionbinding-data-type-assl.md)， [DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md)， [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)|  
|[資料分割](../data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|從衍生的資料類型[ProactiveCachingBinding](../data-type/proactivecachingbinding-data-type-assl.md)，視使用的父代的處理和通知選項`ProactiveCaching`項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationInstance](../objects/aggregationinstance-element-assl.md)， [AggregationInstanceMeasure](../data-type/aggregationinstancemeasure-data-type-assl.md)， [Cube](../objects/cube-element-assl.md)， [DataItem](../data-type/dataitem-data-type-assl.md)，[維度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [MeasureGroup](../objects/group-element-assl.md)， [MeasureGroupDimension](../data-type/dimension-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)，[磁碟分割](../objects/partition-element-assl.md)， [ProactiveCaching](../objects/proactivecaching-element-assl.md)。|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在 `Source` 元素中，允許用於 `Binding` 元素的衍生 `DataItem` 資料類型會因 `DataItem` 元素的父系而不同。  
  
|DataItem 父系|允許的資料類型|  
|---------------------|------------------------|  
|[DimensionAttribute](../data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../data-type/columnbinding-data-type-assl.md)， [TimeAttributeBinding](../data-type/timeattributebinding-data-type-assl.md) (僅適用於[KeyColumns](../collections/columns-element-assl.md))。|  
|[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)|[AttributeBinding](../data-type/attributebinding-data-type-assl.md)， [ColumnBinding](../data-type/columnbinding-data-type-assl.md)， [InheritedBinding](../data-type/inheritedbinding-data-type-assl.md)。|  
|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[ColumnBinding](../data-type/columnbinding-data-type-assl.md)|  
  
 如需有關`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層架構的`Binding`類型，請參閱[繫結資料型別&#40;ASSL&#41;](../data-type/binding-data-type-assl.md).  
  
 如需有關 ASSL 中資料繫結的詳細資訊，請參閱[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  