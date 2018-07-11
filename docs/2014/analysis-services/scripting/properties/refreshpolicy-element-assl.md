---
title: RefreshPolicy 元素 (ASSL) |Microsoft Docs
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
- RefreshPolicy Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RefreshPolicy
helpviewer_keywords:
- RefreshPolicy element
ms.assetid: f4c36280-1a39-4f1c-a3ab-fbeb81742d6d
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf0aa9478a44e7479b20357ae56317b90801f77f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277614"
---
# <a name="refreshpolicy-element-assl"></a>RefreshPolicy 元素 (ASSL)
  決定多久維度或量值群組之動態部分 (依照[持續性](persistence-element-assl.md)項目) 會檢查變更。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding -->  
   ...  
   <RefreshPolicy>...</RefreshPolicy>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
|上階或父系|預設值|  
|------------------------|-------------------|  
|[DimensionBinding](../data-type/binding-data-type-assl.md)|*ByQuery*|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|無|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionBinding](../data-type/binding-data-type-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*ByQuery*|每個查詢都檢查來源資料是否已經變更。|  
|*ByInterval*|來源資料只會檢查變更在所指定的間隔[RefreshInterval](refreshinterval-element-assl.md)。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `RefreshPolicy` 允許值的列舉是 <xref:Microsoft.AnalysisServices.RefreshPolicy>。  
  
## <a name="see-also"></a>另請參閱  
 [Persistence 元素&#40;ASSL&#41;](persistence-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
