---
title: "MeasureGroupAttributeBinding 資料類型 (out out-of-line) (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MeasureGroupAttributeBinding Data Type (out-of-line)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MeasureGroupAttributeBinding data type
ms.assetid: bfe09a95-4e04-4f93-9389-7dd0b4c8f5e4
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b6e2d9f373bd371b19bbedda669cd2e56352ec3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

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
 單行繫結的詳細資訊，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

