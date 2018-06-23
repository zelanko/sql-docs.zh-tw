---
title: ActionID 元素 (ASSL) |Microsoft 文件
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
- ActionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ActionID
helpviewer_keywords:
- ActionID element
ms.assetid: 2c9c66b2-a7ea-4874-a0ed-020ce3feab20
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 13e83d3a022416de56cba7bbf6693ea408b51562
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034457"
---
# <a name="actionid-element-assl"></a>ActionID 元素 (ASSL)
  包含名稱的[動作](../objects/action-element-assl.md)上定義的項目[Cube](../objects/cube-element-assl.md)項目，可在[觀點來看](../objects/perspective-element-assl.md)項目做為[PerspectiveAction](../data-type/action-data-type-assl.md)項目。  
  
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
|父元素|[PerspectiveAction](../data-type/action-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目`ActionID`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.PerspectiveAction>。  
  
## <a name="see-also"></a>另請參閱  
 [Actions 元素&#40;ASSL&#41;](../collections/actions-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  