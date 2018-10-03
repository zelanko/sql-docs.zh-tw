---
title: CubeDimensionID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeDimensionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimensionID
helpviewer_keywords:
- CubeDimensionID element
ms.assetid: d1341fb2-9afe-40f1-a704-ce548bce48fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e50506439d5820bee62015805a19323a20134e55
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076268"
---
# <a name="cubedimensionid-element-assl"></a>CubeDimensionID 元素 (ASSL)
  識別[CubeDimension](../data-type/dimension-data-type-assl.md)與父元素相關聯的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationDesignDimension> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CubeDimensionID>...</CubeDimensionID>  
   ...  
</AggregationDesignDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationDesignDimension](../data-type/aggregationdesigndimension-data-type-assl.md)， [AggregationDimension](../data-type/aggregationdimension-data-type-assl.md)， [AggregationInstanceCubeDimension](../data-type/aggregationinstancecubedimension-data-type-assl.md)， [CubeAttributeBinding](../data-type/binding-data-type-assl.md)， [CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md)， [CubeDimensionPermission](../data-type/permission-data-type-assl.md)， [MeasureGroupDimension](../data-type/measuregroupdimension-data-type-assl.md)， [MeasureGroupDimensionBinding](../data-type/measuregroupdimensionbinding-data-type-assl.md)， [PerspectiveDimension](../data-type/perspectivedimension-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `CubeDimensionID` 父系的元素是 <xref:Microsoft.AnalysisServices.AggregationDesignDimension>、<xref:Microsoft.AnalysisServices.AggregationDimension>、<xref:Microsoft.AnalysisServices.CubeAttributeBinding>、<xref:Microsoft.AnalysisServices.CubeDimensionBinding>、<xref:Microsoft.AnalysisServices.CubeDimensionPermission>、<xref:Microsoft.AnalysisServices.MeasureGroupDimension>、<xref:Microsoft.AnalysisServices.MeasureGroupDimensionBinding> 和 <xref:Microsoft.AnalysisServices.PerspectiveDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
