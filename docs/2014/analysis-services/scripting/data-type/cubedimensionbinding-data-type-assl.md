---
title: CubeDimensionBinding 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeDimensionBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimensionBinding
helpviewer_keywords:
- CubeDimensionBinding data type
ms.assetid: 7288e345-4a3e-4197-82e9-9daa38f6e928
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8fc7a97ebe67e9461a085e6bafe076216f36d63e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153220"
---
# <a name="cubedimensionbinding-data-type-assl"></a>CubeDimensionBinding 資料類型 (ASSL)
  定義衍生的資料類型表示的繫結[維度](../objects/dimension-element-assl.md)，[量值](../objects/measure-element-assl.md)，或[MiningModel](../objects/miningmodel-element-assl.md)的 cube 維度的項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimensionBinding>  
      <!-- The following elements extend Binding -->  
   <DataSourceID>...</DataSourceID>  
   <CubeID>...</CubeID>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Filter>...</Filter>  
</CubeDimensionBinding>  
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
|子元素|[CubeDimensionID](../properties/id-element-assl.md)， [CubeID](../properties/cubeid-element-assl.md)， [DataSourceID](../properties/datasourceid-element-assl.md)，[篩選](../properties/filter-element-trace-assl.md)|  
|衍生的元素|請參閱[繫結](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊`Binding`型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表`Binding`型別和繼承階層`Binding`類型，請參閱[繫結資料型別&#40;ASSL&#41;](binding-data-type-assl.md)。  
  
 如需 ASSL 中資料繫結的概觀，請參閱 <<c0> [ 資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。</c0>  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.CubeDimensionBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
