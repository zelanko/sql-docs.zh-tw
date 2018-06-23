---
title: Aggregation 元素 (ASSL) |Microsoft 文件
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
- Aggregation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aggregation
helpviewer_keywords:
- Aggregation element
ms.assetid: f37af388-b2b3-4234-a1d6-936ee9b7f2ae
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 59f33b45653f614702b1472e57fe4464cf172b73
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131580"
---
# <a name="aggregation-element-assl"></a>Aggregation 元素 (ASSL)
  定義單一彙總[分割](partition-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Aggregations>  
      <Aggregation>  
      <ID>...</ID>  
      <Name>...</Name>  
      <Dimensions>...</Dimensions>  
            <Annotations>...</Annotations>  
      <Description>...</Description>  
   </Aggregation>  
</Aggregations>  
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
|父元素|[彙總](../collections/aggregations-element-assl.md)|  
|子元素|[註解](../collections/annotations-element-assl.md)，[描述](../properties/description-element-assl.md)，[維度](../collections/dimensions-element-assl.md)，[識別碼](../properties/id-element-assl.md)，[名稱](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Aggregation>。  
  
## <a name="see-also"></a>另請參閱  
 [分割項目&#40;ASSL&#41;](partition-element-assl.md)   
 [AggregationDesign 元素&#40;ASSL&#41;](aggregationdesign-element-assl.md)   
 [MeasureGroup 元素&#40;ASSL&#41;](group-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  