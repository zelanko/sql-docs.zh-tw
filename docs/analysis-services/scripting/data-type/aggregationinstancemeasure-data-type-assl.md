---
title: AggregationInstanceMeasure 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c6b5c7ba5f7bae5ad0f76b92aeef70df1b2491dc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031009"
---
# <a name="aggregationinstancemeasure-data-type-assl"></a>AggregationInstanceMeasure 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表彙總執行個體所使用之量值相關資訊的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AggregationInstanceMeasure>  
   <MeasureID>...</MeasureID>  
   <Source>...</Source>  
</AggregationInstanceMeasure>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[MeasureID](../../../analysis-services/scripting/properties/measureid-element-assl.md)，[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|衍生的元素|[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.AggregationInstanceMeasure>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
