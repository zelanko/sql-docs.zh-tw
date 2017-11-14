---
title: "Goal 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Goal Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Goal
helpviewer_keywords:
- Goal element
ms.assetid: 75fa5b57-418e-43ad-8704-764e4f0a40cf
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31a054da277a8ac5df4bc2de468a71b87fffe0f2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="goal-element-assl"></a>Goal 元素 (ASSL)
  識別所需的目標中[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Kpi>  
   ...  
   <Goal>...</Goal>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **目標**元素包含多維度運算式 (MDX) 運算式。  
  
 對應目的父代的項目**目標**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>另請參閱  
 [Status 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/status-element-assl.md)   
 [Trend 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/trend-element-assl.md)   
 [Value 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/value-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

