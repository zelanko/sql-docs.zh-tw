---
title: ActionID 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5fa1c6cc179f79b4040bf13dbcb768be23bfac3b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="actionid-element-assl"></a>ActionID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含名稱的[動作](../../../analysis-services/scripting/objects/action-element-assl.md)上定義的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目，可在[觀點來看](../../../analysis-services/scripting/objects/perspective-element-assl.md)項目做為[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<PerspectiveAction>  
   <ActionID>...</ActionID  
</PerspectiveAction>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**ActionID**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.PerspectiveAction>。  
  
## <a name="see-also"></a>另請參閱  
 [Actions 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/actions-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
