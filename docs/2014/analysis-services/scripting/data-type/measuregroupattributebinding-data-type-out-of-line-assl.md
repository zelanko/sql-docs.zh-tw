---
title: MeasureGroupAttributeBinding 資料類型 (非正規-out-of-line) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupAttributeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MeasureGroupAttributeBinding data type
ms.assetid: bfe09a95-4e04-4f93-9389-7dd0b4c8f5e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 247e96f7994fa076b8641394231b772e80685e32
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156578"
---
# <a name="measuregroupattributebinding-data-type-out-of-line-assl"></a>MeasureGroupAttributeBinding 資料類型 (out-of-line) (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[繫結](binding-data-type-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[CubeID](../properties/id-element-assl.md)， [DatabaseID](../../xmla/xml-elements-properties/id-element-xmla.md)， [MeasureGroupID](../properties/measuregroupid-element-assl.md)， [GranularityAttributeID](../properties/attributeid-element-assl.md)，[來源](../properties/source-element-binding-assl.md)|  
|衍生的元素|[繫結](../../xmla/xml-elements-properties/binding-element-xmla.md)([繫結](../collections/attributes-element-assl.md)集合的 XML for Analysis (XMLA) 所[批次](../../xmla/xml-elements-commands/batch-element-xmla.md)並[程序](../../xmla/xml-elements-commands/process-element-xmla.md)命令)|  
  
## <a name="remarks"></a>備註  
 如需程式碼外部繫結的詳細資訊，請參閱[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
