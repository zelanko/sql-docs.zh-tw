---
title: IntermediateCubeDimensionID 元素 (ASSL) |Microsoft 文件
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
- IntermediateCubeDimensionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IntermediateCubeDimensionID
helpviewer_keywords:
- IntermediateCubeDimensionID element
ms.assetid: 305c0a91-7bc2-4268-ba94-8f19d8c22ca3
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 46b57b224d4c9e69b285491b2df316f84e0f38d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030155"
---
# <a name="intermediatecubedimensionid-element-assl"></a>IntermediateCubeDimensionID 元素 (ASSL)
  包含將參考維度關聯至量值群組之維度的識別碼 (ID)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ReferenceMeasureGroupDimension>  
   ...  
   <IntermediateCubeDimensionID>...</IntermediateCubeDimensionID>  
   ...  
</ReferenceMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ReferenceMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目`IntermediateCubeDimensionID`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  