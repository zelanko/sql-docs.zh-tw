---
title: AggregationDesignDimension 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AggregationDesignDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationDesignDimension
helpviewer_keywords:
- AggregationDesignDimension data type
ms.assetid: 06a0d418-014c-4f40-a63a-5cfeee3f6a41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 758fc3a42b2ff1277deda1e7cff566b9eba17a26
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200408"
---
# <a name="aggregationdesigndimension-data-type-assl"></a>AggregationDesignDimension 資料類型 (ASSL)
  定義代表 cube 維度之間的關聯性的基本資料類型和[AggregationDesign](../objects/aggregationdesign-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationDesignDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
      <Annotations>...</Annotations>  
</AggregationDesignDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|None|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[註釋](../collections/annotations-element-assl.md)，[屬性](../collections/attributes-element-assl.md)， [CubeDimensionID](../properties/id-element-assl.md)|  
|衍生的元素|[維度](../objects/dimension-element-assl.md)([維度](../collections/dimensions-element-assl.md)的集合[AggregationDesign](../objects/aggregationdesign-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.AggregationDesignDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [AggregationDesign 元素&#40;ASSL&#41;](../objects/aggregationdesign-element-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
