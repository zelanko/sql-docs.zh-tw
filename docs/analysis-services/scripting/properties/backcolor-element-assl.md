---
title: "BackColor 元素 (ASSL) |Microsoft 文件"
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
apiname: BackColor Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: BackColor
helpviewer_keywords: BackColor element
ms.assetid: 9024d131-74cc-4815-833a-f8cae57b7453
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4ad241ddacd5b90206dd288c46aefacb7f793304
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="backcolor-element-assl"></a>BackColor 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述父元素的色彩相關顯示特性。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <BackColor>...</BackColor>  
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
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **BackColor**屬性包含多維度運算式 (MDX) 語言運算式並套用至**CalculationProperty**的項目[CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)*成員*或*儲存格*。  
  
 對應目的父代的項目**BackColor**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>請參閱  
 [CalculationProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
