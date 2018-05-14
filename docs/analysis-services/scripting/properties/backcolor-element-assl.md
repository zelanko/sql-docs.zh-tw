---
title: BackColor 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 55bf807cfc82ffe0cb086a122d834a73339d4e79
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="backcolor-element-assl"></a>BackColor 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述父元素的色彩相關顯示特性。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <BackColor>...</BackColor>  
   ...  
</CalculationProperty>  
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
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **BackColor**屬性包含多維度運算式 (MDX) 語言運算式並套用至**CalculationProperty**的項目[CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)*成員*或*儲存格*。  
  
 對應目的父代的項目**BackColor**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [CalculationProperties 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
