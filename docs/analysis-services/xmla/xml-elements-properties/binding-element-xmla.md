---
title: "繫結元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Binding Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.binding
- http://schemas.microsoft.com/analysisservices/2003/engine#Binding
- urn:schemas-microsoft-com:xml-analysis#Binding
helpviewer_keywords: Binding element
ms.assetid: d5acd8d4-8551-449a-ae30-d0ba828cc02d
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c3fb4afd47111911ba067e6f4488b749179cd3ab
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="binding-element-xmla"></a>Binding 元素 (XMLA)
  定義為單行繫結[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]物件，例如在維度中，屬性為[繫結](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)集合[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)或[處理序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Bindings>  
   <Binding xsi:type="DimensionAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="MeasureGroupAttributeBinding">...</Binding>  
   <!-- or -->  
   <Binding xsi:type="PartitionBinding">...</Binding>  
</Bindings>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|[DimensionAttributeBinding](../../../analysis-services/scripting/data-type/dimensionattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupAttributeBinding](../../../analysis-services/scripting/data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[繫結](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **繫結**元素定義-單行繫結，不是資料來源和資料來源檢視，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]所要處理的物件**批次**或**程序**命令。 如需有關處理物件的詳細資訊，請參閱[處理物件 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md).  
  
 單行繫結的詳細資訊，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
