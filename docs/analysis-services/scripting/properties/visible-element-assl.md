---
title: Visible 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4576928f3d0d98c40e43821ea68bc5782e4ecff7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="visible-element-assl"></a>Visible 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  決定父元素的可見性。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CalculationProperty> <!-- or one of the elements listed below in the Element Relationships table -->  
  
   <Visible >...</Visible >  
  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|True|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)， [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)，[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **看得見**元素會決定使用者介面元件是否應該顯示父項目。  
  
 對應至父系的項目**看得見**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CalculationProperty>， <xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.CubeDimension>， <xref:Microsoft.AnalysisServices.CubeHierarchy>， <xref:Microsoft.AnalysisServices.Database>，和<xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
