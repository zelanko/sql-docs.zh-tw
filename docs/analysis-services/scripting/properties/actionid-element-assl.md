---
title: "ActionID 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ActionID Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ActionID
helpviewer_keywords: ActionID element
ms.assetid: 2c9c66b2-a7ea-4874-a0ed-020ce3feab20
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 508a4fce7624979dac8e8180a5e8cfe070682db0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="actionid-element-assl"></a>ActionID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含名稱的[動作](../../../analysis-services/scripting/objects/action-element-assl.md)上定義的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目，可在[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目做為[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<PerspectiveAction>  
   <ActionID>...</ActionID  
</PerspectiveAction>  
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
|父元素|[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**ActionID**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.PerspectiveAction>。  
  
## <a name="see-also"></a>請參閱  
 [Actions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/actions-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
