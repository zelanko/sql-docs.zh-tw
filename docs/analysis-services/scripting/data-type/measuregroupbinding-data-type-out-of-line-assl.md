---
title: MeasureGroupBinding 資料類型 (out out-of-line) (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f30a70c9f373dcd776fbf206fcd97df0983b82aa
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034749"
---
# <a name="measuregroupbinding-data-type-out-of-line-assl"></a>MeasureGroupBinding 資料類型 (out-of-line) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表量值群組之繫結的基本資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroupBinding>  
   <ID>...</ID>  
   <Source>...</Source>  
   <EstimatedRows>...</EstimatedRows>  
   <Dimensions>...</Dimensions>  
   <Measures>...</Measures>  
      <Partitions>...</Partitions>  
</MeasureGroupBinding>  
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
|子元素|[維度](../../../analysis-services/scripting/collections/dimensions-element-assl.md)， [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)，[量值](../../../analysis-services/scripting/collections/measures-element-assl.md)，[分割](../../../analysis-services/scripting/collections/partitions-element-assl.md)，[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|衍生的元素|請參閱[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊，請參閱 < > 一節，超出繫結中,[資料來源和繫結 & #40;SSAS 多維度 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
