---
title: "EstimatedPerformanceGain 元素 (ASSL) |Microsoft 文件"
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
- EstimatedPerformanceGain Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EstimatedPerformanceGain
helpviewer_keywords:
- EstimatedPerformanceGain element
ms.assetid: d7487977-73c3-4244-ad5d-3c357b219db4
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ff2c7edeb2d26a8ecaea19277844c61772e581bd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="estimatedperformancegain-element-assl"></a>EstimatedPerformanceGain 元素 (ASSL)
  包含資料分割之估計效能改善的唯讀百分比。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationDesign>  
      ...  
   <EstimatedPerformanceGain>...</EstimatedPerformanceGain>  
   ...  
</AggregationDesign>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**EstimatedPerformanceGain**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.AggregationDesign>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

