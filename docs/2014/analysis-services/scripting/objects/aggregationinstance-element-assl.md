---
title: AggregationInstance 元素 (ASSL) |Microsoft Docs
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
- AggregationInstance Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- AggregationInstance element
ms.assetid: 2e77e9e1-9f2c-4df4-9aa6-5b7b911016a3
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 089fcff4b01b66f3b2bc1ac98de2f5cb4ba88319
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229768"
---
# <a name="aggregationinstance-element-assl"></a>AggregationInstance 元素 (ASSL)
  定義資料分割的彙總執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationInstances>  
   <AggregationInstance>  
      <AggregationType>...</AggregationType>  
      <AggregationID>...</AggregationID>  
      <Source>...</Source>  
      <Dimensions>...</Dimensions>  
      <Measures>...</Measures>  
      <Annotations>...</Annotations>  
   </AggregationInstance>  
</AggregationInstances>  
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
|父元素|[AggregationInstances](../collections/aggregationinstances-element-assl.md)|  
|子元素|[AggregationID](../properties/id-element-assl.md)， [AggregationType](../properties/aggregationtype-element-assl.md)，[註解](../collections/annotations-element-assl.md)，[維度](../collections/dimensions-element-assl.md)，[措施](../collections/measures-element-assl.md)，[來源](../properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>備註  
 當[資料分割](partition-element-assl.md)項目會使用[AggregationDesign](aggregationdesign-element-assl.md)項目來產生該資料分割的彙總每個[彙總](aggregation-element-assl.md)在`AggregationDesign`是具現化的資料分割。 多個資料分割可以使用相同的彙總設計來產生已定義彙總的多個執行個體。 `AggregationInstance` 元素代表已定義彙總的執行個體。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
