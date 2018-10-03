---
title: RefreshInterval 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RefreshInterval Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RefreshInterval
helpviewer_keywords:
- RefreshInterval element
ms.assetid: 2761d26a-5fb0-452c-9a89-12f8dc658c33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76651edd1818204fed5c2ab9f8d8d787f4501d6a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48175838"
---
# <a name="refreshinterval-element-assl"></a>RefreshInterval 元素 (ASSL)
  指定重新整理與父元素相關聯之繫結資料的間隔。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionBinding> <!-- or MeasureGroupBinding, ProactiveCachingIncrementalProcessingBinding, ProactiveCachingQueryBinding -->  
   ...  
   <RefreshInterval>...</RefreshInterval>  
   ...  
</DimensionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|XML 持續時間|  
|基數|0-1：只能出現一次的選擇性元素。|  
|預設值|[ProactiveCachingIncrementalProcessingBinding](../data-type/binding-data-type-assl.md)或是[ProactiveCachingQueryBinding](../data-type/querybinding-data-type-assl.md) = 太平洋時間 1|  
|預設值|所有其他 = PT1m|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)， [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-assl.md)， [ProactiveCachingIncrementalProcessingBinding](../data-type/binding-data-type-assl.md)， [ProactiveCachingQueryBinding](../data-type/querybinding-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `RefreshInterval` 父系的元素是 <xref:Microsoft.AnalysisServices.DimensionBinding>、<xref:Microsoft.AnalysisServices.MeasureGroupBinding>、<xref:Microsoft.AnalysisServices.ProactiveCachingIncrementalProcessingBinding> 和 <xref:Microsoft.AnalysisServices.ProactiveCachingQueryBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
