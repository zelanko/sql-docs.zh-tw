---
title: "屬性元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Attributes Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Attributes
helpviewer_keywords:
- Attributes element
ms.assetid: d6b545e6-1521-496f-a731-f2c2c44118e4
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0ba9d7698f23f902935e7fa531c9391a2373a002
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationDesignDimension](../../../analysis-services/scripting/data-type/aggregationdesigndimension-data-type-assl.md)， [AggregationDimension](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md)， [AggregationInstanceCubeDimension](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)， [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)， [維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)， [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)， [RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|子元素|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應的元素是 <xref:Microsoft.AnalysisServices.AggregationAttributeCollection>、<xref:Microsoft.AnalysisServices.AggregationDesignAttributeCollection>、<xref:Microsoft.AnalysisServices.AggregationInstanceAttributeCollection>、<xref:Microsoft.AnalysisServices.CubeAttributeCollection>、<xref:Microsoft.AnalysisServices.DimensionAttributeCollection>、<xref:Microsoft.AnalysisServices.MeasureGroupAttributeCollection> 和 <xref:Microsoft.AnalysisServices.PerspectiveAttributeCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

