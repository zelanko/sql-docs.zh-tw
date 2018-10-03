---
title: AttributeHierarchyVisible 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AttributeHierarchyVisible Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeHierarchyVisible
helpviewer_keywords:
- AttributeHierarchyVisible element
ms.assetid: a3289a9a-dbd6-43e8-a7ca-ee8a1da92a32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac33cb91014a32f3795b10ef822ab6c85528ac0b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099268"
---
# <a name="attributehierarchyvisible-element-assl"></a>AttributeHierarchyVisible 元素 (ASSL)
  決定用戶端應用程式是否可看到屬性階層。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute or PerspectiveAttribute -->  
   ...  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|`True`|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeAttribute](../data-type/cubeattribute-data-type-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)， [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `AttributeHierarchyVisible` 元素會決定用戶端應用程式是否可看到與屬性相關聯的屬性階層。 如果這個元素設定為 `False`，此屬性階層仍然可用來建立使用者定義階層，而且可由多維度運算式 (MDX) 陳述式參考。  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `AttributeHierarchyVisible` 父系的元素是 <xref:Microsoft.AnalysisServices.CubeAttribute>、<xref:Microsoft.AnalysisServices.DimensionAttribute> 和 <xref:Microsoft.AnalysisServices.PerspectiveAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [AttributeHierarchyEnabled 元素&#40;ASSL&#41;](enabled-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
