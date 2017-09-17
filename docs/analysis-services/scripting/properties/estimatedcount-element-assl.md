---
title: "EstimatedCount 元素 (ASSL) |Microsoft 文件"
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
- EstimatedCount Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EstimatedCount
helpviewer_keywords:
- EstimatedCount element
ms.assetid: ce84b54a-8ab2-42f4-a7dd-e10a3d41cb4d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 683f8dee8bdb1e765bb6af695a1109093842bd29
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="estimatedcount-element-assl"></a>EstimatedCount 元素 (ASSL)
  包含屬性的預估成員數目 (由使用者定義)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationDesignAttribute> <!-- or DimensionAttribute -->  
      ...  
   <EstimatedCount>...</EstimatedCount>  
   ...  
</AggregationDesignAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|長整數|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationDesignAttribute](../../../analysis-services/scripting/data-type/aggregationdesignattribute-data-type-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個值由使用者所指派，並且由[AggregationDesign 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md).  
  
 對應至父系的項目**EstimatedCount**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.AggregationDesignAttribute>和<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
