---
title: Action 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
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
- Action Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Action
helpviewer_keywords:
- Action element
ms.assetid: aaee06a2-91c6-4007-b787-79cb08d63c77
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 80a0bdc56107980b9865015f07abd8b213d1021c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="action-element-assl"></a>Action 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含中可用動作的相關資訊[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目或[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Actions>  
   <Action xsi:type="DrillThroughAction">...</Action> <!-- ancestor: Cube -->  
   <Action xsi:type="ReportAction">...</Action> <!-- ancestor: Cube -->  
   <Action xsi:type="StandardAction">...</Action> <!-- ancestor: Cube -->  
   <!-- or -->  
   <Action xsi:type="PerspectiveAction">...</Action> <!-- ancestor: Perspective -->  
</Actions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|請參閱下表。|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
|上階或父系|資料類型|  
|------------------------|---------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)， [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)， [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
|[檢視方塊](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/collections/actions-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>請參閱  
 [Cube 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Perspective 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)   
 [PerspectiveAction 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
