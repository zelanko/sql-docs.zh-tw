---
title: ReferenceMeasureGroupDimension 資料類型 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ReferenceMeasureGroupDimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReferenceMeasureGroupDimension
helpviewer_keywords:
- ReferenceMeasureGroupDimension data type
ms.assetid: 81f7b83e-71a3-4eab-b291-0500d05903dc
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c9f43f7f7662ccde1a1fa4c4f8229c785bf9c484
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="referencemeasuregroupdimension-data-type-assl"></a>ReferenceMeasureGroupDimension 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義代表透過中繼維度與事實資料表間接相關的維度的衍生的資料類型。 (例如，Sales 量值群組可以參考透過 Customer 維度相關的 Geography 維度)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ReferenceMeasureGroupDimension>  
   <!-- The following elements extend MeasureGroupDimension -->  
      <IntermediateCubeDimensionID>...</IntermediateCubeDimensionID>  
   <IntermediateGranularityAttributeID>...</IntermediateGranularityAttributeID>  
   <Materialization>...</Materialization>  
</ReferenceMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[IntermediateCubeDimensionID](../../../analysis-services/scripting/properties/intermediatecubedimensionid-element-assl.md)， [IntermediateGranularityAttributeID](../../../analysis-services/scripting/properties/intermediategranularityattributeid-element-assl.md)，[具體化](../../../analysis-services/scripting/properties/materialization-element-assl.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>。  
  
## <a name="see-also"></a>請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
