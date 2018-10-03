---
title: MeasureGroupID 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroupID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupID
helpviewer_keywords:
- MeasureGroupID element
ms.assetid: 3b075f86-dbbc-4285-8d2d-61fa722181c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4eb43414e0fd7da783f4a1ac588c4851e3c9bd9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083629"
---
# <a name="measuregroupid-element-assl"></a>MeasureGroupID 元素 (ASSL)
  將產生關聯[MeasureGroup](../objects/group-element-assl.md)與父元素、 繫結或程式碼外部繫結。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ManyToManyMeasureGroupDimension> <!-- or MeasureGroupAttributeBinding, MeasureGroupBinding, PerspectiveMeasureGroup -->  
   ...  
   <MeasureGroupID>...</MeasureGroupID>  
   ...  
</ManyToManyMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數||  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)， [MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupBinding](../data-type/binding-data-type-assl.md)， [PerspectiveMeasureGroup](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
|子系項目上階或父系|基數|  
|------------------------------------------|-----------------|  
|[ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|0-1：只能出現一次的選擇性元素。|  
|[MeasureGroupAttributeBinding](../data-type/measuregroupattributebinding-data-type-out-of-line-assl.md)， [MeasureGroupBinding](../data-type/binding-data-type-assl.md)和[PerspectiveMeasureGroup](../data-type/perspectivemeasuregroup-data-type-assl.md)|1-1：只出現一次的必要元素。|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `MeasureGroupID` 父系的元素是 <xref:Microsoft.AnalysisServices.ManyToManyMeasureGroupDimension>、<xref:Microsoft.AnalysisServices.MeasureGroupBinding> 和 <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
