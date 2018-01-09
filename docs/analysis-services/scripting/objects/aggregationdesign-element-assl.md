---
title: "AggregationDesign 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AggregationDesign Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AggregationDesign
helpviewer_keywords: AggregationDesign element
ms.assetid: 80ad98d8-73a8-4353-b5ad-d2a9ac3bc531
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 535cf75969963c8b94992fa267034bf4f73c9735
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="aggregationdesign-element-assl"></a>AggregationDesign 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義一組可以橫跨多個資料分割資料庫中的彙總定義。  
  
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
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationDesigns](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md)|  
|子元素|[彙總](../../../analysis-services/scripting/collections/aggregations-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[維度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)， [EstimatedPerformanceGain](../../../analysis-services/scripting/properties/estimatedperformancegain-element-assl.md)， [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>請參閱  
 [Partition 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)   
 [Aggregation 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)   
 [Aggregations 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/aggregations-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
