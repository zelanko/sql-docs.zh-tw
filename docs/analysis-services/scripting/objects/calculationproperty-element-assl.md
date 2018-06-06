---
title: CalculationProperty 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e20f0774b987d0ecd36853485f7fef422175f2c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="calculationproperty-element-assl"></a>CalculationProperty 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的使用者介面中使用之計算的屬性集合[MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CalculationProperties>  
   <CalculationProperty>  
      <CalculationReference>...</CalculationReference>  
      <CalculationType>...</CalculationType>  
      <Translations>...</Translations>  
      <Description>...</Description>  
      <Visible>...</Visible>  
      <SolveOrder>...</SolveOrder>  
      <FormatString>...</FormatString>  
      <ForeColor>...</ForeColor>  
      <BackColor>...</BackColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <NonEmptyBehavior>...</NonEmptyBehavior>  
      <AssociatedMeasureGroupID>...</AssociatedMeasureGroupID>  
      <DisplayFolder>...</DisplayFolder>  
   </CalculationProperty>  
</CalculationProperties>  
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
|父元素|[CalculationProperties](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)|  
|子元素|[AssociatedMeasureGroupID](../../../analysis-services/scripting/properties/associatedmeasuregroupid-element-assl.md)， [BackColor](../../../analysis-services/scripting/properties/backcolor-element-assl.md)， [CalculationReference](../../../analysis-services/scripting/properties/calculationreference-element-assl.md)， [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md)， [FontFlags](../../../analysis-services/scripting/properties/fontflags-element-assl.md)， [FontName](../../../analysis-services/scripting/properties/fontname-element-assl.md)， [FontSize](../../../analysis-services/scripting/properties/fontsize-element-assl.md)， [ForeColor](../../../analysis-services/scripting/properties/forecolor-element-assl.md)，[FormatString](../../../analysis-services/scripting/properties/formatstring-element-assl.md)， [NonEmptyBehavior](../../../analysis-services/scripting/properties/nonemptybehavior-element-assl.md)， [SolveOrder](../../../analysis-services/scripting/properties/solveorder-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)，[可見](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
