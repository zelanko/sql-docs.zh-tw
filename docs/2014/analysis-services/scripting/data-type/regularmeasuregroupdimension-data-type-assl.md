---
title: RegularMeasureGroupDimension 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RegularMeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RegularMeasureGroupDimension
helpviewer_keywords:
- RegularMeasureGroupDimension data type
ms.assetid: 5c4ce400-6d7c-40fc-9bcb-392718b77182
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 072ada60b803f4c8adfde73a228144a4d0157dff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051810"
---
# <a name="regularmeasuregroupdimension-data-type-assl"></a>RegularMeasureGroupDimension 資料類型 (ASSL)
  定義代表維度與量值群組之間一般關聯性的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RegularMeasureGroupDimension>  
   <!-- The following elements extend MeasureGroupDimension -->  
   <Cardinality>...</Cardinality>  
   <Attributes>...</Attributes>  
</RegularMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[MeasureGroupDimension](dimension-data-type-assl.md)|  
|衍生資料類型|[ReferenceMeasureGroupDimension](measuregroupdimension-data-type-assl.md)， [DegenerateMeasureGroupDimension](degeneratemeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[屬性](../collections/attributes-element-assl.md)，[基數](../properties/cardinality-element-assl.md)|  
|衍生的元素|[維度](../objects/dimension-element-assl.md)([維度](../collections/dimensions-element-assl.md)集合)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.RegularMeasureGroupDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
