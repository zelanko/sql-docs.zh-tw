---
title: "Dimensions 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Dimensions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Dimensions
helpviewer_keywords:
- Dimensions element
ms.assetid: 104e3154-92e9-4c6b-9cf3-e3f3fc712b28
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4859da457949e343d00c8fc534089de4d194a102
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dimensions-element-assl"></a>Dimensions 元素 (ASSL)
  包含與父元素相關聯之維度的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database> <!-- or Aggregation, AggregationDesign, AggregationInstance, Cube, MeasureGroup, Perspective -->  
   ...  
   <Dimensions>  
      <Dimension>...</Dimension>  
   </Dimensions>  
   ...  
</Database>  
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
|父元素|[彙總](../../../analysis-services/scripting/objects/aggregation-element-assl.md)， [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)， [AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)，[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[檢視方塊](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|子元素|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DimensionCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  

