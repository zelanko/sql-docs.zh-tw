---
title: PerspectiveMeasure 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c8f0d33d1e68d222ff520143e62a8a92d673afb1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029259"
---
# <a name="perspectivemeasure-data-type-assl"></a>PerspectiveMeasure 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表量值中的相關資訊的基本資料類型[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<PerspectiveMeasure>  
   <MeasureID>...</MeasureID>  
   <Annotations>...</Annotations>  
</PerspectiveMeasure>  
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
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [MeasureID](../../../analysis-services/scripting/properties/measureid-element-assl.md)|  
|衍生的元素|[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)([量值](../../../analysis-services/scripting/collections/measures-element-assl.md)集合[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.PerspectiveMeasure>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
