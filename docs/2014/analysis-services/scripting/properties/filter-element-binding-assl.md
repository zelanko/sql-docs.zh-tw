---
title: Filter 元素 (Binding) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Filter Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- filter
helpviewer_keywords:
- Filter element
ms.assetid: 3d4cd169-2903-4266-8541-540ece424b7b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0fe300ea7c88924fd463968cae680ded50ebb610
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209948"
---
# <a name="filter-element-binding-assl"></a>Filter 元素 (Binding) (ASSL)
  包含篩選父元素內容的多維度運算式 (MDX) 運算式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <Filter>...</Filter>  
   ...  
</CubeDimensionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeDimensionBinding](../data-type/binding-data-type-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊`Binding`型別，包括資料表[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]指令碼語言 (ASSL) 物件的`Binding`型別和繼承階層架構`Binding`類型，請參閱[繫結資料類型 &#40;ASSL&#41;](../data-type/binding-data-type-assl.md).  
  
 如需 ASSL 中資料繫結的概觀，請參閱 <<c0> [ 資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。</c0>  
  
 對應至父系的元素`Filter`在 「 分析管理物件 (AMO) 物件模型所<xref:Microsoft.AnalysisServices.CubeDimensionBinding>和<xref:Microsoft.AnalysisServices.MeasureGroupBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [繫結資料型別&#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [資料來源和繫結&#40;SSAS 多維度&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
