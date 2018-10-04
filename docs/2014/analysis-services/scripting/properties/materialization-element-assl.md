---
title: Materialization 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Materialization Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Materialization element
ms.assetid: a87a95ae-d89c-4005-b22c-47c8991673b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 149c2bdaa147e129b3d25637c46c10983004c1dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106448"
---
# <a name="materialization-element-assl"></a>Materialization 元素 (ASSL)
  指出量值群組與參考維度之間關聯性的類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ReferenceMeasureGroupDimension >  
   ...  
   <Materialization>...</Materialization>  
   ...  
</ReferenceMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*間接*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ReferenceMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*規則*|此參考維度具有一般關聯性，如同一般維度。|  
|*間接*|此參考維度具有間接關聯性，如同多對多維度。|  
  
 對應至父系的元素`Materialization`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [維度項目&#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
