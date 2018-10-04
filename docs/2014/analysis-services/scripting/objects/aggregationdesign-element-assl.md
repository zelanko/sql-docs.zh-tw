---
title: AggregationDesign 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDesign Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesign
helpviewer_keywords:
- AggregationDesign element
ms.assetid: 80ad98d8-73a8-4353-b5ad-d2a9ac3bc531
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 430035dd83cf137cb80a5db5d159da027014e6c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075288"
---
# <a name="aggregationdesign-element-assl"></a>AggregationDesign 元素 (ASSL)
  定義可在資料庫中多個分割區之間共用之彙總定義的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationDesigns>  
   <AggregationDesign>  
      <ID>...</ID>  
      <Name>...</Name>  
            <Description>...</Description>  
      <EstimatedRows>...</EstimatedRows>  
      <Dimensions>...</Dimensions>  
            <Aggregations>...</Aggregation>  
      <EstimatedPerformanceGain>...</EstimatedPerformanceGain>  
      <Annotations>...</Annotations>  
   </AggregationDesign>  
</AggregationDesigns>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationDesigns](../collections/aggregationdesigns-element-assl.md)|  
|子元素|[彙總](../collections/aggregations-element-assl.md)，[註解](../collections/annotations-element-assl.md)，[描述](../properties/description-element-assl.md)，[維度](../collections/dimensions-element-assl.md)， [EstimatedPerformanceGain](../properties/estimatedperformancegain-element-assl.md)， [EstimatedRows](../properties/estimatedrows-element-assl.md)，[識別碼](../properties/id-element-assl.md)，[名稱](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>另請參閱  
 [分割項目&#40;ASSL&#41;](partition-element-assl.md)   
 [Aggregation 元素&#40;ASSL&#41;](aggregation-element-assl.md)   
 [Aggregations 元素&#40;ASSL&#41;](../collections/aggregations-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
