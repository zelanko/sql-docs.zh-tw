---
title: CalculationProperty 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CalculationProperty Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CalculationProperty
helpviewer_keywords:
- CalculationProperty element
ms.assetid: 5f0b4cfc-7d25-4c01-a517-cc2e89859be3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfd8d16293314db4a9ca382d6a4042dd0a493f06
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161698"
---
# <a name="calculationproperty-element-assl"></a>CalculationProperty 元素 (ASSL)
  包含的使用者介面中使用之計算的屬性集合[MdxScript](mdxscript-element-assl.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CalculationProperties](../collections/calculationproperties-element-assl.md)|  
|子元素|[AssociatedMeasureGroupID](../properties/id-element-assl.md)， [BackColor](../properties/backcolor-element-assl.md)， [CalculationReference](../properties/calculationreference-element-assl.md)， [CalculationType](../properties/calculationtype-element-assl.md)，[描述](../properties/description-element-assl.md)，[DisplayFolder](../properties/displayfolder-element-assl.md)， [FontFlags](../properties/fontflags-element-assl.md)， [FontName](../properties/name-element-assl.md)， [FontSize](../properties/fontsize-element-assl.md)， [ForeColor](../properties/forecolor-element-assl.md)，[FormatString](../properties/formatstring-element-assl.md)， [NonEmptyBehavior](../properties/nonemptybehavior-element-assl.md)， [SolveOrder](../properties/solveorder-element-assl.md)，[翻譯](../collections/translations-element-assl.md)，[可見](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
