---
title: Condition 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Condition Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- condition
helpviewer_keywords:
- Condition element
ms.assetid: 9c3cb31c-4aa1-49e4-aeb2-6cab54db0be3
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a4b91dcedde39e7d02c6d0263cf37de0fa7b3e62
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="condition-element-assl"></a>Condition 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含多維度運算式 (MDX) 運算式，可決定是否[動作](../../../analysis-services/scripting/objects/action-element-assl.md)父項目套用至目標。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action>  
   ...  
   <Condition>...</Condition  
      ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **條件**元素包含評估為布林值的 MDX 運算式。 如果運算式傳回**True**，然後在**動作**中指定的目標適用於[目標](../../../analysis-services/scripting/properties/target-element-assl.md)項目。 否則，**動作**不適用。  
  
 對應目的父代的項目**條件**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
