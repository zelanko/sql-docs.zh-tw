---
title: MeasureGroupAttributeBinding 資料類型 (out out-of-line) (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 35b695ea029d78211a0042d330a961bfcb95a494
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34033639"
---
# <a name="measuregroupattributebinding-data-type-out-of-line-assl"></a>MeasureGroupAttributeBinding 資料類型 (out-of-line) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義衍生資料類型，它代表量值群組中包含之維度內某個屬性的非正規 (out-of-line) 繫結。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroupAttributeBinding>  
   <!-- The following elements extend Binding -->  
   <DatabaseID>...</DatabaseID>  
   <CubeID>...</CubeID>  
   <MeasureGroupID>...</MeasureGroupID>  
   <GranularityAttributeID>...</GranularityAttributeID>  
   <Source>...</Source>  
</MeasureGroupAttributeBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[CubeID](../../../analysis-services/scripting/properties/cubeid-element-assl.md)， [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md)， [MeasureGroupID](../../../analysis-services/scripting/properties/measuregroupid-element-assl.md)， [GranularityAttributeID](../../../analysis-services/scripting/properties/granularityattributeid-element-assl.md)，[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|  
|衍生的元素|[繫結](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md)([繫結](../../../analysis-services/scripting/collections/attributes-element-assl.md)集合 XML for Analysis (XMLA)[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)和[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令)|  
  
## <a name="remarks"></a>備註  
 單行繫結的詳細資訊，請參閱[資料來源和繫結 & #40;SSAS 多維度 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
