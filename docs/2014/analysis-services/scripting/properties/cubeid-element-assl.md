---
title: CubeID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CubeID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeID
helpviewer_keywords:
- CubeID element
ms.assetid: cea9cd1b-30e6-48b1-afb9-c2c1243cead8
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 941e8171a183bcbc66521b4f022be185cac7911a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321118"
---
# <a name="cubeid-element-assl"></a>CubeID 元素 (ASSL)
  識別[Cube](../objects/cube-element-assl.md)相關聯的項目[繫結](../data-type/binding-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeAttributeBinding> <!-- or CubeDimensionBinding, MeasureGroupAttributeBinding, MeasureGroupBinding -->  
   ...  
   <CubeID>...</CubeID>  
      ...  
</CubeAttributeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeAttributeBinding](../data-type/attributebinding-data-type-assl.md)， [CubeDimensionBinding](../data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `CubeID` 父系的元素是 <xref:Microsoft.AnalysisServices.CubeAttributeBinding>、<xref:Microsoft.AnalysisServices.CubeDimensionBinding> 和 <xref:Microsoft.AnalysisServices.MeasureGroupBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
