---
title: 屬性元素 (ASSL) |Microsoft 文件
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
- Attributes Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Attributes
helpviewer_keywords:
- Attributes element
ms.assetid: d6b545e6-1521-496f-a731-f2c2c44118e4
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2e3dda6122030b789f9cccbf9f300a0a41a37ec5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135484"
---
# <a name="attributes-element-assl"></a>Attributes 元素 (ASSL)
  包含相關聯維度之屬性的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationDesignDimension> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Attributes>  
      <Attribute>...</Attribute>  
  </Attributes>  
   ...  
</AggregationDesignDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationDesignDimension](../data-type/dimension-data-type-assl.md)， [AggregationDimension](../data-type/aggregationdimension-data-type-assl.md)， [AggregationInstanceCubeDimension](../data-type/cubedimension-data-type-assl.md)， [CubeDimension](../data-type/cubedimension-data-type-assl.md)，[維度](../objects/dimension-element-assl.md)， [PerspectiveDimension](../data-type/perspectivedimension-data-type-assl.md)， [RegularMeasureGroupDimension](../data-type/measuregroupdimension-data-type-assl.md)， [RelationshipEnd](../data-type/relationshipend-data-type-assl.md)|  
|子元素|[Attribute](../objects/attribute-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.AggregationAttributeCollection>、<xref:Microsoft.AnalysisServices.AggregationDesignAttributeCollection>、<xref:Microsoft.AnalysisServices.AggregationInstanceAttributeCollection>、<xref:Microsoft.AnalysisServices.CubeAttributeCollection>、<xref:Microsoft.AnalysisServices.DimensionAttributeCollection>、<xref:Microsoft.AnalysisServices.MeasureGroupAttributeCollection> 和 <xref:Microsoft.AnalysisServices.PerspectiveAttributeCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  