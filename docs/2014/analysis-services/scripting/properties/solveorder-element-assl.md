---
title: SolveOrder 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- SolveOrder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SolveOrder
helpviewer_keywords:
- SolveOrder element
ms.assetid: ec43e055-97dd-4f2a-9a7c-2df2e1119e56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4fbd4132a0dc27d9055956d4b49a1ad02bc5dff5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219508"
---
# <a name="solveorder-element-assl"></a>SolveOrder 元素 (ASSL)
  指出求解順序[CalculationProperty](../objects/calculationproperty-element-assl.md)元素套用至導出的成員或導出資料格定義。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CalculationProperty>  
   ...  
   <SolveOrder>...</SolveOrder>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CalculationProperty](../objects/calculationproperty-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `SolveOrder`屬性會套用至`CalculationProperty`項目[CalculationType](calculationtype-element-assl.md)的*成員*或是*儲存格*。  
  
 對應至父系的元素`SolveOrder`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CalculationProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [CalculationProperties 元素&#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [MdxScript 元素&#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [MdxScripts 元素&#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
