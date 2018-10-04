---
title: AssociatedMeasureGroupID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AssociatedMeasureGroupID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AssociatedMeasureGroupID
helpviewer_keywords:
- AssociatedMeasureGroupID element
ms.assetid: a18ff25b-00a2-4ddf-abcc-ef4d52c8a462
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 753f79f6f0536db7d5ae4c7af77805294c45af21
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054608"
---
# <a name="associatedmeasuregroupid-element-assl"></a>AssociatedMeasureGroupID 元素 (ASSL)
  包含的識別碼[MeasureGroup](../objects/group-element-assl.md)相關聯的項目[CalculationProperty](../objects/calculationproperty-element-assl.md)項目或有[Kpi](../objects/kpi-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CalculationProperty> <!-- or Kpi -->  
   ...  
   <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 當套用至`CalculationProperty`項目，`AssociatedMeasureGroupID`屬性會套用至項目[CalculationType](calculationtype-element-assl.md)的*成員*。  
  
 對應至父系的元素`AssociatedMeasureGroupID`在 「 分析管理物件 (AMO) 物件模型所<xref:Microsoft.AnalysisServices.CalculationProperty>和<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>另請參閱  
 [CalculationProperties 元素&#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 元素&#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
