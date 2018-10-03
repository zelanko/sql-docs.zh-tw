---
title: Relationships 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: e78882c9-b14e-4044-848e-ea7fddd3b75d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b0a83a2e7722fab119df3a0918ea0ecbe7c24131
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134546"
---
# <a name="relationships-element-assl"></a>Relationships 元素 (ASSL)
  包含相關聯維度之關聯性的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimension> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Attributes>  
      <Attribute>...</Attribute>  
  </Attributes>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeDimension](../data-type/dimension-data-type-assl.md)，[維度](../objects/dimension-element-assl.md)， [PerspectiveDimension](../data-type/perspectivedimension-data-type-assl.md)， [RegularMeasureGroupDimension](../data-type/measuregroupdimension-data-type-assl.md)|  
|子元素|[關聯性](../data-type/relationship-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應項目<xref:Microsoft.AnalysisServices.RelationshipCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
