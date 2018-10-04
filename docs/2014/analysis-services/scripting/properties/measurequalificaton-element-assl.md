---
title: MeasureQualificaton 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureQualificaton Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- MeasureQualification element
ms.assetid: 754a037c-f20b-4717-a6e8-12f495e8e3b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aff36cad69d59b7effa51ac9ab3e32490931f779
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123328"
---
# <a name="measurequalificaton-element-assl"></a>MeasureQualificaton 元素 (ASSL)
  決定前置詞是否會套用至中的量值[MeasureGroup](../objects/group-element-assl.md)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <MeasureQualification>...</MeasureQualification>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*無*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MeasureGroup](../objects/group-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*無*|沒有任何前置詞會套用至這個量值群組中的量值。|  
|*PrefixMeasureGroup*|這個量值群組中每個量值的唯一名稱和標題前面會加上量值群組的名稱和單一空格。|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`MeasureQualification`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素&#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [維度項目&#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [MeasureGroup 元素&#40;ASSL&#41;](../objects/group-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
