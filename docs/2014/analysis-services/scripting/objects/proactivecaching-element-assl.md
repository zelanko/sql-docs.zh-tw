---
title: ProactiveCaching 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProactiveCaching Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ProactiveCaching
helpviewer_keywords:
- ProactiveCaching element
ms.assetid: 85f9ed44-2ede-406f-b0ca-237ab2f49722
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c873cc6885d4f3a40f0de9e2f34048aff193c72
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183232"
---
# <a name="proactivecaching-element-assl"></a>ProactiveCaching 元素 (ASSL)
  定義父元素的主動式快取設定。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <ProactiveCaching>  
      <OnlineMode>...</OnlineMode>  
      <AggregationStorage>...</AggregationStorage>  
      <Source>...</Source>  
      <SilenceInterval>...</SilenceInterval>  
      <Latency>...</Latency>  
      <SilenceOverrideInterval>...</SilenceOverrideInterval>  
      <ForceRebuildInterval>...</ForceRebuildInterval>  
      <Enabled >...</Enabled>  
   </ProactiveCaching>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube](cube-element-assl.md)，[維度](dimension-element-assl.md)， [MeasureGroup](group-element-assl.md)，[資料分割](partition-element-assl.md)|  
|子元素|[AggregationStorage](../properties/aggregationstorage-element-assl.md)，[啟用](../properties/enabled-element-assl.md)， [ForceRebuildInterval](../properties/forcerebuildinterval-element-assl.md)，[延遲](../properties/latency-element-assl.md)， [OnlineMode](../properties/onlinemode-element-assl.md)， [SilenceInterval](../properties/silenceinterval-element-assl.md)， [SilenceOverrideInterval](../properties/silenceoverrideinterval-element-assl.md)，[來源](../properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ProactiveCaching>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
