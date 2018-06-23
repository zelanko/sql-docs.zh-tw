---
title: 輸入元素 (MeasureGroupAttribute) (ASSL) |Microsoft 文件
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
- Type Element (MeasureGroupAttribute)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 93740504-297a-4a06-ab3e-b598e466eebb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0d06b5df3ba99e54ec62de5c6f274874289cbbc4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036198"
---
# <a name="type-element-measuregroupattribute-assl"></a>Type 元素 (MeasureGroupAttribute) (ASSL)
  包含的型別[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroupAttribute>  
   ...  
   <Type>...</Type>  
   ...  
</MeasureGroupAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*規則*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*規則*|代表一般屬性。|  
|*資料粒度*|代表資料粒度屬性。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Type` 允許值的列舉是 <xref:Microsoft.AnalysisServices.MeasureGroupAttributeType>。  
  
 對應目的父代的項目`Type`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性項目&#40;ASSL&#41;](../collections/attributes-element-assl.md)   
 [RegularMeasureGroupDimension 資料類型&#40;ASSL&#41;](../data-type/dimension-data-type-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  