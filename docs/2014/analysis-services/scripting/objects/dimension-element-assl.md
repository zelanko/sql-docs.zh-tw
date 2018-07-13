---
title: 維度元素 (ASSL) |Microsoft Docs
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
- Dimension Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension element
ms.assetid: 71886014-f463-4b70-a2a2-d9e5053ba4f0
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d6d8b909b6bf7018f70f381ec8d07b20f6b7d851
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185237"
---
# <a name="dimension-element-assl"></a>Dimension 元素 (ASSL)
  定義維度。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimensions>  
   <Dimension xsi:type="Dimension">...</Dimension> <!-- ancestor: Database -->  
   <!-- or -->  
   <Dimension xsi:type="AggregationDimension">...</Dimension> <!-- ancestor: Aggregation -->  
   <!-- or -->  
   <Dimension xsi:type="AggregationDesignDimension">...</Dimension> <!-- ancestor: AggregationDesign -->  
   <!-- or -->  
   <Dimension xsi:type="AggregationInstanceCubeDimension">...</Dimension> <!-- ancestor: AggregationInstance -->  
      <!-- or -->  
   <Dimension xsi:type="CubeDimension">...</Dimension> <!-- ancestor: Cube -->  
      <!-- or -->  
   <Dimension xsi:type="MeasureGroupDimension">...</Dimension> <!-- ancestor: MeasureGroup -->  
   <!-- or -->  
   <Dimension xsi:type="PerspectiveDimension">...</Dimension> <!-- ancestor: Perspective -->  
</Dimensions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[[資料庫]](../data-type/dimension-data-type-assl.md)|  
|[彙總](../data-type/aggregationdimension-data-type-assl.md)|  
|[AggregationDesign](../data-type/aggregationdesigndimension-data-type-assl.md)|  
|[AggregationInstance](../data-type/cubedimension-data-type-assl.md)|  
|[Cube](cube-element-assl.md)|[CubeDimension](../data-type/cubedimension-data-type-assl.md)|  
|[MeasureGroup](../data-type/measuregroupdimension-data-type-assl.md)|  
|[檢視方塊](../data-type/perspectivedimension-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Dimensions](../collections/dimensions-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應項目<xref:Microsoft.AnalysisServices.Dimension>， <xref:Microsoft.AnalysisServices.AggregationDimension>， <xref:Microsoft.AnalysisServices.AggregationDesignDimension>， <xref:Microsoft.AnalysisServices.CubeDimension>， <xref:Microsoft.AnalysisServices.MeasureGroupDimension>，和<xref:Microsoft.AnalysisServices.PerspectiveDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
