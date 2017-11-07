---
title: "AggregationInstance 元素 (ASSL) |Microsoft 文件"
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
- AggregationInstance Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AggregationInstance element
ms.assetid: 2e77e9e1-9f2c-4df4-9aa6-5b7b911016a3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9a3840c481d63b06357fa8c76b9f3fc7c2ae6bc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)|  
|子元素|[AggregationID](../../../analysis-services/scripting/properties/aggregationid-element-assl.md)， [AggregationType](../../../analysis-services/scripting/properties/aggregationtype-element-assl.md)，[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[維度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)，[量值](../../../analysis-services/scripting/collections/measures-element-assl.md)， [來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
  
## <a name="remarks"></a>備註  
 當[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)項目使用[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)元素來產生彙總的資料分割，每個[彙總](../../../analysis-services/scripting/objects/aggregation-element-assl.md)中**AggregationDesign**具現化的資料分割。 多個資料分割可以使用相同的彙總設計來產生已定義彙總的多個執行個體。 **AggregationInstance**元素代表已定義的彙總的執行個體。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AggregationInstance>。  
  
## <a name="see-also"></a>另請參閱  
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

