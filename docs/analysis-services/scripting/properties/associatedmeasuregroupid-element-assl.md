---
title: "AssociatedMeasureGroupID 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AssociatedMeasureGroupID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AssociatedMeasureGroupID
helpviewer_keywords: AssociatedMeasureGroupID element
ms.assetid: a18ff25b-00a2-4ddf-abcc-ef4d52c8a462
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 14ddb275cf2462812fdbed1430a2503f2f79130d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="associatedmeasuregroupid-element-assl"></a>AssociatedMeasureGroupID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含識別碼的[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)元素相關聯[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)項目或[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)項目。  
  
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
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 當套用至**CalculationProperty**項目， **AssociatedMeasureGroupID**屬性會套用至項目[CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)的*成員*.  
  
 對應至父系的項目**AssociatedMeasureGroupID**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CalculationProperty>和<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>請參閱  
 [CalculationProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
