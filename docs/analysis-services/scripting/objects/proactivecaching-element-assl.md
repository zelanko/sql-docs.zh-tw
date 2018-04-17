---
title: ProactiveCaching 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ProactiveCaching Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ProactiveCaching
helpviewer_keywords:
- ProactiveCaching element
ms.assetid: 85f9ed44-2ede-406f-b0ca-237ab2f49722
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bb72277c288a5a882a31c8bd7744a37114d99a6e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="proactivecaching-element-assl"></a>ProactiveCaching 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義父元素的主動式快取設定。  
  
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
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)，[磁碟分割](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|[AggregationStorage](../../../analysis-services/scripting/properties/aggregationstorage-element-assl.md)，[啟用](../../../analysis-services/scripting/properties/enabled-element-assl.md)， [ForceRebuildInterval](../../../analysis-services/scripting/properties/forcerebuildinterval-element-assl.md)，[延遲](../../../analysis-services/scripting/properties/latency-element-assl.md)， [OnlineMode](../../../analysis-services/scripting/properties/onlinemode-element-assl.md)， [SilenceInterval](../../../analysis-services/scripting/properties/silenceinterval-element-assl.md)， [SilenceOverrideInterval](../../../analysis-services/scripting/properties/silenceoverrideinterval-element-assl.md)，[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ProactiveCaching>。  
  
## <a name="see-also"></a>請參閱  
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
