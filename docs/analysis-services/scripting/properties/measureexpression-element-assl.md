---
title: "MeasureExpression 元素 (ASSL) |Microsoft 文件"
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
- MeasureExpression Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureExpression
helpviewer_keywords:
- MeasureExpression element
ms.assetid: a0b6490d-a793-41be-8c97-41b08e1580a1
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 40e957b6f4797c5346f3f107e2575cbb2eb78a71
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="measureexpression-element-assl"></a>MeasureExpression 元素 (ASSL)
  包含定義如何取得父量值之值的多維度運算式 (MDX) 運算式。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Measure>  
   ...  
   <MeasureExpression>...</MeasureExpression>  
   ...  
</Measure>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**MeasureExpression**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Measure>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

