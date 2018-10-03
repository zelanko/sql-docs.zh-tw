---
title: Application 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Application Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Application
helpviewer_keywords:
- Application element
ms.assetid: dfd780ad-f643-4a1c-b58b-34271ae91240
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b4a9b82bef51b02d65c934a6b8adbbbdb30e2e4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200388"
---
# <a name="application-element-assl"></a>Application 元素 (ASSL)
  識別與相關聯的應用程式[動作](../objects/action-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action>  
   ...  
   <Application>...</Application>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)或其中一個衍生元素： [DrillThroughAction](../data-type/action-data-type-assl.md)， [ReportAction](../data-type/reportaction-data-type-assl.md)， [StandardAction](../data-type/standardaction-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 用戶端應用程式可以使用 `Application` 元素來決定哪些動作適用於給定的用戶端應用程式。 用戶端應用程式會負責評估這個元素的值。  
  
 對應至父系的元素`Application`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [動作項目&#40;ASSL&#41;](../collections/actions-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
