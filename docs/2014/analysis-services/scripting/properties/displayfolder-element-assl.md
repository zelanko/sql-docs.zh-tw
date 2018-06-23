---
title: DisplayFolder 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DisplayFolder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DisplayFolder
helpviewer_keywords:
- DisplayFolder element
ms.assetid: 55184c02-03e7-4d6c-b87a-d4d34bc11d0e
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c959f1c2fe298217b46849c6a13d3e0f313f6803
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034458"
---
# <a name="displayfolder-element-assl"></a>DisplayFolder 元素 (ASSL)
  指定要在其中列出父元素的資料夾。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 開發人員和管理員的應用程式可能會支援使用顯示資料夾以視覺化方式分類多個項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
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
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)，[階層](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)，[量值](../objects/measure-element-assl.md)，[轉譯](../objects/translation-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在較大的 Cube 中，可能會有數百個量值和階層。 `DisplayFolder` 屬性會定義用戶端的使用者外觀。 `DisplayFolder` 屬性的值可以包含下列任何一個選項：  
  
-   空白，表示量值不屬於資料夾。  
  
-   包含單一資料夾名稱，表示量值應該轉譯為屬於具有相同名稱的資料夾。  
  
-   包含反斜線分隔的多個資料夾名稱 (\\)，表示內嵌的資料夾階層。  
  
 `DisplayFolder`屬性會套用至`CalculationProperty`項目才值[CalculationType](calculationtype-element-assl.md)設*成員*。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `DisplayFolder` 父系的元素是 <xref:Microsoft.AnalysisServices.CalculationProperty>、<xref:Microsoft.AnalysisServices.Hierarchy>、<xref:Microsoft.AnalysisServices.Kpi>、<xref:Microsoft.AnalysisServices.Measure> 和 <xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>另請參閱  
 [CalculationProperties 元素&#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 元素&#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  