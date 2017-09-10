---
title: "DisplayFolder 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DisplayFolder Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DisplayFolder
helpviewer_keywords:
- DisplayFolder element
ms.assetid: 55184c02-03e7-4d6c-b87a-d4d34bc11d0e
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc9e0f1479821a0559c9ac105cdbc2fb4f9f666c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="displayfolder-element-assl"></a>DisplayFolder 元素 (ASSL)
  指定要在其中列出父元素的資料夾。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]應用程式開發人員和系統管理員可能會支援使用顯示資料夾以視覺化方式分類多個項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
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
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)，[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)，[轉譯](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在較大的 Cube 中，可能會有數百個量值和階層。 **DisplayFolder**屬性定義用戶端上的使用者外觀。 值**DisplayFolder**屬性可包含下列選項中的任何一個：  
  
-   空白，表示量值不屬於資料夾。  
  
-   包含單一資料夾名稱，表示量值應該轉譯為屬於具有相同名稱的資料夾。  
  
-   包含反斜線分隔的多個資料夾名稱 (\\)，表示內嵌的資料夾階層。  
  
 **DisplayFolder**屬性會套用至**CalculationProperty**項目才值[CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md)設*成員*.  
  
 對應至父系的項目**DisplayFolder**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CalculationProperty>， <xref:Microsoft.AnalysisServices.Hierarchy>， <xref:Microsoft.AnalysisServices.Kpi>， <xref:Microsoft.AnalysisServices.Measure>，和<xref:Microsoft.AnalysisServices.Translation>。  
  
## <a name="see-also"></a>另請參閱  
 [CalculationProperties 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [MdxScript 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [MdxScripts 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
