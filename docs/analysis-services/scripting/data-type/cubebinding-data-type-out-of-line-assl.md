---
title: "CubeBinding 資料類型 (out out-of-line) (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CubeBinding Data Type (out-of-line)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0624bd051d8534e82b608bc925236abc0153798
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cubebinding-data-type-out-of-line-assl"></a>CubeBinding 資料類型 (out-of-line) (ASSL)
  定義表示之間的關聯性的基本資料型別[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目和[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeBinding>  
   <ID>...</ID>  
   <DataSourceID>...</DataSourceID>  
   <DataSource>...</DataSource>  
   <MeasureGroup>...</MeasureGroup>  
</CubeBinding>  
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
|子元素|[資料來源](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|衍生的元素|[繫結](../../../analysis-services/xmla/xml-elements-properties/binding-element-xmla.md)([繫結](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)集合[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)或[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令)|  
  
## <a name="remarks"></a>備註  
 單行繫結的詳細資訊，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>另請參閱  
 [繫結資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

