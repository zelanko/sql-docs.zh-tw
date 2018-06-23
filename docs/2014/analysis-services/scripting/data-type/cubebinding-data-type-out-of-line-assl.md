---
title: CubeBinding 資料類型 (out out-of-line) (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b919e8f28d5cb102268ed3338aa0309e45a738c2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133549"
---
# <a name="cubebinding-data-type-out-of-line-assl"></a>CubeBinding 資料類型 (out-of-line) (ASSL)
  定義表示之間的關聯性的基本資料型別[Cube](../objects/cube-element-assl.md)項目和[DataSource](../objects/datasource-element-assl.md)項目。  
  
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
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[資料來源](../objects/datasource-element-assl.md)， [DataSourceID](../properties/id-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)|  
|衍生的元素|[繫結](../../xmla/xml-elements-properties/binding-element-xmla.md)([繫結](../../xmla/xml-elements-properties/bindings-element-xmla.md)集合[程序](../../xmla/xml-elements-commands/process-element-xmla.md)或[批次](../../xmla/xml-elements-commands/batch-element-xmla.md)命令)|  
  
## <a name="remarks"></a>備註  
 單行繫結的詳細資訊，請參閱[資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>另請參閱  
 [繫結資料型別&#40;ASSL&#41;](binding-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  