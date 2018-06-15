---
title: DataMiningMeasureGroupDimension 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0d42836a434a5aa91ec0b13726d4dd482e434850
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032279"
---
# <a name="dataminingmeasuregroupdimension-data-type-assl"></a>DataMiningMeasureGroupDimension 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表量值群組與資料採礦維度之間關聯性的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataMiningMeasureGroupDimension>  
   <!-- The following elements extend MeasureGroupDimension -->  
      <CaseCubeDimensionID>...</CaseCubeDimensionID>  
</DataMiningMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[CaseCubeDimensionID](../../../analysis-services/scripting/properties/casecubedimensionid-element-assl.md)|  
|衍生的元素|請參閱[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)([維度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)集合[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DataMiningMeasureGroupDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
