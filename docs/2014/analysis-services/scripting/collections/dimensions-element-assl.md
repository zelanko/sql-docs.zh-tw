---
title: Dimensions 元素 (ASSL) |Microsoft Docs
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
- Dimensions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Dimensions
helpviewer_keywords:
- Dimensions element
ms.assetid: 104e3154-92e9-4c6b-9cf3-e3f3fc712b28
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ff15cecd5e5d4451a580d8ee73922dc4ab05364
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241608"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[彙總](../objects/aggregation-element-assl.md)， [AggregationDesign](../objects/aggregationdesign-element-assl.md)， [AggregationInstance](../objects/aggregationinstance-element-assl.md)， [Cube](../objects/cube-element-assl.md)，[資料庫](../objects/database-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)，[檢視方塊](../objects/perspective-element-assl.md)|  
|子元素|[Dimension](../objects/dimension-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.DimensionCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
