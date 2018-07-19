---
title: IgnoreUnrelatedDimensions 元素 (ASSL) |Microsoft Docs
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
- IgnoreUnrelatedDimensions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IgnoreUnrelatedDimensions
helpviewer_keywords:
- IgnoreUnrelatedDimensions element
ms.assetid: c7d7a1cd-a8e0-4ae7-9464-a1d2a55a86ab
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c278a3109180dbd058bc7ed8212c7b05782ce3d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295458"
---
# <a name="ignoreunrelateddimensions-element-assl"></a>IgnoreUnrelatedDimensions 元素 (ASSL)
  決定當查詢中包含與量值群組不相關的維度成員時，是否將不相關的維度強制在其最上層。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MeasureGroup>  
   ...  
   <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|True|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MeasureGroup](../objects/group-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 當 `IgnoreUnrelatedDimensions` 為 `true` 時，系統就會將不相關的維度強制在其最上層。當此值為 `false` 時，系統不會將維度強制在其最上層。 這個屬性是以多維度運算式 (MDX) 類似[ValidMeasure](/sql/mdx/validmeasure-mdx)函式。  
  
 對應至父系的元素`IgnoreUnrelatedDimensions`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
