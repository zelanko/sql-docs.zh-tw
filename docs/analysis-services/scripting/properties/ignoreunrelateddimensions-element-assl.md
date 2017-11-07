---
title: "IgnoreUnrelatedDimensions 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- IgnoreUnrelatedDimensions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- IgnoreUnrelatedDimensions
helpviewer_keywords:
- IgnoreUnrelatedDimensions element
ms.assetid: c7d7a1cd-a8e0-4ae7-9464-a1d2a55a86ab
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6985abe0a62c0430ca494418659b0bd168ceb20d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|True|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[量值群組](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 當**IgnoreUnrelatedDimensions**是**true**，不相關的維度強制在其最上層，則當此值是**false**，維度不強制在其最上層。 這個屬性是以多維度運算式 (MDX) 類似[ValidMeasure](../../../mdx/validmeasure-mdx.md)函式。  
  
 對應目的父代的項目**IgnoreUnrelatedDimensions**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MeasureGroup>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

