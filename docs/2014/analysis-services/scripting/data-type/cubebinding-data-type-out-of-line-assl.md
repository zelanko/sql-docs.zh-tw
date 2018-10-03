---
title: CubeBinding 資料類型 (非正規-out-of-line) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeBinding Data Type (out-of-line)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeBinding
helpviewer_keywords:
- CubeBinding data type
ms.assetid: 5e1ee8ef-855c-4f3d-ae21-a33360d00d66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee354905f21670a143d8ec711bb45495086dbf05
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136649"
---
# <a name="cubebinding-data-type-out-of-line-assl"></a>CubeBinding 資料類型 (out-of-line) (ASSL)
  定義表示之間的關聯性的基本資料型別[Cube](../objects/cube-element-assl.md)項目並[DataSource](../objects/datasource-element-assl.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|None|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[資料來源](../objects/datasource-element-assl.md)， [DataSourceID](../properties/id-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)|  
|衍生的元素|[繫結](../../xmla/xml-elements-properties/binding-element-xmla.md)([繫結](../../xmla/xml-elements-properties/bindings-element-xmla.md)的集合[程序](../../xmla/xml-elements-commands/process-element-xmla.md)或是[批次](../../xmla/xml-elements-commands/batch-element-xmla.md)命令)|  
  
## <a name="remarks"></a>備註  
 如需程式碼外部繫結的詳細資訊，請參閱[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>另請參閱  
 [繫結資料型別&#40;ASSL&#41;](binding-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
